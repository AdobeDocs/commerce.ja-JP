---
title: コマンドライン設定
description: インストール後、コマンドラインインターフェイス（CLI）を使用して [!DNL Payment Services] を設定できます。
role: Admin, Developer
level: Intermediate
exl-id: 265ab1be-fe52-41f3-85cb-addbc2ddfb17
feature: Payments, Checkout, Configuration, Integration, Paas
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%

---

# コマンドライン設定

[!DNL Payment Services]をインストールした後、ホーム [&#128279;](payments-home.md)内またはコマンドラインインターフェイス（CLI）経由でから簡単に設定できます。

## データ書き出しの設定

[!DNL Payment Services]は、[!DNL Magento Open Source]および[!DNL Adobe Commerce]からエクスポートされた注文データと、支払いプロバイダーからの集約された支払いデータを組み合わせて、有用なレポートを作成します。 [!DNL Payment Services]拡張機能は、レポートに必要なすべてのデータを効率的に収集するためにインデクサーを使用します。

[!DNL Payment Services]のレポートで使用されるデータについて詳しくは、[注文支払い状況レポート &#x200B;](order-payment-status.md#data-used-in-the-report)を参照してください。

### [!DNL Magento Open Source]でcronを設定

[!DNL Magento Open Source]で`BY SCHEDULE` インデックスモードを使用する場合は、cronを設定する必要があります。 [cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)の設定と実行を参照してください。

### インデクサーの設定

注文データは、2つのインデックスモード（`ON SAVE` （デフォルト）または`BY SCHEDULE` （推奨）のいずれかを使用して、決済サービスに書き出され、保持されます。

次のインデックスは[!DNL Payment Services]に対するものです：

| コード | 名前 | 説明 |
|    ---    |  ---  |  ---  |
| `sales_order_data_exporter` | 販売注文フィード | 注文データのインデックスを作成します |
| `sales_order_status_data_exporter` | 受注状況フィード | 販売注文ステータス データのインデックスを作成します |
| `store_data_exporter` | ストアフィード | ストアデータのインデックスを作成 |

3つのインデクサーすべてのインデックスモードを変更するには、次のコマンドを実行します。

```bash
bin/magento indexer:set-mode schedule sales_order_data_exporter sales_order_status_data_exporter store_data_exporter
```

>[!TIP]
>
>コマンドでインデクサーを指定しない場合、すべてのインデクサーが同じ値に更新されます。 特定のインデクサーを変更する場合は、そのインデクサーをコマンドにリストする必要があります。

インデクサーのモードを手動で変更する方法について詳しくは、開発者ドキュメントの「[&#x200B; インデクサーの設定](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers#configure-indexers){target="_blank"}」を参照してください。 管理画面で変更する方法については、コアユーザーガイドの[&#x200B; インデックス管理](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management#change-the-index-mode){target="_blank"}を参照してください。

### データを手動で再インデックス付け

データが自動的に処理されるのを待つのではなく、手動でデータのインデックスを再作成できます。 詳しくは、[&#x200B; インデクサーの管理](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers){target="_blank"}の[&#x200B; インデックス再作成](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers#reindex){target="_blank"}を参照してください。

`BY SCHEDULE` モードが設定されると、システムは変更されたエンティティを追跡し、cron ジョブは設定されたスケジュールに基づいてエンティティのインデックスを更新します。 cron ジョブを使用してインデックス作成を手動でトリガーする方法については、[Configure and run cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)）の「[&#x200B; コマンドラインからcronを実行](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs#config-cli-cron-group-run)」を参照してください。

### インデックス再作成されたデータを支払いサービスに送信する

データのインデックスが作成されると、自動的に[!DNL Payment Services]に送信されます。 このコマンドを使用して、インデックス付きデータを送信するプロセスを手動でトリガーすることもできます。

```bash
bin/magento saas:resync --feed [feedName]
```

次のコマンドオプションを使用します。

| コマンド | 説明 |
|  ---  |  ---  |
| `bin/magento saas:resync --feed [feedName]` | 指定したフィードのインデックス再作成を実行し、対応するサービスに送信します |
| `bin/magento saas:resync --no-reindex` | インデックスをスキップし、インデックスから同期されていないデータを送信します |

`--feed` パラメーターを使用すると、送信するフィードを指定できます。

| フィード | 説明 |
|  ---  |  ---  |
| `paymentServicesOrdersProduction` | 実稼動モードでの注文フィード |
| `paymentServicesOrdersSandbox` | サンドボックスモードでの注文フィード |
| `paymentServicesOrderStatusesProduction` | 実稼動モードでの注文ステータス |
| `paymentServicesOrderStatusesSandbox` | サンドボックスモードでの注文ステータス |
| `paymentServicesStoresProduction` | 実稼動モードでのストア |
| `paymentServicesStoresSandbox` | サンドボックスモードでのストア |

cronを設定してインストールすると、レポートに必要なすべてのデータが自動的に[!DNL Payment Services]に送信されます。 cron データを[!DNL Payment Services]に送信するプロセスを手動でトリガーすることもできます。

```bash
bin/magento cron:run --group payment_services_data_export
```

インデックス再作成とインデックス作成について詳しくは、開発者ドキュメントの「[&#x200B; インデックスの管理](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers)」トピックを参照してください。

## CLIによるスコープの設定

[!DNL Payment Services]では、販売者が[複数のPayPal アカウント &#x200B;](configure-admin.md#use-multiple-paypal-accounts)を使用できます。 次に、CLIを使用してこれらのアカウントのスコープを変更できます。

スコープを`website` レベルに設定するには、次を実行します。

```bash
bin/magento config:set payment/payment_services/mba_scoping_level website
```

スコープを`store` レベルに設定するには、次を使用します。

```bash
bin/magento config:set payment/payment_services/mba_scoping_level store
```

>[!TIP]
>
> 範囲を店舗レベルに変更する場合は、[!DNL Payment Services]の営業担当者にお問い合わせください。

範囲を変更したら、キャッシュをフラッシュして変更を表示します。

```bash
bin/magento cache:clean:payment_services_merchant_scopes
```

## L2/L3処理の設定

[!DNL Payment Services]は、カード支払いトランザクションからレベル 2およびレベル 3のデータを処理して、加盟店に追加情報を提供できます。

>[!WARNING]
>
> PayPalを使用したレベル 2およびレベル 3の処理との統合は、米国の販売者のみが利用できます。 詳しくは、PayPal デベロッパーのドキュメントの[決済処理](https://developer.paypal.com/docs/checkout/advanced/processing/){target=_blank}を参照してください。

[!DNL Payment Services]のL2/L3処理データを使用する場合、または質問がある場合は、[!DNL Payment Services]のアカウントマネージャーにお問い合わせください。

[!DNL Payment Services]で使用されるL2およびL3処理について詳しくは、[&#x200B; レベル 2およびレベル 3処理](levels-card-payment-transactions.md)を参照してください。
