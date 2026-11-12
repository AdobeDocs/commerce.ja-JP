---
title: カタログビュー
description: カタログビューの概要と、ビジネス構造、ポリシー、価格設定によって商品カタログを整理するための作成方法について説明します。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよび[!DNL Adobe Commerce Optimizer]件のプロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"
exl-id: 76c1b81c-b456-4334-89bd-6027308cbc47
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
nudge: true
source-git-commit: d081e975b03805a0f46d5194f8c3cd46e3c86839
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%
---
# マーチャンダイジングサービスのカタログビュー

{{$include /help/_includes/ccdm-shared/setup/catalog-view.md}}

## カタログビューの管理

カタログビューを管理するには、次の手順を使用します。

- [ カタログ ビューを作成](#create-a-catalog-view)：名前、カタログ ソース、ポリシー、価格表を設定します。 次に、[ レコメンデーションと製品発見ルール ](#specify-catalog-views-for-recommendations-and-product-discovery-rules)のカタログビューを指定し、製品属性を上書きする[ カタログレイヤー](#catalog-layers)を確認するか、[ カタログビューを非公開](#make-a-catalog-view-private)にします。
- [ カタログビューを編集](#edit-a-catalog-view)：そのソース、ポリシー、価格表、保護設定を更新します。
- [ カタログビューを削除](#delete-a-catalog-view) – 不要になったカタログビューを削除します。
- [ カタログビューの詳細を表示](#view-catalog-view-details) - カタログビューテーブルからカタログビューの設定を確認します。

### カタログビューの作成

カタログビューを作成する前に、必要に応じて次の項目を準備します。

- [ カタログソース ](catalog-sources.md)
- 製品フィルターを定義する[ ポリシー](policies.md)
- 製品属性を上書きする必要がある場合は、[ カタログレイヤー](catalog-layer.md)
- ビューに表示される価格に関する[価格表](pricebooks.md)
- プライベート カタログ ビューを作成する場合は、[ アクセス キー](restricted-access-keys.md)が制限されています

#### 設定

このセクションでは、カタログ ビューを作成し、[ ポリシー](policies.md)と[価格表](pricebooks.md)を選択します。

1. 左側のメニューから、**[!UICONTROL Store setup]**&#x200B;に移動し、**[!UICONTROL Catalog views]**&#x200B;をクリックします。

1. **[!UICONTROL Create catalog view]**&#x200B;をクリックします。 &#x200B;

1. カタログビューの詳細を設定します。

   - **名前** - カタログ ビューの名前（例：`Celport`）を入力します。 &#x200B;
   - **カタログソース** - [ カタログソース ](catalog-sources.md)を選択（例：`en-US`）。
   - **カタログレイヤー** – 取り込んだレイヤーと優先度を確認します。
   - **ポリシー** - ドロップダウンを使用して、関連するポリシーを選択します。 例えば、「ブランド」、「モデル」などです。 &#x200B;既に[ ポリシーを作成していることを確認してください](policies.md)。

1. カタログ ビューにリンクする価格表を選択します。

   - **利用可能なすべての価格表を使用** – このオプションは、利用可能なすべての価格表から価格データを引き出します。
   - **選択した価格表のみを許可** – このオプションには、**許可された価格表を追加** ダイアログが表示されます。 このダイアログを使用して、カタログビューに使用する特定の価格表を選択します。
   - **単品価格表のみ** - 1つの価格表のみが適用される場合は、このオプションを選択します。 プライベートカタログビューを設定する場合は、このオプションが必要です。このオプションは、1つの価格表のみを参照できます。 プライベートカタログビューの[価格表の制限](private-catalog-view.md#price-book-restriction-on-private-catalog-views)を参照してください。
   - **価格設定を無効にする** – 現在、このオプションは利用できません。

   >[!NOTE]
   >
   >価格表IDは、どの価格設定を要求するかを制御します。 カタログビューへのアクセスは制限されません。 アクセスを制限するには、カタログ保護を有効にして[ プライベートカタログビュー](private-catalog-view.md)を作成します。

1. （オプション） **[!UICONTROL Catalog Protection]**&#x200B;を&#x200B;**[!UICONTROL Enabled]**&#x200B;に切り替えて、このカタログビューのデータを有効な署名済みトークンを持つクライアントに制限します。 設定手順については、[ カタログビューの保護](private-catalog-view.md#protect-a-catalog-view)を参照してください。

1. リンクされた価格表とポリシーを含むカタログ ビューを作成するには、**[!UICONTROL Add]**&#x200B;をクリックします。

カタログビューページが更新され、新しいカタログビューが表示されます&#x200B;。

これらの手順を完了すると、カタログビューが設定され、選択したソースとポリシーに基づいて製品と価格が表示されるようになりました。

#### レコメンデーションと製品発見ルールのカタログビューの指定

[ レコメンデーションユニット ](../merchandising/recommendations/create.md)または[ マーチャンダイジングルール ](../merchandising/rules/add.md)を作成するときに、カタログビューを指定できます。

#### カタログレイヤー

カタログレイヤーを使用すると、ソースカタログデータを変更せずに、選択した製品属性を上書きできます。 レイヤーを使用して、カタログビューの名前、説明、画像、リンク、メタデータをカスタマイズします。

[ カタログレイヤー](catalog-layer.md)を参照してください。

#### カタログビューを非公開にする

デフォルトでは、カタログビューは、GraphQL Merchandising APIにアクセスできるクライアントアプリケーションに対して公開されます。 アクセスを制限するには、**[!UICONTROL Catalog Protection]**&#x200B;を有効にしてプライベートカタログビューを設定します。

カタログビューを保護し、アクセスが強制されていることを確認する方法については、[ プライベートカタログビュー](private-catalog-view.md)を参照してください。

### カタログビューの編集

1. **[!UICONTROL Catalog views]** ワークスペースで、カタログ ビューを見つけます。
1. アクションメニューを開くには、（**[!UICONTROL ...]**）を選択します。
1. カタログ ビューエディターにアクセスするには、**[!UICONTROL Edit]**&#x200B;を選択します。
1. 必要に応じて、名前、カタログソース、ポリシー、価格表情報、および&#x200B;**[!UICONTROL Catalog Protection]**&#x200B;設定（割り当てられた制限付きアクセスキーを含む）を更新します。
1. **[!UICONTROL Save]**&#x200B;をクリックします。

### カタログビューの削除

1. **[!UICONTROL Catalog views]** ワークスペースで、カタログ ビューを見つけます。
1. アクションメニューを開くには、（**[!UICONTROL ...]**）を選択します。
1. **[!UICONTROL Delete]**&#x200B;を選択します。
1. 削除を確認します。

   確認ダイアログが表示されたら、**[!UICONTROL Delete]**&#x200B;をクリックします。

### カタログ ビューの詳細の表示

このオプションを使用すると、**[!UICONTROL Catalog views]** テーブルを維持しながら、すべてのカタログ表示パラメーターを簡単に表示できます。

**[!UICONTROL Catalog views]** ワークスペースで、カタログビューの![情報アイコン ](/help/assets/ccdm-shared/recommendations/info-icon.png)を選択して、その設定の詳細を表示します。

![ カタログ表示の詳細](../assets/catalog-view-details.png)

ここから、次のようなカタログビュー設定の詳細を確認できます。

- ビューID
- 名前
- カタログソース
- ポリシー
- 作成日
- 変更されたデータ

これらの設定設定の一部は、ストアフロントを設定したり、データ取り込みAPIを使用したりするときに必要です。
