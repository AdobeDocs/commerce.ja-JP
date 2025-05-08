---
title: コマンドライン設定
description: インストール後、コマンドラインインターフェイス（CLI）を使用して設定  [!DNL Payment Services]  使用できます。
role: Admin, Developer
level: Intermediate
exl-id: 265ab1be-fe52-41f3-85cb-addbc2ddfb17
feature: Payments, Checkout, Configuration, Integration, Paas
badgePaas: label="PaaS のみ" type="Informative" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeが管理する PaaS インフラストラクチャ）およびオンプレミスプロジェクトにのみ適用されます。"
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 0%

---

# コマンドライン設定

[!DNL Payment Services] をインストールしたら、[ ホーム内 ](payments-home.md) またはコマンドラインインターフェイス（CLI）を使用して簡単に設定できます。

## データの書き出しの設定

[!DNL Payment Services] は、[!DNL Magento Open Source] および [!DNL Adobe Commerce] から書き出された注文データを、支払いプロバイダーからの集計された支払いデータと組み合わせて、有用なレポートを作成します。 [!DNL Payment Services] 拡張機能では、インデクサーを使用して、レポートに必要なすべてのデータを効率的に収集します。

[!DNL Payment Services] のレポートで使用されるデータについて詳しくは、[ 注文支払いステータスレポート ](order-payment-status.md#data-used-in-the-report) を参照してください。

### [!DNL Magento Open Source] での cron の設定

[!DNL Magento Open Source] で `BY SCHEDULE` インデックスモードを使用する場合は、cron を設定する必要があります。 [cron の設定と実行 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) を参照してください。

### インデクサーの設定

注文データは、`ON SAVE` （デフォルト）または `BY SCHEDULE` （推奨）のいずれかのインデックスモードを使用して、支払いサービスに書き出され、保持されます。

次のインデックスは [!DNL Payment Services] 用です。

| コード | 名前 | 説明 |
|    ---    |  ---  |  ---  |
| `sales_order_data_exporter` | 販売注文フィード | 注文データのインデックスを作成 |
| `sales_order_status_data_exporter` | 販売注文ステータス フィード | 販売注文の状態データのインデックスを作成します |
| `store_data_exporter` | フィードを保存 | ストアデータのインデックスを作成します |

3 つのインデクサーすべてのインデックスモードを変更するには、次を実行します。

```bash
bin/magento indexer:set-mode schedule sales_order_data_exporter sales_order_status_data_exporter store_data_exporter
```

>[!TIP]
>
>コマンドでインデクサーを指定しない場合、すべてのインデクサーが同じ値に更新されます。 特定のインデクサーを変更する場合は、コマンドでそのインデクサーをリストする必要があります。

インデクサーのモードを手動で変更する方法については、開発者向けドキュメントの [ インデクサーの設定 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/cli/manage-indexers#configure-indexers){target="_blank"} を参照してください。 管理者で変更する方法については、『コアユーザーガイド』の [ インデックス管理 ](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/tools/index-management#change-the-index-mode){target="_blank"} を参照してください。

### データを手動で再インデックス化

データが自動的に実行されるのを待たずに、手動でデータをインデックス再作成できます。 詳しくは、[&#128279;](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/cli/manage-indexers#reindex) インデクサーの管理 [ の ](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/cli/manage-indexers){target="_blank"} インデックス再作成 {target="_blank"} を参照してください。

モード `BY SCHEDULE` 設定すると、システムは変更されたエンティティを追跡し、cron ジョブは設定されたスケジュールに基づいてエンティティのインデックスを更新します。 Cron ジョブを使用してインデックスを手動でトリガーする方法については、[Configure and run cron](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) の [ コマンドラインからの Run cron](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs#config-cli-cron-group-run) を参照してください。

### インデックス再作成されたデータを支払サービスに送信

インデックスが作成されたデータは、[!DNL Payment Services] に自動的に送信されます。 また、次のコマンドを使用して、インデックス付きデータを送信するプロセスを手動でトリガーすることもできます。

```bash
bin/magento saas:resync --feed [feedName]
```

次のコマンドオプションを使用します。

| コマンド | 説明 |
|  ---  |  ---  |
| `bin/magento saas:resync --feed [feedName]` | 指定されたフィードのインデックス再作成を実行し、対応するサービスに送信します |
| `bin/magento saas:resync --no-reindex` | インデックス化をスキップし、非同期データをインデックスから送信します。 |

`--feed` パラメーターを使用すると、送信するフィードを指定できます。

| フィード | 説明 |
|  ---  |  ---  |
| `paymentServicesOrdersProduction` | 生産モードでの注文フィード |
| `paymentServicesOrdersSandbox` | サンドボックスモードでの注文フィード |
| `paymentServicesOrderStatusesProduction` | 生産モードでの注文ステータス |
| `paymentServicesOrderStatusesSandbox` | サンドボックスモードでのステータスの並べ替え |
| `paymentServicesStoresProduction` | 実稼動モードのストア |
| `paymentServicesStoresSandbox` | サンドボックスモードのストア |

cron が設定およびインストールされている場合、レポートに必要なすべてのデータは自動的に [!DNL Payment Services] に送信されます。 cron データを [!DNL Payment Services] に送信するプロセスを手動でトリガーすることもできます。

```bash
bin/magento cron:run --group payment_services_data_export
```

再インデックスとインデクサーについて詳しくは、開発者向けドキュメントの [ インデクサーの管理 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/cli/manage-indexers) に関するトピックを参照してください。

## CLI を使用したスコープの設定

[!DNL Payment Services] では、マーチャントは [ 複数の PayPal アカウント ](settings.md#use-multiple-paypal-accounts) を使用できます。 これで、CLI を使用してこれらのアカウントのスコープを変更できます。

スコープを `website` レベルに設定するには、次を実行します。

```bash
bin/magento config:set payment/payment_services/mba_scoping_level website
```

スコープを `store` レベルに設定するには、次を使用します。

```bash
bin/magento config:set payment/payment_services/mba_scoping_level store
```

>[!TIP]
>
> 範囲を店舗レベルに変更する場合は、[!DNL Payment Services] の販売担当者にお問い合わせください。

範囲を変更したら、キャッシュをフラッシュして変更を表示します。

```bash
bin/magento cache:clean:payment_services_merchant_scopes
```

## L2/L3 処理の設定

カ [!DNL Payment Services] ド支払取引のレベル 2 およびレベル 3 のデータを処理して、マーチャントに追加情報を提供できます。

>[!WARNING]
>
> PayPal を使用したレベル 2 およびレベル 3 の処理との統合は、米国のマーチャントのみが利用できます。 詳しくは、PayPal Developer ドキュメントの [ 支払い処理 ](https://developer.paypal.com/docs/checkout/advanced/processing/){target=_blank} を参照してください。

L2/L3 の処理データを [!DNL Payment Services] に使用する場合、またはご質問がある場合は、[!DNL Payment Services] アカウントマネージャーにお問い合わせください。

[!DNL Payment Services] で使用される L2 および L3 処理については、[ レベル 2 およびレベル 3 処理 ](levels-card-payment-transactions.md) を参照してください。
