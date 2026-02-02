---
title: データを SaaS データ書き出しと同期
description: Adobe Commerce インスタンスと接続された SaaS サ  [!DNL SaaS Data Export]  ビスとの間でデータを収集および同期する方法について説明します。
role: Admin, Developer
exl-id: 2ca7c92a-fb52-4055-ae16-11e99b38d161
source-git-commit: ea425b56fe7afd9bdaa813d040ac9e47b7022908
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 0%

---

# SaaS データ エクスポートを使用してデータを同期する

カタログサービス、Live Search、Product Recommendations などのデータのエクスポートを必要とするCommerce サービスをインストールすると、データの収集と同期のプロセスを管理するために、Saas データのエクスポートモジュールのコレクションがインストールされます。

SaaS データのエクスポートでは、商品データをAdobe Commerce インスタンスからCommerce サービスプラットフォームに継続的に移動して、データを最新の状態に保ちます。 例えば、製品レコメンデーションでは、現在のカタログ情報を使用して、正確な名前、価格、在庫を含むレコメンデーションを正確に返す必要があります。 [ データ管理ダッシュボード ](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) を使用して、同期プロセスまたはコマンドラインインターフェイスを監視および管理し、同期をトリガーして、Commerce Services で使用するために製品データを再インデックス化します。

次の図は、SaaS データの書き出しフローを示しています。

![Adobe Commerceの SaaS データ書き出し収集および同期フロー ](assets/data-export-flow.png){width="900" zoomable="yes"}

SaaS データ書き出しフローの主なコンポーネントは次のとおりです。

- Adobe Commerceからフィードのデータを収集し、フィード項目を組み立て、更新をリッスンし、フィードステータスを保持する SaaS データエクスポートモジュール。
- SaaS は、データをエクスポートするモジュールをエクスポートし、ルーティングを設定して、接続されたサービスにフィードを公開します。
- Adobe Commerce サービスは、データ取得プロセスを管理して、受信フィードを検証し、接続されたサービスの更新を保持します。

>[!NOTE]
>
>スケジュールをスムーズに設定し、サイト操作の中断を避けるために、Adobeでは、データフィードの同期を開始する前に、データの量と同期時間を予測することをお勧めします。 この見積もりは、初期同期や大規模なカタログ更新（一括価格変更など）を計画する際に重要です。 詳しくは、[ データ同期のデータ量と送信時間の予測 ](estimate-data-volume-sync-time.md) を参照してください。

## 同期モード

SaaS データ エクスポートには、エンティティ フィードを処理するための 2 つのモードがあります。

- **即時エクスポートモード** – このモードでは、データが収集され、1 回のイテレーションでCommerce サービスにすぐに送信されます。 このモードでは、Commerce サービスへのエンティティの更新の配信が高速化され、フィードテーブルのストレージサイズが縮小されます。

- **レガシーエクスポートモード** – このモードでは、データは 1 つのプロセスで収集されます。 次に、cron ジョブが、収集したデータを接続されたコマースサービスに送信します。 データ書き出しログエントリでは、レガシーモードを使用するフィードには `(legacy)` というラベルが付けられます。

## 同期タイプ

SaaS データのエクスポートでは、フル同期、部分同期、および失敗した項目同期の再試行の 3 種類の同期タイプがサポートされています。

### 完全同期

Adobe Commerce インスタンスをCommerce サービスに接続した後、完全同期を実行して、Adobe Commerceから接続されたサービスにエンティティフィードデータを送信します。

>[!NOTE]
>
>フル同期は主にオンボーディングフェーズ用です。 データベース容量超過を防ぐために、通常の使用は避けます。 初期同期の後、進行中の変更は、部分同期を使用して自動的に同期されます。

### 部分同期

部分同期を使用すると、SaaS データの書き出しは、Commerce アプリケーションから接続されたコマースサービスに、商品名の変更や価格の更新などのアップデートを自動的に送信します。

データの書き出しプロセスでは、次の cron ジョブを使用して部分同期操作を自動化します。

