---
title: Commerce サービスの設定
description: Commerce Services Connectorを使用して、Adobe Commerceをマーチャンダイジングサービスに、Magento Open Sourceを決済サービスに接続する方法を説明します。
role: Admin, Developer
feature: Integration, Configuration
recommendations: noCatalog
autotag-review: '2026-10-20T11:14:04.410Z'
TQID: 'https://experienceleague.adobe.com/yyUDw1y5CYHxdLlC3bNo0DKK0byamPAKUjK-wwxVEX4'
product_v2:
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
subfeature_v2:
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%
---

# Commerce サービスの設定

クラウド インフラストラクチャおよびオンプレミス プロジェクト上のAdobe Commerceは、Commerce Services Connectorを介して[!DNL Catalog Service]、[!DNL Live Search]、[!DNL Product Recommendations]、[!DNL Payment Services]などのサービスに接続します。 [!DNL Adobe Commerce as a Cloud Service]では、この接続は自動的に設定されます。

Magento Open Sourceは、[!DNL Payment Services]にCommerce Services Connectorを使用しています。 [!DNL Catalog Service]、[!DNL Live Search]および[!DNL Product Recommendations]はAdobe Commerceが必要で、Magento Open Sourceでは利用できません。

>[!NOTE]
>
>Adobe Commerce Optimizerでは、[!DNL Live Search]、[!DNL Catalog Service]、[!DNL Product Recommendations]の個別のサービスを使用する代わりに、ネイティブでカタログおよびマーチャンダイジング機能を提供します。 カタログの同期には、Commerce Services Connectorは必要ありません。 Commerce バックエンド上のその他の統合（[!DNL Payment Services]や[!DNL Data Connection]など）では、引き続きコネクタが必要です。 Optimizerの設定については、[Adobe Commerce Optimizerを有効にする](enable-aco.md)を参照してください。


## Adobe Experience Managerの導入方法

1. API キーを取得して設定するには、[Commerce Services Connector](/help/landing/saas.md)のドキュメントを参照してください。

1. コネクタを通じて利用できる個々のサービスについては、[Adobe Commerce サービスガイド &#x200B;](/help/landing/home.md)を参照してください。

## 関連するガイダンス

- [支払いの設定](configure-payments.md)
- [AEM Assetsとの連携](connect-aem-assets.md)
- [Adobe Experience Platformとの統合](integrate-aep.md)
