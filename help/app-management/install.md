---
title: インストールして [!DNL App Management]にアクセス
description: Adobe Commerce [!DNL App Management]を使用するための前提条件とアクセス要件。
feature: App Builder, Extensibility, Integration
source-git-commit: 86c0945bbb0a562de1b66d420dec2a05d4d81e5f
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# [!DNL App Management]をインストールしてアクセス

[!DNL App Management]は、適格なCommerce インスタンスのCommerce Adminで利用できます。 ご利用いただけるかどうかは、デプロイメントタイプによって異なります。

## 対象

次の要件を満たしたら、以下のデプロイメントタイプに対応するタブを選択して、[!DNL App Management]がインストールを必要としているか、インスタンスで既に使用可能かどうかを確認します。

## 前提条件

アプリを関連付ける前に、次の項目を確認してください。

| 要件 | 説明 |
|-------------|-------------|
| **管理者アクセス** | [!DNL App Management]権限を持つCommerce管理者 |
| **アプリをデプロイしました** | App Builder アプリケーションが組織にデプロイされ、接続する準備ができました |
| **組織アクセス** | アプリがデプロイされるAdobe組織へのアクセス |

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

[!DNL App Management]は[!DNL Adobe Commerce as a Cloud Service]に自動的に利用できます。 インストールは必要ありません。 [管理者](#access-app-management)で有効にし、アプリの関連付けを開始します。

>[!TAB Adobe Commerce on Cloud （PaaS）およびオンプレミス ]

* **Adobe Commerce 2.4.8以降**—[!DNL App Management]が自動的に含まれます。 インストールは必要ありません。

* **Adobe Commerce 2.4.5から2.4.7** - Composerを使用して[!DNL Admin UI SDK] （[!DNL App Management]を含む）をインストールします。

  ```bash
  composer require "magento/commerce-backend-sdk": ">=3.3"
  ```

  次に実行：

  ```bash
  composer update
  bin/magento setup:upgrade
  bin/magento indexer:reindex
  bin/magento cache:clean
  ```

詳しくは、[Adobe Commerce管理UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/installation/){target="_blank"}のインストールまたは更新を参照してください。

>[!ENDTABS]

## [!DNL App Management]へのアクセス

1. Commerce Adminにログインします。

1. **[!UICONTROL Apps]** > **[!UICONTROL App Management]**&#x200B;に移動します。

[!DNL App Management] ビューが表示されます。 ここでは、App Builder アプリケーションを関連付け、設定および管理できます。

## App Builder アプリのインストール

Adobe ExchangeからApp Builder アプリをインストールする必要がある場合（事前定義済みの統合アプリやマーケットプレイスアプリなど）、ステップバイステップの手順については、[Adobe ExchangeからApp Builder アプリをインストール &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-learn/tutorials/adobe-developer-app-builder/install-app-builder-app){target="_blank"}を参照してください。

アプリをインストールしてデプロイしたら、[!DNL App Management]を使用して[Commerce インスタンスに関連付け](manage-app.md#associate-an-app)し、設定を行います。

## CommerceのWebhookとアプリ

一部のApp Builder アプリケーションでは、[Adobe Commerce Webhook](https://developer.adobe.com/commerce/extensibility/webhooks/)を使用して、特定のイベントが発生した場合（商品が保存された後など）にCommerceからHTTP経由でアプリを呼び出すことができます。 Webhook エンドポイントとサブスクリプション ロジックは、アプリケーションのビルドおよびデプロイ時に&#x200B;**アプリ開発者**&#x200B;によって定義されます。ストア管理者は、アプリ管理でWebhookを個別に設定しません。

アプリを[Commerce インスタンスに関連付け](https://experienceleague.adobe.com/ja/docs/commerce/app-management/manage-app/manage-app)し、アプリの設定手順を完了すると、Webhookの動作はアプリの実装に従います。

[!DNL App Management]がアプリの検証エンドポイントをトリガーできない場合（例えば、URLに到達できない、または回答が要件を満たさない）、[!DNL App Management] ダッシュボードに次のようなエラーが表示される可能性があります。

![Webhook検証エラー](assets/webhook-validation-error.png){width="600" zoomable="yes"}

**アプリ開発者**&#x200B;と協力して、Webhookの設定またはデプロイメントを修正し、検証を成功させることができます。

**アプリ開発者**。 App BuilderからWebhook サブスクリプションとハンドラー応答を実装するには、Commerce拡張性開発者ドキュメントの[Webhook](https://developer.adobe.com/commerce/extensibility/app-management/installation/webhooks/)とGitHubの[`@adobe/aio-commerce-lib-webhooks`](https://github.com/adobe/aio-commerce-sdk/tree/main/packages/aio-commerce-lib-webhooks) パッケージを参照してください。
