---
title: Commerce向けAEM Assets統合
description: Adobe Experience Manager Assetsを [!DNL Commerce]  インスタンスと統合して、Commerce ストアフロントのメディアファイルを作成および管理する方法について説明します。
feature: CMS, Media, Configuration, Integration
exl-id: f450752a-bef1-419e-ad14-ff8879ab204b
TQID: https://experienceleague.adobe.com/CTDmM7Ox2rQ-55F1BVTg-C8DPBEuEpzFxXGtWpnjXKs
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: e91a50b1-0b31-436e-9033-00e4776e94cb
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: da3860b0-d637-47df-bef0-273751180266
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: e631346aa13737ded2c14daecbb91457e15417eb
workflow-type: tm+mt
source-wordcount: 805
ht-degree: 1%

---

# Commerce向けAEM Assets統合

マーケティング予算がプレッシャーにさらされる中、パーソナライズされたコンテンツに対する需要が急速に高まっています。 小売企業やブランドは、地域や季節限定、セグメント固有の要件などに後押しされ、製品画像のバリエーションに対するニーズの高まりに対応することに苦慮しています。

Retailerの1,000以上の商品を紹介。 属性のバリエーションを考慮する前であっても、異なる地域、顧客セグメント、パーソナライゼーションの取り組みを考慮すると、必要なデジタルアセット数は大幅に増加します。 これにより、アセットのバリエーションが膨大に生成され、数百万人に達する可能性があります。

![概要](assets/product-visuals-example.png){width="700" zoomable="yes"}

AEM Assetsとの連携により、アセット管理ワークフローを自動化することでこの課題に対処します。 この統合により、商品画像やマーケティングコンテンツなどのデジタルアセットは、SKUやその他の主要属性にもとづいて、Adobe Commerceの商品やカテゴリーなどの適切なマーチャンダイジングエンティティに動的にリンクされます。 このプロセスは、次のことを可能にすることで、業務を合理化し、効率を向上させます。

* **シームレスなインストールと設定**- マーチャンダイジングチームと開発者は、使い慣れたAdobe ツールとワークフローを使用して、統合をすばやく設定できます。

* **動的なアセット更新** – 製品画像とマーケティングアセットは、AEM Assetsの最新の変更を自動的に反映し、ストアフロントを正確かつ関連性のある状態に保ちます。

* **合理化されたカタログ管理** – アセットの更新とクリーンアップを自動化して、手作業を最小限に抑え、一貫性のある適切に管理された製品カタログを確保します。

## 統合の使用要件

この統合を[製品ビジュアルまたはAEM Assets](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview#product-visuals-powered-by-aem-assets)のいずれかで活用するには、次の要件を満たす必要があります。

>[!BEGINTABS]

>[!TAB 製品ビジュアル ]

[!BADGE SaaSのみ]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"} Adobe Commerceのアクティブライセンス、AEM Assetsを利用した製品ビジュアル、および[AEM Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/dynamic/administering-dynamic-media) （これらのライセンスは、[!DNL Adobe Commerce as a Cloud Service]および[!DNL Adobe Commerce Optimizer]ですぐに利用できます）。

>[!TAB AEM Assets]

[!BADGE SaaSのみ]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"}Adobe Commerce、Adobe Experience Manager Assets、および[AEM Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/dynamic/administering-dynamic-media)のアクティブライセンス。

[!BADGE PaaSのみ]{type=Informative tooltip="Cloud プロジェクト上のAdobe Commerce（Adobeで管理されるPaaS インフラストラクチャ）にのみ適用されます。"} Adobe Commerce 2.4.5以降

* PHP 8.1、8.2、8.3、および8.4

* Composer 2.x

[!BADGE SaaSのみ]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"} Adobe Experience Managerは[Adobe Experience Manager Assets as a Cloud Service](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/overview)でプロビジョニングされています

>[!ENDTABS]

統合を設定するAdobe Commerce ユーザーは、AEM Assets プロジェクトがプロビジョニングされている[IMS Organization](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255)にアクセスできる必要があります。

>[!BEGINSHADEBOX]

## 主なメリット

![check](assets/icon-check.png) **追加費用なし** – この統合は、ライセンス要件を満たす販売者に無料で提供されます。

![check](assets/icon-check.png) **公式Adobe ソリューション**&#x200B;は、Adobeによって開発、維持、完全にサポートされ、将来のプラットフォームの機能強化に伴う安定性と整合性を確保します。

![check](assets/icon-check.png) **Adobe Managed Support Model** – 支援とトラブルシューティングは、Adobeによって直接処理され、安心と合理的な問題解決を実現します。

![check](assets/icon-check.png) **Adobe Storefront Builder capabilities**- デジタルアセット管理（DAM）ソリューションを使用すると、[Storefront Builder](https://experienceleague.adobe.com/developer/commerce/storefront/merchants/storefront-builder/#userlabs-commerce-genai-product-visuals)で画像、ビデオ、その他のメディアなどのアセットを使用できます。

>[!ENDSHADEBOX]

## チュートリアル

Adobe CommerceとAEM Assetsの統合機能を設定して使用する方法については、次のビデオをご覧ください。

>[!BEGINTABS]

>[!TAB PaaS チュートリアル ]

Adobe CommerceとAEM Assetsが連携し、コンテンツワークフローを効率化する方法を動画でご確認ください。

>[!VIDEO](https://video.tv.adobe.com/v/3447837)

>[!TAB Adobe Commerce as a Cloud Service チュートリアル ]

AEM Assetsとの連携でAdobe Commerce as a Cloud Serviceを使用する方法について説明します。

>[!VIDEO](https://video.tv.adobe.com/v/3478140?quality=12&learn=on)

>[!ENDTABS]

## 次のステップ

Experience Manager AssetsとのCommerce統合を有効にするには、次の3つの手順を実行します。

1. [Commerce メタデータをサポートするようにAEM Assets プロジェクトを設定します](get-started/configure-aem.md)。

1. [!BADGE PaaSのみ]{type=Informative tooltip="Cloud プロジェクト上のAdobe Commerce（Adobeで管理されるPaaS インフラストラクチャ）にのみ適用されます。"} [Adobe Commerce パッケージをインストール &#x200B;](get-started/configure-commerce.md)。

1. 環境の統合を設定します。

   * [!BADGE PaaSのみ]{type=Informative tooltip="Cloud プロジェクト上のAdobe Commerce（Adobeで管理されるPaaS インフラストラクチャ）にのみ適用されます。"} [Adobe Commerce](get-started/setup-synchronization.md)
   * [!BADGE SaaSのみ]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"} [Adobe Commerce Optimizer](get-started/configure-aco.md)

## サポート

このガイドに記載されていない情報や質問がある場合は、AEM Assets統合の営業担当者にお問い合わせいただくか、[&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket)を作成して追加のヘルプを受け取ってください。
