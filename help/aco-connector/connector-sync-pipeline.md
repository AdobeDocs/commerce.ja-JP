---
title: カタログ同期パイプライン
description: フィード変換、cron スケジュール、スコープ管理、エラー処理など、 [!DNL Adobe Commerce Optimizer Connector] 同期パイプラインの仕組みについて説明します。
feature: Integration, Configuration
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
autotag-review: '2026-06-09T16:21:52.214Z'
TQID: 'https://experienceleague.adobe.com/EXUQzAd0I6Hnq4twzhaBZZnv0jLjeGBuTx-QgQz-5MA'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2: id: c18ed297-2187-4aec-affb-9d9654eca6fcid: c32adafa-ed01-4b31-997e-2413013911b0id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: cc250cf1-34eb-4863-80d0-d170d45ea067id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: addc3a3a-2b1c-4fdf-aea4-4b1eb2931ba6id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 662
ht-degree: 1%

---

# コネクタ同期パイプライン

[[!DNL SaaS Data Export]](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/overview)に基づいて構築された&#x200B;**[!DNL Adobe Commerce Optimizer Connector]**&#x200B;は、[!DNL SaaS Data Export]個のインデクサーによって収集されたデータを[!DNL Adobe Commerce Optimizer]個の[!DNL Catalog Data Ingestion API]で必要な形式にマッピングし、認証、一括送信、およびスコープベースの同期制御を処理します。 以下の節では、その同期の仕組みについて説明します。

関連トピック：

- 統合のビジネス価値、主な機能、アーキテクチャについては、[[!DNL Commerce Optimizer Connector] 概要](overview.md) トピックを参照してください。

- モジュールパッケージ名、フィード API エンドポイント、設定キーパスについては、[ コネクタリファレンス ](reference/connector-reference.md)を参照してください

## 同期の仕組み

次の図は、[!DNL Adobe Commerce]から[!DNL Commerce Optimizer]まで[!DNL Adobe I/O Gateway]までのデータ同期を示しています。

![Commerce Optimizer Connectorの高度な同期図](assets/aco-connector-sync-high-level-diagram.png){width="800" zoomable="yes"}

[!DNL Adobe Commerce]でカタログデータが変更されると、同期はこれらのステージを移動します。

