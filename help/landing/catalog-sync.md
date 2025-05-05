---
title: カタログ同期
description: ' [!DNL Commerce] server から  [!DNL Commerce Services] に製品データを書き出す方法を説明します。'
feature: Catalog Management, Data Import/Export, Catalog Service
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---


# カタログ同期

>[!NOTE]
>
> カタログ同期ダッシュボードが、データ管理ダッシュボードになりました。 この刷新されたダッシュボードは、[[!DNL Product Recommendations]](../product-recommendations/guide-overview.md) v6.0.0 以降、[[!DNL Live Search]](../live-search/overview.md) v4.1.0 以降および [[!DNL Catalog Service]](../catalog-service/overview.md) v1.17 以降をサポートするようになりました。 お客様は、これらのサービスのいずれかの最新バージョンに更新することで、データ管理ダッシュボードを取得できます。 詳しくは、[ データ管理ダッシュボード ](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-dashboard.html) ドキュメントを参照してください。 この現在のトピックは、まだアップグレードしておらず、カタログ同期ダッシュボードを使用しているユーザー向けです。

Adobe Commerceはインデクサーを使用して、カタログデータをテーブルにコンパイルします。 プロセスは、製品価格や在庫レベルの変更など [&#128279;](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/index-management.html#events-that-trigger-full-reindexing) イベント  によって自動的にトリガーされます。

カタログ同期サービスは、製品データを [!DNL Adobe Commerce] インスタンスから [!DNL Commerce Services] プラットフォームに継続的に移動して、データを最新の状態に保ちます。 例えば、[[!DNL Product Recommendations]](/help/product-recommendations/overview.md) では、現在のカタログ情報を使用して、正確な名前、価格、在庫状況のレコメンデーションを正確に返す必要があります。 _カタログ同期_ ダッシュボードを使用すると、同期プロセスまたはコマンドラインインターフェイスを監視および管理して、カタログ同期をトリガーし、[!DNL Commerce Services] で使用するために製品データを再インデックス化できます。 『 [SaaS データ書き出し ](../data-export/data-export-cli-commands.md) ガイド』の「_コマンド ライン インターフェイス リファレンス_」を参照してください。

## カタログ同期ダッシュボードへのアクセス

カタログ同期ダッシュボードにアクセスするには、**システム**/_データ転送_/**カタログ同期** を選択します。

**カタログ同期** ダッシュボードを使用すると、次のことができます。

- 同期ステータス （**処理中**、**成功**、**失敗**）を表示します
- 同期された製品の合計数を表示します
- 同期された製品を検索して現在の状態を表示
- 名前、SKU などでストアカタログを検索
- 同期の不一致を診断するのに役立つ、同期された製品の詳細を JSON で表示します
- 同期プロセスの再開

### 最終同期

次の同期ステータスを報告：

- **成功** – 同期が成功した日時と、更新された製品数を表示します
- **失敗** – 同期が試行された日時を表示します
- **処理中** – 前回成功した同期の日時を表示します

カタログ同期プロセスは、1 時間ごとに自動的に実行されます。 ストアフロントに期待した製品が表示されない場合、または製品が最近の変更を反映していない場合は、[ カタログ同期の問題 ](#resolvesync) を解決できます。

### 同期済み製品

[!DNL Commerce] カタログから同期された製品の合計数を表示します。 最初の同期の後は、変更された製品のみ同期する必要があります。

## 再同期 {#resync}

1 時間ごとのスケジュールされた同期が発生する前にカタログの再同期を開始する必要がある場合は、再同期を強制できます。

>[!NOTE]
>
> 再同期を強制すると、商品カタログ全体の再同期がトリガーされ、ハードウェアリソースの負荷が増す可能性があります。

1. _カタログ同期_ ダッシュボードから、「**設定**」を選択します。

   _カタログ同期設定_ ページが表示されます。

1. 「_データの再同期_」セクションで、「[!UICONTROL Resync]」をクリックします。

   [!DNL Commerce] は、次にスケジュールされた同期期間中にカタログを同期します。 カタログのサイズによっては、この操作に時間がかかる場合があります。

## 同期されたカタログ製品

**同期されたカタログ製品** テーブルには、次の情報が表示されます。

| フィールド | 説明 |
|---|---|
| ID | 商品の一意の ID |
| 名前 | 商品のストアフロント名 |
| タイプ | 商品タイプ（シンプル、設定可能、ダウンロード可能など）を識別します |
| 前回のエクスポート | 商品が最後にカタログから正常に書き出された日付 |
| 最終変更日 | カタログで製品が最後に変更された日付 |
| SKU | 商品の在庫管理単位を表示します |
| 価格 | 商品の価格 |
| 可視性 | [!DNL Commerce] カタログで定義された製品の表示設定 |

## カタログ同期の問題を解決 {#resolvesync}

_SaaS データ書き出しガイド [&#128279;](../data-export/troubleshooting-logging.md#troubleshooting) の  ログとトラブルシューティング_ を参照してください。
