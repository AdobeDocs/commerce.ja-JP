---
title: ' [!DNL Adobe Commerce Optimizer] の基本を学ぶ'
description: ' [!DNL Adobe Commerce Optimizer] の使用を開始する方法について説明します。'
hide: true
recommendations: noCatalog
exl-id: de57d93d-e156-45c1-86aa-de29a8c34bd2
source-git-commit: 9c3f5d1d5e7fd57d2306502d654a854bc5c66c71
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# はじめに

>[!NOTE]
>
>このドキュメントでは、製品の早期アクセス開発について説明しており、一般提供を目的とした機能のすべてを反映しているわけではありません。

このガイドでは、[!DNL Adobe Commerce Optimizer] インスタンスの作成と操作について説明します。

<!--Click the tabs below to see high-level workflow overviews for the following user types:

- Administrators
- Merchants
- Developers

>[!BEGINTABS]

>[!TAB Administrator and merchant workflow]

This diagram provides a high-level overview of how administrators and merchants access and manage [!DNL Adobe Commerce Optimizer] instances. See the [Adobe Admin Console Guide](https://helpx.adobe.com/jp/enterprise/admin-guide.html) for more information about administrator workflows.

NEED DIAGRAM

>[!TAB Developer workflow]

This diagram provides a high-level overview of how developers create integrations for [!DNL Adobe Commerce Optimizer] using App Builder. See the [API documentation](https://developer.adobe.com/commerce/webapi/rest/) for more information.

NEED DIAGRAM

>[!ENDTABS]
-->

## プロビジョニング

[!DNL Adobe Commerce Optimizer] インスタンスの準備が整うと、[!DNL Adobe Commerce Optimizer] プロビジョニングチームは次のエンドポイントを提供します。

| 項目 | サンプル URL | 目的 |
|---|---|---|
| [!DNL Adobe Commerce Optimizer] UI | `https://experience.adobe.com/#/@commerceprojectbeacon/commerce-optimizer-studio?tenant=<tenantId>` | Commerce Optimizer UI にアクセスして、<br>1 の間でカタログを管理します。 マーチャンダイジングルール （製品検出、製品レコメンデーション）。<br>2。 カタログ管理（チャネルとポリシーの作成）。<br>3。 データインサイト （カタログデータ取り込みステータスを表示）。 |
| ストアフロント API | `https://na1-sandbox.api.commerce.adobe.com/<tenantId>/graphql` | Edge Delivery Servicesを活用したCommerce ストアフロントの設定に必要な API にアクセスします。 |
| カタログデータ取得 API | `https://na1-sandbox.api.commerce.adobe.com/<tenantId>/v1/catalog/<entity>` | カタログデータの取り込みに必要な API にアクセスします。 |

>[!NOTE]
>
>ストアフロントの設定とカタログの取り込みに必要な API について詳しくは、[ 開発者向けドキュメント ](https://developer-stage.adobe.com/commerce/services/composable-catalog/) を参照してください。

早期アクセス参加者には、IMS トークンと共に、[!DNL Adobe Commerce Optimizer] にログインするか API 呼び出しを行うためのセキュアリンクが記載されたメールが届きます。

## ストアフロントの設定

これで [!DNL Adobe Commerce Optimizer] インスタンスが作成されたので、Edge Delivery Servicesを使用したCommerce Storefront の [ 設定 ](./storefront.md) を続行する準備が整いました。

## 早期アクセス参加者向けに利用可能なカタログデータ

早期アクセス参加者の場合、[!DNL Adobe Commerce Optimizer] インスタンスには [Carvelo ユースケース ](./use-case/admin-use-case.md) に基づくモックカタログデータが含まれます。 モックデータは、事前設定済みのチャネルとポリシーと共に、[!DNL Adobe Commerce Optimizer] UI に慣れるのに役立ちます。

<!--Ingest catalog data

By default, [!DNL Adobe Commerce Optimizer] instances do not include any product data.

See the [Ingestion API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/) documentation to learn how you can import your catalog data into [!DNL Adobe Commerce Optimizer].

The catalog data that you ingest is visible in the [data insights](./insights-overview.md) page. Additionally, you can use the [Catalog](./catalog-overview.md) page to define the channels and policies.-->
