---
title: リリースノート
description: ' [!DNL Adobe Commerce Optimizer]の最新のリリース情報。'
role: Admin, Developer, User, Leader
recommendations: noCatalog
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよび [!DNL Adobe Commerce Optimizer]  プロジェクトにのみ適用されます（Adobeで管理されるSaaS インフラストラクチャ）。"
exl-id: e420d461-9ea2-4e32-aa37-230b14a297d7
source-git-commit: d0967674d05018f13dc6c8a562005d65d44e42ab
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---

# リリースノート

次のリリースノートには、[!DNL Adobe Commerce Optimizer]の更新が含まれています。

## 2026年4月

**リリース日**: 2026年4月7日

>[!BEGINSHADEBOX]

### カタログルール

マーチャンダイジングルールに[&#x200B; カテゴリルール &#x200B;](./merchandising/rules/add.md)が含まれるようになりました。これにより、検索と同じインテリジェントなランキングと手動アクション（ピン、ブースト、埋め込み）を使用して、1つ以上のカテゴリをターゲットにして、カテゴリページ上の商品の順序を制御できます。

### 価格フィルター

レコメンデーションフィルターは、商品の最低価格帯と最高価格帯の設定に使用できる[価格フィルター](./merchandising/recommendations/filters.md#price)をサポートするようになりました。

### その他のリリースノート

[!DNL Adobe Commerce Optimizer]は、AEM Assets統合の最新リリース、Commerce Optimizer コネクタ、および[!DNL Adobe Commerce Storefront]で動作します。 以下のリンクを使用して、各領域のリリースノートを表示します。

| 拡張機能 | ストアフロント |
| --- | --- |
| [AEM Assetsとの統合](../aem-assets-integration/release-notes.md)<br>[Commerce Optimizer コネクタ &#x200B;](../aco-connector/release-notes.md) | [&#x200B; ストアフロントのリリース情報](https://experienceleague.adobe.com/developer/commerce/storefront/releases/)<br>[&#x200B; ストアフロントの変更履歴](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/) |

>[!ENDSHADEBOX]

## 2026年2月

**リリース日**: 2026年2月19日

>[!BEGINSHADEBOX]

レコメンデーションユニットを[作成](./merchandising/recommendations/create.md)または[&#x200B; マーチャンダイジングルール &#x200B;](./merchandising/rules/add.md)するときに、カタログビューを指定する機能を追加しました。

### その他のリリースノート

[!DNL Adobe Commerce Optimizer]は、AEM Assets統合の最新リリース、Commerce Optimizer コネクタ、および[!DNL Adobe Commerce Storefront]で動作します。 以下のリンクを使用して、各領域のリリースノートを表示します。

| 拡張機能 | ストアフロント |
| --- | --- |
| [AEM Assetsとの統合](../aem-assets-integration/release-notes.md)<br>[Commerce Optimizer コネクタ &#x200B;](../aco-connector/release-notes.md) | [&#x200B; ストアフロントのリリース情報](https://experienceleague.adobe.com/developer/commerce/storefront/releases/)<br>[&#x200B; ストアフロントの変更履歴](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/) |

>[!ENDSHADEBOX]

## 2025年12月

**リリース日**: 2025年12月10日

>[!BEGINSHADEBOX]

### 機会

AIを活用したサイト最適化のレコメンデーションは、[Adobe Sites Optimizerとの統合](./manage-results/opportunities.md)を通じて利用できるようになりました。 この機能は、自動検出とインテリジェントなレコメンデーションにより、マーチャンダイジング担当者がコマースサイトのパフォーマンスに影響を与える問題を特定し、対処するのに役立ちます。

### カタログレイヤー

[&#x200B; カタログレイヤー](./setup/catalog-layer.md)を追加しました。これにより、レイヤーの優先度管理やAdobe Sites Optimizerの自動修正機能との統合など、ソースデータを変更せずに商品データを変更できます。

### その他のリリースノート

[!DNL Adobe Commerce Optimizer]は、AEM Assets統合の最新リリース、Commerce Optimizer コネクタ、および[!DNL Adobe Commerce Storefront]で動作します。 以下のリンクを使用して、各領域のリリースノートを表示します。

| 拡張機能 | ストアフロント |
| --- | --- |
| [AEM Assetsとの統合](../aem-assets-integration/release-notes.md)<br>[Commerce Optimizer コネクタ &#x200B;](../aco-connector/release-notes.md) | [&#x200B; ストアフロントのリリース情報](https://experienceleague.adobe.com/developer/commerce/storefront/releases/)<br>[&#x200B; ストアフロントの変更履歴](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/) |

>[!ENDSHADEBOX]

## 2025年10月

**リリース日**: 2025年10月14日

>[!BEGINSHADEBOX]

### Commerce Optimizer Salesforce Commerce Connector

[!DNL Commerce Optimizer Salesforce Commerce Connector]は、Commerce管理者と開発者がSalesforce B2C Commerce カタログ データを[!DNL Commerce Optimizer]とシームレスに接続できるようにする新しいApp Builder統合スターターキットです。<!--COMOPT-536-->

**管理者向け：**

* Salesforceでカタログを更新すると（商品、価格、メタデータ、価格表）、Commerce Optimizerと自動的に同期されるため、手作業の余地はありません。
* この統合は、Adobe Commerceとは独立して動作するため、複雑さや潜在的な障害点を減らすことができます。
* 管理者は、定期的なスケジュール更新を活用して、Commerce Optimizer内の正確なカタログデータを確保し、マーチャンダイジングと商品レコメンデーションを強化することができます。

**開発者向け：**

* スターターキットは、Salesforce カタログデータをSaaS マーチャンダイジングサービスに取り込むための、合理化された拡張可能なフレームワークを提供します。
* カスタム統合やトラブルシューティングを高速化するために、参照実装、設計ドキュメント、コードサンプルを利用できます。<!--COMOPT-536-->

### 階層検索

* 次の高度な検索機能のGA リリース：`startsWith`と`contains`を使用した階層検索。 [学習を増やす](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#layered-search-and-expansion-of-search-types)。

### カテゴリ API

新しいカテゴリ REST APIが利用可能になり、管理者と開発者は、ナビゲーションと製品グループ化のために複数のカテゴリーツリーをプログラムで作成、更新、管理できるようになりました。 このAPIは、グローバル設定とチャネル固有の設定の両方をサポートし、高い拡張性を実現するように設計されており、1つのツリーにつき最大10,000個のカテゴリーツリーと500個のカテゴリーをサポートできます。 詳しくは、[&#x200B; マーチャンダイジングサービス開発者ガイド &#x200B;](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#categories)の&#x200B;_カテゴリー_&#x200B;を参照してください。<!--DCAT-2649-->

### その他のリリースノート

[!DNL Adobe Commerce Optimizer]は、AEM Assets統合の最新リリース、Commerce Optimizer コネクタ、および[!DNL Adobe Commerce Storefront]で動作します。 以下のリンクを使用して、各領域のリリースノートを表示します。

| 拡張機能 | ストアフロント |
| --- | --- |
| [AEM Assetsとの統合](../aem-assets-integration/release-notes.md)<br>[Commerce Optimizer コネクタ &#x200B;](../aco-connector/release-notes.md) | [&#x200B; ストアフロントのリリース情報](https://experienceleague.adobe.com/developer/commerce/storefront/releases/)<br>[&#x200B; ストアフロントの変更履歴](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/) |

>[!ENDSHADEBOX]

## 2025年8月

**リリース日**: 2025年8月28日

>[!BEGINSHADEBOX]

### EU地域が利用可能になりました

お客様のIMS組織に対する欧州連合地域（eu1）のサポートが利用可能になりました。 Cloud Managerで&#x200B;**Commerce Optimizer インスタンス**&#x200B;を追加すると、**欧州連合**&#x200B;を[地域](./get-started.md#step-1-create-an-instance)として選択できるようになりました。 欧州連合の地域は、実稼動環境でのみ使用できます。

欧州連合リージョンのベースの本番URLは次のとおりです。

* 管理者：`https://eu1.admin.commerce.adobe.com`
* RESTとGraphQL: `https://eu1.api.commerce.adobe.com`

![&#x200B; インスタンスを作成](./assets/create-instance.png){width="600" align="center" zoomable="yes"}

### その他のリリースノート

[!DNL Adobe Commerce Optimizer]は、AEM Assets統合の最新リリース、Commerce Optimizer コネクタ、および[!DNL Adobe Commerce Storefront]で動作します。 以下のリンクを使用して、各領域のリリースノートを表示します。

| 拡張機能 | ストアフロント |
| --- | --- |
| [AEM Assetsとの統合](../aem-assets-integration/release-notes.md)<br>[Commerce Optimizer コネクタ &#x200B;](../aco-connector/release-notes.md) | [&#x200B; ストアフロントのリリース情報](https://experienceleague.adobe.com/developer/commerce/storefront/releases/)<br>[&#x200B; ストアフロントの変更履歴](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/) |

>[!ENDSHADEBOX]
