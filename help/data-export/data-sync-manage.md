---
title: 同期プロセスの表示と管理
description: データ管理ダッシュボードとデータフィード同期ステータス ページを使用して、 [!DNL SaaS Data Export] 同期プロセスを表示および管理する方法について説明します。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: e7d9c056ef8d565b4a143b05ff4e06d607fbfa8e
workflow-type: tm+mt
source-wordcount: 544
ht-degree: 0%

---

# 同期プロセスの表示と管理

ほとんどの同期アクティビティは、完全同期、部分同期、または失敗した項目の再試行の同期を使用して自動的に処理されます。 各タイプが実行されるタイミングについて詳しくは、[同期タイプ ](sync-overview.md#synchronization-types)を参照してください。 [!DNL SaaS Data Export]には、プロセスを監視、管理、およびトラブルシューティングするためのツールも用意されています。 同期ステータスを表示し、デプロイメント用のダッシュボードを使用してデータ同期プロセスを管理できます。

>[!BEGINTABS]

>[!TAB Adobe Commerce]

Adobe Commerce オンクラウド、オンプレミス、またはAdobe Commerce as a Cloud Service デプロイメントの場合は、次のCommerce管理者リソースから同期プロセスを表示および管理します。

- **[データフィードの同期ステータス ページ ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)** - [!DNL Live Search]、[!DNL Product Recommendations]または[!DNL Catalog Service]に接続されたデプロイメントのフィード書き出しステータスを確認します。 このダッシュボードには、各フィードのフィード書き出しステータス（発生したエラーを含む）が表示されます。 詳細ビューには、個々のフィード項目のフィード書き出しステータスが表示されます。

- **[Data Management ダッシュボード ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)**：管理者ユーザーは、正常にエクスポートされ、接続されたCommerce サービスに同期されたデータを表示および追跡できます。 このダッシュボードには、Commerce Servicesに同期された商品データが表示されます。

>[!NOTE]
>
>データ管理ダッシュボードとデータフィードの同期ステータス ページは、[!DNL Live Search]、[!DNL Product Recommendations]、または[!DNL Catalog Service]がインストールされている場合にのみ使用できます。

>[!TAB Commerce Optimizer付きAdobe Commerce]

[!DNL Commerce Optimizer]と統合されたCommerce オンクラウドまたはオンプレミスのデプロイメントの場合、次のリソースを使用して同期プロセスを表示および管理します。

- **[データフィードの同期ステータス ページ ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)** - Commerce管理者からのコネクタフィードの書き出しステータスを監視します。 このページは、フィードごとのエラーとアイテムごとのエラーの詳細を含め、[!DNL Adobe Commerce]からカタログデータが正常にエクスポートされたかどうかを示します。

- **[データ同期ページ](../optimizer/setup/data-sync.md)** - データ同期ページには、アップストリーム カタログ ソースから[!DNL Commerce Optimizer]に送信される製品データの同期ステータスの概要が表示されます。

これらのダッシュボードを使用してデータ同期が機能していることを確認し、データを手動で再同期する方法について詳しくは、_Adobe Commerce Optimizer コネクタ ガイド_&#x200B;の[同期の管理](../aco-connector/data-sync-manage.md)を参照してください。

>[!ENDTABS]

## データ同期が機能していることを確認します {#verify-that-the-data-sync-is-working}


{{$include /help/_includes/data-export/verify-commerce-service-data-sync.md}}

## データを手動で再同期

部分同期と自動再試行が同期の問題を解決しない場合は、Commerce管理者またはCommerce CLI コマンドを使用してデータを手動で再同期できます。 利用できるオプションは、デプロイメントによって異なります。

### 使用可能な手動再同期オプション {#manual-resync-options-commerce}

フィード データを手動で再同期するには、次のオプションを使用します。

| タスク | オプション | メモ |
| --- | --- | --- |
| 選択した失敗したフィード項目または問題のあるフィード項目の再同期 | **[!UICONTROL Data Feed Sync Status]ページ** | 選択したフィード項目をCommerce管理者からモニタリングして再同期します。 [ データ同期が機能していることを確認してください](#verify-that-the-data-sync-is-working)。 |
| すべてのフィードの完全再同期 | **[!UICONTROL Data Management Dashboard]** | Commerce管理者から、すべてのフィードの完全な再同期を実行します。Adobeでは、Commerce サービスに初めて接続する場合に主に再同期を推奨します。 [ データ同期が機能していることを確認してください](#verify-that-the-data-sync-is-working)。 |
| 運用管理によるターゲットフィードの再同期 | **Commerce CLI** | ターゲット フィードの再同期には、`saas:resync` コマンドを使用します。 Commerce CLI](data-export-cli-commands.md)を使用した[Sync フィードの同期を参照してください。 |

>[!MORELIKETHIS]
>
> - [同期の仕組み](sync-overview.md) – 同期モード、完全同期、部分同期、失敗した項目の再試行について説明します。
> - [Commerce CLI](data-export-cli-commands.md)を使用してフィードを同期する – ターゲットフィードの再同期には`saas:resync` コマンドを使用します。
> - [ ログを確認し、トラブルシューティング ](troubleshooting/logging.md) — データ書き出しとSaaS書き出しのエラーを診断します。
> - [同期を [!DNL Commerce Optimizer]](../aco-connector/data-sync-manage.md)に管理 – カタログデータの同期を確認し、コネクタのフィードを手動で再同期します。
