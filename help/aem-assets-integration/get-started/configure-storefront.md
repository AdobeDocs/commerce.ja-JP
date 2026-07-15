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
source-git-commit: 7f901cec90291e264376e3f93e6ebaaccf7c15f0
workflow-type: tm+mt
source-wordcount: 610
ht-degree: 0%

---

# ストアフロントの設定

## AEM Assetsから商品画像表示を有効にする {#enable-product-images}

AEM Assetsとの統合により、Adobe CommerceではなくAEM Assetsから製品画像が表示され、高度な最適化、トリミング、CDN配信が可能になります。

Edge Delivery Servicesを利用したCommerce ストアフロントでの統合を有効にするには、ストアフロント設定ファイル （`config.json`）に`"commerce-assets-enabled": true` パラメーターを追加します。

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

Edge Delivery Servicesを搭載したCommerce StorefrontでAEM Assetsを使用する方法について詳しくは、*AEM Assets Storefront* ドキュメントの[Adobe Commerce統合](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/?lang=ja) トピックを参照してください。

>[!TIP]
>
>作成者がAEM Assetsを参照して静的コンテンツページに挿入できるようにするには、[静的コンテンツオーサリング用にAEM AssetsをDa.liveに接続](#connect-aem-assets-authoring)するを参照してください。

## AEM AssetsをDa.liveに接続して静的コンテンツを作成 {#connect-aem-assets-authoring}

>[!NOTE]
>
>この設定は、AEM Assets Integration拡張機能とは別のものです。 [Da.live](https://da.live){target="_blank"}によって提供され、作成者は[!UICONTROL Library] パネルと[!UICONTROL Content Advisor]を通じて、AEM Assetsを参照し、静的コンテンツページ（ランディングページやコンテンツブロックなど）に挿入できます。 AEM Assets統合を通じて同期された製品画像は、`commerce-assets-enabled`設定を使用して個別に設定されます。

次の手順を使用して、AEM AssetsをDocument Authoring （Da.live）ストアフロントに接続し、作成者が静的コンテンツの編集中に&#x200B;**[!UICONTROL Content Advisor]**&#x200B;からAEM Assetsを参照して挿入できるようにします。

>[!NOTE]
>
>設定の手順について詳しくは、Da.live ドキュメントの[AEM Assetsの設定](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank}を参照し、[AEM Assets ドキュメントのEdge Delivery Servicesのコンテンツのオーサリング中にAEM Assetsを統合する](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/integrate-aem-assets-edge-delivery-services/integrate-aem-assets-edge-delivery-services){target=_blank}を参照してください。

### 手順1:Da.liveでサイト設定を開く

1. [Da.live](https://da.live){target=_blank}から、ストアフロントを探して開きます。

1. パンくずナビゲーションで、サイト名の横にある&#x200B;**[!UICONTROL Settings]** アイコンを選択して、サイト設定スプレッドシートを開きます。

### 手順2:AEM リポジトリ URLをコピーする

1. 新しいタブで、[experience.adobe.com](https://experience.adobe.com){target=_blank}に移動し、**[!UICONTROL Experience Manager]**&#x200B;に移動します。

1. Adobe Experience Manager Assetsを開く：**[!UICONTROL My Authoring]** セクションまでスクロールし、**[!UICONTROL Production]**&#x200B;環境の横にある&#x200B;**[!UICONTROL Assets]**&#x200B;を選択します。

1. ブラウザーのアドレスバーから、`author`から`.com`までのセグメント（例：`author-p107634-e1009805.adobeaemcloud.com`）をコピーします。

### 手順3：リポジトリ IDを設定に追加する

1. サイトを設定するには、Da.liveに戻り、サイト設定で「**[!UICONTROL data]**」を選択します。

1. 次のようにスプレッドシートを完成させます。

   | セル | 値 |
   |---|---|
   | A1 | `key` |
   | B1 | `value` |
   | A2 | `aem.repositoryId` |
   | B2 | 手順2でコピーしたURL |

1. 「**[!UICONTROL Save]**」を選択し、サイト名の横にある後方矢印を選択して、サイトのルートに戻ります。

   >[!NOTE]
   >
   > 接頭辞が`author-`のホストは、オーサー層からアセットを参照します。 代わりに、`delivery-`接頭辞を付けたホストを使用して、Dynamic Mediaを通じてアセットを配信します。 すべての`aem.repositoryId` オプションについては、[AEM Assetsの設定](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank}を参照してください。

### 手順4：ライブラリを介したAEM Assetsの接続

1. サイト ルートから、**[!UICONTROL index]** フォルダーを選択して開きます。

1. エディターで&#x200B;**[!UICONTROL Library]** パネルを開き、**[!UICONTROL AEM Assets]**&#x200B;を選択します。

   **[!UICONTROL Content Advisor]** ポップオーバーが開き、AEM Assets フォルダーとファイルが表示されます。

これで、ストアフロントとAEM Assetsが接続されました。 **[!UICONTROL Content Advisor]**&#x200B;から直接アセットを参照して挿入できます。

## 関連ドキュメント

* *AEM Assets Storefront* ドキュメントの[Adobe Commerce統合](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/?lang=ja){target=_blank} - ストアフロントの設定とイメージ処理の動作。

* [AEM Assetsを統合して、Edge Delivery Services](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/integrate-aem-assets-edge-delivery-services/integrate-aem-assets-edge-delivery-services){target=_blank}のコンテンツをオーサリングします（*AEM Assets* ドキュメント）。

* Da.live ドキュメントの[AEM Assets](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank}と[&#x200B; メディアの操作](https://docs.da.live/authors/guides/adding-media){target=_blank}を設定します。
