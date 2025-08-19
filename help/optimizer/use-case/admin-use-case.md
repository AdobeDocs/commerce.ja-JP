---
title: ストアフロントとカタログ管理者のエンドツーエンドの使用例
description: カタログビュー  [!DNL Adobe Commerce Optimizer]  ポリシーを使用してカタログを管理する方法、およびカタログ設定に基づいてストアフロントを設定する方法について説明します。
role: Admin, Developer
feature: Personalization, Integration
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
exl-id: d11663f8-607e-4f1d-b68f-466a69bcbd91
source-git-commit: e5844cad1d666a81042db64e51e124e6444d19ac
workflow-type: tm+mt
source-wordcount: '2179'
ht-degree: 0%

---

# ストアフロントとカタログ管理者のエンドツーエンドの使用例

このユースケースは、複雑な運用設定を持つ Carvelo Automobile という架空の自動車コングロマリットに基づいています。 [!DNL Adobe Commerce Optimizer] を使用して、カスタマイズされたストアフロントのエクスペリエンスを提供しながら、複数のブランド、販売店、価格台帳をサポートするカタログを管理する方法を示します。

## 前提条件

このユースケースは、ストアフロントを設定し、[!DNL Adobe Commerce Optimizer] を使用してカタログを管理する方法を学びたいと考える管理者および開発者を対象としています。 ここでは、[!DNL Adobe Commerce Optimizer] とその機能について基本的に理解していることを前提としています。

**完了までの推定時間：** 45 ～ 60 分

### 必要な設定

このチュートリアルを開始する前に、次の前提条件を満たしていることを確認してください。

- **Adobe Commerce Optimizer インスタンス**
   - Cloud Managerのテストインスタンスへのアクセス
   - 設定手順については、[ はじめに ](../get-started.md) を参照してください

- **ユーザー権限**
   - Adobe Admin Consoleへの管理者アクセス
   - アカウント設定については、[User Management](../user-management.md) を参照してください
   - アクセス権がない場合は、Adobe アカウント担当者にお問い合わせください。

