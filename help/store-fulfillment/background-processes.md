---
title: バックグラウンドプロセス設定
description: データをフルフィルメントサービス  [!DNL Store Fulfillment]  同期する際に使用する、バックグラウンドプロセスのスケジュールを設定します。
role: Admin, Developer
level: Intermediate
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# バックグラウンドプロセス設定

ストアフルフィルメント統合では、最適なパフォーマンスと拡張性を実現するために、バックグラウンドプロセスとメッセージキューを使用します。 自動的に開始する [ デプロイメント変数 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy#cron_consumers_runner) を使用して、Adobe Commerce ストアの環境を作成します [ メッセージキューランナー ](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/message-queues/message-queue-framework)。

バックグラウンドプロセスは、標準のAdobe Commerce[ スケジュールされたタスク ](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/tools/cron) 機能を使用して管理されます。 これらのプロセスは、注文とマーチャントストアの設定データをストアフルフィルメント web サービスと同期する役割を果たします。

## Store Fulfillment のスケジュールされたタスクの管理

管理者から、**[!UICONTROL Stores > Configuration > Advanced > System > Cron (Scheduled Tasks) > Cron configuration options for group:store_fulfillment]** に移動します。

Store Fulfillment サービスのデフォルト設定を確認します。 これらの設定は、注文処理量とリソースの可用性に基づいてカスタマイズできます。
