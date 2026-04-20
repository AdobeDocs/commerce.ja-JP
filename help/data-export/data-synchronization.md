---
title: SaaS データ書き出しとデータの同期
description: Adobe Commerce インスタンスと接続されたSaaS サービス間で [!DNL SaaS Data Export] がデータを収集して同期する方法について説明します。
role: Admin, Developer
exl-id: 2ca7c92a-fb52-4055-ae16-11e99b38d161
source-git-commit: 966daee60fa8945a68424fca8bda4fe4b9599872
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 0%

---

# SaaS データ書き出しとデータの同期

カタログサービス、ライブサーチ、商品レコメンデーションなどのデータ書き出しを必要とするCommerce サービスをインストールすると、データ収集と同期プロセスを管理するために、Saas データエクスポートモジュールのコレクションがインストールされます。

SaaS データ書き出しは、データを最新の状態に保つために、継続的にAdobe CommerceインスタンスからCommerce Services プラットフォームに商品データを移動します。 たとえば、商品レコメンデーションを利用するには、正しい名前、価格、在庫状況を反映したレコメンデーションを正確に返すために、最新のカタログ情報が必要です。 同期プロセスの監視について詳しくは、[同期プロセスの表示と管理](#view-and-manage-the-synchronization-process)を参照してください。


次の図は、SaaS データ書き出しフローを示しています。

Adobe Commerce![の](assets/data-export-flow.png){width="900" zoomable="yes"}SaaS データ書き出し収集と同期フロー

SaaS データエクスポートフローの主な要素には、次のようなものがあります。

- Adobe Commerceからフィード用にデータを収集し、フィード項目を組み立て、更新をリッスンして、フィードのステータスを保持するSaaS データエクスポートモジュール。
- SaaS書き出しモジュール：データの書き出し、ルーティングの設定、接続されたサービスへのフィードの公開を行います。
- Adobe Commerce Serviceは、データ収集プロセスを管理し、受信フィードを検証して、接続されたサービスに更新を永続化します。

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

### 部分同期

部分的な同期により、SaaS データの書き出しは、Commerceアプリケーションから、製品名の変更や価格の更新などの更新情報を、接続されたコマースサービスに自動的に送信します。

データ書き出しプロセスでは、次のcron ジョブを使用して、部分同期操作を自動化します。

- 「インデックス」 cron グループジョブ：
   - `indexer_reindex_all_invalid` ジョブは、すべての無効なフィードのインデックスを再作成します。 これはAdobe Commerceの標準的なcron ジョブです。
   - `saas_data_exporter` ジョブは従来の書き出しフィード用です。
   - `sales_data_exporter` ジョブは、セールスデータ書き出しフィードに固有です。

毎分このジョブが実行されます。

部分的な同期を機能させるには、Commerce アプリケーションで次の設定が必要です。

- [&#x200B; タスクのスケジュール設定はcron ジョブを使用して有効になっています](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html?lang=ja)

- すべてのSaaS データ書き出しインデクサーは`Update by Schedule` モードで設定されます。

  SaaS データ書き出しバージョン 103.1.0以降では、`Update by Schedule` モードがデフォルトで有効になっています。 Commerce CLI コマンド `bin/magento indexer:show-mode | grep -i feed`を使用して、サーバーのインデックス設定を確認できます

### 失敗した項目の同期を再試行

再試行に失敗した項目の同期では、同期プロセス中のエラー（アプリケーションエラー、ネットワークの中断、SaaS サービスエラーなど）が原因で同期に失敗した項目を再送信するために、別のプロセスを使用します。 この同期の実装もcron ジョブに基づいています。

- `resync_failed_feeds_data_exporter`件のcron グループジョブ：
   - `<feed name>_feed_resend_failed_feeds_items` ジョブは、同期に失敗した項目（例：`products_feed_resend_failed_items`）を再送信します。

### 同期プロセスの表示と管理

ほとんどの同期アクティビティは、アプリケーション設定に基づいて自動的に処理されます。 ただし、SaaS データの書き出しは、プロセスを監視および管理するためのツールも提供します。

- [!BADGE PaaSのみ]{type=Informative url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"} **[Data Management ダッシュボード &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)**：管理者ユーザーは、Commerce サービスに同期され、ストアフロントサービスで利用可能なデータを表示および追跡できます。 このダッシュボードには、Commerce Servicesに同期された商品が表示されます。

  {{aco-data-sync-verification}}

- [!BADGE SaaSのみ]{type=Positive url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce Optimizer（Adobeが管理するSaaS インフラストラクチャ）と統合されたAdobe Commerce プロジェクトに適用されます。"} **[データ同期フィード同期の状態ページ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/setup/data-sync)**-[!DNL Adobe Commerce Optimizer]を使用するCommerce プロジェクトの場合、Adobe Commerce Optimizerのデータフィード同期の状態ページから、ストアフロントのカタログデータの可用性を確認します。 このダッシュボードには、データ書き出しフィードの同期ステータスが表示されます。

>[!NOTE]
>
>データ管理ダッシュボードは、ライブサーチ、製品レコメンデーション、またはカタログサービスがインストールされている場合にのみ使用できます。 これらのサービスがある場合、または[Adobe Commerce Optimizer Connector](../aco-connector/overview.md)がインストールされている場合は、データフィード同期ステータスダッシュボードを利用できます。

### Commerce アプリケーション設定の検証

一部の同期と失敗した項目の再試行は、Commerce インスタンスが正しく設定されている場合にのみ機能します。 通常、Commerce サービスの設定時に設定は完了します。 データの書き出しが正しく機能しない場合は、次の設定を確認してください。

- [cron ジョブが実行中であることを確認します](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues)。

- インデックスが[管理者](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/tools/index-management)から実行されているか、またはCommerce CLI コマンド `bin/magento indexer:info`を使用して実行されていることを確認します。

- 次のフィードのインデックスが`Update by Schedule`に設定されていることを確認します。カタログ属性、製品、製品の上書き、製品バリアント。 管理者またはCLI （[）を使用して、](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/tools/index-management)Index Management`bin/magento indexer:show-mode | grep -i feed`のインデクサーを確認できます。

### データ転送ログのイベントマネージャー通知

バージョン 103.3.4以降では、Commerce インスタンスからAdobe Commerce サービスにデータが送信されると、SaaS Data Exportによって`data_sent_outside` イベントがディスパッチされます。

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
>イベントとそのサブスクライブ方法について詳しくは、Adobe Commerce Developer ドキュメントの[&#x200B; イベントとオブザーバー](https://developer.adobe.com/commerce/php/development/components/events-and-observers)を参照してください。
