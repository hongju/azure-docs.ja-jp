---
title: Java を使用した Azure Storage サンプル | Microsoft Docs
description: Azure Storage のサンプル コードとアプリケーションを表示、ダウンロード、実行します。 Java のストレージ クライアント ライブラリを使用して、BLOB、キュー、テーブル、ファイルのサンプルの概要について説明します。
services: storage
author: mhopkins-msft
ms.service: storage
ms.devlang: java
ms.topic: article
ms.date: 05/03/2019
ms.author: mhopkins
ms.subservice: common
ms.openlocfilehash: 3d241f1905244d3a8039372262f84ba0fd25220d
ms.sourcegitcommit: 0568c7aefd67185fd8e1400aed84c5af4f1597f9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65209798"
---
# <a name="azure-storage-samples-using-java"></a>Java を使用した Azure Storage サンプル

## <a name="java-sample-index"></a>Java サンプルのインデックス

次の表は、各サンプルで扱っているサンプル リポジトリとシナリオの概要を示したものです。 リンクをクリックすると、対応するサンプル コードが GitHub で表示されます。

<table style="font-size:90%"><thead><tr><th style="font-size:110%">エンドポイント</th><th style="font-size:110%">シナリオ</th><th style="font-size:110%">サンプル コード</th></tr></thead><tbody>
<tr>
<td rowspan="16"><b>BLOB</b></td>
<td>Append Blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java での Azure Blob service の概要</a></td>
</tr>
<tr>
<td>ブロック BLOB</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java での Azure Blob service の概要</a></td>
</tr>
<tr>
<td>クライアント側の暗号化</td>
<td><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Java での Azure クライアント側暗号化の概要</a></td>
</tr>
<tr>
<td>BLOB のコピー</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java での Azure Blob service の概要</a></td>
</tr>
<tr>
<td>コンテナーの作成</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java での Azure Blob service の概要</a></td>
</tr>
<tr>
<td>Delete Blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java での Azure Blob service の概要</a></td>
</tr>
<tr>
<td>Delete Container</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java での Azure Blob service の概要</a></td>
</tr>
<tr>
<td>BLOB のメタデータ/プロパティ/統計</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Java での Azure Blob service の概要</a></td>
</tr>
<tr>
<td>コンテナーの ACL/メタデータ/プロパティ</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Java での Azure Blob service の概要</a></td>
</tr>
<tr>
<td>ページ範囲の取得</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java#L399">Java での Azure Blob service の概要</a></td>
</tr>
<tr>
<td>BLOB/コンテナーのリース</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java での Azure Blob service の概要</a></td>
</tr>
<tr>
<td>BLOB/コンテナーのリスト</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java での Azure Blob service の概要</a></td>
</tr>
<tr>
<td>ページ BLOB</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java での Azure Blob service の概要</a></td>
</tr>
<tr>
<td>SAS</td>
<td><a href="https://github.com/Azure/azure-storage-java/blob/89540f018f1160ce55619c6fe7b5f5ff57d0ce10/src/test/java/com/microsoft/azure/storage/Samples.java#L513">SAS テストのサンプル</a></td>
</tr>   
<tr>
<td>サービスのプロパティ</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Java での Azure Blob service の概要</a></td>
</tr>
<tr>
<td>Snapshot Blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java での Azure Blob service の概要</a></td>
</tr>
<tr>
<td rowspan="9"><b>ファイル</b></td>
<td>共有/ディレクトリ/ファイルの作成</td>
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java での Azure File サービスの概要</a></td>
</tr>
<tr>
<td>共有/ディレクトリ/ファイルの削除</td>
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java での Azure File サービスの概要</a></td>
</tr>
<tr>
<td>ディレクトリのプロパティ/メタデータ</td>
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java での Azure File サービスの概要</a></td>
</tr>
<tr>
<td>ファイルのダウンロード</td>
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java での Azure File サービスの概要</a></td>
</tr>
<tr>
<td>ファイルのプロパティ/メタデータ/メトリック</td>
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java での Azure File サービスの概要</a></td>
</tr>
<tr>
<td>ファイル サービスのプロパティ</td>
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java での Azure File サービスの概要</a></td>
</tr>
<tr>
<td>ディレクトリとファイルのリスト</td>
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java での Azure File サービスの概要</a></td>
</tr>
<tr>
<td>共有のリスト</td>
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java での Azure File サービスの概要</a></td>
</tr>
<tr>
<td>共有のプロパティ/メタデータ/統計</td>
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java での Azure File サービスの概要</a></td>
</tr>
<tr>
<td rowspan="8"><b>キュー</b></td>
<td>メッセージの追加</td>
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java#L63">Java での Azure Queue サービスの概要</a></td>
</tr>
<tr>
<td>クライアント側の暗号化</td>
<td><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption/blob/master/src/gettingstarted/KeyVaultGettingStarted.java">Java での Azure クライアント側暗号化の概要</a></td>
</tr>
<tr>
<td>キューの作成</td>
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java での Azure Queue サービスの概要</a></td>
</tr>
<tr>
<td>メッセージ/キューの削除</td>
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java での Azure Queue サービスの概要</a></td>
</tr>
<tr>
<td>メッセージのピーク</td>
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java での Azure Queue サービスの概要</a></td>
</tr>
<tr>
<td>キューの ACL/メタデータ/統計</td>
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Java での Azure Queue サービスの概要</a></td>
</tr>
<tr>
<td>キュー サービスのプロパティ</td>
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Java での Azure Queue サービスの概要</a></td>
</tr>
<tr>
<td>更新メッセージ</td>
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java での Azure Queue サービスの概要</a></td>
</tr>
<tr>
<td rowspan="7"><b>テーブル</b></td>
<td>テーブルの作成</td>
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/main/java/com/microsoft/azure/cosmosdb/tablesample/TableBasics.java">Java での Azure Table service の概要</a></td>
</tr>
<tr>
<td>エンティティ/テーブルの削除</td>
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/main/java/com/microsoft/azure/cosmosdb/tablesample/TableBasics.java">Java での Azure Table service の概要</a></td>
</tr>
<tr>
<td>エンティティの挿入/マージ/置換</td>
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/main/java/com/microsoft/azure/cosmosdb/tablesample/TableBasics.java">Java での Azure Table service の概要</a></td>
</tr>
<tr>
<td>エンティティのクエリ</td>
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/main/java/com/microsoft/azure/cosmosdb/tablesample/TableBasics.java">Java での Azure Table service の概要</a></td>
</tr>
<tr>
<td>テーブルの照会</td>
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/main/java/com/microsoft/azure/cosmosdb/tablesample/TableBasics.java">Java での Azure Table service の概要</a></td>
</tr>
<tr>
<td>テーブルの ACL/プロパティ</td>
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/main/java/com/microsoft/azure/cosmosdb/tablesample/TableAdvanced.java">Java での Azure Table service の概要</a></td>
</tr>
<tr>
<td>エンティティの更新</td>
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/main/java/com/microsoft/azure/cosmosdb/tablesample/TableBasics.java">Java での Azure Table service の概要</a></td>
</tr>
</tbody>
</table>
<br/>

