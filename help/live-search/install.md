---
title: 入門 [!DNL Live Search]
description: Adobe Commerceの必要システム構成とインストール手順  [!DNL Live Search]  説明します。
role: Admin, Developer
exl-id: 45b985f1-9afb-4a07-93e8-f2fe231c5400
badgePaas: label="PaaS のみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeが管理する PaaS インフラストラクチャ）およびオンプレミスプロジェクトにのみ適用されます。"
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '3139'
ht-degree: 0%

---

# [!DNL Live Search] で成功するための設定

Adobe Commerce [!DNL Live Search] と [[!DNL Catalog Service]](../catalog-service/guide-overview.md) は連携して、パフォーマンスが高く関連性の高い直感的な検索ソリューションを提供し、顧客が必要なものを正確かつ迅速に見つけられるようにします。 特に、[!DNL Catalog Service] は、使用する [!DNL Live Search] など、SaaS サービスのカタログデータを表示します。

この記事では、[!DNL Catalog Service] で [!DNL Live Search] を実装する手順を順を追って説明します。

>[!IMPORTANT]
>
>サイト検索に関しては、Adobe Systemsコマースにはオプションがあります。 実装する前に [境界と制限](boundaries-limits.md) を必ず読み、 [!DNL Live Search] がビジネスニーズに適合していることを確認してください。

## オーディエンス

この記事は、Adobe Systems Commerce インスタンスのインストールと構成を担当するチーム開発者またはシステム インテグレーターを対象としています。

## 必要条件

- [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) 2.4.4 以降
- PHP バージョン 8.1、8.2、または 8.3
- [!DNL Composer]

## サポートされるプラットフォーム

- クラウド上のAdobe Commerce（ECE） :2.4.4 以降
- Adobe Commerce オンプレミス（EE） :2.4.4 以降

## ワークフローの概要

大まかに言えば、オンボーディング [!DNL Live Search] では、次の操作が必要です。

