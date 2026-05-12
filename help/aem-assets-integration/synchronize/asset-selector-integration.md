---
title: アセットの手動選択
description: Commerceに統合されたAEM Asset Selectorを利用して、マーケターやマーチャンダイジング担当者がAEM Assetsの画像をAdobe Commerceに簡単に追加し、アセット管理を効率化する方法をご確認ください。
feature: CMS, Media, Integration
exl-id: 3c1f906f-3ec3-4eac-a47e-b21792767359
TQID: https://experienceleague.adobe.com/3fYabUvRiY8KTxQX1YiTBbLxABpQqfZLu0a6IBDsM3E
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: da3860b0-d637-47df-bef0-273751180266
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 396
ht-degree: 0%

---

# アセットの手動選択

**AEM Asset Selector**&#x200B;を使用すると、マーケターやマーチャンダイザーは、AEM AssetsからAdobe Commerceに画像を簡単に追加できるので、アセット管理プロセスが効率化されます。 この方法は、アセットの選択を[!DNL DAM (Digital Asset Management system)]でレビューおよび承認されたアセットに制限することで、ブランドの一貫性とコンプライアンスを確保します。

**AEM Asset Selector**&#x200B;は、AEM Assets プロジェクトのIMS クライアント IDがCommerce管理者で設定されており、ユーザーが必要な[権限とIMS認証](../get-started/permissions.md)を持っている場合に使用できます。 [AEM Asset Selectorの設定](#configure-the-aem-asset-selector-in-adobe-commerce)を参照してください。

**AEM Asset Selector**&#x200B;統合が設定されると、マーケターとマーチャンダイザーは次のことが可能になります。

* カテゴリー画像を容易に管理し、ブランドとキャンペーンのガイドラインに沿ったものにできます。
* [!BADGE PaaSのみ]{type=Informative tooltip="Cloud プロジェクト上のAdobe Commerce（Adobeで管理されるPaaS インフラストラクチャ）にのみ適用されます。"} ページビルダーで直接アセットを割り当てて、視覚的に充実したコンテンツを提供します。
* [!BADGE SaaSのみ]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"} Edge Delivery Servicesを活用したCommerce Storefrontで直接Assetsを割り当てて、視覚的に充実したコンテンツを提供します。

>[!NOTE]
>
> AEM Asset Selectorは、AEMとオーサリングアプリケーションを統合するためのAEM Assets Assets フロントエンドコンポーネントです。 このコンポーネントについて詳しくは、*AEM as a Cloud Service ユーザーガイド*&#x200B;の[&#x200B; マイクロフロントエンドアセットセレクター](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector){target=_blank}を参照してください。

## 主な特長

Adobe Commerce管理パネルにAEM Asset Selectorを組み込むと、次のような主な利点が得られます。

* **ブランドの一貫性** – 承認済みアセットのみを表示し、ストアフロントで古い画像やコンプライアンスに準拠していない画像が表示されるリスクを最小限に抑えます。

* **効率性** – マーケターとマーチャンダイザーは、異なるプラットフォームを切り替えることなく、アセットをすばやく割り当てることができます。

* **合理化されたCollaboration** - DAMから直接画像を選択できるようにし、手動でのダウンロードやアップロードを排除することで、シームレスなチームワークを促進します。

* **コンテンツ品質の向上** – 製品ページ、カテゴリ、ページビルダー全体で、高解像度で最適化された画像を使用します。

![&#x200B; アセットセレクター](../assets/asset-selector.png){width="600" zoomable="yes"}

## Adobe CommerceでのAEM Asset Selectorの設定

1. Commerce管理者から、**[!UICONTROL Store]** / 設定/ **[!UICONTROL ADOBE SERVICES]** / **[!UICONTROL AEM Assets Integration]**&#x200B;に移動します。

1. **[!UICONTROL IMS Client ID]** フィールドに入力します。 必要な権限と、このIDの取得方法については、[&#x200B; ユーザー権限とIMS](../get-started/permissions.md)を参照してください。

1. **設定を保存**&#x200B;します。

## 次のステップ

* [アセットセレクターでカテゴリ画像を管理](../manage-assets.md#category-images)
* [ページビルダーコンテンツでの画像の管理](../manage-assets.md#using-aem-asset-selector-in-page-builder)
