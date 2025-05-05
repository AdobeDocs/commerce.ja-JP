---
title: 入門 [!DNL Adobe Commerce Optimizer]
description: ' [!DNL Adobe Commerce Optimizer] の使用を開始する方法をご覧ください。'
hide: true
recommendations: noCatalog
source-git-commit: d716dd9d75beb642bfad30271b6ecd3490ee7328
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# 入門

>[!NOTE]
>
>このドキュメントでは、早期アクセス開発中の製品について説明しており、一般提供を目的としたすべての機能を反映しているわけではありません。

このガイドでは、 [!DNL Adobe Commerce Optimizer] インスタンスの作成と操作の順を追って説明します。

<!--Click the tabs below to see high-level workflow overviews for the following user types:

- Administrators
- Merchants
- Developers

>[!BEGINTABS]

>[!TAB Administrator and merchant workflow]

This diagram provides a high-level overview of how administrators and merchants access and manage [!DNL Adobe Commerce Optimizer] instances. See the [Adobe Admin Console Guide](https://helpx.adobe.com/jp/enterprise/admin-guide.html) for more information about administrator workflows.

NEED DIAGRAM

>[!TAB Developer workflow]

This diagram provides a high-level overview of how developers create integrations for [!DNL Adobe Commerce Optimizer] using App Builder. See the [API documentation](https://developer.adobe.com/commerce/services/cloud/) for more information.

NEED DIAGRAM

>[!ENDTABS]
-->

## プロビジョニング

[!DNL Adobe Commerce Optimizer]インスタンスの準備が整うと、[!DNL Adobe Commerce Optimizer] プロビジョニング チームによって次のエンドポイントが提供されます。

| アイテム | サンプルURL | 目的 |
|---|---|---|
| [!DNL Adobe Commerce Optimizer] UI | `https://experience.adobe.com/#/@commerceprojectbeacon/commerce-optimizer-studio?tenant=<tenantId>` | Commerce Optimizer UIにアクセスしてカタログを管理する:<br>1. マーチャンダイジングルール(製品ディスカバリー、製品Recommendations)。<br>2. カタログ管理(チャンネルおよびポリシーの作成)。<br>3. データInsights(カタログデータの取得ステータス表示)。 |
| ストアフロント API | `https://na1-sandbox.api.commerce.adobe.com/<tenantId>/graphql` | Edge 配信 サービスを利用したコマースストアフロントの設定に必要な API にアクセスします。 |
| カタログデータ取得 API | `https://na1-sandbox.api.commerce.adobe.com/<tenantId>/v1/catalog/<entity>` | カタログ データの取り込みに必要な API にアクセスします。 |

早期アクセスに参加すると、IMSトークンとともに、 [!DNL Adobe Commerce Optimizer] にログインしたりAPI呼び出しを実行したりできる安全なリンクが記載されたメールが届きます。

## ストアフロントの設定アップ

[!DNL Adobe Commerce Optimizer]インスタンスができたので、Edge 配信 サービスを利用したコマースストアフロントの[設定](./storefront.md)に進む準備が整いました。

## 早期アクセス参加者が利用できるカタログデータ

早期アクセス参加者として、 [!DNL Adobe Commerce Optimizer] インスタンスには [Carveloユースケース](./use-case/admin-use-case.md)に基づく模擬カタログデータが含まれています。 モックデータは、いくつかの事前構成されたチャネルとポリシーとともに、 [!DNL Adobe Commerce Optimizer] UIに慣れるのに役立ちます。

<!--Ingest catalog data

By default, [!DNL Adobe Commerce Optimizer] instances do not include any product data.

See the [Ingestion API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/) documentation to learn how you can import your catalog data into [!DNL Adobe Commerce Optimizer].

The catalog data that you ingest is visible in the [data insights](./insights-overview.md) page. Additionally, you can use the [Catalog](./catalog-overview.md) page to define the channels and policies.-->
