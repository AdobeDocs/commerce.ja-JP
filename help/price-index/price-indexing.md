---
title: SaaS価格インデックス
description: パフォーマンスを向上させるためのSaaS価格インデックスの使用
autotag-review: '2026-06-17T15:08:59.000Z'
seo-title: Adobe SaaS Price Indexing
seo-description: Price indexing give performance improvements using SaaS infrastructure
exl-id: d1bf3879-3e86-4665-a55c-494963c87f90
TQID: https://experienceleague.adobe.com/dfZjgp5wR6H4c7WkNNhjLYUgKNTPIqPWxKiShlTU1yA
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
last-update: 2026-07-29
source-git-commit: 7ce47d7abf7519a7e3ecd436faabf4089005cd63
workflow-type: tm+mt
source-wordcount: 491
ht-degree: 0%

---

# SaaS価格インデックス

SaaS価格インデックス機能は、インデックス作成や価格計算など、リソースを必要とする作業をCommerceアプリケーションからAdobe Cloud インフラストラクチャにオフロードすることで、サイトパフォーマンスを最適化します。 このアプローチにより、リソースを迅速に拡張して、価格インデックス時間を短縮し、ストアフロントやコネクテッドCommerceサービスの価格アップデートをより迅速に提供できるようになります。

次の図は、CommerceがCommerce アプリケーションに含まれる[価格インデックス ](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers) プロセスを使用している場合のSaaS サービスへのデータフローを示しています。

![既定のデータ フロー](assets/old_way.png)

SaaS価格インデックスを有効にすると、データフローが変更されます。 価格インデックス作成は、[Commerce SaaS データ書き出し](../data-export/sync-overview.md)を使用して実行されます。

![SaaS価格インデックス データ フロー](assets/new_way.png)

SaaS価格インデックスを利用すれば、あらゆる販売者がメリットを得られます。次の特徴を持つプロジェクトを運営する販売者は、最大のメリットを享受できます。

* **一定の価格変更** – 頻繁なプロモーション、季節割引、在庫値下げなどの戦略目標を達成するために、繰り返し価格の変更を必要とする販売者。
* **複数のweb サイトまたは顧客グループ** – 複数のweb サイト（ドメイン/ブランド）または顧客グループ間で商品カタログを共有しているマーチャント。
* **Web サイトまたは顧客グループ全体で多くの一意の価格** - Web サイトまたは顧客グループ全体で一意の価格を含む広範な共有製品カタログを持つマーチャント。 たとえば、価格交渉をおこなうB2B企業や、価格戦略が異なる企業などがあります。

## SaaS価格インデックスの利用

Adobe Commerce サービスをインストールすると、SaaS価格インデックスが自動的に有効になります。 すべての組み込みAdobe Commerce製品タイプの価格計算をサポートしています。

### 要件定義

* [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) 2.4.4以降。 詳しくは、[必要システム構成](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/system-requirements){target="_blank"}を参照してください。

### 前提条件

* 次のいずれかのCommerce サービスを、最新バージョンのCommerce拡張機能と共にインストールする必要があります。

  * [カタログサービス](../catalog-service/overview.md)
  * [ライブサーチ](../live-search/overview.md)
  * [商品レコメンデーション](../product-recommendations/guide-overview.md)

>[!NOTE]
>
>必要に応じて、[ カタログ アダプタ ](catalog-adapter.md)を使用して、Commerce アプリケーションのデフォルトの価格インデクサーを無効にすることができます。

## SaaS価格インデックスによる価格の同期

Adobe CommerceのSaaS価格インデックスを有効にした後、新しいフィードを同期して、ストアフロントおよびCommerce サービスで価格を更新します。

```bash
bin/magento saas:resync --feed=scopesCustomerGroup
bin/magento saas:resync --feed=scopesWebsite
bin/magento saas:resync --feed=prices
```

## 同期の進行状況を監視

{{$include /help/_includes/data-export/verify-commerce-service-data-sync.md}}

必要に応じて手動でフィードを再同期するには、[Commerce CLI](../data-export/data-export-cli-commands.md)を使用します。 再同期オプションとその他のトラブルシューティング手順については、_SaaS データ書き出しガイド_&#x200B;の[同期の管理](../data-export/data-sync-manage.md)を参照してください。

>[!NOTE]
>
>Commerce Admin for Commerce on Cloudまたはオンプレミスのデプロイメントで使用できない場合にデータフィードの同期ステータス ページを有効にするには、[拡張機能のインストール手順](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status#install-the-extension)に従います。

## カスタム商品タイプの価格

価格計算は、基本、特殊、グループ、カタログ ルールの価格などのカスタム製品タイプでサポートされています。

特定の数式を使用して最終価格を計算するカスタム製品タイプがある場合は、製品価格フィードの動作を拡張できます。

1. `Magento\ProductPriceDataExporter\Model\Provider\ProductPrice` クラスにプラグインを作成します。

   ```xml
   <config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
       <type name="Magento\ProductPriceDataExporter\Model\Provider\ProductPrice">
           <plugin name="custom_type_price_feed" type="YourModule\CustomProductType\Plugin\UpdatePriceFromFeed" />
       </type>
   </config>
   ```

1. カスタム式を使用してメソッドを作成します。

   ```php
   class UpdatePriceFromFeed
   {
       /**
       * @param ProductPrice $subject
       * @param array $result
       * @param array $values
       *
       * @return array
       */
       public function afterGet(ProductPrice $subject, array $result, array $values) : array
       {
           // Override the output $result with your data for the corresponding products (see original method for details)
           return $result;
       }
   }
   ```
