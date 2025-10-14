---
title: データ同期
description: Commerce データソースから  [!DNL Adobe Commerce Optimizer] に同期されているカタログデータを確認します。
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
exl-id: c0f4664c-6afc-4762-856b-5e26a865d3a2
source-git-commit: 0b8e0222a1de1c425964f9f54294d7e0435a26d8
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# データ同期

**データ同期** ページには、データソース（既存のCommerce カタログ、Product Information Management （PIM）システム、Enterprise Resource Planning （ERP）システムなど）から [!DNL Adobe Commerce Optimizer] に転送された商品データの同期ステータスの概要が表示されます。

**データ同期** ページは、ストアフロントの製品データの可用性に関する貴重なインサイトを提供し、買い物客に迅速に表示できるようにします。

**データ同期** ページは *設定*/**データ同期** にあります。

![&#x200B; データ同期 &#x200B;](../assets/data-sync.png)

**データ同期** ページには、次のフィールドが含まれています。

| フィールド | 説明 |
|--- |--- |
| カタログソース | 同期されたデータ固有のロケール。 |
| [!DNL Catalog Service] | 最新の同期更新、受信した製品の総数、検索フィールド、同期した [!DNL Catalog Service] の製品のテーブルが表示されます。 |
| 製品の検出 | 最新の同期更新、受信した製品の総数、検索フィールド、および検索用に同期された製品のテーブルを表示します。 |
| 推奨事項 | 最新の同期更新、受信した製品の合計、検索フィールド、Recommendations に対して同期された製品のテーブルを表示します。 |
| 過去 3 時間以内に受領した製品 | 過去 3 時間以内にカタログソースからAdobe Commerce Optimizerに転送された商品の数を表示します。 カタログを更新する頻度が低い場合、この値は頻繁にゼロになります。 |
| カタログ内の合計製品数 | Adobe Commerce Optimizerで使用可能なカタログ商品の合計数を反映します。 |
| 同期された製品 | Adobe Commerce Optimizerに同期された商品に関する詳細を提供します。 デフォルトでは、このテーブルは「最終更新日」で並べ替えられます。 特定の製品を検索するには、「**[!UICONTROL Search by Name or SKU]**」フィールドを使用します。 |

## 同期された製品のリスト

同期された製品の詳細を JSON 形式で確認するには、同期された製品テーブルの製品の行にあるコードアイコン ![&#x200B; コードリンク &#x200B;](../assets/data-sync-details.png) をクリックします。

![Syncd 製品詳細 &#x200B;](../assets/synced-products.png)

## カタログデータを再同期

**データ同期** ページに特定の製品が表示されない場合は、アップストリームシステムから再同期を開始する必要があります。 ただし、再同期を行うと、ハードウェア リソースの負荷が増大する可能性があることに注意してください。 ただし、次のようなシナリオでは、カタログの再同期が必要になる場合があります。

- 新製品の追加、製品の詳細の更新、カテゴリの変更など、製品カタログに大きな変更が加えられた場合

- ストアフロントでの製品データの表示に不一致やパフォーマンスの問題が発生した場合

>[!IMPORTANT]
>
>同期の完了に要する時間は、カタログのサイズと、更新されるデータの量に応じて異なります。
