---
title: Carvelo のユースケース
description: チャネル  [!DNL Adobe Commerce Optimizer]  ポリシーを使用してカタログを管理する方法、およびカタログ設定に基づいてストアフロントを設定する方法について説明します。
hide: true
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: d716dd9d75beb642bfad30271b6ecd3490ee7328
workflow-type: tm+mt
source-wordcount: '1656'
ht-degree: 0%

---

# Carvelo のユースケース

>[!NOTE]
>
>このドキュメントでは、製品の早期アクセス開発について説明しており、一般提供を目的とした機能のすべてを反映しているわけではありません。

次のユースケースは、[!DNL Adobe Commerce Optimizer] を使用して、単一の基本カタログを使用して小売操作に合わせてカタログを整理する方法を示しています。 また、Edge Delivery Servicesを使用したストアフロントの設定方法についても説明します。

## 前提条件

この使用例を実行する前に、[ ストアフロントの設定 ](../storefront.md) が完了していることを確認します。

## それでは、始めましょう

このユースケースでは、以下を使用して作業を行います。

1. [!DNL Adobe Commerce Optimizer] UI – 複雑なカタログ運用のセットアップを管理するために必要なチャネルとポリシーを設定します。

1. Commerce Storefront - UI 内に設定されたカタログデータとCommerce Storefront 設定ファイル（`fstab.yaml` および `config.json`） [!DNL Adobe Commerce Optimizer] 使用してストアフロントをレンダリングします。

### ‌重要ポイント

この記事を終了すると、次のことができるようになります。

- 独自のパフォーマンスと拡張性の高いカタログデータモデルを使用した、[!DNL Adobe Commerce Optimizer] の基本を説明します。
- カタログデータモデルが、Adobeで作成された、プラットフォームに依存しないストアフロントコンポーネントとシームレスに結び付く仕組みを説明します。
- Adobe Commerce Optimizer チャネルとポリシーを使用して、カスタムカタログビューとデータアクセスフィルターを作成し、Edge Deliveryを活用したAdobe Commerce ストアフロントにデータを送信する方法について説明します。

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

Carvelo は、3 つのブランド（Aurora、Bolt、Cruz）のパーツを、様々な販売代理店（Akbridge、Kingsbluff、Celport）を通じて販売したいと考えています。 カーベロは、販売代理店がそれぞれのライセンス契約に従って正しい部品と価格にのみアクセスできるようにしたいと考えています。

最終的に、Carvelo には 2 つの大きな目標があります。

1. 「グローバル」な web サイトを維持します。この web サイトには、3 つのブランドすべてのすべての SKU があります。
1. 販売店が、販売店ごとに固有の SKU の可視性と各 SKU の価格に基づいて独自のストアフロントを設定するためのパスを提供します。

>[!ENDSHADEBOX]

次に、[!DNL Adobe Commerce Optimizer] インスタンスにアクセスします。

## 1. [!DNL Adobe Commerce Optimizer] インスタンスにアクセスする

早期アクセスプログラムにオンボードすると、Adobeからメールが送信され、プロビジョニングされた l[!DNL Adobe Commerce Optimizer] インスタンスにアクセスするための URL が記載されます。 このインスタンスには、Carvelo Automobile のユースケースをサポートするカタログデータなど、このチュートリアルで概要を説明する手順を正常に完了するために必要なすべての情報が事前に設定されています。

[!DNL Adobe Commerce Optimizer] を起動すると、次の情報が表示されます。

![[!DNL Adobe Commerce Optimizer] UI](../assets/user-interface.png)

>[!NOTE]
>
>[!DNL Adobe Commerce Optimizer] UI を構成する様々なパーツの詳細については、[ 概要 ](../overview.md) の記事を参照してください。

左側のナビゲーションで、「**[!UICONTROL Catalog]**」セクションを展開し、「**[!UICONTROL Channels]**」をクリックします。 Arkbridge および Kingsbluff の販売代理店では、既に次のチャネルが作成されています。

![ 事前設定済みのチャネル ](../assets/existing-channels-list.png)

>[!NOTE]
>
>現時点では、**グローバル** チャネルは無視できます。

情報アイコンをクリックして、チャネルの詳細を確認します。

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

次のセクションでは、Celport 販売店のチャネルとポリシーを作成します。

## 2. ポリシーとチャネルを作成する

