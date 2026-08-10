---
title: カタログイベントの設定と統合ガイド
description: カタログデータの検証、Adobe Commerceの [!DNL Adobe I/O Events] の設定、カタログイベントタイプの購読、消費者への配信の検証の方法について説明します。
level: Intermediate
recommendations: noCatalog
role: Admin, Developer
feature: Services, Catalog Service
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 818efacb8dbf63e48cdc83506d228c665d7a8b22
workflow-type: tm+mt
source-wordcount: 1568
ht-degree: 0%

---

# Adobe I/Oでのカタログイベントの有効化と設定

カタログイベントは、[!DNL Catalog Service]を通じて使用可能になった、サポートされているカタログの変更を説明する機械生成の通知です。 これらのツールは、次のようなイベント駆動型ワークフローを実現します。

* 外部キャッシュまたはサービスをカタログの更新と同期させる。
* 製品、バリエーション、価格、カテゴリーが変更されたときに下流プロセスをトリガーします。
* ほぼリアルタイムのカタログ更新を必要とする、Experience Edgeと[!DNL Edge Delivery Services]のユースケースを強化しています。

[!DNL Adobe Commerce]からイベントコンシューマーへのエンドツーエンドのパスについては、[&#x200B; イベント配信から [!DNL Adobe I/O Events]](#event-delivery-through-adobe-io-events)を参照してください。

## サポートされているイベントタイプ {#supported-event-types}

カタログイベントは、[!DNL Adobe Developer Console]を通じて公開されたストアフロント関連の変更に焦点を当てています。 現在、次のサブスクリプションがサポートされています。

| 購読 | イベント |
| --- | --- |
| 製品アップデート | [!DNL Catalog Service]を通じて利用可能な製品の変更を作成、更新、削除する |
| 価格更新 | ストアフロントのカタログデータに影響を与える変更の価格作成、更新、削除 |

各イベントには、次のものが含まれます。

* 変更タイプを説明するイベント ID。
* インスタンス IDやSKUなどのエンティティと環境のコンテキスト。
* 変更されたエンティティと関連するスコープ情報を説明するペイロード。


## イベントペイロードの例

**ProductUpdated イベント**

```json
{
  "imsOrgId": "aaa-0",
  "instanceId": "instance-9",
  "eventCode": "productUpdated",
  "sku": "1234",
  "links": [
    {"type":  "variantOf", "sku": "5678"}
   ],
  "scope": [
    { "storeViewCode": "US-us" },
    { "storeViewCode": "FR-fr" },
    { "storeViewCode": "DE-de" }
  ]
}
```

**PriceUpdated イベント**

```json
{
  "imsOrgId": "aaa-0",
  "instanceId": "instance-9",
  "eventCode": "priceUpdated",
  "sku": "1234",
  "scope": [
    {
      "websiteCode": "website1",
      "customerGroupCode": "customer-group-code1"
    },
    {
      "websiteCode": "website2",
      "customerGroupCode": "customer-group-code2"
    }
  ]
}
```

## [!DNL Adobe I/O Events]を通じたイベント配信 {#event-delivery-through-adobe-io-events}

[!DNL Adobe I/O Events]は、統合にカタログイベントを配信します。 次の図は、購読済み消費者に対する[!DNL Adobe Commerce]から[!DNL Catalog Service]および[!DNL Adobe I/O Events]までのカタログ変更の上位レベルのフローを示しています。

![Adobe CommerceからカタログサービスおよびAdobe I/O Eventsを通じて、購読済み消費者に対してカタログイベントの高レベルのフロー](assets/catalog-service-event-pipeline.png)

以下の手順では、各ハンドオフについて詳しく説明します。

1. **Adobe Commerce → Catalog Service**

[!DNL Adobe Commerce]は、サポートされているSaaS データ書き出し拡張機能を使用して、カタログデータを[!DNL Catalog Service]に書き出します。

1. **カタログサービス処理**

   * [!DNL Catalog Service]件のプロセスがカタログの変更をサポートし、イベントの配信用に準備しました。

1. **カタログサービス → Adobe I/O Events**

* カタログイベントは[!DNL Adobe I/O Events]に公開されます。
* 消費者は、ジャーナリング、webhook、[!DNL Adobe I/O Runtime]、Amazon EventBridge、またはその他のサポートされている配信メカニズムを使用して購読します。

[!DNL Adobe I/O Events]の提供：

* 購読者ごとに&#x200B;*少なくとも1回の配信* （重複イベントが可能）。
* 配送をまたいだ注文保証はありません。

消費者は、重複したイベントや不定期な配信に対応する必要があります。 実装ガイダンスについては、[Idempotency](#idempotency)を参照してください。

## ユースケース {#use-cases}

カタログイベントは、複数のシナリオで使用できます。

### 静的なサイトとエッジ配信

* カタログデータが変更されたときに、カタログページとストアフロントフラグメントを再生成または無効化します。
* [!DNL Catalog Service]個のAPIに対する頻繁なポーリングは避けてください。

### 検索のインデックス作成とキャッシュ

* 下流の検索インデックスの増分更新をトリガーします。
* 製品またはカテゴリデータが変更されたときに、カタログのキャッシュレイヤーまたは外部ビューを更新します。

### 外部システムとの統合

* カタログの変更を、PIM、価格設定エンジン、その他の基幹システムなどの外部システムに転送します。
* データベースに直接アクセスすることなく、アプリケーションを同期できます。

### 監視と監視

カタログイベントを既存の監視（例：[!DNL Grafana]および[!DNL Prometheus]）と組み合わせて、次の操作を行います。

* イベントのスループットの監視：
* カタログの更新量の異常値を検出します。

## カタログイベントの有効化 {#enable-catalog-events}

カタログイベントをエンドツーエンドで有効にするには、次の手順に従います。

>[!PREREQUISITES]
>
>カタログイベントを有効にする前に、次のことを確認してください。
>
>* [!DNL Catalog Service]が有効になっている、サポートされているAdobe Commerce環境。
>* [Adobe Commerce](https://developer.adobe.com/commerce/extensibility/events/configure-commerce)用に [!DNL Adobe I/O] 接続が構成されています。
>* Commerce環境がプロビジョニングされている同じIMS組織内の[!DNL Adobe Developer Console]へのアクセス。
>* Commerce SaaS サービスへの同期を確認するには、管理者で&#x200B;**[!UICONTROL Data Management Dashboard]**&#x200B;を使用します。
>* ダッシュボードの検証には、製品レコメンデーション v6.0、[!DNL Live Search] v4.1.0以降、または[!DNL Catalog Service] v1.17以降が必要です。 Adobeでは、Commerce プロジェクトを、サポートされている最新バージョンのサービスにアップデートすることをお勧めします。 以前のバージョンのサービスの場合は、[&#x200B; カタログ同期](https://experienceleague.adobe.com/ja/docs/commerce/user-guides/data-services/catalog-sync)を使用して同期検証を行います。


>[!NOTE]
>
>カタログイベントを使用するには、まず[!DNL Adobe I/O Events]用にCommerce環境を設定し、次に[!DNL Adobe Developer Console]にイベントサブスクリプションを登録します。
>
>設定後に環境が[!DNL Adobe Developer Console]に表示されない場合は、正しいIMS組織にサインインしていること、およびアカウントに必要なアクセス権があることを確認してください。 それでも環境が表示されない場合は、Adobe サポートにお問い合わせください。

### カタログデータの検証 {#verify-catalog-data}

設定する前に、[!DNL Catalog Service]が[!DNL Commerce] インスタンスからの現在のカタログ データを持っていることを確認してください。 カタログイベントは、[!DNL SaaS Data Export]が2つのステージを完了するかどうかによって異なります。**両方**&#x200B;を確認してください。

1. Commerce **からの** フィードの書き出しが正常に完了したことを確認します。

   [!DNL Adobe Commerce]管理者から、[&#x200B; データフィード同期ステータス &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) ページ （**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**）を開き、[!DNL Catalog Service]個のフィードごとに最後の書き出しステータスが成功したことを確認します。

1. [!DNL Adobe Commerce]管理者から接続されたCommerce サービス **への**&#x200B;同期が正常に完了したことを確認します。

   [!DNL Adobe Commerce]管理者から、[&#x200B; データ管理ダッシュボード &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) （**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Management Dashboard]**）を開き、同期された製品データに必要な製品が含まれていることを確認します。

### [!DNL Adobe I/O Events]に登録して購読 {#register-events}

サブスクライブするCommerce イベントを定義し、プロジェクトに登録します。

インスタンスが選択リストに含まれていない場合は、[!DNL Adobe I/O]に接続されていません。 この問題を解決する手順については、*Adobe Commerce Developer* ドキュメントの[Configure the [!DNL Adobe I/O] connection](https://developer.adobe.com/commerce/extensibility/events/configure-commerce#configure-the-adobe-io-connection)を参照してください。

1. [!DNL Adobe Developer Console]から、Commerce プロジェクトに使用されているのと同じIMS組織にログインします。

1. Commerce カタログイベント用のプロジェクトを作成するか、イベント APIを既存のプロジェクトに追加します。

   * 上部のナビゲーションで「**[!UICONTROL APIs and services]**」を選択します。

   * **[!UICONTROL Browse APIs and services]** ページで、「**[!UICONTROL Events]**」タブを選択します。

   * Commerce Catalog Events APIを迅速に検索します。 検索ボックスに「_カタログ_」と入力するか、商品&#x200B;**[!UICONTROL Commerce]**&#x200B;で絞り込みます。

   * **[!UICONTROL Commerce Catalog Events]** カードで、**[!UICONTROL Project]**&#x200B;を選択します。

   ![Commerce カタログイベントプロバイダーが「APIとサービスを参照」ページで選択されました](assets/catalog-event-select-provider.png){width="600" zoomable="yes"}

1. イベント登録を設定します。

   イベント通知を受け取るCommerce インスタンスを選択します。 次に、**[!UICONTROL Next]**&#x200B;を選択します。

   イベント登録画面で![Commerce インスタンスが選択されました](assets/catalog-event-registration.png){width="600" zoomable="yes"}

1. 購読するイベントを選択します。

   受信するサポートされているイベント サブスクリプション（**[!UICONTROL Product Update]**&#x200B;または&#x200B;**[!UICONTROL Price Update]**&#x200B;など）を選択します。 次に、**[!UICONTROL Next]**&#x200B;を選択します。

   登録画面で![&#x200B; サブスクリプション用に選択されたイベントカテゴリ &#x200B;](assets/catalog-event-subscription.png){width="600" zoomable="yes"}

1. OAuth サーバー間資格情報を追加します。

   **[!UICONTROL Credential name]**&#x200B;を入力します。 次に、**[!UICONTROL Next]**&#x200B;を選択します。

1. **[!UICONTROL Event registration name]**&#x200B;と&#x200B;**[!UICONTROL Event registration description]**&#x200B;を入力します。 次に、**[!UICONTROL Next]**&#x200B;を選択します。

1. 最終的な登録画面で、デフォルトのコンシューマーであるJournaling APIを受け入れます。

   デフォルトのJournaling API コンシューマーでは、イベント登録をテストし、イベントが配信されていることを確認できます。 Webhookまたは[!DNL Adobe I/O Runtime]個のアクションコンシューマーを既に設定している場合は、ここで選択します。 それ以外の場合は、消費者の準備が整ったら、後でイベント登録を編集します。

   イベント登録完了画面で![Journaling API コンシューマーのデフォルトが選択されました](assets/catalog-event-consumer.png){width="600" zoomable="yes"}

1. **[!UICONTROL Complete registration]**&#x200B;を選択します。

### イベントコンシューマーの設定 {#configure-consumer}

1. 次のようなコンシューマーを設定します。

   * Webhook エンドポイント
   * [!DNL Adobe I/O Runtime] アクション
   * サポートされている別の宛先

1. 登録中に消費者を選択しなかった場合は、イベント登録を編集して消費者の詳細を追加します。

   * [!DNL Adobe Developer Console]から、プロジェクトを編集します。 次に、作成したイベント登録を選択します。

   * イベント登録の詳細ページで、**[!UICONTROL Edit Events Registration]**&#x200B;を選択します。

   * コンシューマー選択画面に到達するまで&#x200B;**[!UICONTROL Next]**&#x200B;を選択します。 次に、設定したコンシューマーを選択します。

   * 設定した宛先にコンシューマーを更新します。 次に、**[!UICONTROL Save configured events]**&#x200B;を選択します。

### イベントフローの検証 {#validate-event-flow}

カタログイベントは、環境に対して有効になっています。 [!DNL Commerce]でカタログデータが変更されると、更新は[!DNL Catalog Service]から[!DNL Adobe I/O Events]に流れ、購読者の消費者は対応するカタログイベントを受け取ります。 実稼動統合を構築する前に、[制限とベストプラクティス &#x200B;](#limits-and-best-practices)を確認してください。
1. 商品名の更新や価格の変更など、サポートされている単純なカタログを変更します。

1. 次の結果を確認します。

   * 変更は[!DNL Catalog Service] APIを通じて表示されます。
   * お客様の[!DNL Adobe I/O Events] コンシューマーは、対応する製品または価格イベントを受け取ります。


## 制限事項とベストプラクティス {#limits-and-best-practices}

カタログイベントを作成する場合は、次のベストプラクティスに従います。

### Idempotency {#idempotency}

[!DNL Adobe I/O Events]は同じカタログ イベントを複数回配信でき、1つの製品のイベントは注文をキャンセルできます。 次のような能力を顧客向けに設計：

* バージョンまたはタイムスタンプフィールドでエンティティ IDを使用する。
* 同じ変更に対して重複する通知を安全に無視します。

### スループットとバックプレッシャー

更新率が高い大規模なカタログは、大きなイベント量を生み出す可能性があります。 次のことを確認します。

* 消費者は、ピーク時のスループットでイベントを処理できます。
* 必要に応じて、バッファリング、バッチ、キューを使用します。

### セキュリティと分離

* [!DNL Adobe I/O Events]では、*テナント分離*&#x200B;が適用されます。
* 組織は、独自の環境と使用権限に対してのみイベントを受け取ります。

### スキーマの進化

カタログイベントペイロードは、[!DNL Catalog Service] APIと同じ概念モデルに従います。 前方互換性を維持するには：

* 可能な限り、厳格なスキーマ適用を避けます。
* 失敗する代わりに、不明なフィールドを無視します。

## カタログイベントのトラブルシューティング {#troubleshoot-catalog-events}

カタログイベントが欠落または遅延している場合は、次の手順に従います。

1. **カタログサービスデータを確認**

   [&#x200B; [!DNL Catalog Service] API](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/)を使用して、カタログの変更が正常に保存されていることを確認します。

1. **確認[!DNL SaaS Data Export]**

   カタログイベントには[!DNL Catalog Service]の現在のデータが必要です。 エクスポートパスの両方のステージを確認します。

   * **Commerce**&#x200B;からのフィードの書き出し – [&#x200B; データフィードの同期ステータス &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) ページまたは`var/log/saas-export.log`で、[!DNL Catalog Service] フィードが[!DNL Commerce]から正常に書き出されたことを確認します。

   * **接続済みのCommerce SaaS サービスへの同期** — [Data Management ダッシュボード &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)、[&#x200B; カタログ同期](https://experienceleague.adobe.com/ja/docs/commerce/user-guides/data-services/catalog-sync)または書き出しログで、データが[!DNL Catalog Service]に正常に同期されたことを確認します。

   書き出しと同期のジョブのトラブルシューティングについては、[&#x200B; データとSaaS データの書き出しの同期](../data-export/data-sync-manage.md)および[&#x200B; ログとトラブルシューティング &#x200B;](../data-export/troubleshooting/logging.md)を参照してください。

1. **設定[!DNL Adobe I/O Events]を検証**

   次のことを確認します。

   * [!DNL Adobe Developer Console]の正しいIMS組織にログインしています。
   * **[!UICONTROL Commerce Catalog Events]** プロバイダーが有効になっています。
   * 予想される&#x200B;**[!UICONTROL Commerce Catalog Events]** プロバイダーと環境が表示されます。
   * サブスクリプションはアクティブです。
   * エンドポイント、アクション、またはジャーナルコンシューマーは、テストイベントを受信して処理できます。

1. **Adobe サポートへのお問い合わせ**

   サポートチケットを開く際に、**Adobe Commerce アプリケーション**&#x200B;に対応する問題の理由を選択し、次の情報を含めます。

   * カタログサービス詳細（環境、地域）。
   * [!DNL Adobe I/O Events] サブスクリプションの詳細。
   * 欠落しているイベントの概算の時間と説明。

   詳細なヘルプについては、[&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#support-case)を参照してください。

>[!MORELIKETHIS]
>
>
>* [&#x200B; オンボーディングとインストール &#x200B;](installation.md)
>* [&#x200B; カタログサービスの基本を学ぶ](get-started.md)
>* [SaaS データ書き出しとデータの同期](../data-export/data-sync-manage.md)
>* [GraphQL APIを使用したカタログデータの取得](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/){target="_blank"}
>* [[!DNL Catalog Service] およびAPI メッシュ &#x200B;](mesh.md)
>* [接続 [!DNL Adobe I/O] を設定](https://developer.adobe.com/commerce/extensibility/events/configure-commerce#configure-the-adobe-io-connection){target="_blank"}
>* [[!DNL Adobe I/O Events]](https://developer.adobe.com/events/docs/guides/){target="_blank"}
