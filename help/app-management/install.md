---
title: インストールしてアクセス  [!DNL App Management]
description: Adobe Commerce [!DNL App Management] を使用するための前提条件とアクセス要件。
feature: App Builder, Extensibility, Integration
source-git-commit: ab635fecb7b82294bd4a4fd045ed71931e9d265d
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

---

# [!DNL App Management] のインストールとアクセス

[!DNL App Management] は、対象となるCommerce インスタンスのCommerce管理者で利用できます。 使用できるかどうかは、デプロイメントタイプによって異なります。

## 対象

次の要件を満たした後、以下のデプロイメントタイプに対応するタブを選択し、インストールが必要かどうか、[!DNL App Management] れがお使いのインスタンスで既に使用可能かどうかを確認します。

## 前提条件

アプリを関連付ける前に、次の点を確認します。

| 要件 | 説明 |
|-------------|-------------|
| **管理者アクセス** | [!DNL App Management] 権限を持つCommerce管理者 |
| **デプロイされたアプリ** | App Builder アプリケーションが組織にデプロイされ、接続する準備が整いました |
| **組織アクセス** | アプリケーションがデプロイされているAdobe組織にアクセスします。 |

>[!BEGINTABS]

>[!TAB Adobe Commerceas a Cloud Service]

[!DNL App Management] は [!DNL Adobe Commerce as a Cloud Service] で自動的に使用可能になります。 インストールは不要です。 [&#x200B; 管理者で有効にします &#x200B;](#access-app-management) アプリの関連付けを開始します。

>[!TAB Adobe Commerce on Cloud （PaaS）およびオンプレミス ]

* **Adobe Commerce 2.4.8 以降** - [!DNL App Management] が自動的に含まれます。 インストールは不要です。

* **Adobe Commerce 2.4.5 ～ 2.4.7** - Composer を使用して [!DNL Admin UI SDK] （[!DNL App Management] を含む）をインストールします。

  ```bash
  composer require "magento/commerce-backend-sdk": ">=3.3"
  ```

  次を実行します。

  ```bash
  composer update
  bin/magento setup:upgrade
  bin/magento indexer:reindex
  bin/magento cache:clean
  ```

詳しくは、[Adobe Commerce管理 UI SDKのインストールまたは更新 &#x200B;](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/installation/){target="_blank"} を参照してください。

>[!ENDTABS]

## アクセス [!DNL App Management]

1. Commerce Admin にログインします。

1. **[!UICONTROL Apps]**/**[!UICONTROL App Management]** に移動します。

[!DNL App Management] ビューが表示されます。 ここでは、App Builder アプリケーションを関連付け、設定および管理できます。

## App Builder アプリのインストール

Adobe ExchangeからApp Builder アプリ（事前定義済みの統合や Marketplace アプリなど）をインストールする必要がある場合は、[Adobe ExchangeからのApp Builder アプリのインストール &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-learn/tutorials/adobe-developer-app-builder/install-app-builder-app){target="_blank"} を参照してください。

アプリケーションをインストールしてデプロイした後、[!DNL App Management] を使用して [Commerce インスタンスに関連付け &#x200B;](manage-app.md#associate-an-app) 設定を行います。