カーヴェロの商務部長は、*イースト・コースト社* の会社に属する *セルポート* と呼ばれるディーラーの新しい店舗フロントを設置する必要がある。 Celport は、Bolt および Cruz ブランドのブレーキとサスペンションを販売します。

![ セルポート販売業者 ](../assets/celport-dealer.png)

[!DNL Adobe Commerce Optimizer] を使用すると、コマースマネージャーは次のようになります。

1. Celport がブレーキパーツとサスペンションパーツのみを販売するために、*Celport パートカテゴリ* と呼ばれる新しいポリシーを作成します。
1. Celport ストアフロントの新しいチャネルを作成します。

   このチャネルでは、新しく作成したポリシー *Celport part categories* と既存の *East Coast Inc Brands* を使用して、Celport が East Coast Inc.との契約の一環として Bolt と Cruz のブランドのみを販売できるようにします。Celport チャネルは、`east_coast_inc` 価格台帳を使用して、ブランドライセンス契約に沿った製品価格スケジュールをサポートします。
1. 作成した Celport チャネルのデータを使用するようにコマースストアフロント設定を更新します。

このセクションの最後では、Celport が起動し、Carvelo の製品を販売する準備が整います。

### ポリシーの作成

*Celport 部品カテゴリ* と呼ばれる新しいポリシーを作成して、Celport ディーラーが販売する SKU （ブレーキ部品とサスペンション部品を含む）をフィルタリングします。

1. 左側のナビゲーションで、「**[!UICONTROL Catalog]**」セクションを展開し、「**[!UICONTROL Policies]**」をクリックします。

1. 「**[!UICONTROL Add Policy]**」をクリックします。

   新しいページが表示され、ポリシーの詳細が追加されます。

1. 必要な詳細を追加します。

   **名前** = *Celport パーツ カテゴリ*

1. 「**[!UICONTROL Add Filter]**」をクリックします。

   フィルターの詳細を追加するためのダイアログが表示されます。

