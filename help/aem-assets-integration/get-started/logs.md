---
title: ログの表示と管理
description: Commerce向けAEM Assets統合のログを検索および管理する場所について説明します。
feature: CMS, Media, Integration
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
exl-id: 9c6c8694-6ded-4cc8-a3ab-d1dfb50e3583
source-git-commit: d425bad4d3314aa0e14b639ffb8d89dd8b6b0f74
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# ログの表示と管理

AEM Assets統合では、Commerce インスタンスに次のログファイルが提供されます。

- `/var/log/aem-assets-integration.log`
- `/var/log/aem-assets-integration-errors.log`

検索、フィルター、同期エラーの概要など、管理画面の同期されたアセットのアセット中心のビューについては、[AEM Assetsの同期ステータスの表示](sync-status.md)を参照してください。

システム管理者に、これらのログのログファイルのローテーションスケジュールを確認して、サイズが大きすぎないようにしてください。 一部の環境では、ログが自動的に回転します。また、ログの回転を手動で設定する必要がある環境もあります。  詳しくは、次のトピックを参照してください。

- Adobe Commerce オンプレミスのインストールの場合は、システム管理者に[ ログローテーション ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html#server-settings)の設定を依頼します。
- クラウドインフラストラクチャプロジェクト上のAdobe Commerceについては、[ ログの表示と管理](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html)を参照してください。
