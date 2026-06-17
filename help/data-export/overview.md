---
title: '[!DNL SaaS Data Export Guide]'
description: Adobe Commerceと接続されたCommerce サービス間でデータを同期するAdobe Commerce SaaS サービスに [!DNL data export] 拡張機能を使用する方法について説明します。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 8a0067ba-90a4-48a6-8276-208d09abe6fc
TQID: https://experienceleague.adobe.com/OHE1GBUEd8hHFPwFlO9fJa3Y0wK2xZ0HOYnwUn0-DSk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 402
ht-degree: 0%

---

# [!DNL SaaS Data Export] ガイド

[!DNL SaaS data export]は、Adobe Commerce インスタンスと接続されたCommerce サービスとの間でデータを同期します。 ライブサーチ、商品レコメンデーション、カタログサービス、または[!DNL Adobe Commerce Optimizer Connector]をAdobe Commerce インストールに追加すると、[!DNL Data Export]拡張機能が自動的にインストールされます。

>[!NOTE]
>
>[!DNL Adobe Commerce Optimizer Connector]をインストールすると、同じ[!DNL Data Export]拡張機能が[!DNL Adobe Commerce]からカタログと価格フィードを収集します。 コネクタは、コンポーザブルカタログデータモデル（CCDM）を使用して、これらのフィードを[!DNL Adobe Commerce Optimizer]にマッピングして送信します。 セットアップとアーキテクチャについては[[!DNL Adobe Commerce Optimizer Connector] 概要](../aco-connector/overview.md)を、エクスポート後の同期動作については[&#x200B; コネクタ同期パイプライン &#x200B;](../aco-connector/connector-sync-pipeline.md)を参照してください。

SaaS データ書き出しは、_フィード_&#x200B;と呼ばれる様々なタイプのデータを収集および書き出し、特定のタイプの情報を集約します。 インストールされているCommerce サービスに応じて、SaaS データエクスポートフィードには次のものが含まれます。

- **カタログエンティフィード**&#x200B;の製品データの集約。 データには、製品、製品属性、製品価格、製品バリエーション、カテゴリー、カテゴリー権限、製品権限が含まれます。
- **スコープフィード**&#x200B;は、顧客グループ、web サイト、ストア、ストアビューのデータを集計します。
- **販売注文フィード**&#x200B;は、請求書、出荷、クレジットメモなどの関連エンティティを含む注文データを集計します。
- **マルチSource在庫フィード**&#x200B;は、在庫の在庫状況アイテムに関するデータを集計します。

SaaS データエクスポートは、自動化された同期と手動による同期の両方をサポートするPHP拡張機能として提供されます。

- **自動同期**—Commerce サービスを接続する際に最初の完全同期後、cron ジョブは、一部の同期と失敗した項目の自動再試行を使用して、接続されたサービスを最新の状態に保ちます。管理者ユーザーまたはシステムインテグレーターは操作を必要としません。

- **手動同期** - Commerce管理者または[Commerce CLI](data-export-cli-commands.md)から、選択したフィードの完全再同期または再同期を実行します。

- **監視** - Commerce管理者の[!UICONTROL Data Feed Sync Status] ページおよびData Management ダッシュボードから、フィードの正常性、ステータス、配信を追跡します。 確認と再同期手順については、[同期の管理](data-sync-manage.md)を参照してください。

同期動作、モード、および書き出しフロー図については、[同期の仕組み](sync-overview.md)を参照してください。

SaaS データ書き出しは、同期プロセスを計画およびトラブルシューティングするツールも提供します。

- **スケジュールとパフォーマンス** – 処理をスケジュールし、サイトの中断を回避するための同期時間を見積もり、パフォーマンスを向上させるために書き出し処理をカスタマイズします。 [&#x200B; データ量と送信時間の見積もり](estimate-data-volume-sync-time.md)および[&#x200B; データ書き出しのパフォーマンスの向上](customize-export-processing.md)を参照してください。

- **追跡とトラブルシューティング** - データ書き出しとsaas書き出しのログを使用して、同期ステータスとフィード ペイロードを確認します。 [&#x200B; ログの確認とトラブルシューティング &#x200B;](troubleshooting/logging.md)を参照してください。

>[!MORELIKETHIS]
>
> - [SaaS データエクスポート フィードの拡張とカスタマイズ &#x200B;](extensibility-and-customizations.md) — フィード データの追加または変更。
> - [&#x200B; トラブルシューティング シナリオ &#x200B;](troubleshooting/troubleshooting-scenarios.md) – 設定ミスと予期しない同期結果を診断します。
> - [&#x200B; リリースノート &#x200B;](release-notes.md) – 拡張機能の更新と既知の問題。
