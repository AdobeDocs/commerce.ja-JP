---
title: CommerceのAEM Assets統合
description: Adobe Experience Manager Assetsをインスタンスと統合して、Commerce ストアフロント  [!DNL Commerce]  メディアファイルを作成および管理する方法について説明します。
feature: CMS, Media, Configuration, Integration
exl-id: f450752a-bef1-419e-ad14-ff8879ab204b
source-git-commit: 9e6f8ae86b28577e2b2c675dbf274c762abe9f3f
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# CommerceのAEM Assets統合

マーケティング予算にプレッシャーがかかっている中、パーソナライズされたコンテンツの需要は急速に高まっています。 小売業者やブランドは、地域、季節、セグメント固有の要件に牽引され、商品画像のバリエーションに対するニーズの高まりに対応するのに苦労しています。

例えば、retailerに 1,000 個の商品があるとします。 様々な地域、顧客セグメントおよびパーソナライゼーションの取り組みを検討する際に、属性の変化を考慮に入れる前であっても、必要なデジタルアセットの数は大幅に増加します。 これにより、アセットのバリエーションが膨大な数になり、数百万人に及ぶ可能性があります。

![&#x200B; 概要 &#x200B;](assets/product-visuals-example.png){width="700" zoomable="yes"}

AEM Assetsの統合は、アセット管理ワークフローを自動化することでこの課題に対処します。 統合により、商品画像やマーケティングコンテンツなどのデジタルアセットが、SKU やその他の主要な属性に基づいて、Adobe Commerceの商品やカテゴリなどの適切なマーチャンダイジングエンティティに動的にリンクされます。 このプロセスにより、次のことが可能になり、運用が合理化され、効率が向上します。

* **シームレスなインストールと設定**- マーチャンダイジングチームや開発者は、使い慣れたAdobeのツールやワークフローを使用して、統合をすばやくセットアップできます。

* **アセットの動的な更新** 商品画像とマーケティングアセットは、AEM Assetsの最新の変更内容を自動的に反映し、ストアフロントの正確さと関連性を維持します。

* **合理化されたカタログ管理** アセットの更新とクリーンアップを自動化して、手動での作業を最小限に抑え、一貫性のある適切に維持された製品カタログを確保します。

## 統合を使用するための要件

この連携を Product Visuals またはAEM Assetsで活用するには、以下の要件を満たす必要があります。

>[!BEGINTABS]

>[!TAB  製品ビジュアル ]

[!BADGE SaaS のみ &#x200B;]{type=Positive url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"}Adobe Commerce、Product Visuals powered by AEM Assets、および [AEM Dynamic Media のアクティブなライセンス &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/assets/dynamic/administering-dynamic-media) これらのライセンスは、[!DNL Adobe Commerce as a Cloud Service] と [!DNL Adobe Commerce Optimizer] が標準で提供されています）。

>[!TAB AEM Assets]

[!BADGE SaaS のみ &#x200B;]{type=Positive url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"}Adobe Commerce、Adobe Experience Manager Assets、[AEM Dynamic Media のアクティブなライセンス &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/assets/dynamic/administering-dynamic-media)

[!BADGE PaaS のみ &#x200B;]{type=Informative tooltip="クラウドプロジェクト上のAdobe Commerceにのみ適用されます（Adobeが管理する PaaS インフラストラクチャ）。"}Adobe Commerce 2.4.5 以降

* PHP 8.1、8.2、8.3、および 8.4

* Composer 2.x

[!BADGE SaaS のみ &#x200B;]{type=Positive url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"}Adobe Experience Managerは [Adobe Experience Manager Assets as a Cloud Serviceでプロビジョニングされます &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/overview)

>[!ENDTABS]

統合を設定するAdobe Commerce ユーザーには、AEM Assets プロジェクトがプロビジョニングされている [IMS 組織 &#x200B;](https://experienceleague.adobe.com/ja/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255) へのアクセス権が必要です。

>[!BEGINSHADEBOX]

## 主なビジネス上のメリット

![&#x200B; チェック &#x200B;](assets/icon-check.png)**追加費用なし** – この統合は、ライセンス要件を満たすマーチャントに無料で提供されます。

![check](assets/icon-check.png)**Adobeの公式ソリューション** Adobeで開発、維持管理、完全なサポートが行われているので、安定性と将来のプラットフォーム機能強化との整合性が確保されます。

![&#x200B; チェック &#x200B;](assets/icon-check.png) **Adobe マネージドサポートモデル** のサポートとトラブルシューティングはAdobeで直接行われるため、お客様の負担を軽減し、問題の解決を効率化できます。

![&#x200B; チェック &#x200B;](assets/icon-check.png) **Adobe Storefront Builder の機能** - デジタルアセット管理（DAM）ソリューションを使用すると、[Storefront Builder](https://experienceleague.adobe.com/developer/commerce/storefront/merchants/storefront-builder/?lang=ja#userlabs-commerce-genai-product-visuals) で画像、ビデオ、その他のメディアなどのアセットを使用できます。

>[!ENDSHADEBOX]

このビデオでは、Adobe CommerceとAEM Assetsを連携させてコンテンツワークフローを効率化する方法を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/3447884?captions=jpn)

## 次の手順

CommerceとExperience Manager Assetsの統合を有効にするには、次の 3 つの手順を実行します。

1. [Commerce メタデータをサポートするようにAEM Assets プロジェクトを設定します &#x200B;](get-started/configure-aem.md)。

1. [!BADGE PaaS のみ &#x200B;]{type=Informative tooltip="クラウドプロジェクト上のAdobe Commerceにのみ適用されます（Adobeが管理する PaaS インフラストラクチャ）。"}Adobe Commerce パッケージ [&#x200B; インストール &#x200B;](get-started/configure-commerce.md)。

1. [&#x200B; 統合を設定します &#x200B;](get-started/setup-synchronization.md)。

## サポート

情報が必要な場合や、このガイドで扱われていない質問がある場合は、AEM Assets Integration の営業担当または [&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=ja#submit-ticket) を作成して、追加のヘルプを受けてください。
