---
title: Azure Database for PostgreSQL でディストリビューション列を選択する - Hyperscale (Citus) (プレビュー)
description: 一般的な Hyperscale シナリオでのディストリビューション列の適切な選択
author: jonels-msft
ms.author: jonels
ms.service: postgresql
ms.subservice: hyperscale-citus
ms.topic: conceptual
ms.date: 05/06/2019
ms.openlocfilehash: e9fba14b8979f739fd29bc277e32fb544221d08a
ms.sourcegitcommit: 0ae3139c7e2f9d27e8200ae02e6eed6f52aca476
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65080647"
---
# <a name="choose-distribution-columns-in-azure-database-for-postgresql--hyperscale-citus-preview"></a>Azure Database for PostgreSQL でディストリビューション列を選択する - Hyperscale (Citus) (プレビュー)

各テーブルのディストリビューション列を選択することは、モデリングに関する決定事項の中でも**最も重要なものの 1 つ**です。 Hyperscale は、行のディストリビューション列の値に基づいて、行をシャードに格納します。

適切な選択では、同じ物理ノード上の関連データがまとめてグループ化され、クエリが高速になり、すべての SQL 機能のサポートが追加されます。 不適切な選択では、システムの動作が遅くなり、ノード全体ですべての SQL 機能をサポートできなくなります。

このセクションでは、最も一般的な 2 つの Hyperscale シナリオに関するディストリビューション列のヒントを紹介します。

### <a name="multi-tenant-apps"></a>マルチテナント アプリ

マルチテナント アーキテクチャでは、階層型データベース モデリングの形式を使用して、サーバー グループ内のノードにクエリを分散します。  データ階層の最上位は "*テナント ID*" と呼ばれ、各テーブルの列に格納する必要があります。

Hyperscale は、クエリを検査してどのテナント ID が関係しているかを確認し、一致するテーブル シャードを見つけます。 クエリはシャードを含む単一のワーカー ノードにルーティングされます。 同じノード上にあるすべての関連データに対してクエリを実行することは、コロケーションと呼ばれます。

次の図は、マルチテナント データ モデルのコロケーションを示します。 これには Accounts と Campaigns という 2 つのテーブルがあり、それぞれ `account_id` で分散されます。 網掛けのボックスはシャードを表し、それぞれの色はどのワーカー ノードに含まれるかを表します。 緑色のシャードは 1 つのワーカー ノードにまとめて格納され、青色は別のワーカー ノードに格納されます。 両方のテーブルを同じ account\_id に制限すると、Accounts と Campaigns 間の結合クエリですべての必要なデータが 1 つのノードにまとめられる点に注目してください。

![マルチテナント コロケーション](media/concepts-hyperscale-choosing-distribution-column/multi-tenant-colocation.png)

この設計を自分のスキーマに適用するには、アプリケーションのテナントを構成する要素を特定します。 一般的なインスタンスには、会社、アカウント、組織、または顧客が含まれます。 列名は `company_id` や `customer_id` のようになります。 各クエリを調べて、関連するすべてのテーブルをテナント ID が同じ行に制限する追加の WHERE 句があればうまくいくかどうかを自問してみてください。
マルチテナント モデルのクエリはテナントにスコープされています。たとえば、売上や在庫に対するクエリは特定の店舗内にスコープされています。

#### <a name="best-practices"></a>ベスト プラクティス

-   **共通 tenant\_id 列で分散テーブルをパーティション化します。** たとえば、テナントが会社である SaaS アプリケーションでは、tenant\_id はおそらく company\_id になります。
-   **小さなクロステナント テーブルを参照テーブルに変換します。** 複数のテナントが小さな情報テーブルを共有する場合は、それを参照テーブルとして配布します。
-   **すべてのアプリケーション クエリのフィルター処理を tenant\_id で制限します。** 各クエリでは、一度に 1 つのテナントの情報を要求するようにします。

このような種類のアプリケーションを構築する例については、[マルチテナント チュートリアル](./tutorial-design-database-hyperscale-multi-tenant.md)に関する記事を参照してください。

