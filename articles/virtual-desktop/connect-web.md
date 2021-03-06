---
title: Web ブラウザーから Windows Virtual Desktop プレビューに接続する - Azure
description: Web ブラウザーから Windows Virtual Desktop プレビューに接続する方法。
services: virtual-desktop
author: Heidilohr
ms.service: virtual-desktop
ms.topic: how-to
ms.date: 04/12/2019
ms.author: helohr
ms.openlocfilehash: 9696f3c32f8b903257e337191a5ce32645bfd198
ms.sourcegitcommit: f6ba5c5a4b1ec4e35c41a4e799fb669ad5099522
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65142445"
---
# <a name="connect-from-a-web-browser"></a>Web ブラウザーから接続する

Web クライアントでは、時間のかかるインストール プロセスなしで Web ブラウザーから Windows Virtual Desktop プレビュー リソースにアクセスすることができます。

>[!NOTE]
>現在、Web クライアントにはモバイル OS のサポートがありません。

## <a name="supported-operating-systems-and-browsers"></a>サポートされているオペレーティング システムとブラウザー

任意の HTML5 対応ブラウザーが動作しますが、正式にサポートしているオペレーティング システムとブラウザーは次のとおりです。

| ブラウザー           | サポート対象 OS                     | メモ               |
|-------------------|----------------------------------|---------------------|
| Microsoft Edge    | Windows                          |                     |
| Internet Explorer | Windows                          |                     |
| Apple Safari      | macOS                            |                     |
| Mozilla Firefox   | Windows、macOS、Linux            | バージョン 55 以降 |
| Google Chrome     | Windows、macOS、Linux、Chrome OS |                     |

## <a name="access-remote-resources-feed"></a>リモート リソース フィードにアクセスする

ブラウザーで、[Windows Virtual Desktop Web クライアント](https://rdweb.wvd.microsoft.com/webclient)に移動し、ユーザー アカウントを使用してサインインします。

>[!NOTE]
>Windows Virtual Desktop に使用するものとは異なる Azure AD アカウントを使用して既にサインインしている場合は、サインアウトするか、プライベート ブラウザー ウィンドウを使用する必要があります。

サインインすると、リソースの一覧が表示されます。 リソースを起動するには、**[すべてのリソース]** タブで通常のアプリと同様にそのリソースを選択します。