1. [!DNL Live Search] 拡張機能の [ インストール ](#1-install-the-live-search-extension)
1. API キーの [ 設定 ](#2-configure-api-keys)
1. カタログデータの [ 同期 ](#3-sync-your-catalog-data)
1. カタログ データがエクスポートされたことを [ 確認 ](#4-verify-that-the-data-was-exported) します
1. データ [&#128279;](#5-configure-the-data) 設定）
1. [ テスト ](#6-test-the-connection) 接続
1. イベントでデータがキャプチャされていることを [ 確認 ](#7-validate-events-are-capturing-data) します
1. ストアフロントの [ カスタマイズ ](#8-customize-for-your-storefront)

## 1. [!DNL Live Search] 拡張機能をインストールする

[!DNL Live Search] は、[Adobe Marketplace&rbrace; から &lbrace;Composer](https://getcomposer.org/) を通じて拡張機能と [&#128279;](https://commercemarketplace.adobe.com/magento-live-search.html) てインストールさ  ます。 [!DNL Live Search] をインストールして設定すると、Adobe [!DNL Commerce] は検索とカタログデータの SaaS サービスとの共有を開始します。 この時点で、*管理者* ユーザーは、検索ファセット、同義語およびマーチャンダイジングルールの設定、カスタマイズおよび管理を行うことができます。

>[!NOTE]
>
>[!DNL Live Search] 3.0.2 の時点では、[!DNL Catalog Service] 拡張機能は [!DNL Live Search] インストールにバンドルされています。

>[!IMPORTANT]
>
>[!DNL Live Search] 4.0.0 以降、検索アダプタは非推奨になりました。 今後、検索アダプタは、セキュリティ上の問題に対処するためにのみ更新されます。

1. [cron ジョブ ](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) と [ インデクサー ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) が実行中であることを確認します。

   >[!IMPORTANT]
   >
   >2023 年 8 月のElasticsearch 7 のサポート終了のお知らせに伴い、Adobe Commerceをご利用のすべてのお客様に OpenSearch 2.x 検索エンジンを利用することをお勧めします。 製品のアップグレード中に検索エンジンを移行する方法については、[ アップグレード ガイド ](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/prepare/opensearch-migration) の _OpenSearch への移行_ を参照してください。

1. [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-live-search.html) から `live-search` パッケージをダウンロードします。

1. コマンドラインから次を実行します。

   ```bash
   composer require magento/live-search
   ```

   [!DNL Live Search] 拡張機能を **新規** Adobe Commerceのインストールに追加する場合は、次のコマンドを実行して、[!DNL OpenSearch] および関連モジュールを一時的に無効にし、[!DNL Live Search] をインストールします。 次に、手順 4 に進みます。

   ```bash
      bin/magento module:disable Magento_Elasticsearch Magento_Elasticsearch7 Magento_OpenSearch Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   [!DNL Live Search]拡張機能を&#x200B;**既存の** Adobe Systems Commerce インストールに追加する場合は、次のコマンドを実行して、ストアフロント検索の結果を提供する[!DNL Live Search]モジュールを無効にします。次に、手順 4 に進みます。

   ```bash
      bin/magento module:disable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover Magento_LiveSearchProductListing 
   ```

   [!DNL Elasticsearch][!DNL Live Search]サービスがカタログデータを同期し、製品のインデックスをバックグラウンドで作成している間、ストアフロントからの検索リクエストを引き続き管理します。

1. 以下を実行します。

   ```bash
   bin/magento setup:upgrade
   ```

1. 次の [インデクサー](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) が「Update by スケジュール」に設定されていることを確認します。

   - 製品フィード
   - 製品バリアントフィード
   - カタログ属性フィード
   - 商品価格フィード
   - 範囲 Web サイトデータフィード
   - 顧客グループデータフィードの範囲
   - カテゴリフィード
   - カテゴリ権限フィード

1. 新しいCommerce インスタンスに [!DNL Live Search] をインストールする場合は、作業が完了し、[2 にスキップできます。 API キーを設定 ](#2-configure-api-keys) セクション。 Live Search を既存のCommerce インスタンスにインストールする場合は、次の手順に進んでください。

1. 次のコマンドを実行して、[!DNL Live Search] 拡張機能を有効にし、[!DNL OpenSearch] を無効にして、`setup` を実行します。

   ```bash
   bin/magento module:enable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover  Magento_LiveSearchProductListing 
   ```

   ```bash
   bin/magento module:disable Magento_Elasticsearch Magento_Elasticsearch6 Magento_Elasticsearch7 Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch 
   Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   ```bash
   bin/magento setup:upgrade
   ```

### [!DNL Live Search] ベータ版のインストール

>[!IMPORTANT]
>
>次の機能はベータ版です。 ベータ版に参加するには、 [commerce-storefront-services](mailto:commerce-storefront-services@adobe.com) に電子メールリクエストを送信してください。

このベータ版では、[&#128279;](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/) の 3 つの新しい機能が `productSearch` クエリでサポートされています。

- **階層化された検索** - 別の検索コンテキスト内でSearch - この機能を使用すると、検索クエリに対して最大 2 層の検索を実行できます。 例：

   - **レイヤー 1 検索** - 「product_attribute_1」の「モーター」のSearch。
   - **レイヤー 2 検索** - 「product_attribute_2」の「部品番号123」のSearch。 この例では、&quot;モーター&quot; の結果内で &quot;部品番号 123&quot; を検索します。

  レイヤー検索は、以下に説明するように、`startsWith` 検索インデックスと `contains` 検索インデックスの両方で使用できます。

- **startsWith 検索インデックス付け** - `startsWith` インデックス付けを使用して検索します。 この新機能により、次のことが可能になります。

   - 属性値が特定の文字列で始まる製品の検索。
   - 「次で終わる」検索の設定による、買い物客での属性値が特定の文字列で終わる製品の検索。 「次で終わる」検索を有効にするには、製品属性を逆に取り込む必要があり、API 呼び出しも逆の文字列にする必要があります。

- **contains search indexation** -contains indexation を使用して属性を検索します。 この新機能により、次のことが可能になります。

   - より大きな文字列内のクエリを検索する。 たとえば、買い物客文字列 &quot;HAPE-123&quot; 内の製品番号 &quot;PE-123&quot; を検索するとします。

      - 注: この検索タイプは、オートコンプリート検索を実行する既存の [フレーズ 検索](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#phrase) とは異なります。 たとえば、商品属性値が「アウトドアパンツ」の場合、フレーズ検索は「アウトパン」の応答を返しますが、「oor ants」の応答は返しません。 ただし、A contains検索は「oor ants」の応答を返します。

これらの新しい条件により、検索クエリのフィルタリングメカニズムが強化され、検索結果を絞り込むことができます。 これらの新しい条件は、メイン検索クエリーには影響しません。

これらの新しい条件は、検索結果ページに実装できます。 例えば、ページに新しいセクションを追加して、買い物客が検索結果をさらに絞り込めるようにすることができます。 買い物客が「製造元」、「部品番号」、「説明」など、特定の製品属性を選択できるようにすることができます。 そこから、`contains` 条件または `startsWith` 条件を使用して、これらの属性内を検索します。 検索可能な [ 属性 ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types) のリストについては、管理ガイドを参照してください。

1. ベータ版をインストールするには、次の依存関係をプロジェクトに追加します。

   ```bash
   composer require magento/module-live-search-search-types:"^1.0.0-beta1"
   ```

1. 変更をコミットして `composer.json` にプッシュし、ファイル `composer.lock` クラウドプロジェクトにプッシュします。 [詳細情報](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension)。

   このベータ版では、管理者に **[!UICONTROL Autocomplete]**、**[!UICONTROL Contains]**、**[!UICONTROL Starts with]** の **[!UICONTROL Search types]** チェックボックスが追加されています。 また、[`productSearch`](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#filtering-using-search-capability) GraphQL API を更新して、これらの新しい検索機能を組み込みます。

1. 管理者で、検索可能にする [ 製品属性を設定する ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes-add#step-5-describe-the-storefront-properties) と、その属性の検索機能を指定します。例えば、**次を含む** （デフォルト）や **次で始まる** などです。 **Contains** に対して有効にする属性を最大 6 つ指定し、**Starts with** に対して有効にする属性を最大 6 つ指定できます。 ベータ版の場合、管理者はこの制限を強制しませんが、API 検索では強制されます。

   ![ 検索機能の指定 ](./assets/search-filters-admin.png)

1. 新しい `contains` および `startsWith` の検索機能を使用して [!DNL Live Search] API 呼び出しを更新する方法については、[ 開発者向けドキュメント ](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#filtering-using-search-capability) を参照してください。

### フィールドの説明

| フィールド | 説明 |
|--- |--- |
| `Autocomplete` | デフォルトで有効になっており、変更できません。 `Autocomplete` では、[ 検索フィルター ](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#filtering) で `contains` を使用できます。 ここで、`contains` の検索クエリは、オートコンプリートタイプの検索応答を返します。 Adobeでは、通常 50 文字を超える説明フィールドに、このタイプの検索を使用することをお勧めします。 |
| `Contains` | オートコンプリート検索ではなく、真の「文字列に含まれるテキスト」検索を有効にします。 [ 検索フィルター ](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#filtering-using-search-capability) で `contains` を使用します。 詳しくは、[ 制限事項 ](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#limitations) を参照してください。 |
| `Starts with` | 特定の値で始まる文字列をクエリできます。 [ 検索フィルター ](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#filtering-using-search-capability) で `startsWith` を使用します。 |

## 2. API キーの設定

Adobe Commerce API キーとそれに関連する秘密鍵は、Adobe Commerceのインストールに接続する [!DNL Live Search] めに必要です。 API キーは、[!DNL Commerce] のライセンス所有者のアカウントで生成および管理され、開発者またはシステムインテグレーターと共有できます。 その後、開発者は、ライセンス所有者に代わって SaaS データスペースを作成および管理できます。 既に一連の API キーがある場合は、それらを再生成する必要はありません。

API キーを設定する方法については、[Commerce サービスコネクタ ](../landing/saas.md) の記事を参照してください。

## 3. カタログデータを同期する

[!DNL Live Search] は、カタログデータをAdobeの SaaS インフラストラクチャに移動します。 データのインデックスが作成され検索結果はこのインデックスから直接ストアフロントに配信されます。 サイズと複雑さに応じて、インデックス作成には 30 分から数時間かかる場合があります。

SaaS サービスへのカタログ データの初期同期を開始するには、次のコマンドをこの順序で実行します。

```bash
bin/magento saas:resync --feed productattributes
bin/magento saas:resync --feed products
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed productoverrides
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed categoryPermissions
```

これらのコマンドを実行すると、SaaS サービスへのカタログ データの初期同期が開始されます。

>[!WARNING]
>
> データのインデックス作成と同期の間、検索操作とカテゴリ参照操作はストアフロントでは使用できません。 カタログのサイズによっては、データを SaaS サービスに同期するために `cron` 実行されてからプロセスに少なくとも 1 時間かかる場合があります。

### 同期進行状況の監視

同期および共有されるデータは、 [データ 管理ダッシュボードを使用して表示できます](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard)。 このダッシュボードは、ストアフロントの商品データの可用性に関する貴重な洞察を提供し、買い物客に迅速に表示できるようにします。

![ データ管理ダッシュボード ](assets/data-management-dashboard.png)

また、[Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting) およびデータ書き出し拡張機能のログを使用して、同期コマンドを実行し、同期プロセスのトラブルシューティングを行うこともできます。

#### 今後の製品アップデート

初回同期後、製品の増分更新がストアフロント検索で使用できるようになるまで最大 15 分かかる場合があります。 詳しくは、インデックス作成ドキュメントの [ 製品アップデートのストリーミング ](indexing.md) を参照してください。

## 4. データがエクスポートされたことを確認する

カタログデータが Adobe Systems Commerce からエクスポートされ、 [!DNL Live Search]と同期されているかどうかを確認するには、いくつかのオプションがあります。

- Look、次の表のエントリを参照してください。

   - `cde_products_feed`
   - `cde_product_attributes_feed`

  >[!NOTE]
  >
  >`table does not exist`エラーが発生した場合は、`catalog_data_exporter_products` および `catalog_data_exporter_product_attributes` テーブルでエントリを探します。これらのテーブル名は、4.2.1 より前の [!DNL Live Search] バージョンで使用されます。

- デフォルトの クエリ で [GraphQL プレイグラウンド](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/graphql) を使用して (詳細については [GraphQL リファレンス](https://developer.adobe.com/commerce/services/graphql/live-search/) を参照)、以下を確認します。

   - 返される製品数は、ストア 表示で期待される数に近いものです。
   - ファセットが返されます。

その他のヘルプについては、サポートナレッジベースの「 [[!DNL Live Search] カタログが同期されていません](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync) を参照してください。

## 5. データを構成する

商品データを正しく設定することで検索良好な結果が得られます。 このセクションでは、製品リストウィジェットを有効にし、カテゴリを割り当てます。

### 製品リストウィジェットの有効化

[!DNL Live Search] 4.0.0 以降をインストールすると、製品リストへのウィジェットはデフォルトで有効になります。 ウィジェットを有効にすると、検索結果ページとカテゴリ参照製品リストページで別の UI コンポーネントが使用されます。 この UI コンポーネントは、[Catalog Service API](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/) を直接呼び出すことで、応答時間を短縮します。

バージョン 4.0.0 以降の [!DNL Live Search] がある場合は、手動で製品一覧ウィジェットを有効にする必要があります。

1. *管理者* から、**[!UICONTROL Stores]**/_[!UICONTROL Settings]_/**[!UICONTROL Configuration]**&#x200B;に移動します。
1. [ **[!UICONTROL Live Search]**] で [ **[!UICONTROL Storefront Features]**] を選択します。
1. 設定&#x200B;**[!UICONTROL Enable Product Listing Widgets]**`Yes`。

   ![製品リストウィジェットの有効化](assets/ls-admin-enable-widget.png)

この設定を変更すると、 `Page cache is invalidated` メッセージが表示されます。 変更を保存するには、Magento キャッシュをフラッシュする必要があります。

1. 次のいずれかの方法で [キャッシュ管理](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management) ページにアクセスします。

   - メッセージの上にあるワークスペースの **[!UICONTROL Cache Management]** リンクをクリックします。
   - _管理者_ サイドバーで、**[!UICONTROL System]**/_[!UICONTROL Tools]_/**[!UICONTROL Cache Management]**&#x200B;に移動します。

1. **Configuration**&#x200B;[!UICONTROL Cache Type] を選択し、「**[!UICONTROL Flush Magento Cache]**」をクリックします。

   ストアフロントに対する変更は、キャッシュをフラッシュした直後に行われます。

### カテゴリの割り当て

[!DNL Live Search] で返された製品は、[ カテゴリ ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/categories) に割り当てられている必要があります。 例えば Luma では、製品が「男性」、「女性」、「歯車」などのカテゴリに分類されます。 サブカテゴリも「トップス」、「ボトムス」、「ウォッチポイント」に設定されます。 これらのカテゴリの割り当てにより、フィルタリング時の精度が向上します。

## 6.接続をテストする

カタログデータを SaaS にして、テストを行い、次のシナリオで製品データが返されることを確認します。

- [!UICONTROL Search] ボックスは正しく結果を返します
- カテゴリの参照で結果が正しく返される
- ファセットは、検索結果ページでフィルターとして使用できます

すべてが正しく動作している場合は、[!DNL Live Search] がインストールされ、接続され、使用できる状態になっています。

ストアフロントで問題が発生した場合は、`var/log/system.log` ファイルで API 通信の失敗やサービス側のエラーを確認します。

ファイアウォールを通過する [!DNL Live Search] を許可するには、`commerce.adobe.io` を許可リストに追加します。

## 7. イベントでデータが取り込まれていることを確認する

サイトにデプロイしたストアフロントイベントが機能していることを確認します。 これは、ヘッドレス実装で特に重要です。

- リク [!DNL Live Search] ストに必要な [ イベント ](events.md) を確認します。
- [ ライブ検索ダッシュボード ](performance.md) に実稼動以外の環境のデータが表示されていることを確認します。
- [ イベント コレクションの検証 ](../product-recommendations/verify.md). このページは [!DNL Product Recommendations] ガイドですが、検証手順は [!DNL Live Search] にも適用されます。

## 8. ストアフロントに合わせたカスタマイズ

[!DNL Live Search] 拡張機能のインストール、データの同期、検証および設定が完了していること。 次の手順では、[!DNL Live Search] ウィジェットがストアのルックアンドフィールに合っていることを確認します。

必要に応じてカスタム CSS ルールを定義することにより、ポップオーバーウィジェットと PLP ウィジェットのスタイルを設定できます。 「 [ポップオーバー要素のスタイル設定](storefront-popover.md#styling-popover-example) およびウィジェットページ [製品リスト](plp-styling.md#styling-example)を参照してください。

ウィジェットの機能を拡張する場合は、ウィジェットのソースコードを公開リポジトリで入手できます。このシナリオでは、独自のニーズに合わせてJavaScriptをカスタマイズし、CDN にカスタム コードをホストできます。 このカスタムスクリプトは [!DNL Live Search] サービスと通信し、通常どおり結果を返して、ウィジェットの機能を制御できます。

- [PLP ウィジェットリポジトリ](https://github.com/adobe/storefront-product-listing-page)
- [ 検索バーのリポジトリ ](https://github.com/adobe/storefront-search-as-you-type)

## [!DNL Live Search] を更新中

Live Search を更新する前に、コマンドラインから次のコマンドを実行して、インストールされている Live Search のバージョンを確認します。

```bash
composer show magento/module-live-search | grep version
```

[!DNL Live Search] を更新するには、コマンドラインから次のコマンドを実行します。

```bash
composer update magento/live-search --with-dependencies
```

3.1.1 から 4.0.0 などのメジャーバージョンにアップデートするには、プロジェクトのルート [!DNL Composer] `.json` ファイルを次のように編集します。

1. 現在インストールされている `magento/live-search` のバージョンが `3.1.1` 以下で、バージョン `4.0.0` 以降にアップグレードする場合は、アップグレードの前に次のコマンドを実行します。

   ```bash
   bin/magento module:enable Magento_AdvancedSearch
   ```

   現在インストールされている `magento/live-search` バージョンについて詳しくは、次のコマンドを実行してください。

   ```bash
   composer show magento/live-search
   ```

1. ルート `composer.json` ファイルを開き、`magento/live-search` を検索します。

1. `require` セクションで、バージョン番号を次のように更新します。

   ```json
   "require": {
      ...
      "magento/live-search": "^4.0",
      ...
    }
   ```

1. 保存 `composer.json` ます。 コマンドラインから次のコマンドを実行します。

   ```bash
   composer update magento/live-search --with-dependencies
   ```

## アンインストール [!DNL Live Search]

[!DNL Live Search]をアンインストールするには、[モジュールのアンインストール](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/uninstall-modules)を参照してください。

## [!DNL Live Search] パッケージ

[!DNL Live Search] 拡張機能は、次のパッケージで構成されています。

| パッケージ | 説明 |
|--- |--- |
| `module-live-search` | を使用すると、マーチャントは、ファセット、同義語、クエリルールなどの検索設定を指定したり、読み取り専用のGraphQL プレイグラウンドにアクセスして *Admin* からクエリをテストしたりできます。 |
| `module-live-search-adapter` | リクエスト検索ストアフロントから [!DNL Live Search] サービスにルーティングし、結果をストアフロントにレンダリングします。 <br />- カテゴリー参照 - ストアフロント [最上位ナビゲーション](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/navigation/navigation-top) から検索サービスにリクエストをルーティングします。<br />- グローバル 検索 - ストアフロントの右上にある [クイック 検索](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search) ボックスから [!DNL Live Search] サービスに要求をルーティングします。 |
| `module-live-search-storefront-popover` | 「入力時に検索」ポップオーバーは、標準のクイック検索に取って代わり、上位検索結果のデータとサムネイルを返します。 |

## [!DNL Live Search] 依存関係

[!DNL Live Search] 拡張機能をインストールするための [!DNL Composer] メタパッケージには、次のモジュール依存関係が含まれています。

- `magento/module-saas-catalog`
- `magento/module-saas-category`
- `magento/module-saas-category-permissions`
- `magento/module-saas-product-override`
- `magento/module-saas-product-variant`
- `magento/module-saas-price`
- `magento/module-saas-scopes`
- `magento/module-bundle-product-data-exporter`
- `magento/module-catalog-inventory-data-exporter`
- `magento/module-catalog-url-rewrite-data-exporter`
- `magento/module-configurable-product-data-exporter`
- `magento/module-parent-product-data-exporter`
- `magento/module-gift-card-product-data-exporter`
- `magento/module-bundle-product-override-data-exporter`
- `data-services`
- `services-id`

## 高度な概念

以下のセクションでは、[!DNL Live Search] と [!DNL Catalog Service] を使用する際の、より高度なトピックを示します。

### エンドポイント

[!DNL Live Search] は、`https://catalog-service.adobe.io/graphql` のエンドポイントを介して通信します。

[!DNL Live Search]は完全な製品データベースにアクセスできないため、[!DNL Live Search] GraphQL およびコマースコア GraphQL API には完全なパリティがありません。

Adobe Systems では、SaaS API (具体的にはカタログ サービス エンドポイント) を直接呼び出すことをお勧めします。

- コマースデータベース/Graphqlプロセスをバイパスすることでパフォーマンスを向上させ、プロセッサの負荷を軽減します
- [!DNL Catalog Service] フェデレーションを利用して、単一のエンドポイントから[!DNL Live Search]、[!DNL Catalog Service]、および[!DNL Product Recommendations]を呼び出します。

一部のユースケースでは、製品の詳細や同様のケースについては、[!DNL Catalog Service] に問い合わせることをお勧めします。 詳しくは [refineProduct](https://developer.adobe.com/commerce/services/graphql/catalog-service/refine-product/) を参照してください。

カスタムヘッドレス実装がある場合は、 [!DNL Live Search] リファレンス実装を確認してください。

- [PLP ウィジェット ](https://github.com/adobe/storefront-product-listing-page)
- [ ライブ検索フィールド ](https://github.com/adobe/storefront-search-as-you-type)

検索アダプター、Luma ウィジェット、AEM CIF ウィジェットなどの標準コンポーネントを使用しない場合、ユーザーインタラクションデータの自動収集はデフォルトでは機能しません。 Adobe Senseiでは、この収集されたデータを使用して、インテリジェントなマーチャンダイジングとパフォーマンスのトラッキングを行います。 この問題を解決するには、このデータ収集をヘッドレスで実装するカスタムソリューションを開発する必要があります。

[!DNL Live Search] の最新バージョンでは、既に [!DNL Catalog Service] が使用されています。

### 言語サポート

[!DNL Live Search] ウィジェットは次の言語をサポートしています。

|  |  |  |  |
|--- |--- |--- |--- |
| 言語 | 地域 | 言語コード | Magento ロケール |
| ブルガリア語 | ブルガリア | bg_BG | bg_BG |
| カタルニア語 | スペイン | ca_ES | ca_ES |
| チェコ語 | チェコ共和国 | cs_CZ | cs_CZ |
| デンマーク語 | デンマーク | da_DK | da_DK |
| ドイツ語 | ドイツ | de_DE | de_DE |
| ギリシャ語 | ギリシャ | el_GR | el_GR |
| 英語 | 英国 | en_GB | en_GB |
| 英語 | 米国 | en_US | en_US |
| スペイン語 | スペイン | es_ES | es_ES |
| エストニア語 | エストニア | et_EE | et_EE |
| バスク語 | スペイン | eu_ES | eu_ES |
| ペルシャ語 | イラン | fa_IR | fa_IR |
| フィンランド語 | フィンランド | fi_FI | fi_FI |
| フランス語 | フランス | fr_FR | fr_FR |
| ガリシア語 | スペイン | gl_ES | gl_ES |
| ヒンディー語 | インド | hi_IN | hi_IN |
| ハンガリー語 | ハンガリー | hu_HU | hu_HU |
| インドネシア | インドネシア | id_ID | id_ID |
| イタリア語 | イタリア | it_IT | it_IT |
| 韓国語 | 韓国 | ko_KR | ko_KR |
| リトアニア語 | リトアニア | lt_LT | lt_LT |
| ラトビアン | ラトビア | lv_LV | lv_LV |
| ノルウェー語 | ノルウェー ブークモール | nb_NO | nb_NO |
| オランダ語 | オランダ | nl_NL | nl_NL |
| ポーランド語 | ポーランド | pl_PL | pl_PL |
| ポルトガル語 | ブラジル | pt_BR | pt_BR |
| ポルトガル語 | ポルトガル | pt_PT | pt_PT |
| ルーマニア語 | ルーマニア | ro_RO | ro_RO |
| ロシア | ロシア | ru_RU | ru_RU |
| スウェーデン語 | スウェーデン | 参照（_S） | 参照（_S） |
| タイ語 | タイ | th_TH | th_TH |
| トルコ語 | トルコ | tr_TR | tr_TR |
| 中国語 | 中国 | zh_CN | zh_Hans_CN |
| 中国語 | 台湾 | zh_TW | zh_Hant_TW |

Commerce管理者の言語設定がサポートされている言語と一致することが検出された場合、デフォルトではその言語に設定されます。 それ以外の場合、ウィジェットのデフォルト値は英語になります。 管理者で、_[!UICONTROL Stores]_/[!UICONTROL Settings]/_[!UICONTROL Configuration]_/_[!UICONTROL General]_/[!UICONTROL Country Options] に移動して、言語設定を指定します。

また、管理者は [ 検索インデックス ](settings.md#language) の言語を設定して、検索結果を向上させることもできます。

### ウィジェットコードリポジトリー

製品一覧表示ページウィジェットとライブ検索フィールドウィジェットのコードは、GitHub からダウンロードできます。

コードにアクセスできる開発者は、その動作と外観を完全にカスタマイズできます。 ユーザーは独自のサーバーでコードをホストしますが、 [!DNL Live Search] サービスを使用します。

- [PLP ウィジェット ](https://github.com/adobe/storefront-product-listing-page)
- [ 検索バー ](https://github.com/adobe/storefront-search-as-you-type)

### データエクスポート拡張機能

Live Search を有効にすると、データ書き出し拡張機能によってCommerce アプリケーションと Live Search の間でCommerce データが同期されます。 このプロセスにより、最新のコマース データをストアフロントで使用できるようになります。 管理者では、データ管理ダッシュボードを使用して同期ステータスを確認できます。 Commerce CLI とログを使用して、データ エクスポート プロセスの管理とトラブルシューティングを行うことができます。 詳しくは、『 [データ 書き出しガイド](../data-export/overview.md)』を参照してください。

### 在庫管理

[!DNL Live Search] コマースの [在庫管理](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction) 機能をサポートします (以前は複数出力元在庫、または MSI と呼ばれていました)。 フル サポートを有効にするには、依存関係モジュール`commerce-data-export`バージョン 102.2.0+ に[更新](install.md#updating-live-search)必要があります。

[!DNL Live Search] は、商品がInventory management内で使用可能かどうかを示すブール値を返しますが、どのソースが在庫を持っているかに関する情報は含まれません。

### 価格インデクサー

Live Search のお客様は、[SaaS 価格インデクサー ](../price-index/price-indexing.md) を使用できます。これにより、価格変更の更新と同期時間が短縮されます。

### 価格サポート

ライブ検索ウィジェットは、Adobe Commerceでサポートされているすべての価格タイプではなく、ほとんどの価格タイプをサポートしています。

現在、基本価格がサポートされています。 サポートされていない高度な価格は次のとおりです。

- コスト
- 広告の最低価格

より複雑な価格計算については、[API メッシュ ](../catalog-service/mesh.md) を参照してください。

価格フォーマットは、Commerce インスタンス内の次のロケール設定をサポートしています。*ストア* /設定/ *設定* /一般/ *一般* / ローカルオプション / ロケール

### ヘッドレスストアフロントのサポート

オプションで、アプリケーションの既存のGraphQL範囲を拡張する `module-data-services-graphql` モジュールをインストールし、ストアフロントの行動データ収集に必要なフィールドを含める必要が生じる場合があります。

```bash
composer require magento/module-data-services-graphql
```

このモジュールは、GraphQL クエリにコンテキストを追加します。

- `dataServicesStorefrontInstanceContext`
- `dataServicesMagentoExtensionContext`
- `dataServicesStoreConfigurationContext`

### B2B サポート

[!DNL Live Search] では、追加の [ 制限事項 ](boundaries-limits.md#b2b-and-category-permissions) を追加して [&#128279;](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/guide-overview)B2B 機能をサポートしています。

### PWA サポート

[!DNL Live Search] はPWA Studioで動作しますが、他のCommerceの実装と比較すると、わずかな違いがあります。 検索や製品リストのページなどの基本的な機能は Venia で機能しますが、Graphql の一部の並べ替えが正しく機能しない場合があります。 パフォーマンスの違いもあります。

- [!DNL Live Search] の現在のPWA実装では、検索結果を返すのにネイティブのCommerce ストアフロントよりも多くの処理時間 [!DNL Live Search] 必要です。
- PWAの [!DNL Live Search] は、[ イベント処理 ](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/) をサポートしていません。 その結果、検索レポートとインテリジェントマーチャンダイジングがPWAのストアフロントで機能しません。
- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) を使用する場合、GraphQLは `description`、`name`、`short_description` に対する直接フィルタリングをサポートしていませんが、これらのフィールドはより一般的なフィルターで返すことができます。

PWA Studioで [!DNL Live Search] を使用する場合、インテグレーターは次の要件も満たす必要があります。

1. [livesearch-storefront-utils](https://www.npmjs.com/package/@magento/ds-livesearch-storefront-utils) をインストールします。
1. `storeDetails` オブジェクトに `environmentId` を設定します。

   ```javascript
   const storeDetails: StoreDetailsProps = {
       environmentId: <Storefront_ID>,
       websiteCode: "base",
       storeCode: "main_website_store",
       storeViewCode: "default",
       searchUnitId: searchUnitId,
       config: {
           minQueryLength: 5,
           pageSize: 8,
           currencySymbol: "$",
           },
       };
   ```

### の Cookie

[!DNL Live Search] は、基本機能の一部としてユーザーインタラクションデータを収集し、このデータを保存するために cookie が使用されます。 ユーザー情報を収集する場合、ユーザーは Cookie の保存に同意する必要があります。 [!DNL Live Search] と [!DNL Product Recommendations] はデータストリームを共有するので、同じ cookie メカニズムになります。 詳しくは、[Cookie 制限の処理 ](https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/developer/setting-cookie) を参照してください。
