---
title: カタログ同期
description: 製品データを [!DNL Commerce]  サーバーから [!DNL Commerce Services]に書き出す方法について説明します。
feature: Catalog Management, Data Import/Export, Catalog Service
exl-id: 99f96b93-b036-490c-8c57-40463a0de365
TQID: https://experienceleague.adobe.com/-X5W4TJNW6pduPsWH-SLuAXrfP7iReCpaVg5qeu2odA
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: c18ed297-2187-4aec-affb-9d9654eca6fcid: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 567
ht-degree: 0%

---

# カタログ同期

>[!NOTE]
>
> カタログ同期ダッシュボードがデータ管理ダッシュボードになりました。 この刷新されたダッシュボードでは、[[!DNL Product Recommendations]](../product-recommendations/guide-overview.md) v6.0.0以降、[[!DNL Live Search]](../live-search/overview.md) v4.1.0以降、[[!DNL Catalog Service]](../catalog-service/overview.md) v1.17以降がサポートされるようになりました。 お客様は、これらのサービスの最新バージョンに更新することで、データ管理ダッシュボードを入手できます。 詳しくは、[ データ管理ダッシュボード ](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html)のドキュメントを参照してください。 この現在のトピックは、まだアップグレードしておらず、カタログ同期ダッシュボードを持っているユーザーに残ります。

Adobe Commerceでは、インデックスを使用してカタログデータをテーブルにコンパイルします。 このプロセスは、製品価格や在庫レベルの変更など、[ イベント ](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/index-management.html#events-that-trigger-full-reindexing)によって自動的にトリガーされます。

カタログ同期サービスは、製品データを継続的に[!DNL Adobe Commerce] インスタンスから[!DNL Commerce Services] プラットフォームに移動し、データを最新の状態に保ちます。 例えば、[[!DNL Product Recommendations]](/help/product-recommendations/overview.md)では、現在のカタログ情報を使用して、正しい名前、価格、および空き状況のレコメンデーションを正確に返す必要があります。 _カタログ同期_ ダッシュボードを使用して、同期プロセスまたはコマンドラインインターフェイスを監視および管理し、カタログ同期をトリガーして、[!DNL Commerce Services]までに商品データを再インデックス化します。 _SaaS データ書き出し_ ガイドの[ コマンドラインインターフェイスのリファレンス ](../data-export/data-export-cli-commands.md)を参照してください。

## カタログ同期ダッシュボードにアクセスする

カタログ同期ダッシュボードにアクセスするには、**システム**/_データ転送_/**カタログ同期**&#x200B;を選択します。

**カタログ同期** ダッシュボードを使用すると、次のことが可能になります。

- 同期ステータスの表示（**進行中**、**成功**、**失敗**）
- 同期済み製品の合計数を表示
- 同期した商品を検索して現在の状態を確認
- ストア カタログを名前、SKUなどで検索します。
- 同期された製品の詳細をJSONで表示し、同期の不一致を診断できます
- 同期プロセスを再開します

### 前回の同期

次の同期ステータスをレポートします。

- **成功** – 同期が成功した日時と、更新された製品数を表示します
- **失敗** – 同期が試行された日時を表示します
- **処理中** – 前回の同期が成功した日時を表示します

カタログ同期プロセスは、1時間ごとに自動的に実行されます。 ストアフロントに予想される製品が表示されない場合、または製品が最近の変更を反映しない場合は、[ カタログ同期の問題](#resolvesync)を解決できます。

### 製品の同期

[!DNL Commerce] カタログから同期された製品の合計数を表示します。 最初の同期後、変更された製品のみが同期されます。

## 再同期 {#resync}

時間単位でスケジュールされた同期が実行される前にカタログの再同期を開始する必要がある場合は、再同期を強制的に実行できます。

>[!NOTE]
>
> 再同期を強制すると、商品カタログ全体が再トリガーされ、ハードウェアリソースの負荷が増加する可能性があります。

1. _カタログ同期_ ダッシュボードから、**設定**&#x200B;を選択します。

   _カタログ同期設定_ ページが表示されます。

1. _データの再同期_ セクションで、[!UICONTROL Resync]をクリックします。

   [!DNL Commerce]は、次のスケジュールされた同期ウィンドウ中にカタログを同期します。 カタログのサイズによっては、この操作に時間がかかる場合があります。

## 同期されたカタログ商品

**同期済みカタログ製品** テーブルには、次の情報が表示されます。

| フィールド | 説明 |
|---|---|
| ID | 製品の一意のID |
| 名前 | 製品のストアフロント名 |
| タイプ | シンプル、設定可能、ダウンロード可能など、製品タイプを示します |
| 最終書き出し | 商品がカタログから最後に正常にエクスポートされた日付 |
| 最終変更日 | 商品がカタログで最後に変更された日付 |
| SKU | 製品の在庫保管単位を表示します |
| 価格 | 製品の価格 |
| 表示 | [!DNL Commerce] カタログで定義された製品の表示設定 |

## カタログ同期の問題を解決する {#resolvesync}

_SaaS データ書き出しガイド_&#x200B;の「[ ログとトラブルシューティング ](../data-export/troubleshooting-logging.md#troubleshooting)」を参照してください。
