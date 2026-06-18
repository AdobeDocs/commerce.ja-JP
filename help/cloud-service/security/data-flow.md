---
title: セキュリティアーキテクチャとデータフロー
description: Adobe Commerce as a Cloud Serviceのセキュリティアーキテクチャとデータフローについて説明します。
role: Admin, Developer, Leader
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"
autotag-review: '2026-06-18T16:16:18.600Z'
TQID: 'https://experienceleague.adobe.com/2yK-VVec98nFH9LPpfSe4kQ2YvQr2yy3G0Rym5-HCbI'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 15a99ce130efaf3a35968cfc01747fe1b6ab93c9
workflow-type: tm+mt
source-wordcount: 387
ht-degree: 0%

---


# セキュリティアーキテクチャとデータフロー

次の例は、[!DNL Adobe Commerce as a Cloud Service]でのデータの一般的な流れを示しています。

![Adobe Commerce as a Cloud Service データフロー図](../assets/data-flow-1.png)

## データフローのストーリー

**手順1**：買い物客はブラウザーでマーチャントのストアフロントのURLを入力し、そのURLをCommerce StorefrontのContent Delivery Network （外部CDN）に送信します。

**手順2**: サイト URLがキャッシュされている場合、ストアフロント CDNは買い物客に返します。 リソースの最初のリクエストである場合に発生する可能性がある、まだキャッシュされていない場合、外部CDNは買い物客のリクエストを内部CDNに転送し、後続のリクエストに対する応答をキャッシュします。

**手順2a**：要求が画像またはビデオの場合、フルフィルメントのために[!DNL Product Visuals]に送信され、ストアフロントに戻されます。

**手順3**：サイト URLが内部CDNにキャッシュされている場合、そのキャッシュから返されます。 そうでない場合は、[!DNL API Mesh]に送信され、後続のリクエストに対して応答がキャッシュされます。

**手順4**: [!DNL API Mesh]はオーケストレーションレイヤーとして機能し、リクエストを[!DNL Adobe Commerce as a Cloud Service]またはサードパーティシステムに送信してリクエストを処理するかどうかを決定します。

>[!NOTE]
>
>[!DNL API Mesh]は、メッシュ設定をカスタマイズした場合にのみ、サードパーティシステムにリクエストを送信します。

**手順5**: [!DNL Adobe Commerce as a Cloud Service]に送信されたリクエストは、疑わしいリクエストや悪意のあるリクエストをブロックするWeb Application Firewall （WAF）を通過します。 要求されたURLが[!DNL Commerce] CDNにキャッシュされている場合、そのURLはそのキャッシュから配信されます。 キャッシュされていない場合は、1つ以上の[!DNL Adobe Commerce as a Cloud Service] マイクロサービス（基礎、検索、レコメンデーションなど）から返され、今後のリクエスト用にキャッシュされます。

**手順5a**：リクエストがサードパーティ システムに送信された場合、応答は[!DNL API Mesh]に返されます。

**手順5b**：支払い処理用のリクエストの場合、支払いプロバイダーはiframeをストアフロントにレンダリングして、買い物客がクレジットカード情報を安全に入力し、支払い取引を完了できるようにします。

**手順6**: [!DNL Adobe Commerce as a Cloud Service]またはサードパーティサービスからの応答を[!DNL API Mesh]が受信すると、それらの応答は統合グラフに合成され、買い物客の要求に応じて[!DNL Commerce Storefront]に戻されます。
