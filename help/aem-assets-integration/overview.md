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
source-git-commit: 0c2e50338cbf286704239b6d1f628180e85a3bef
workflow-type: tm+mt
source-wordcount: 1081
ht-degree: 1%

---

# Commerce向けAEM Assets統合

マーケティング予算がプレッシャーにさらされる中、パーソナライズされたコンテンツに対する需要が急速に高まっています。 小売企業やブランドは、地域や季節限定、セグメント固有の要件などに後押しされ、製品画像のバリエーションに対するニーズの高まりに対応することに苦慮しています。

Retailerの1,000以上の商品を紹介。 さまざまな地域、顧客セグメント、パーソナライゼーションの取り組みを検討する際に、必要なデジタルアセットの数が大幅に増加します。 このような状況では、膨大な数のアセットバリエーションが何百万もの人々に届く可能性があります。

![概要](assets/product-visuals-example.png){width="700" zoomable="yes"}

AEM Assetsとの連携により、アセット管理ワークフローを自動化することでこの課題に対処します。 この統合により、デジタルアセットは、SKUまたはその他の主要属性にもとづいて、適切なAdobe Commerce製品とカテゴリーに動的にリンクされます。 このプロセスは、次のことを可能にすることで、業務を合理化し、効率を向上させます。

* **シームレスなインストールと設定**- マーチャンダイジングチームと開発者は、使い慣れたAdobe ツールとワークフローを使用して、統合をすばやく設定できます。

* **動的なアセットの更新** – 製品画像とマーケティングアセットは、AEM Assetsの最新の変更を自動的に反映し、ストアフロントを正確かつ関連性のある状態に保ちます。

* **合理化されたカタログ管理** - アセットの更新とクリーンアップを自動化して、手作業を最小限に抑え、一貫性のある適切に管理された製品カタログを確保します。

## 統合の使用要件

