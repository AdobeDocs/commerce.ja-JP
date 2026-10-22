---
title: 支払いの設定
description: Adobe Commerceの決済サービスを設定して、複数の支払い方法と決済、注文、請求書の統合ダッシュボードをサポートする方法をご確認ください。
role: Admin, Developer
feature: Configuration
recommendations: noCatalog
autotag-review: '2026-10-20T11:00:28.278Z'
TQID: 'https://experienceleague.adobe.com/egM9HoywqOQgL27ykw5SBdvoMHsmagYNoDMtNSLPds0'
product_v2:
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 591c578b-908e-5b79-a9d3-931dfe60c24c
    internal-label: Invoices
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%
---

# 支払いの設定

[!DNL Payment Services]では、無利息の分割払いを含む複数の支払い方法が提供され、支払い、注文、請求書を管理するための統合ダッシュボードがマーチャントに提供されます。

>[!NOTE]
>
>このガイドは、Adobe Commerce（クラウドまたはオンプレミス）、Adobe Commerce as a Cloud Service、またはMagento Open Sourceでトランザクションを処理する場合に適用されます。 Adobe Commerce Optimizer プロジェクトの場合は、トランザクションバックエンドがサポートされているプラットフォームの1つである場合にのみ、このフローに従います。 サードパーティのバックエンドでトランザクションを処理する場合は、代わりにそのバックエンドの支払い設定を使用してください。

## Adobe Experience Managerの導入方法

1. [支払いサービスの互換性](https://experienceleague.adobe.com/ja/docs/commerce/payment-services/compatibility)で、製品のバージョンと国の空き状況を確認します。

1. [&#x200B; オンボーディング決済サービスのフロー](/help/payment-services/onboard.md)に従います。

1. Commerce オンクラウドまたはオンプレミス インスタンスがCommerce サービスに接続されていない場合は、まず[Commerce サービスの設定](set-up-commerce-services.md)に従ってください。

## 関連するガイダンス

- [決済サービスガイドの概要](/help/payment-services/guide-overview.md)
- [Commerce サービスの設定](set-up-commerce-services.md)
