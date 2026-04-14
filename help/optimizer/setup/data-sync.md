---
title: データの同期
description: Commerce データソースから [!DNL Adobe Commerce Optimizer]に同期中のカタログデータを確認します。
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよび [!DNL Adobe Commerce Optimizer]  プロジェクトにのみ適用されます（Adobeで管理されるSaaS インフラストラクチャ）。"
exl-id: c0f4664c-6afc-4762-856b-5e26a865d3a2
source-git-commit: 604f46a65b2bfa84e1be07f410a4e36051eb1a29
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# データ同期

**Data Sync** ページには、データソース（既存のCommerce カタログ、Product Information Management （PIM） システム、Enterprise Resource Planning （ERP） システムなど）から[!DNL Adobe Commerce Optimizer]に転送された製品データの同期ステータスの概要が表示されます。

**データ同期** ページは、ストアフロントの商品データの可用性に関する貴重なインサイトを提供し、買い物客に迅速に表示できるようにします。

**データ同期** ページは、*設定* > **データ同期**&#x200B;にあります。

![&#x200B; データ同期](../assets/data-sync.png)

**データ同期** ページには、次のフィールドが含まれています。

| フィールド | 説明 |
|--- |--- |
| カタログソース | 同期データの特定のロケール。 |
| [!DNL Catalog Service] | 最新の同期更新、受信した合計製品、検索フィールド、および[!DNL Catalog Service]の同期製品のテーブルを表示します。 |
| 製品の発見 | 最新の同期更新、受信した合計製品、検索フィールド、および同期済み製品のテーブルを検索用に表示します。 |
| 推奨事項 | 最新の同期更新、受信した製品合計、検索フィールド、およびRecommendations用の同期済み製品のテーブルが表示されます。 |
| 過去3時間以内に受け取った商品 | 過去3時間以内にカタログ ソースから[!DNL Adobe Commerce Optimizer]に転送された製品の数を表示します。 カタログの更新頻度が低い場合、この値は頻繁にゼロになります。 |
| カタログ内の合計製品数 | [!DNL Adobe Commerce Optimizer]様が利用できるカタログ製品の合計数を反映します。 |
| 同期済み製品 | [!DNL Adobe Commerce Optimizer]に同期された製品の詳細を提供します。 デフォルトでは、このテーブルは「最終更新日」でソートされます。 特定の製品を検索するには、**[!UICONTROL Search by Name or SKU]** フィールドを使用します。 |

## 同期済み製品のリスト

同期済み製品の詳細をJSON形式で表示するには、同期済み製品テーブルの製品の行にあるコードアイコン ![&#x200B; コードリンク &#x200B;](../assets/data-sync-details.png)をクリックします。

![製品の詳細を同期](../assets/synced-products.png)

## カタログデータの再同期

**データ同期** ページに特定の製品が表示されない場合は、アップストリームシステムから再同期を開始する必要があります。 ただし、再同期によってハードウェアリソースの負荷が増大する可能性があることに注意してください。 ただし、次のシナリオでは、カタログの再同期が必要になる場合があります。

- 新製品の追加、製品詳細の更新、カテゴリの変更など、製品カタログに大きな変更が加えられた場合

- ストアフロントへの商品データの表示において、矛盾やパフォーマンスの問題が発生した場合

>[!IMPORTANT]
>
>同期を完了するのにかかる時間は、カタログサイズや更新されるデータ量によって異なります。

## データ同期ステータスの監視

Commerce Optimizer コネクタを介してAdobe Commerceをアップストリームのデータソースとして使用するプロジェクトの場合、Commerce管理者の[&#x200B; データフィード同期ステータス ページ &#x200B;](../../data-export/data-synchronization.md)からデータ書き出しプロセスを監視し、再同期操作を開始できます。

## 関連トピック

- [Adobe Commerce Optimizer コネクタ &#x200B;](../../aco-connector/overview.md){target="_blank"}