1. **Entity Change Detection** — （1分ごと） cron ジョブ （`indexer_reindex_all_invalid`）は、[!DNL Adobe Commerce]個のエンティティの変更を検出し、フィード項目を組み立てる[!DNL SaaS Data Export]をトリガーします。
1. **変換** — [!DNL Commerce Optimizer Connector]は、組み立てられたフィードをピックアップし、[!DNL Adobe Commerce]個のエンティティとスコープを[!DNL Commerce Optimizer] APIで必要な形式にマッピングし、送信のためのペイロードを準備します。
1. **送信** – 変換されたデータはHTTP POST （`/v1/catalog/<feed name>`）を介して[!DNL Adobe I/O Gateway]から[!DNL Commerce Optimizer]まで送信され、受信フィードを検証して保持します。
1. **結果を永続化** — API応答ステータスを[ フィード テーブル ](reference/connector-reference.md#supported-feeds)に永続化します。
1. **失敗の再試行** （5分ごと） – 別のcron ジョブ （`*_resend_failed_items`）が失敗したフィード項目を検出し、同じパイプラインを通じて再送信します。

### スケジュール済みcron ジョブ

次のcron ジョブは、固定スケジュールでパイプラインを自動化します。

| Cron グループ | Cron ジョブ | 目的 | スケジュール |
|-------------------------------------|-------------------------------|------------------------------------------------------------------------------|----------------|
| `index` | `indexer_update_all_views` | エンティティの更新をリッスンし、フィード項目をアセンブリし、フィードのステータスを保持します | 1分ごと |
| `index` | `indexer_reindex_all_invalid` | 「Reindex required」としてマークされたフィード インデックスに対して完全な再同期を実行します | 1分ごと |
| `resync_failed_feeds_data_exporter` | `*_resend_failed_items` | 失敗したフィード項目を確認し、[!DNL Commerce Optimizer]に再送信します | 5分ごとに |
| `commerce_data_export` | `cleanup_deleted_feed_items` | 保存期間（7日間）を過ぎて同期された削除されたフィード項目をクリーンアップします | 毎日、午前2:00時 |

**[!DNL SaaS Data Export]**&#x200B;拡張機能は、フィードの収集とステータスの追跡を処理します。 コネクタレイヤーは、エンティティとスコープを[!DNL Commerce Optimizer] APIで必要な形式にマッピングし、`POST /v1/catalog/<feed name>`を介して送信します。

#### 要件定義

- [Commerce cronが実行中である必要があります](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues){target="_blank"}。
- フィードのインデクサーは&#x200B;**[!UICONTROL Update by Schedule]** モードを使用する必要があります。 [部分同期](../data-export/sync-overview.md#partial-sync){target="_blank"}を参照してください。

## スコープベースの同期制御

`CommerceOptimizerScopeMapper` モジュールは、web サイトごとの書き出し設定およびストア ビューごとの書き出し設定を読み取り、フィードの収集および送信中にそれらを適用します。

- **有効なスコープ**&#x200B;は、通常の差分スケジュールでデータを書き出します。
- **無効なスコープ**はパイプラインから除外されます。
以前に同期されたエンティティは、次回のcron実行時に[!DNL Commerce Optimizer]から削除されます。

同期の問題が1つのカタログ ソースまたは価格表のみに影響する場合は、[ データが同期されていません](troubleshooting.md#data-not-syncing)を参照してください。

同期スコープのカスタマイズについて詳しくは、[Commerce スコープの書き出し設定のカスタマイズ ](get-started.md#customize-the-commerce-scopes-export-configuration)を参照してください。

## タイミングとモニタリング

| シナリオ | 典型的なタイミング |
| -------- | -------------- |
| カタログの定期的な更新 | 1-2 delta-sync サイクル（インデックス作成と送信の場合は約1～2分） |
| 一時的なエラー | 5分ごとに再試行 |
| フルシンクまたは大きなカタログ | 分から時間 |

Commerce Adminの[[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) ページからフィードごとのステータスを監視します。 [ データ同期が機能していることを確認してください](./data-sync-manage.md#verify-that-the-data-sync-is-working)。

## フィードの送信とエラー処理

`FeedSubmitter` プロセスは[!DNL Catalog Data Ingestion API]件の呼び出しを処理します。

1. 更新項目を削除項目（異なるAPI エンドポイント）から分離します。
1. エンドポイントの更新と削除を個別に呼び出します。
1. 項目ごとのステータス結果を単一の応答にマージします。

### HTTP ステータスコード結合

更新呼び出しと削除呼び出しが異なるステータスコードを返す場合、`FeedSubmitter`は次のように結果を組み合わせます。

| 結果を更新 | 結果を削除 | 最終結果 |
| --------------- | --------------- | ------------- |
| 200 | 200またはなし | 200件の成功 |
| 200 | 400 | 200 （削除エラーあり） |
| 400 | 400 | 400件の結合エラー |
| その他 | その他 | 再試行可能 |

| エラータイプ | 動作 |
| ---------- | -------- |
| **400** | 応答`errors` フィールドにリストされている項目は、管理者に表示され、注意が必要です。 バッチ内の他の項目が再試行されます。 |
| **5xx** | `resync_failed_feeds_data_exporter` グループのフィード固有の`*_feed_resend_failed_items` cron ジョブによって再試行されました。 |

>[!MORELIKETHIS]
>
> - [ コネクタの概要](overview.md) — ビジネスのコンテキストとスコープのマッピングについて説明します
> - [ コネクタ参照](reference/connector-reference.md) — モジュール、API エンドポイント、設定キーの確認
> - [Commerce スコープの書き出し設定をカスタマイズ ](./get-started.md#customize-the-commerce-scopes-export-configuration) — スコープレベルごとにフィードを設定し、ビヘイビアーを有効または無効にし、管理手順を実行します
> - [ トラブルシューティング ](troubleshooting.md) – 同期エラーの診断
