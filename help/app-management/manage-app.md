---
title: アプリを管理
description: App Builder アプリケーションをCommerce インスタンスに関連付け、設定、関連付けを解除します。
feature: App Builder, Extensibility, Integration
source-git-commit: 780cef7af3574cd846fd7ee82d7814f2ebe9d6cc
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---


# アプリを管理

App Managerは、App Builder アプリケーションをCommerce インスタンスに関連付けます。 設定フォームはアプリのスキーマに基づいて動的にレンダリングされるため、カスタムの管理UI開発は必要ありません。 App managerは、Commerceが自動生成するフォームを通じて設定を行います。

![&#x200B; アプリ管理](assets/app-management-view.png){width="500" zoomable="yes"}

## 管理画面でアプリケーションを検索

**[!UICONTROL Apps]** > **[!UICONTROL App Management]**&#x200B;の下では、各アプリケーションがカードとして表示されます。 リストには、選択したAdobe IMS組織のAdobe Commerce インスタンスに関連付けられたすべてのアプリを含めることができます。 カードの上にあるコントロールを使用して、結果を絞り込みます。

| 制御 | 説明 |
| --- | --- |
| **アプリで絞り込む…** | アプリケーション名で検索します。 |
| **ステータス** | ライフサイクルの状態ごとにカードを制限する： **すべてのステータス**&#x200B;はすべてのアプリを表示します。その他の値には、**関連**、**インストール**、**一部インストール**、**関連なし**&#x200B;が含まれます。 各カードのステータスは、リストの色付きインジケーターと一致します。 |
| **拡張性パターン** | アプリが使用する機能によってカードを制限します。 **すべての拡張性パターン**&#x200B;はすべてのアプリを示します。その他の値は、**Business Configuration**、**Admin UI SDK**、**Webhook**、**Events**&#x200B;など、各カードのバッジと一致します。 |

検索テキストと両方のドロップダウンが一緒に適用されます（論理AND）。 完全なリストをもう一度表示するには、**ステータス**&#x200B;と&#x200B;**拡張性パターン**&#x200B;を&#x200B;**すべて…** オプションに戻し、検索フィールドをクリアします。

## アプリを入手

**[!UICONTROL Acquire App]**&#x200B;さんが新しいブラウザータブ （または別のブラウザビュー）を[Adobe Exchange](https://exchange.adobe.com/experiencecloud){target="_blank"}に開き、Commerce関連のマーケットプレイスのリストを見つけて、Adobe IMS組織にアプリケーションを追加できます。 アプリを取得、承認およびデプロイすると、アプリは[!DNL App Management]に[関連付けおよびインストール &#x200B;](#associate-an-app)用に表示されます。

## 前提条件

アプリを関連付ける前に、次の項目を確認してください。

| 要件 | 説明 |
|-------------|-------------|
| **管理者アクセス** | [!DNL App Management]権限を持つCommerce管理者 |
| **アプリをデプロイしました** | App Builder アプリケーションが組織にデプロイされ、接続する準備ができました |
| **組織アクセス** | アプリがデプロイされるAdobe組織へのアクセス |

## チュートリアル

このビデオでは、アプリをCommerce インスタンスに関連付けて設定する方法を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/3478956?captions=jpn)

## アプリの関連付け

関連付けプロセスでは、Commerceからweb サイト、ストア、ストアビューを読み込み、アプリとCommerce インスタンス間のリンクを作成します。

App Builder アプリケーションをCommerce インスタンスにリンクするには：

1. **[!UICONTROL Apps]** > **[!UICONTROL App Management]**&#x200B;に移動します。

1. **[!UICONTROL Associate App]**&#x200B;をクリックします。

   ![&#x200B; アプリの関連付け](assets/associate-app.png){width="500" zoomable="yes"}

1. リストから&#x200B;**[!UICONTROL Project]**&#x200B;を選択します。

1. **[!UICONTROL Workspace]**&#x200B;を選択します。

1. **[!UICONTROL Associate]**&#x200B;をクリックします。

   ![&#x200B; アプリの詳細](assets/app-details.png){width="500" zoomable="yes"}

>[!WARNING]
>
>スコープの同期が失敗しても、関連付けは完了します。 関連付けられたアプリの設定の&#x200B;**[!UICONTROL Manage Scopes]** ビューから、後でスコープを手動で同期できます。

## 設定の設定

[!DNL App Management] ビューでアプリを関連付けた後、次のフォームで設定を行います。

1. 関連付けられたアプリで「**[!UICONTROL Configure]**」をクリックします。

1. フォームには、アプリの設定可能な設定が表示されます。

1. 必要に応じて値を変更します。

1. **[!UICONTROL Save]**&#x200B;をクリックします。

### スコープ固有の設定

さまざまなweb サイト、ストア、ストアビューに一意の設定が必要な場合は、スコープに特化した設定を利用できます。 例えば、特定の地域やストアビューに対してのみ機能を有効にしたり、ブランドごとに異なる設定を使用したりできます。 より低い範囲の設定は、より高い範囲の設定よりも優先されます。

特定の範囲レベルでグローバル値を上書きするには：

1. **[!UICONTROL Change Scope]**&#x200B;をクリックします。

1. リストから範囲を選択します。

1. このスコープの値を変更します。

1. **[!UICONTROL Save]**&#x200B;をクリックします。

## スコープの管理

アプリの詳細画面から&#x200B;**[!UICONTROL Manage Scopes]**&#x200B;にアクセスして、アプリのスコープ階層を管理します。

![&#x200B; スコープの管理](assets/manage-scopes.png){width="500" zoomable="yes"}

| アクション | 説明 |
|--------|-------------|
| **[!UICONTROL Add root scope]** | アプリにのみ適用される範囲を追加します。 |
| **[!UICONTROL Sync Commerce scopes]** | 追加または変更後に、Commerceからweb サイト、ストア、ストアビューのリストを更新します。 |
| **[!UICONTROL Import scopes]** | ファイルからスコープを一括インポートします。 |

## アプリの関連付けを解除

Commerce インスタンスに接続する必要がなくなったアプリの関連付けを解除します。 例えば、統合を廃止する、別のワークスペースに切り替える、テスト設定をクリーンアップする必要があるとします。

>[!WARNING]
>
> 関連付けを解除すると、このインスタンスのすべての設定値が削除されます。 この操作は元に戻せません。

Commerce インスタンスからアプリを削除するには：

1. **[!UICONTROL Apps]** > **[!UICONTROL App Management]**&#x200B;に移動します。

1. アプリで「**[!UICONTROL Unassociate]**」をクリックします。

1. アクションを確認します。

## 関連ドキュメント

* [&#x200B; トラブルシューティング  [!DNL App Management]](troubleshooting.md) - アプリの関連付けと設定に関する一般的な問題を解決します。
