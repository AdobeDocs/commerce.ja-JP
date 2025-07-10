---
title: ログの表示と管理
description: CommerceのAEM Assets統合のログを検索および管理する場所について説明します。
feature: CMS, Media, Integration
badgePaas: label="PaaS のみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeが管理する PaaS インフラストラクチャ）およびオンプレミスプロジェクトにのみ適用されます。"
exl-id: 9c6c8694-6ded-4cc8-a3ab-d1dfb50e3583
source-git-commit: 202eca18c71a211cbbf1d210be00543049170c3f
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# ログの表示と管理

AEM Assets統合は、Commerce インスタンスに次のログファイルを提供します。

- `/var/log/aem-assets-integration.log`
- `/var/log/aem-assets-integration-errors.log`

これらのログが大きくなりすぎないようにするには、システム管理者にこれらのログのログファイル回転スケジュールを確認するように依頼してください。 ログが自動的にローテーションされる環境もあれば、手動でログローテーションを設定する必要がある環境もあります。  詳しくは、次のトピックを参照してください。

- Adobe Commerceのオンプレミスインストールの場合は、システム管理者に依頼して [ ログローテーション ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html#server-settings) を設定します。
- クラウドインフラストラクチャプロジェクトのAdobe Commerceについては、[ ログの表示と管理 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html) を参照してください。
