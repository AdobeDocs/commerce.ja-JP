---
title: SaaS データ書き出しとデータの同期
description: ' [!DNL SaaS Data Export] 様が、Adobe Commerce インスタンスと接続されたCommerce サービスとの間でデータを収集および同期する方法について説明します。'
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 2ca7c92a-fb52-4055-ae16-11e99b38d161
TQID: https://experienceleague.adobe.com/wM71qxvduDr77EW6Y8mSNfBXlqkloC-PGOOBOl-mZQM
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: ef1a9efc579d8d21c145e6981235489a2e4ea203
workflow-type: tm+mt
source-wordcount: 907
ht-degree: 0%

---

# SaaS データ書き出しとデータの同期

カタログサービス、ライブサーチ、製品レコメンデーションなどのデータ書き出しを必要とする[!DNL Adobe Commerce] サービスをインストールすると、データ収集と同期プロセスを管理するために、SaaS データ書き出しモジュールのコレクションがインストールされます。

SaaS データ書き出しは、データを最新の状態に保つために、継続的にAdobe CommerceインスタンスからCommerce Services プラットフォームに商品データを移動します。 たとえば、商品レコメンデーションを利用するには、正しい名前、価格、在庫状況を反映したレコメンデーションを正確に返すために、最新のカタログ情報が必要です。 同期プロセスの監視について詳しくは、[同期プロセスの表示と管理](data-sync-manage.md)を参照してください。

次の図は、SaaS データ書き出しフローを示しています。

