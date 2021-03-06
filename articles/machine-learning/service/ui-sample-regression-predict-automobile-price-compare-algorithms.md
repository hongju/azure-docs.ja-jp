---
title: 回帰価格を予測し、アルゴリズムを比較する
titleSuffix: Azure Machine Learning service
description: このビジュアル インターフェイス サンプルの実験では、自動車の価格を予測する 2 つの回帰モデルのパフォーマンスを比較する方法を示します。 このプロセスには、Automobile price data (Raw) データセットに対するモデルのトレーニング、テスト、評価が含まれます。
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.topic: article
author: xiaoharper
ms.author: zhanxia
ms.reviewer: sgilley
ms.date: 05/02/2019
ms.openlocfilehash: 2a4a9e74fa7f56b67f0f4a64f6619db1c5c69a2c
ms.sourcegitcommit: 4891f404c1816ebd247467a12d7789b9a38cee7e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2019
ms.locfileid: "65442136"
---
# <a name="sample-2---regression-predict-price-and-compare-algorithms"></a>サンプル 2 - 回帰:価格を予測し、アルゴリズムを比較する

このビジュアル インターフェイス サンプルの実験では、自動車の価格を予測する 2 つの回帰モデルのパフォーマンスを比較する方法を示します。 このプロセスには、**Automobile price data (Raw)** データセットを使用したモデルのトレーニング、テスト、評価が含まれます。

## <a name="prerequisites"></a>前提条件

[!INCLUDE [aml-ui-prereq](../../../includes/aml-ui-prereq.md)]

4. サンプル 2 実験の **[Open]\(開く\)** ボタンを選択します。

    ![実験を開く](media/ui-sample-regression-predict-automobile-price-compare-algorithms/open-sample2.png)

## <a name="related-sample"></a>関連サンプル

[サンプル 1 - 回帰:自動車価格予測 (基本)](ui-sample-regression-predict-automobile-price-basic.md) では、この実験と同じ問題を解決しますが、回帰モデルを 1 つしか使用しない、より単純な実験を示しています。 回帰の基本的なサンプルをお探しの場合は、そちらを参照してください。

## <a name="experiment-summary"></a>実験の概要

次の手順を使用して実験を構築します。

1. データを取得する。
1. データを前処理する。
1. モデルをトレーニングする。
1. モデルをテスト、評価、比較する。

この実験の完全なグラフを次に示します。

[![実験のグラフ](media/ui-sample-regression-predict-automobile-price-compare-algorithms/graph.png)](media/ui-sample-regression-predict-automobile-price-compare-algorithms/graph.png#lightbox)


## <a name="get-the-data"></a>データを取得する

この実験では、UCI Machine Learning Repository から取得された **Automobile price data (Raw)** データセットを使用します。 このデータセットには、メーカー、モデル、価格、車両特徴 (シリンダー数など)、MPG、保険リスク スコアなど、自動車に関する情報を含む 26 列が含まれています。 この実験の目的は、自動車の価格を予測することです。

## <a name="pre-process-the-data"></a>データを前処理する

主なデータ準備タスクには、データのクリーニング、統合、変換、削減、および離散化または量子化が含まれます。 ビジュアル インターフェイスには、左側のパネルの **Data Transformation (データ変換)** グループに、これらの操作およびその他のデータ前処理タスクを実行するためのモジュールがあります。

この実験では、**Select Columns in Dataset (データセット内の列の選択)** モジュールを使用して、欠損値が多い正規化された損失を除外します。 次に、**Clean Missing Data (欠損データのクリーニング)** を使用して、欠損値がある行を削除します。 これにより、クリーンなトレーニング データセットを作成できます。

![データの前処理](media/ui-sample-regression-predict-automobile-price-compare-algorithms/data-processing.png)

## <a name="train-the-model"></a>モデルをトレーニングする

機械学習の問題はさまざまです。 一般的な機械学習タスクには、分類、クラスタリング、回帰、推奨システムなどがあり、それぞれに異なるアルゴリズムが必要になる場合があります。 アルゴリズムの選択は、多くの場合、ユース ケースの要件によって異なります。 アルゴリズムを選択したら、より正確なモデルをトレーニングするためにそのパラメーターを調整する必要があります。 次に、精度、明瞭度、効率性などのメトリックに基づいて、すべてのモデルを評価する必要があります。

この実験の目的は自動車の価格を予測することであり、またラベル列 (価格) には実数が含まれるため、回帰モデルを選択することをお勧めします。 特徴の数が比較的少なく (100 未満)、これらの特徴が疎でないことを考慮すると、決定境界は非線形である可能性があります。

異なるアルゴリズムのパフォーマンスを比較するために、**Boosted Decision Tree Regression** と **Decision Forest Regression** の 2 つの非線形アルゴリズムを使用してモデルを構築します。 どちらのアルゴリズムにも変更可能なパラメーターがありますが、この実験では既定値を使用します。

**Split Data (データの分割)** モジュールを使用して、トレーニング データセットが元のデータの 70% を含み、テスト データセットが元のデータの 30% を含むように、入力データをランダムに分割します。

## <a name="test-evaluate-and-compare-the-models"></a>モデルをテスト、評価、比較する

前のセクションで説明したように、ランダムに選択した 2 つの異なるデータセットを使用してモデルをトレーニングし、テストします。 モデルの評価をより客観的に行うために、データセットを分割し、異なるデータセットを使用してモデルをトレーニングおよびテストします。

モデルのトレーニングが終わったら、**Score Model (モデルのスコア付け)** モジュールと **Evaluate Model (モデルの評価)** モジュールを使用して予測結果を生成し、モデルを評価します。 **Score Model (モデルのスコア付け)** は、トレーニングされたモデルを使用してテスト データセットの予測を生成します。 次に、そのスコアを **Evaluate Model (モデルの評価)** に渡して評価メトリックを生成します。

この実験では、**Evaluate Model (モデルの評価)** の 2 つのインスタンスを使用して、2 組のモデルを比較します。

まず、トレーニング データセットで 2 つのアルゴリズムを比較します。
次に、テスト データセットで 2 つのアルゴリズムを比較します。
結果は次のとおりです。

![結果を比較する](media/ui-sample-regression-predict-automobile-price-compare-algorithms/result.png)

これらの結果は、**Boosted Decision Tree Regression** で構築したモデルが、**Decision Forest Regression** で構築したモデルよりも二乗平均平方根誤差が小さいことを示しています。

どちらのアルゴリズムも、目に見えないテスト データセットよりもトレーニング データセットで誤差が少なくなります。

## <a name="clean-up-resources"></a>リソースのクリーンアップ

[!INCLUDE [aml-ui-cleanup](../../../includes/aml-ui-cleanup.md)]

## <a name="next-steps"></a>次の手順

ビジュアル インターフェイスで利用できるその他のサンプルを確認します。

- [サンプル 1 - 回帰: 自動車の価格を予測する](ui-sample-regression-predict-automobile-price-basic.md)
- [サンプル 3 - 分類:信用リスクを予測する](ui-sample-classification-predict-credit-risk-basic.md)
- [サンプル 4 - 分類: 信用リスクを予測する (費用重視)](ui-sample-classification-predict-credit-risk-cost-sensitive.md)
- [サンプル 5 - 分類:顧客離れを予測する](ui-sample-classification-predict-churn.md)