この統合を[製品ビジュアルまたはAEM Assets](https://experienceleague.adobe.com/ja/docs/commerce/cloud-service/overview#product-visuals-powered-by-aem-assets)のいずれかで活用するには、次の要件を満たす必要があります。

>[!BEGINTABS]

>[!TAB 製品ビジュアル ]

[!BADGE SaaSのみ]{type=Positive url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"} Adobe Commerceのアクティブライセンス、AEM Assetsを利用した製品ビジュアル、および[AEM Dynamic Media](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/assets/dynamic/administering-dynamic-media) （これらのライセンスは、[!DNL Adobe Commerce as a Cloud Service]および[!DNL Adobe Commerce Optimizer]ですぐに利用できます）。

>[!TAB AEM Assets]

[!BADGE SaaSのみ]{type=Positive url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"}Adobe Commerce、Adobe Experience Manager Assets、および[AEM Dynamic Media](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/assets/dynamic/administering-dynamic-media)のアクティブライセンス。

[!BADGE PaaSのみ]{type=Informative tooltip="Cloud プロジェクト上のAdobe Commerce（Adobeで管理されるPaaS インフラストラクチャ）にのみ適用されます。"} Adobe Commerce 2.4.5以降

* PHP 8.1、8.2、8.3、および8.4

* Composer 2.x

[!BADGE SaaSのみ]{type=Positive url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"} Adobe Experience Managerは[Adobe Experience Manager Assets as a Cloud Service](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/overview)でプロビジョニングされています

>[!ENDTABS]

統合を設定するAdobe Commerce ユーザーは、AEM Assets プロジェクトがプロビジョニングされている[IMS Organization](https://experienceleague.adobe.com/ja/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255)にアクセスできる必要があります。

>[!BEGINSHADEBOX]

## 主なメリット

![check](assets/icon-check.png) **追加費用なし** – この統合は、ライセンス要件を満たす販売者に無料で提供されます。

![check](assets/icon-check.png) **公式Adobe ソリューション** - Adobeによって開発、維持、完全にサポートされ、将来のプラットフォームの機能強化に伴う安定性と整合性が確保されます。

![check](assets/icon-check.png) **Adobe Managed Support Model** - Adobeがサポートとトラブルシューティングを直接処理し、信頼性の高いサポートと合理的な問題解決を提供します。

![check](assets/icon-check.png) **Adobe Storefront Builder capabilities** - デジタルアセット管理（DAM）ソリューションを使用すると、[Storefront Builder](https://experienceleague.adobe.com/developer/commerce/storefront/merchants/storefront-builder/?lang=ja#userlabs-commerce-genai-product-visuals)で画像、ビデオ、その他のメディアなどのアセットを使用できます。

>[!ENDSHADEBOX]

## チュートリアル

AEM AssetsとAdobe Commerceの統合機能を設定および使用する方法については、次のビデオをご覧ください。

>[!BEGINTABS]

>[!TAB Adobe Commerce オンクラウドまたはオンプレミスのチュートリアル ]

Adobe CommerceとAEM Assetsが連携し、コンテンツワークフローを効率化する方法をご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3447837)

>[!TAB Adobe Commerce as a Cloud Service チュートリアル ]

AEM Assetsとの連携でAdobe Commerce as a Cloud Serviceを使用する方法について説明します。

>[!VIDEO](https://video.tv.adobe.com/v/3478140?quality=12&learn=on)

>[!ENDTABS]

## 次のステップ

AEM Assets統合をインストールして設定するプロセスは、Adobe Commerceのデプロイメントによって異なります。 いずれの場合も、最初にAEM Assetsを設定してから、Commerceを接続します。

統合がAEM Assets環境に追加する名前空間、メタデータスキーマ、および&#x200B;**[!UICONTROL Commerce]** タブについて理解するには、開始する前に、[AEM AssetsのCommerce メタデータを確認してください。](metadata.md)

デプロイメントを選択し、必要な手順に従って順番に実行します。

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

[!BADGE SaaSのみ]{type=Positive tooltip="Adobe Commerce as a Cloud Service プロジェクト（Adobeで管理されるSaaS インフラストラクチャ）にのみ適用されます。"}

1. Commerce メタデータをサポートするには、[AEM Assets プロジェクトを設定](get-started/configure-aem.md)します。 AEM リリース `2026.5.26309`以降では、[&#x200B; セルフサービスオンボーディング &#x200B;](get-started/configure-aem.md#enable-aem-commerce-self-service)を使用します。以前のリリースでは、`assets-commerce` パッケージを手動でインストールします。

1. [IMS ユーザー権限](get-started/permissions.md)を設定して、アセットセレクターと、自動入力された&#x200B;**[!UICONTROL Program ID]**&#x200B;および&#x200B;**[!UICONTROL Environment ID]** フィールドを使用できるようにします。

1. [Commerce Admin](get-started/setup-synchronization.md)で統合を設定します。

1. オプション。 [商品画像の表示](get-started/configure-storefront.md#enable-product-images)を有効にして、Edge Delivery Servicesを搭載したストアフロントでAEMが管理する商品画像をレンダリングします。

>[!TAB  クラウド上のAdobe Commerce （PaaS） ]

[!BADGE PaaSのみ]{type=Informative tooltip="Cloud プロジェクト上のAdobe Commerce（Adobeで管理されるPaaS インフラストラクチャ）にのみ適用されます。"}

1. Commerce メタデータをサポートするには、[AEM Assets プロジェクトを設定](get-started/configure-aem.md)します。 AEM リリース `2026.5.26309`以降では、[&#x200B; セルフサービスオンボーディング &#x200B;](get-started/configure-aem.md#enable-aem-commerce-self-service)を使用します。以前のリリースでは、`assets-commerce` パッケージを手動でインストールします。

1. [Adobe Commerce パッケージ &#x200B;](get-started/configure-commerce.md)をインストールして、拡張機能を追加し、必要な資格情報と接続を生成します。

1. [IMS ユーザー権限](get-started/permissions.md)を設定して、アセットセレクターと、自動入力された&#x200B;**[!UICONTROL Program ID]**&#x200B;および&#x200B;**[!UICONTROL Environment ID]** フィールドを使用できるようにします。

1. [Commerce Admin](get-started/setup-synchronization.md)で統合を設定します。

1. オプション。 [商品画像の表示](get-started/configure-storefront.md#enable-product-images)を有効にして、Edge Delivery Servicesを搭載したストアフロントでAEMが管理する商品画像をレンダリングします。

>[!TAB Adobe Commerce Optimizer]

[!BADGE SaaSのみ]{type=Positive tooltip="Adobe Commerce Optimizer プロジェクトにのみ適用されます。"}

[!DNL Adobe Commerce Optimizer]管理者設定UIがありません。 Adobe サポートは、オンボーディングチケットからの統合を設定するので、まずAEM Assetsを準備してください。

1. Commerce メタデータをサポートするには、[AEM Assets プロジェクトを設定](get-started/configure-aem.md)します。 AEM リリース `2026.5.26309`以降では、[&#x200B; セルフサービスオンボーディング &#x200B;](get-started/configure-aem.md#enable-aem-commerce-self-service)を使用します。以前のリリースでは、`assets-commerce` パッケージを手動でインストールします。

1. [&#x200B; オンボーディングサポートチケット &#x200B;](get-started/configure-aco.md#onboarding)を、テナント ID、AEM プログラム ID、AEM Environment ID、一致するルール、レイヤー、ロケールを使用して送信します。

1. [&#x200B; チケットに登録したのと同じロケールとレイヤーを使用して、カタログビュー](get-started/configure-aco.md#onboarding)を設定します。

1. オプション。 [商品画像の表示](get-started/configure-storefront.md#enable-product-images)を有効にして、Edge Delivery Servicesを搭載したストアフロントでAEMが管理する商品画像をレンダリングします。

   完全な手順、制限、およびレイヤーガイダンスについては、[Commerce Optimizer用AEM Assetsの設定](get-started/configure-aco.md)を参照してください。

>[!ENDTABS]

## サポート

このガイドに記載されていない情報や質問がある場合は、AEM Assets統合の営業担当者にお問い合わせいただくか、[&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#support-case)を作成して追加のヘルプを受け取ってください。