Adobe Commerce![&#128279;](assets/data-export-flow.png){width="900" zoomable="yes"}のSaaS データ書き出し収集と同期フロー

[!DNL Adobe Commerce]でカタログデータが変更されると、同期はこれらのステージを移動します。

1. **エンティティの変更の検出** - MagentoのMview システムは、購読されたデータベース テーブル （例：`catalog_product_entity`）の行の変更を検出し、変更ログ テーブルにエントリを書き込みます。
1. **フィードのインデックス作成** - フィードのインデクサーは、変更ログを読み取り、ソーステーブルからエンティティ データを読み込み、フィード アイテムをアセンブリします。
1. **データの収集と変換** - フィード スキーマ [`et_schema.xml`](extensibility-and-customizations.md#feed-schema-overview)に登録されているプロバイダーは、フィールド データを収集します。
1. **ハッシュ重複排除** - フィード項目ごとにコンテンツハッシュが計算されます。 前回の書き出しからハッシュが変更されていない項目はスキップされるので、変更されたデータのみが送信されます。
1. **HTTP送信** - フィード項目は、認証されたHTTP POST バッチとしてAdobe SaaS フィード取得サービスに送信されます。
1. **ステータスの永続性** - API応答のステータスが、各項目の[&#x200B; フィードテーブル &#x200B;](reference/feed-table-reference.md)に書き戻されます。
1. **失敗の再試行** – 書き出しに失敗したアイテムは、スケジュールされたcron ジョブによって自動的に再試行されます。

>[!NOTE]
>
>[!DNL Adobe Commerce Optimizer Connector]回のデプロイメントの場合、[!DNL SaaS Data Export]はエンティティの変更の検出とフィード アセンブリを処理します。 その後、コネクタはフィードを[!DNL Catalog Data Ingestion API]形式にマッピングし、[!DNL Adobe Commerce Optimizer]に送信します。 スコープの制御、送信、エラー処理については、[&#x200B; コネクタ同期パイプライン &#x200B;](../aco-connector/connector-sync-pipeline.md)を参照してください。

>[!NOTE]
>
>スムーズなスケジュール設定を実現し、サイト運用の中断を回避するために、Adobeでは、データフィードの同期を開始する前に、データ量と同期時間を見積もることをお勧めします。 この見積もりは、初回の同期や、大量価格の変更などの大規模なカタログ更新を計画する際に重要です。 詳しくは、[&#x200B; データ同期のデータ量と送信時間の見積もり](estimate-data-volume-sync-time.md)を参照してください

## 同期モード

SaaS データの書き出しには、エンティティフィードを処理するための2つのモードがあります。

- **即時エクスポート モード** – このモードでは、データが収集され、1回のイテレーションですぐにCommerce サービスに送信されます。 このモードは、Commerce サービスへのエンティティ更新の配信を高速化し、フィードテーブルのストレージサイズを削減します。

- **従来の書き出しモード** – このモードでは、データは単一のプロセスで収集されます。 次に、cron ジョブが、収集したデータを接続されたコマースサービスに送信します。 データ書き出しログのエントリでは、従来のモードを使用するフィードには`(legacy)`というラベルが付けられます。

## 同期タイプ

SaaS データの書き出しは、3つの同期タイプのフル同期、部分同期、失敗した項目の同期を再試行することをサポートしています。

### 完全同期

Adobe Commerce インスタンスをCommerce サービスに接続した後、完全同期を実行して、Adobe Commerceから接続されたサービスにエンティティ フィード データを送信します。

>[!NOTE]
>
>完全同期は主にオンボーディングフェーズ用です。 データベースの過負荷を防ぐために、定期的な使用は避けてください。 初期同期後、部分同期を使用して継続的な変更が自動的に同期されます。

>[!NOTE]
>
>`saas:resync` コマンドは、新しい項目、更新された項目、以前に書き出せなかった項目のみを送信します。 前回の書き出し以降にコンテンツハッシュが変更されていない項目はスキップされます。

### 部分同期 {#partial-sync}

部分的な同期により、SaaS データの書き出しは、Commerceアプリケーションから、製品名の変更や価格の更新などの更新情報を、接続されたコマースサービスに自動的に送信します。
部分的な同期を機能させるには、Commerce アプリケーションで次の設定が必要です。

- [タスクのスケジュール設定は、cron ジョブを介して有効になります](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html)
- すべてのSaaS データ書き出しインデクサーは`Update by Schedule` モードで設定されます。

### 失敗した項目の同期を再試行 {#retry-failed-items-sync}

再試行に失敗した項目の同期では、同期プロセス中のエラー（アプリケーションエラー、ネットワークの中断、SaaS サービスエラーなど）が原因で同期に失敗した項目を再送信するために、別のプロセスを使用します。 `resync_failed_feeds_data_exporter` グループの`*_resend_failed_items` cron ジョブは、5分ごとに自動的にこれを処理します。

## スケジュール済みcron ジョブ

次のcron グループは、固定スケジュールでパイプラインを自動化します。

| Cron グループ | Cron ジョブ | 目的 | スケジュール |
|---|---|---|---|
| `index` | `indexer_update_all_views` | プロセス Mviewの変更ログとトリガーの部分的なフィード更新 | 1分ごと |
| `index` | `indexer_reindex_all_invalid` | 「Reindex required」としてマークされたフィード インデックスの完全な再同期を実行します | 1分ごと |
| `resync_failed_feeds_data_exporter` | `*_resend_failed_items` | 失敗したフィード項目を検出して再送信します | 5分ごとに |
| `commerce_data_export` | `saas_data_exporter` | レガシーモードのフィード（注文、スコープ）のデータを送信します | 5分ごとに |
| `commerce_data_export` | `cleanup_deleted_feed_items` | 保存期間（7日間）を過ぎて同期された削除されたフィード項目をクリーンアップします | 毎日、午前2:00時 |

## フィード送信とHTTP エラー処理 {#feed-submission-and-http-error-handling}

フィード項目は、HTTP POST経由で認証されたgzip圧縮JSON バッチとして送信されます。 次の表は、HTTP応答コードがステータスのエクスポートと再試行動作にどのようにマッピングされるかを示しています。

| ステータスコード | 再試行しますか？ | 意味 |
|-------------|--------|---------------------------------------------------------------------------------------------------------------------|
| 200 | いいえ | 正常に承認されました |
| 400 | いいえ | 不正なデータまたは検証エラー – 手作業による調査が必要です。 詳細については、`var/log/saas-export-errors.log`を確認してください。 |
| 429 | はい | レート制限ヒット - [書き出し処理設定](customize-export-processing.md)の`thread_count`を減らします |
| 5xx | はい | SaaS側エラー – 自動再試行 |
| 2 | はい | アイテムは再試行の予定です |

HTTP レベルのエラーに加えて、ローカル処理エラーやネットワーク障害などのアプリケーションレベルのエラーも、`*_resend_failed_items` cron ジョブによる自動再試行のためにスケジュールされます。

Commerce Adminの[[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) ページからフィードごとのステータスを監視します。

>[!MORELIKETHIS]
>
> - [同期を管理](data-sync-manage.md) – 同期ステータスを確認し、フィードを手動で再同期します。
> - [&#x200B; フィード テーブル スキーマ &#x200B;](reference/feed-table-reference.md) – 項目レベルのステータスとエラーの詳細を調べます。
> - [&#x200B; データ書き出しのパフォーマンスを向上](customize-export-processing.md) — バッチ サイズとスレッド数を調整します。
