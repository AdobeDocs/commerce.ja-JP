---
title: ストアフロントの設定
description: Edge Delivery Services ストアフロントをAEM Assets統合に接続する方法について説明します。
feature: CMS, Media, Integration
source-git-commit: d426c7878f7a66fe1047673be7c5bf65ae1949a7
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# ストアフロントの設定

AEM Assets統合では、Adobe Commerceでホストされている画像を使用する代わりに、AEM Assetsで管理されている製品画像が表示されます。 この統合により、Adobeのコンテンツ配信ネットワーク（CDN）を介した高度な最適化、切り抜き、配信などの画像管理機能が強化されます。

Edge Delivery Servicesを使用したCommerce ストアフロントの統合を有効にするには、ストアフロント設定ファイル（`config.json`）を更新して、`"commerce-assets-enabled": true` パラメーターを追加します。

```json
{
  "public": {
    "default": {
      "commerce-assets-enabled": true
    }
  }
}
```

Commerceのドロップダウンが `commerce-assets-enabled` 設定を自動的に検出し、それに応じて画像処理を調整します。

Edge Delivery Servicesを利用したCommerce Storefront でAEM Assetsを使用する方法について詳しくは、[Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/) ドキュメントの *AEM Assetsの統合* に関するトピックに記載されているストアフロント設定を完了してください。