1. フィルターの詳細を追加します。

   - **属性** = *part_category*
   - **演算子** = **IN**
   - **値Source** = **STATIC**
   - **値** = *brakes*, *suspension*

   >[!IMPORTANT]
   >
   >指定する属性名が、カタログ内の SKU 属性名と完全に一致していることを確認します。

   STATIC 値ソースとトリガー値ソースの違いについて詳しくは、[ 値ソースのタイプ ](../catalog/policies.md#value-source-types) を参照してください。

1. **[!UICONTROL Filter details]** ダイアログで、「**[!UICONTROL Save]**」をクリックします。

1. 作成したフィルターを有効にするには、アクションドット（...）をクリックし、「**有効**」を選択します。

1. 「**[!UICONTROL Save]**」をクリックします。

   >[!NOTE]
   >
   >**[!UICONTROL Save]** ボタンがアクティブ（青）でない場合は、ポリシー名がない可能性があります。 *新規ポリシー* の横にある鉛筆アイコンをクリックして追加します。

1. 戻る矢印をクリックして、ポリシーのリストに戻ります。

   新しい *Celport パーツ カテゴリ* ポリシーがリストに表示されます。

### チャネルの作成

*Celport* ディーラーの新しいチャネルを作成し、*East Coast Inc brands* と *Celport Part Categories* のポリシーをリンクします。

1. 左側のナビゲーションで、「**[!UICONTROL Catalog]**」セクションを展開し、「**[!UICONTROL Channels]**」をクリックします。

   ![ チャネル ](../assets/channels.png)

   既存のチャネル（*Arkbridge*、*Kingsbluff* および *Global*）に注意してください。

   ![ 既存のチャネルページ ](../assets/existing-channels-list.png)

1. 「**[!UICONTROL Add Channel]**」をクリックします。

1. チャネルの詳細を入力します。

   - **名前** = *Celport*
   - **Scopes** = *en-US* （enter キーを押す）
   - **ポリシー** （ドロップダウンを使用） = *East Coast Inc Brands*; *Celport 部品カテゴリ*; *ブランド*; *モデル*                          

1. 「**[!UICONTROL Add]**」をクリックして、チャネルを作成します。

   チャネル ページが更新され、新しいチャネルが表示されます。

   ![ 更新されたチャネルリスト ](../assets/updated-channels-list.png)

   >[!NOTE]
   >
   >**[!UICONTROL Add]** ボタンが青でない場合は、カーソルを **[!UICONTROL Scopes]** のセクションに置いて **enter** キーを押して、スコープが選択されていることを確認します。

1. Celport チャネル ID を取得します。

   **チャネル** ページの Celport チャネルの情報アイコンをクリックします。

   ![Celport チャネル ID](../assets/celport-channel-id.png)

   チャネル ID をコピーして保存します。 この ID は、新しい Celport カタログにデータを配信するようにストアフロント設定を更新する際に必要になります。

Celport チャネルと関連ポリシーを作成したら、次の手順は、新しい Celport カタログを作成するようにストアフロントを設定することです。

## 3. ストアフロントを更新する

このチュートリアルの最後の部分では、新しい Celport カタログにデータを配信するために [ 作成済み ](#prerequisite) ストアフロントを更新します。 この節では、ストアフロント設定ファイルのチャネル ID を Celport のチャネル ID に置き換えます。

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
            "ac-channel-id": "9ced53d7-35a6-40c5-830e-8288c00985ad",
            "ac-environment-id": "Fwus6kdpvYCmeEdcCX7PZg",
            "ac-price-book-id": "west_coast_inc",
            "ac-scope-locale": "en-US"
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

   チャネルヘッダーには、次の行が含まれています。

   - `ac-channel-id`:`"9ced53d7-35a6-40c5-830e-8288c00985ad"`
   - `ac-environment-id`: `"Fwus6kdpvYCmeEdcCX7PZg"`
   - `ac-price-book-id`: `"west_coast_inc"`

+++

1. `ac-channel-id` の値を、以前にコピーした Celport チャネル ID に置き換えます。
1. 必要に応じて、`ac-environment-id` の値を [!DNL Adobe Commerce Optimizer] インスタンスのテナント ID に置き換えます。 ID は、早期アクセスプログラムのオンボーディングメールで確認するか、Adobe アカウント担当者にお問い合わせください。

   `commerce-endpoint` の値が、[!DNL Adobe Commerce Optimizer] インスタンスのGraphQL エンドポイントと一致することを確認します。

1. `ac-price-book-id` の値を `"east_coast_inc"` に置き換えます。
1. ファイルを保存します。

変更を保存すると、ブレーキとサスペンション パーツのみを販売するように設定された Carvelo チャネルを使用するようにカタログ設定が更新されます。

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

   ブレーキ部品の画像をクリックすると、製品詳細と価格情報が表示され、製品価格情報がメモされます。

1. 次に、`tires` を検索します。これは、[!DNL Adobe Commerce Optimizer] インスタンス上のユースケースデータで使用できるもう 1 つのパーツカテゴリです。

   ![ ストアフロント設定のヘッダーが正しくない ](../assets/storefront-configuration-with-incorrect-headers.png)

   結果が返されないことに注意してください。 これは、Celport チャンネルがブレーキとサスペンションの部品のみを販売するように構成されているためです。

1. ストアフロント設定ファイル（`config.json`）を試して更新します。

   1. `ac-channel-id` と `ac-price-book` の値を変更します。

      例えば、チャネル ID を Kingsbluff チャネルに、価格台帳 ID を `east_coast_inc` に変更できます。 「キングスブラフ」パーツ カテゴリのポリシーを確認すると、キングスブラフで使用できるパーツ カテゴリを確認 *きます*

   1. ファイルを保存します。

      ファイルを保存すると、ローカルストアフロントのプレビューが自動的に更新されます。

   1. 検索機能を使用してタイヤ部品を検索することにより、ブラウザーで変更をプレビューします。

      使用可能なパーツ タイプが異なることに注目してください。また、Kingsbluff チャンネルに割り当てられている価格にも注目してください。

      ストアフロント設定ファイルのヘッダー値を変更し、更新されたストアフロントを確認すると、カタログ表示とデータフィルターを更新してストアフロントのエクスペリエンスを簡単にカスタマイズできることが分かります。

## それだ！

このチュートリアルでは、単一の基本カタログを使用 [!DNL Adobe Commerce Optimizer] て、小売業務に合わせてカタログを整理する方法を学習しました。 また、Edge Delivery Servicesを活用してストアフロントを設定する方法についても説明しました。

## 今後の展開

製品検出と Recommendations を使用して顧客向けにショッピングエクスペリエンスをパーソナライズする方法については、[ マーチャンダイジングの概要 ](../merchandising/overview.md) を参照してください。