## <a name="azure-code-samples-library"></a>Azure のコード サンプル ライブラリ

完全なサンプル ライブラリを表示するには、[Azure のコード サンプル](https://azure.microsoft.com/resources/samples/?service=storage) ライブラリにアクセスしてください。このライブラリには、ダウンロードしてローカルで実行できる Azure Storage のサンプルが用意されています。 コード サンプル ライブラリでは、サンプル コードが .zip 形式で提供されます。 また、各サンプルの GitHub リポジトリを参照して複製することもできます。

[!INCLUDE [storage-java-samples-include](../../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a>概要ガイド

Azure Storage ライブラリのインストール方法と概要については、以下のガイドをご覧ください。

* [Java での Azure Blob service の概要](../blobs/storage-quickstart-blobs-java.md)
* [Java での Azure Queue サービスの概要](../queues/storage-java-how-to-use-queue-storage.md)
* [Java での Azure Table service の概要](../../cosmos-db/table-storage-how-to-use-java.md)
* [Java での Azure File サービスの概要](../files/storage-java-how-to-use-file-storage.md)

## <a name="next-steps"></a>次の手順

他の言語のサンプルについては、以下のページをご覧ください。

* .NET:[.NET を使用した Azure Storage サンプル](storage-samples-dotnet.md)
* その他すべての言語: [Azure Storage のサンプル](storage-samples.md)
