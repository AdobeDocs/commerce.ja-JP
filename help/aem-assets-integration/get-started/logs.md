---
title: ログの表示と管理
description: Commerce向けAEM Assets統合のログを検索および管理する場所について説明します。
feature: CMS, Media, Integration
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
exl-id: 9c6c8694-6ded-4cc8-a3ab-d1dfb50e3583
TQID: https://experienceleague.adobe.com/im5QUgqayCNj9lZfZ-7UvxiUW9NmgHyhVbyBdjjPxAA
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 154
ht-degree: 0%

---

# ログの表示と管理

AEM Assets統合では、Commerce インスタンスに次のログファイルが提供されます。

- `/var/log/aem-assets-integration.log`
- `/var/log/aem-assets-integration-errors.log`

システム管理者に、これらのログのログファイルのローテーションスケジュールを確認して、サイズが大きすぎないようにしてください。 一部の環境では、ログが自動的に回転します。また、ログの回転を手動で設定する必要がある環境もあります。  詳しくは、次のトピックを参照してください。

- Adobe Commerce オンプレミスのインストールの場合は、システム管理者に[&#x200B; ログローテーション &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html?lang=ja#server-settings)の設定を依頼します。
- クラウドインフラストラクチャプロジェクト上のAdobe Commerceについては、[&#x200B; ログの表示と管理](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html?lang=ja)を参照してください。
