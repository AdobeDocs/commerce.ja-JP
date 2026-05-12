---
title: ストアフロントの設定
description: Edge Delivery Services ストアフロントとAEM Assetsの連携の方法について説明します。
feature: CMS, Media, Integration
TQID: https://experienceleague.adobe.com/gl0Y2UNs3sYkXE9QYwLtAltyX1dxE699y23ey-y0KUU
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 137
ht-degree: 0%

---

# ストアフロントの設定

AEM Assetsとの統合により、Adobe Commerceでホストされている画像を使用する代わりに、AEM Assetsで管理されている商品画像が表示されます。 この統合により、Adobe Content Delivery Network （CDN）を通じた高度な最適化、トリミング、配信など、高度な画像管理機能が可能になります。

Edge Delivery Servicesを利用したCommerce ストアフロントでの統合を有効にするには、ストアフロント設定ファイル （`config.json`）を更新して`"commerce-assets-enabled": true` パラメーターを追加します。

```json
{
  "public": {
    "default": {
      "commerce-assets-enabled": true
    }
  }
}
```

Commerce ドロップインは、`commerce-assets-enabled`設定を自動的に検出し、それに応じて画像の処理を調整します。

Edge Delivery Servicesを搭載したCommerce StorefrontでAEM Assetsを使用する方法について詳しくは、*Adobe Commerce Storefront* ドキュメントの[AEM Assets統合](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/) トピックで説明されているストアフロント設定を完了してください。