- cron グループジョブの「インデックス」:
   - `indexer_reindex_all_invalid` ジョブでは、無効なフィードのインデックスがすべて再作成されます。 これは、標準のAdobe Commerce cron ジョブです。
   - `saas_data_exporter` のジョブは、従来のエクスポートフィードに対するものです。
   - `sales_data_exporter` ジョブは、販売データのエクスポート フィードに固有です。

これらのジョブは毎分実行されます。

部分同期を機能させるには、Commerce アプリケーションで次の設定が必要です。

- [Cron ジョブを介してタスクスケジュールが有効になる ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html)

- すべての SaaS データ書き出しインデクサーは、`Update by Schedule` モードで設定されます。

  SaaS データ エクスポート バージョン 103.1.0 以降では、`Update by Schedule` モードはデフォルトで有効になっています。 Commerce CLI コマンド（`bin/magento indexer:show-mode | grep -i feed`）を使用して、サーバー上のインデックス設定を確認できます。

### 失敗した項目の同期を再試行

失敗した項目の同期の再試行では、アプリケーション エラー、ネットワーク障害、SaaS サービス エラーなど、同期プロセス中のエラーが原因で同期に失敗した項目を、別のプロセスを使用して再送信します。 この同期の実装は、cron ジョブにも基づいています。

- `resync_failed_feeds_data_exporter` cron グループジョブ：
   - `<feed name>_feed_resend_failed_feeds_items` ジョブは、同期に失敗した項目（例：`products_feed_resend_failed_items`）を再送信します。

### 同期プロセスの表示と管理

ほとんどの同期アクティビティは、アプリケーション設定に基づいて自動的に処理されます。 ただし、SaaS データのエクスポートには、プロセスを監視および管理するためのツールも用意されています。

- [!BADGE PaaS のみ ]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeが管理する PaaS インフラストラクチャ）およびオンプレミスプロジェクトにのみ適用されます。"}**[Data Management dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)** – 管理者ユーザーは、Commerce サービスに同期され、ストアフロントサービスで使用可能なデータを表示および追跡できます。

- [!BADGE SaaS のみ ]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce Optimizer（Adobeが管理する SaaS インフラストラクチャ）と統合されたAdobe Commerce プロジェクトに適用されます。"}**[データ同期ページ ](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/data-sync)** - [!DNL Adobe Commerce Optimizer] を使用するCommerce プロジェクトの場合、Adobe Commerce Optimizerのデータ同期ページで、ストアフロントのカタログデータの可用性を確認します。

### Commerce アプリケーション設定の確認

部分同期および失敗した項目の再試行同期は、Commerce インスタンスが正しく設定されている場合にのみ機能します。 通常、設定はCommerce サービスを設定する際に完了します。 データの書き出しが正しく機能しない場合は、次の設定を確認します。

- [cron ジョブが実行中であることを確認 ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues)

- インデクサーが [ 管理者 ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) から、またはCommerce CLI コマンド `bin/magento indexer:info` ールを使用して実行されていることを確認します。

- カタログ属性、製品、製品オーバーライド、製品バリアントのフィードのインデクサーが `Update by Schedule` に設定されていることを確認します。 インデクサーは、管理者の [ インデックス管理 ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) または CLI （`bin/magento indexer:show-mode | grep -i feed`）を使用して確認できます。

### データ転送ログのイベント マネージャー通知

バージョン 103.3.4 以降では、Commerce インスタンスからAdobe Commerce サービスにデータが送信されると、SaaS データエクスポートによって `data_sent_outside` イベントがディスパッチされます。

```php
$this->eventManager->dispatch(
   "data_sent_outside",
   [
       "timestamp" => time(),
       "type" => $metadata->getFeedName(),
       "data" => $data
   ]
);
```

>[!NOTE]
>
>イベントとその登録方法について詳しくは、Adobe Commerce Developer ドキュメントの [ イベントとオブザーバー ](https://developer.adobe.com/commerce/php/development/components/events-and-observers) を参照してください。
