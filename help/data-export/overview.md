---
title: '[!DNL SaaS Data Export Guide]'
description: 'Adobe Commerceと接続されたCommerce サービスの間でデータを同期するAdobe Commerce SaaS サービス用の拡張機能の使用について説明します  [!DNL data export] '
role: Admin, Developer
exl-id: 8a0067ba-90a4-48a6-8276-208d09abe6fc
source-git-commit: ae672ed3f2693e2f14e8c7f379e59ef117a34fc3
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# [!DNL SaaS Data Export] ガイド

Adobe Commerce インスタンスと接続されたCommerce サービスの間でデータを同期で [!DNL SaaS data export] ます。 Adobe Commerceのインストールに Live Search、Product Recommendations またはカタログサービスを追加すると、[!DNL Data export] 拡張機能が自動的にインストールされます。

SaaS データ エクスポートは、さまざまな種類のデータを収集してエクスポートします。これらのデータは _フィード_ と呼ばれ、特定の種類の情報を集計します。 インストールされているCommerce サービスに応じて、SaaS データ書き出しフィードには次のものが含まれます。

- **カタログエンティティフィード** 製品データを集計します。 データには、製品、製品属性、製品価格、製品バリエーション、カテゴリ、カテゴリ権限、製品権限が含まれます。
- **スコープフィード** は、顧客グループ、web サイト、ストアおよびストアビューのデータを集計します。
- **受注フィード** は、請求書、出荷、クレジット・メモなどの関連エンティティを含む受注データを集約します。
- **マルチSourceインベントリフィード** は、在庫ステータス項目に関するデータを集計します。

SaaS データのエクスポートは、PHP 拡張モジュールとして提供されます。 データ同期プロセスを開始および管理するためのいくつかの方法をサポートしています。

- **管理者またはコマンドラインからの手動同期**

   - Commerce管理の [ データ管理ダッシュボード ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) には、同期ステータスがグラフィカルに表示されます。 ダッシュボードを使用して、すべてのフィードの完全再同期（_完全同期_）を実行できます。 ただし、Adobeでは、Adobe CommerceをCommerce サービスに初めて接続する際にのみ、完全同期を実行することをお勧めします。 [ 同期処理 ](data-synchronization.md) を参照してください。

   - [Adobe Commerce コマンドラインツール ](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/config-cli) （CLI）には、特定のフィードを同期するコマンドが用意されており、フィード処理をカスタマイズするオプションが追加されています。

- **Cron ジョブとの自動同期**

   - [ 部分的なデータ同期 ](data-synchronization.md#partial-synchronization-with-cron-jobs) - Commerce管理者ユーザーがエンティティを更新すると、Cron ジョブは部分的なデータ同期をトリガーにします。 データの書き出しプロセスでは、接続されたCommerce サービスに対してこれらの更新のみが送信されます。 部分同期プロセスはビューメカニズムに基づいており、管理者ユーザーまたはシステムインテグレーターの操作は必要ありません。

   - [Automatic retry for synchronization errors](data-synchronization.md#failed-items-sync-for-error-recovery):Cron ジョブ・トリガーーデータ同期プロセス中にエラーが発生した場合の同期プロセスの自動再試行。

- **輸出の予定及び実施**

   - 開発者とシステムインテグレーターは、SaaS データの書き出しに要する時間を推定して、Adobe Commerceと接続されたサービスの間でデータを同期させることができます。 この概算は、サイトの中断を防ぐためにデータのエクスポート処理をスケジュールするのに役立ちます。 [ データ量と送信時間の予測 ](estimate-data-volume-sync-time.md) を参照してください。

   - 同期をより迅速に行う必要がある場合は、SaaS データのエクスポートを使用すると、エクスポート処理のパフォーマンスを向上させるためのカスタマイズオプションを利用できます。 [ データ書き出しのパフォーマンスの向上 ](customize-export-processing.md) を参照してください。

- **データの書き出しアクティビティの追跡とトラブルシューティング** - データの書き出しログと saas-export ログを使用して、同期とインデックス作成のプロセス中に同期ステータスを確認し、ペイロードをフィードします。 [ ログとトラブルシューティング ](troubleshooting-logging.md) を参照してください。