- **サンプルデータ**
   - インスタンスに読み込まれた Carvelo Automobile カタログデータ
   - [Sample catalog data ingestion](https://github.com/adobe-commerce/aco-sample-catalog-data-ingestion) の手順に従います
   - サンプルデータは、付属の `reset.js` スクリプトを使用して、完了後に削除できます

- **ストアフロント環境**
   - Node.js のローカル開発環境
   - 複製および設定済みのストアフロントボイラープレートプロジェクト
   - 手順について詳しくは、[ ストアフロントの設定 ](../storefront.md) を参照してください

## それでは、始めましょう

このユースケースでは、以下を使用しています。

1. [!DNL Adobe Commerce Optimizer] UI - カタログビューとポリシーを設定して、Carvelo ユースケースの複雑なカタログ運用設定を管理します。

1. Commerce Storefront - [!DNL Adobe Commerce Optimizer] インスタンスに読み込まれたサンプルカタログデータと、Commerce Storefront 設定ファイル（`fstab.yaml`、`config.json`）を使用してストアフロントをレンダリングします。

>[!NOTE]
>
> Adobe Commerce Storefront ドキュメントの [ ボイラープレートの探索 ](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/boilerplate-project/?lang=ja) トピックを確認して、ストアフロントの設定ファイルについて学びます。

### ‌重要ポイント

この記事を終了すると、次のことができるようになります。

- パフォーマンスと拡張性に優れたカタログデータモデルを使用して、[!DNL Adobe Commerce Optimizer] の基本を説明します。
- カタログデータモデルが、Adobeで作成された、プラットフォームに依存しないストアフロントコンポーネントと統合される仕組みについて説明します。
- Adobe Commerce Optimizerのカタログビューとポリシーを使用して、カスタムのカタログビューとデータアクセスフィルターを作成し、Edge Deliveryを活用してAdobe Commerce ストアフロントにデータを送信する方法について説明します。

## ビジネスシナリオ - Carvelo Automobile

Carvelo Automobile は、複雑な運用セットアップを備えた架空の自動車コングロマリットです。

![ カーベロ自動車 ](../assets/carvelo.png)

この図では、カーベロが 3 つのブランドの自動車製品を販売していることがわかります。 各ブランドは異なる子会社です。

- オーロラ（電気自動車）
- ボルト （SUV）
- Cruz （ハイブリッド）

同社はこれらのブランドを以下の 3 つの販売店で販売している。

- アークブリッジ
- Kingsbluff
- Celport

これらの販売店は 2 つの異なる親販売会社に属しています。

- West Coast Inc. （アークブリッジ）
- East Coast Inc. （Kingsbluff, Celport）

各企業には 2 つの価格台帳があり、それぞれ異なる買い物客（ベース、VIP）に対して特定の価格で商品を販売するために使用されます。

- `west_coast_inc` と `vip_west_coast_inc`
- `east_coast_inc` と `vip_east_coast_inc`

ご覧のように、これは非常に複雑なビジネスユースケースです。 [!DNL Adobe Commerce Optimizer] を使用すると、マーチャントは、単一の基本カタログを使用して複雑なビジネス構造をサポートし、カタログの重複のないデータを同時配信し、価格台帳（30,000 件以上の価格台帳）を拡大し、これらのデータをすべてEdge Delivery Servicesストアフロントに配信できます。

これで、ビジネスユースケースの概要を確認したので、このチュートリアルの目的は次のとおりです。

>[!BEGINSHADEBOX]

Carvelo は、3 つのブランド（Aurora、Bolt、Cruz）のパーツを、異なる販売代理店（Arkbridge、Kingsbluff、Celport）を通じて販売したいと考えています。 カーベロは、販売代理店がそれぞれのライセンス契約に従って正しい部品と価格にのみアクセスできるようにしたいと考えています。

最終的に、Carvelo には 2 つの大きな目標があります。

1. 「グローバル」な web サイトを維持します。この web サイトには、3 つのブランドすべてのすべての SKU があります。
1. 販売店が、販売店ごとに固有の SKU の可視性と各 SKU の価格に基づいて独自のストアフロントを設定するためのパスを提供します。 一方、単一の基本カタログを使用することで、カタログの重複を排除できます。

>[!ENDSHADEBOX]

## &#x200B;1. [!DNL Adobe Commerce Optimizer] インスタンスにアクセスする

サンプルデータで事前設定されているCommerce Optimizer アプリケーションの URL に移動します。 Commerce Optimizer プロジェクトのインスタンスの詳細からCommerce Cloud Manager で URL を見つけることも、システム管理者から URL を取得することもできます。 （[ インスタンスへのアクセス ](../get-started.md#access-an-instance) を参照。）

[!DNL Adobe Commerce Optimizer] を起動すると、次の情報が表示されます。

![[!DNL Adobe Commerce Optimizer] UI](../assets/user-interface.png)

>[!NOTE]
>
>UI の主要コンポーネントについて詳しくは、[ 概要 ](../overview.md) の記事を参照 [!DNL Adobe Commerce Optimizer] てください。

左側のナビゲーションで、「_ストアの設定_」セクションを展開し、「**[!UICONTROL Catalog views]**」をクリックします。 Arkbridge および Kingsbluff の販売代理店では、すでにカタログ・ビューが作成されていることに注意してください。

![ サンプルデータ用に設定された既存のカタログビュー ](../assets/existing-channels-list.png)

>[!NOTE]
>
>現時点では、**グローバル** カタログビューは無視できます。

情報アイコンをクリックして、カタログ表示の詳細を確認します。

Arkbridge には次のポリシーがあります。

- ブランド
- モデル
- West Coast Inc のブランド
- Arkbridge パーツ カテゴリ

Kingsbluff には次のポリシーがあります。

- ブランド
- モデル
- East Coast Inc のブランド
- キングスブラフ パーツ カテゴリ

次のセクションでは、Celport ディーラーのカタログ・ビューとポリシーを作成します。

## &#x200B;2. ポリシーとカタログ表示の作成

カーヴェロの商務部長は、*イースト・コースト社* の会社に属する *セルポート* と呼ばれるディーラーの新しい店舗フロントを設置する必要がある。 Celport は、Bolt および Cruz ブランドのブレーキとサスペンションを販売します。

![ セルポート販売業者 ](../assets/celport-dealer.png)

[!DNL Adobe Commerce Optimizer] を使用すると、コマースマネージャーは次のようになります。

1. Celport がブレーキパーツとサスペンションパーツのみを販売するために、*Celport パートカテゴリ* と呼ばれる新しいポリシーを作成します。
1. Celport ストアフロントの新しいカタログビューを作成します。

   このカタログビューでは、新しく作成したポリシー *Celport part categories* と既存の *East Coast Inc Brands* を使用して、Celport が East Coast Inc.との契約の一環として Bolt と Cruz のブランドのみを販売できるようにします。Celport カタログビューでは、`east_coast_inc` 価格台帳を使用して、ブランドライセンス契約に沿った製品価格スケジュールをサポートしています。
1. 作成した Celport カタログ表示のデータを使用するように、コマースストアフロント設定を更新します。

このセクションの最後では、Celport が起動し、Carvelo の製品を販売する準備が整います。

### ポリシーの作成

*Celport 部品カテゴリ* と呼ばれる新しいポリシーを作成して、Celport ディーラーが販売する SKU （ブレーキ部品とサスペンション部品を含む）をフィルタリングします。

1. 左側のレールで、「_ストアの設定_ セクションを展開し、「**[!UICONTROL Policies]**」をクリックします。

1. 「**[!UICONTROL Create Policy]**」をクリックします。

   新しいページが表示され、ポリシーの詳細が追加されます。

1. 必要な詳細を追加します。

   **名前** = *Celport パーツ カテゴリ*

1. 「**[!UICONTROL Add Filter]**」をクリックします。

   フィルターの詳細を追加するためのダイアログが表示されます。

1. フィルターの詳細を追加します。

   - **属性** = *part_category*
   - **演算子** = **IN**
   - **値Source** = **STATIC**
   - **値** = *brakes*
   - **Value** = *suspension*

   >[!IMPORTANT]
   >
   >各属性値は個別に入力する必要があります。 値を入力したら、**Enter** キーを押して、その値をフィルター設定に追加します。 次に、次の値を入力します。 すべての値は、カタログの SKU 属性名と完全に一致する必要があります。

   STATIC 値ソースとトリガー値ソースの違いについて詳しくは、[ 値ソースのタイプ ](../setup/policies.md#value-source-types) を参照してください。

1. **[!UICONTROL Filter details]** ダイアログで、「**[!UICONTROL Save]**」をクリックします。

1. 作成したフィルターを有効にするには、アクションドット（...）をクリックし、「**有効**」を選択します。

1. 「**[!UICONTROL Save]**」をクリックします。

   >[!NOTE]
   >
   >**[!UICONTROL Save]** ボタンがアクティブ（青）でない場合は、ポリシー名がない可能性があります。 *新規ポリシー* の横にある鉛筆アイコンをクリックして追加します。

1. 戻る矢印をクリックして、ポリシーのリストに戻ります。

   新しい *Celport パーツ カテゴリ* ポリシーがリストに表示されます。

**この手順が正しく完了したことを確認するには：**

- ポリシーリストにポリシーが表示されます
- ポリシーのステータスが有効と表示されます（緑色のインジケーター）
- フィルタの詳細に「part_category IN （ブレーキ、サスペンション）」と表示される
- ポリシー名は「Celport Part Categories」

### カタログビューの作成

*Celport* ディーラーの新しいカタログビューを作成し、*East Coast Inc ブランド* と *Celport Part Categories* のポリシーをリンクします。

1. 左側のレールで、「_ストアの設定_ セクションを展開し、「**[!UICONTROL Catalog views]** 定」をクリックします。

   既存のカタログビュー *Arkbridge*、*Kingsbluff* および *Global* に注目してください。

   ![ 既存のカタログビューページ ](../assets/existing-channels-list.png)

1. 「**[!UICONTROL Add catalog view]**」をクリックします。

1. カタログ表示の詳細を入力します。

   - **名前** = *Celport*
   - **カタログソース** = *en-US*
   - **ポリシー** （ドロップダウンを使用） = *East Coast Inc Brands*; *Celport 部品カテゴリ*; *ブランド*; *モデル*
                         
1. 「**[!UICONTROL Add]**」をクリックして、カタログビューを作成します。

   「カタログビュー」ページが更新され、新しいカタログビューが表示されます。

   ![ 更新されたカタログビューリスト ](../assets/updated-catalog-view-list.png)

1. Celport カタログビュー ID を取得します。

   **カタログビュー** ページで、Celport カタログビューの情報アイコンをクリックします。

   ![Celport カタログ ビュー ID](../assets/celport-channel-id.png)

   カタログビュー ID をコピーして保存します。 この ID は、新しい Celport カタログにデータを配信するようにストアフロント設定を更新する際に必要になります。

   **この手順が正しく完了したことを確認するには：**
   - カタログ ビュー名は&quot;Celport&quot;です
   - カタログ表示には、4 つの関連ポリシーが表示されます
   - カタログビュー ID が表示され、コピーできます
   - カタログソースが「en-US」と表示される

Celport カタログビューおよび関連するポリシーを作成したら、次の手順では、新しい Celport カタログを使用するようにストアフロントを設定します。

## &#x200B;3. ストアフロントを更新する

このチュートリアルの最後の部分では、新しい Celport カタログにデータを配信するために [ 作成済み ](#prerequisite) ストアフロントを更新します。 このセクションでは、ストアフロント設定ファイルのカタログビュー ID を Celport のカタログビュー ID に置き換えます。

1. ローカル開発環境で、ストアフロントボイラープレートの設定ファイルを使用して GitHub リポジトリのクローンを作成したフォルダーを開きます。

1. フォルダーのルートディレクトリで、`config.json` ファイルを開きます。

   +++config.json コード

   ```json
   {
    "public": {
      "default": {
      "commerce-core-endpoint": "https://www.aemshop.net/graphql",
      "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/Fwus6kdpvYCmeEdcCX7PZg/graphql",
      "headers": {
         "cs": {
            "ac-view-id": "9ced53d7-35a6-40c5-830e-8288c00985ad",
            "ac-price-book-id": "west_coast_inc",
            "ac-source-locale": "en-US"
           }
         },
         "analytics": {
            "base-currency-code": "USD",
            "environment": "Production",
            "store-id": 1,
            "store-name": "ACO Demo",
            "store-url": "https://www.aemshop.net",
            "store-view-id": 1,
            "store-view-name": "Default Store View",
            "website-id": 1,
            "website-name": "Main Website"
          }
       }
      }
   }
   ```

   カタログビューヘッダーには次の値が含まれています。

   - `commerce-endpoint`: `"https://na1-sandbox.api.commerce.adobe.com/Fwus6kdpvYCmeEdcCX7PZg/graphql"`
   - `ac-view-id`:`"9ced53d7-35a6-40c5-830e-8288c00985ad"`
   - `ac-price-book-id`: `"west_coast_inc"`
   - `ac-source-locale`: `"en-US"`

1. `commerce-endpoint` の値で、URL のテナント ID を [!DNL Adobe Commerce Optimizer] インスタンスの URL に置き換えます。

   テナント ID は、Commerce Optimizer UI の URL 内にあります。 例えば、次の URL では、テナント ID は `XDevkG9W6UbwgQmPn995r3` です。

   ```text
   https://experience.adobe.com/#/@commerceprojectbeacon/in:XDevkG9W6UbwgQmPn995r3/commerce-optimizer-studio/catalog
   ```

1. `ac-view-id` の値を、以前にコピーした Celport カタログビュー ID に置き換えます。

1. `ac-price-book-id` の値を `"east_coast_inc"` に置き換えます。

   これらの変更を行うと、`config.json` ファイルは次のようになり、`ACO-tenant-id` と `celport-catalog-view-id` のプレースホルダーが値に置き換えられます。

   ```json
   {
     "public": {
        "default": {
        "commerce-core-endpoint": "https://www.aemshop.net/graphql",
        "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/{{ACO-tenant-id}}/graphql",
        "headers": {
            "cs": {
                "ac-view-id": "{{celport-catalog-view-id}}",
                "ac-price-book-id": "east_coast_inc",
                "ac-source-locale": "en-US"
              }
            },
            "analytics": {
                "base-currency-code": "USD",
                "environment": "Production",
                "store-id": 1,
                "store-name": "ACO Demo",
                "store-url": "https://www.aemshop.net",
                "store-view-id": 1,
                "store-view-name": "Default Store View",
                "website-id": 1,
                "website-name": "Main Website"
             }
         }
     }
   }
   ```

1. ファイルを保存します。

   変更を保存すると、ブレーキとサスペンション パーツのみを販売するように設定されている Carvelo カタログ ビューを使用するように、カタログ設定が更新されます。

## &#x200B;4. ストアフロントのプレビュー

Celport カタログ表示を使用するようにストアフロント設定を更新したので、ストアフロントをプレビューして、カタログデータのレンダリング方法を確認できます。

1. ストアフロントを起動して、ストアフロントの設定で作成した Celport 固有のカタログエクスペリエンスを表示します。

   1. IDE のターミナルウィンドウから、ローカルストアフロントのプレビューを開始します。

      ```shell
      npm start
      ```

      ブラウザーが開き、`http://localhost:3000` にローカル開発のプレビューが表示されます。

      コマンドの実行に失敗した場合や、ブラウザが開かない場合は、「Storefront のセットアップ」の [ローカル開発手順 ](../storefront.md) を参照してください。

1. ブラウザーで `brakes` を検索し、**Enter** キーを押します。

   ストアフロントが更新され、ブレーキパーツを示す製品リストページが表示されます。

   ![ ブレーキ製品一覧ページ ](../assets/brakes-listing-page.png)

   ブレーキ部品の画像をクリックすると、製品情報と共に製品の詳細が表示され、製品価格情報がメモされます。

1. `tires` を検索します。これは、[!DNL Adobe Commerce Optimizer] インスタンス上のユースケースデータで使用できるもう 1 つのパーツカテゴリです。

   ![ ストアフロント設定のヘッダーが正しくない ](../assets/storefront-configuration-with-incorrect-headers.png)

   結果が返されないことに注意してください。 これは、Celport カタログ ビューが、ブレーキとサスペンションのパーツのみを販売するように設定されているためです。

1. ストアフロント設定ファイル（`config.json`）を試して更新します。

   1. `ac-view-id` と `ac-price-book` の値を変更します。

   例えば、カタログビュー ID を Kingsbluff カタログビューに変更し、価格台帳 ID を `east_coast_inc` に変更できます。 「キングスブラフ」パーツ カテゴリのポリシーを確認すると、キングスブラフで使用できるパーツ カテゴリを確認 *きます*

   1. ファイルを保存します。

      ファイルを保存すると、ローカルストアフロントのプレビューが自動的に更新されます。

   1. 検索機能を使用してタイヤ部品を検索することで、ブラウザで変更内容をプレビューします。

      使用可能なパーツ タイプが異なることに注目してください。また、Kingsbluff カタログ ビューに割り当てられている価格にも注目してください。

   これらの実験は、Adobe Commerce Optimizerの柔軟性を示しています。異なるカタログビューと価格台帳をすばやく切り替えて、カタログデータを複製することなく、異なるオーディエンス向けにカスタマイズされたショッピングエクスペリエンスを作成できます。

## トラブルシューティング

このチュートリアルで問題が発生した場合は、次の解決策を試してください。

### ポリシー作成の問題

**問題：** 「保存」ボタンがアクティブにならない

- **解決策：** ポリシー名が入力され、すべての必須フィールドに入力されていることを確認します

**問題：** フィルターが期待どおりに動作しません

- **解決策：** 属性名がカタログの SKU 属性と完全に一致することを確認します

### カタログ表示の問題

**問題：** カタログビューがリストに表示されない

- **解決策：** 関連するすべてのポリシーが有効であり、適切に設定されていることを確認します

### ストアフロントの設定の問題

**問題：** ストアフロントが読み込まれない

- **解決策：** テナント ID とカタログビュー ID が config.json ファイルに正しく入力されていることを確認します

**問題：** 製品が表示されない

- **解決策：** 価格台帳 ID がAdobe Commerce Optimizer インスタンスで使用可能な ID と一致していることを確認します

**問題：** 検索で結果が返されない

- **解決策：** カタログ表示ポリシーで、検索した製品カテゴリが許可されていることを確認します

その他のヘルプについては、[Adobe Commerce Optimizer ドキュメントを参照するか ](../overview.md)Adobe サポートにお問い合わせください。

## 概要

このチュートリアルでは、次の操作を実行しました。

- Celport 販売代理店向けに製品カテゴリをフィルタリングする新しいポリシーを作成しました
- 製品の表示を制御する複数のポリシーを持つカタログビューの設定
- 新しいカタログ表示を使用するようにストアフロントを設定しました
- 製品の表示と価格をテストして構成を確認

## 次の手順

Adobe Commerce Optimizerについて引き続き学習するには：

- [ マーチャンダイジング機能 ](../merchandising/overview.md) を探索して、ショッピングエクスペリエンスをパーソナライズします
- [ 詳細なポリシー設定 ](../setup/policies.md) について
- 他の販売特約店に対する [ 追加のカタログ表示 ](../setup/catalog-view.md) の設定
- プログラムによるカタログ管理については、[API ドキュメント ](https://developer.adobe.com/commerce/services/optimizer/) を参照してください
- Edge Delivery Services ストアフロントのドロップインコンポーネントを設定して、製品検出、レコメンデーション、その他のストアフロント機能のためのカスタムストアフロントエクスペリエンスを作成する方法について説明します。 [ ストアフロントのドキュメント ](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/?lang=ja) を参照してください。
