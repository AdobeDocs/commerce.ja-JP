---
title: アプリの管理
description: App Builder アプリケーションとCommerce インスタンスの関連付け、設定、関連付け解除を行います。
feature: App Builder, Extensibility, Integration
source-git-commit: ab635fecb7b82294bd4a4fd045ed71931e9d265d
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---


# アプリの管理

App Manager は、App Builder アプリケーションをCommerce インスタンスに関連付けます。 設定フォームは、アプリのスキーマに基づいて動的にレンダリングされるので、カスタムの管理 UI 開発は必要ありません。 App Manager は、Commerceが自動生成するフォームを使用して設定を行います。

![&#x200B; アプリ管理 &#x200B;](assets/app-management-ui.png){width="500" zoomable="yes"}

## 前提条件

アプリを関連付ける前に、次の点を確認します。

| 要件 | 説明 |
|-------------|-------------|
| **管理者アクセス** | [!DNL App Management] 権限を持つCommerce管理者 |
| **デプロイされたアプリ** | App Builder アプリケーションが組織にデプロイされ、接続する準備が整いました |
| **組織アクセス** | アプリケーションがデプロイされているAdobe組織にアクセスします。 |

## チュートリアル

アプリをCommerce インスタンスに関連付けて設定する方法については、このビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3478956?captions=jpn)

## アプリの関連付け

関連付けプロセスは、Commerceから web サイト、ストア、ストアビューを読み込み、アプリとCommerce インスタンスの間にリンクを作成します。

App Builder アプリケーションをCommerce インスタンスにリンクするには：

1. **[!UICONTROL Apps]**/**[!UICONTROL App Management]** に移動します。

1. 「**[!UICONTROL Associate App]**」をクリックします。

   ![&#x200B; アプリを関連付ける &#x200B;](assets/associate-app.png){width="500" zoomable="yes"}

1. リストから **[!UICONTROL Project]** を選択します。

1. **[!UICONTROL Workspace]** を選択します。

1. 「**[!UICONTROL Associate]**」をクリックします。

   ![&#x200B; アプリの詳細 &#x200B;](assets/app-details.png){width="500" zoomable="yes"}

>[!WARNING]
>
>スコープの同期に失敗しても、関連付けは完了します。 後で、関連するアプリの設定の **[!UICONTROL Manage Scopes]** ビューから範囲を手動で同期できます。

## 設定

[!DNL App Management] ビューでアプリを関連付けた後、フォームを使用して設定を指定します。

1. 関連するアプリで **[!UICONTROL Configure]** をクリックします。

1. フォームに、アプリの設定可能な設定が表示されます。

1. 必要に応じて値を変更します。

1. 「**[!UICONTROL Save]**」をクリックします。

### スコープ固有の設定

様々な web サイト、ストアまたはストアビューで一意の設定が必要な場合は、範囲固有の設定を使用します。 例えば、特定の地域またはストア表示に対してのみ機能を有効にするか、ブランドごとに異なる設定を使用します。 下位スコープの設定は、上位スコープの設定よりも優先されます。

特定のスコープ レベルでグローバル値を上書きするには：

1. 「**[!UICONTROL Change Scope]**」をクリックします。

1. リストから範囲を選択します。

1. このスコープの値を変更します。

1. 「**[!UICONTROL Save]**」をクリックします。

## 範囲の管理

アプリの詳細画面から **[!UICONTROL Manage Scopes]** にアクセスして、アプリの範囲階層を管理します。

![&#x200B; 範囲の管理 &#x200B;](assets/manage-scopes.png){width="500" zoomable="yes"}

| アクション | 説明 |
|--------|-------------|
| **[!UICONTROL Add root scope]** | アプリにのみ適用される範囲を追加します。 |
| **[!UICONTROL Sync Commerce scopes]** | Web サイト、ストア、ストアビューのリストを追加または変更した後に、Commerceからリストを更新します。 |
| **[!UICONTROL Import scopes]** | ファイルからスコープを一括でインポートします。 |

## アプリの関連付けを解除する

Commerce インスタンスへの接続が不要になったら、アプリの関連付けを解除します。 例えば、統合を廃止したり、別のワークスペースに切り替えたり、テスト設定をクリーンアップしたりする必要がある場合があります。

>[!WARNING]
>
> 関連付けを解除すると、このインスタンスのすべての設定値が削除されます。 これは元に戻すことができません。

Commerce インスタンスからアプリを削除するには：

1. **[!UICONTROL Apps]**/**[!UICONTROL App Management]** に移動します。

1. アプリの「**[!UICONTROL Unassociate]**」をクリックします。

1. アクションを確認します。

## 関連ドキュメント

* [&#x200B; トラブルシューティング  [!DNL App Management]](troubleshooting.md) - アプリの関連付けと設定に関する一般的な問題を解決します。
