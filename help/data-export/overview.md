---
title: '[!DNL SaaS Data Export Guide]'
description: Adobe Commerceと接続されたCommerce サービス間でデータを同期するAdobe Commerce SaaS サービスに [!DNL data export] 拡張機能を使用する方法について説明します。
role: Admin, Developer
exl-id: 8a0067ba-90a4-48a6-8276-208d09abe6fc
TQID: https://experienceleague.adobe.com/OHE1GBUEd8hHFPwFlO9fJa3Y0wK2xZ0HOYnwUn0-DSk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 69f39a6a62e05c86a0e2897d09079543b3d8830e
workflow-type: tm+mt
source-wordcount: 571
ht-degree: 0%

---

# [!DNL SaaS Data Export] ガイド

[!DNL SaaS data export]は、Adobe Commerce インスタンスと接続されたCommerce サービスとの間でデータを同期します。 ライブサーチ、商品レコメンデーション、カタログサービス、または[!DNL Adobe Commerce Optimizer Connector]をAdobe Commerce インストールに追加すると、[!DNL Data export]拡張機能が自動的にインストールされます。

>[!NOTE]
>
>[!DNL Adobe Commerce Optimizer Connector]をインストールすると、同じ[!DNL Data Export]拡張機能が[!DNL Adobe Commerce]からカタログと価格フィードを収集します。 コネクタは、コンポーザブルカタログデータモデル（CCDM）を使用して、これらのフィードを[!DNL Adobe Commerce Optimizer]にマッピングして送信します。 セットアップとアーキテクチャについては[[!DNL Adobe Commerce Optimizer Connector] 概要](../aco-connector/overview.md)を、エクスポート後の同期動作については[&#x200B; コネクタ同期パイプライン &#x200B;](../aco-connector/connector-sync-pipeline.md)を参照してください。

SaaS データ書き出しは、_フィード_&#x200B;と呼ばれる様々なタイプのデータを収集および書き出し、特定のタイプの情報を集約します。 インストールされているCommerce サービスに応じて、SaaS データエクスポートフィードには次のものが含まれます。

- **カタログエンティフィード**&#x200B;の製品データの集約。 データには、製品、製品属性、製品価格、製品バリエーション、カテゴリー、カテゴリー権限、製品権限が含まれます。
- **スコープフィード**&#x200B;は、顧客グループ、web サイト、ストア、ストアビューのデータを集計します。
- **販売注文フィード**&#x200B;は、請求書、出荷、クレジットメモなどの関連エンティティを含む注文データを集計します。
- **マルチSource在庫フィード**&#x200B;は、在庫の在庫状況アイテムに関するデータを集計します。

SaaS データエクスポートは、PHP拡張機能として配信されます。 データ同期プロセスを開始および管理するための複数の方法をサポートしています。

- **管理者またはコマンドラインからの手動同期**

   - Commerce Adminの[Data Management ダッシュボード &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)には、商品データがコマースサービスに正常に同期されたことを示す同期ステータスのグラフィカルビューが表示されます。 ダッシュボードを使用して、すべてのフィードの完全な再同期（_完全同期_）を実行できます。 ただし、Adobeでは、Adobe CommerceをCommerce サービスに初めて接続する場合にのみ、完全同期を実行することをお勧めします。 [同期プロセス &#x200B;](data-synchronization.md)を参照してください。

     {{aco-data-sync-verification}}

   - [&#x200B; データフィードの同期ステータス &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) ページでは、Commerceから商品レコメンデーション、ライブサーチ、カタログサービス、Adobe Commerce Optimizerなどの外部サービスに商品データやカテゴリデータを転送するデータエクスポートフィードの健全性とパフォーマンスに関するリアルタイムのインサイトを提供します。

   - [Adobe Commerce コマンドライン ツール &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/config-cli) （CLI）には、特定のフィードを同期するコマンドが用意されており、フィード処理をカスタマイズするためのその他のオプションも用意されています。

- **cron ジョブとの自動同期**

   - [部分データトリガー](data-synchronization.md#partial-sync) - Commerce管理者ユーザーがエンティティを更新すると、Cron ジョブが部分的データ同期を同期します。 データ書き出しプロセスでは、これらの更新のみが接続されたCommerce サービスに送信されます。 部分同期プロセスはMView メカニズムに基づいており、管理者ユーザーまたはシステムインテグレーターのアクションは必要ありません。

   - [同期エラーに対する自動再試行](data-synchronization.md#retry-failed-items-sync) - Cron ジョブのトリガーデータ同期プロセス中にエラーが発生した場合の同期プロセスの自動再試行。

- **スケジュールとパフォーマンスの書き出し**

   - 開発者やシステムインテグレーターは、Adobe Commerceと接続されたサービス間でSaaS データを同期するために必要な時間を見積もることができます。 この見積もりは、データ書き出し処理のスケジュールを設定し、サイトの混乱を防ぐのに役立ちます。 [&#x200B; データ量と送信時間の見積もり](estimate-data-volume-sync-time.md)を参照してください。

   - SaaS データ書き出しは、同期をより迅速におこなう必要がある場合、書き出し処理のパフォーマンスを向上させるためのカスタマイズオプションを提供します。 [&#x200B; データ書き出しのパフォーマンスの向上](customize-export-processing.md)を参照してください。

- **データ書き出しアクティビティの追跡とトラブルシューティング** - データ書き出しとsaas書き出しのログを使用して、同期およびインデックス作成プロセス中に同期ステータスとフィード ペイロードを確認します。 [&#x200B; ログとトラブルシューティング &#x200B;](troubleshooting-logging.md)を参照してください。