### <a name="real-time-apps"></a>リアルタイム アプリ

マルチテナント アーキテクチャは階層構造を導入し、データ コロケーションを使用してテナントごとにクエリをルーティングします。 対照的に、リアルタイム アーキテクチャは、高度な並列処理を実現するために、データの特定の分散プロパティに依存しています。

ここでは、リアルタイム モデルのディストリビューション列の用語として "エンティティ ID" を使用します。 一般的なエンティティは、ユーザー、ホスト、またはデバイスです。

通常、リアルタイム クエリには、日付またはカテゴリでグループ化された数値の集計が必要です。 Hyperscale では、部分的な結果を得るためにこれらのクエリが各シャードに送信され、コーディネーター ノード上で最終的な答えがまとめられます。 可能な限り多数のノードが参加し、過度な量の作業を行う必要があるノードが 1 つもない場合に、最も高速にクエリが実行されます。

#### <a name="best-practices"></a>ベスト プラクティス

-   **カーディナリティの高い列をディストリビューション列として選択します。** 比較として、order テーブルの値が "new"、"pay"、および "shipping" の \"status\" フィールドは、ディストリビューション列には適していません。 データを保持できるシャードの数とそれを処理できるノードの数が制限されるため、これらの値はごくわずかと想定されます。 さらに、カーディナリティの高い列の中で、group-by 句や結合キーとして頻繁に使用されるものを選択することをお勧めします。
-   **均等な分散の列を選択します。** 特定の共通値に偏った列についてテーブルを分散させると、テーブル内のデータは特定のシャードに蓄積される傾向があります。 このようなシャードを保持しているノードは、他のノードよりも多くの作業を実行することになります。
-   **共通の列についてファクト テーブルとディメンション テーブルを分散させます。**
    ファクト テーブルが持つことができる分散キーは 1 つのみです。 別のキーで結合するテーブルは、ファクト テーブルと併置されません。 結合する頻度と結合する行のサイズに基づいて、併置するディメンションを 1 つ選択します。
-   **一部のディメンション テーブルを参照テーブルに変更します。** ディメンション テーブルをファクト テーブルと併置できない場合は、ディメンション テーブルのコピーを参照テーブルの形式ですべてのノードに分散させることで、クエリのパフォーマンスを向上することができます。

このような種類のアプリケーションを構築する例については、[リアルタイム ダッシュボードのチュートリアル](./tutorial-design-database-hyperscale-realtime.md)に関する記事を参照してください。

### <a name="timeseries-data"></a>時系列データ

時系列ワークロードでは、アプリケーションは古い情報をアーカイブしながら最新の情報をクエリします。

Hyperscale で時系列情報をモデル化する際に最も一般的な誤りは、タイムスタンプ自体を分散列として使用することです。 時間に基づくハッシュ分散は、時間の範囲をシャードにまとめるのではなく、見かけ上ランダムに時間を異なるシャードに分散させます。 時間に関係する含むクエリは、通常、時間の範囲 (たとえば最新のデータ) を参照するため、このようなハッシュ分散はネットワークのオーバーヘッドにつながります。

#### <a name="best-practices"></a>ベスト プラクティス

-   **分散列としてタイムスタンプを選択しないでください。** 別の分散列を選択します。 マルチテナント アプリでは、テナント ID を使用します。また、リアルタイム アプリではエンティティ ID を使用します。
-   **代わりに PostgreSQL のテーブル パーティションを使用します。** 時系列データの大きなテーブルを、それぞれ時間の範囲が異なる複数の継承テーブルに分割するには、テーブルのパーティション分割を使用します。  Postgres でパーティション分割されたテーブルを Hyperscale で分散すると、継承テーブルのシャードが作成されます。

このような種類のアプリケーションを構築する例については、[時系列チュートリアル](https://aka.ms/hyperscale-tutorial-timeseries)に関する記事を参照してください。

## <a name="next-steps"></a>次の手順
- 分散データ間の[コロケーション](concepts-hyperscale-colocation.md)がクエリの高速実行にどのように役立つかについて学習します
