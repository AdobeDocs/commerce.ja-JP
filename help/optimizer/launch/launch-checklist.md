---
title: チェックリストを起動
description: ' [!DNL Adobe Commerce Optimizer] 本番環境の設定、ストアフロント、SEO、CDN、統合、セキュリティ、分析、テストを検証する方法について説明します。'
solution: Commerce
feature: Integration, Storefront, Search, Catalog Management, Personalization
feature-set: Commerce
role: Admin, Developer
level: Intermediate
topic: Administration
recommendations: noCatalog
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよび [!DNL Adobe Commerce Optimizer]  プロジェクトにのみ適用されます（Adobeで管理されるSaaS インフラストラクチャ）。"
source-git-commit: 37b8b8a334ca11daacfd3da03b0441e77329e2e1
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 0%

---


# チェックリストを起動

このチェックリストを使用して、実稼動[!DNL Adobe Commerce Optimizer] プロジェクトが設定され、テストされ、起動の準備ができていることを確認します。 チームで各セクションを作業し、独自のプロジェクト計画やトラッカーで完了状況を追跡します。 以下で参照する製品機能とUI領域については、[[!DNL Adobe Commerce Optimizer]  ドキュメント &#x200B;](../overview.md)を参照してください。

## ユースケースとアーキテクチャ {#use-case}

このチェックリストは、[!DNL Adobe Commerce Optimizer]とEdge Delivery Services（EDS）を既存のAdobe Commerce on Cloud インスタンスと組み合わせたB2C エクスペリエンスを提供する場合に使用します。

一般的なソリューションには、次のコンポーネントが含まれます。

- **Cloud** - Adobe Commerce on Cloudは、カタログデータ、顧客、アセット、購入フロー（チェックアウト、注文管理、配送など）を管理します。
- **Optimizer**—[!DNL Adobe Commerce Optimizer]は、マーチャンダイジング体験を提供します。
- **Storefront** - Edge Delivery ServicesのAdobe Commerce StorefrontにはUIが用意されています。
- **サードパーティのサービス** – 支払い、送料、税金事業者。
- **App Builder** – 拡張性。
- **API メッシュ** - ルーティングをリクエストします。

## CloudでのAdobe Commerceの検証 {#verify-cloud}

Adobe Commerce on Cloud環境が本番環境に対応していることを確認します。

▢ クラウドインスタンスは[&#x200B; プロビジョニングされています](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/start/new-project)。
▢ テスト データとダミーデータがインスタンスから削除されます。
▢実稼動データがインスタンスに読み込まれます。
▢ [GraphQL エンドポイント &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/)をご存知でしょう。
▢ インスタンスは[配信準備完了](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/launch/checklist)の要件を満たしています。

## Commerce Optimizer インスタンスの検証 {#verify-optimizer}

[!DNL Adobe Commerce Optimizer]実稼動インスタンスが正しく設定されていることを確認します。

▢実稼動インスタンスはアクティブです。 プロビジョニング方法については、[入門](../get-started.md)を参照してください。
▢ インスタンスが正しい地域にあります。
▢環境タイプは実稼動環境です。
▢組織ID、クライアント ID、取り込みURL、およびCommerce Optimizer URLをご存知です。 [開始](../get-started.md)を参照してください。
▢設定された制限と境界は、Adobe カスタマーテクニカルアドバイザー（CTA）が確認した値と一致します。
▢ テスト アーティファクトとダミーデータがインスタンスから削除されました。

## ストアフロントサイトの確認 {#verify-storefront-site}

Edge Delivery Services ストアフロントサイトが存在し、アクセスが制限されていることを確認します。

▢ ストアフロントサイトが存在します。 [&#x200B; ストアフロントの作成](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/)を参照してください。
▢ サイト名を知っています。
▢承認済みのユーザーのみが[を公開する](https://tools.aem.live/tools/user-admin/index.html)権限を持っています。
▢承認済みのユーザーのみが[作成権限](https://docs.da.live/administrators/guides/permissions)を持っています。

## CloudとOptimizerの統合の検証 {#cloud-optimizer-integration}

クラウド上のAdobe Commerceと[!DNL Adobe Commerce Optimizer]のデータ交換が正しいことを確認します。

### Adobe Commerceの

Cloud プロジェクトでこれらのチェックを完了します。

▢ Commerce Optimizer コネクタは[&#x200B; インストールされ、設定されています](../../aco-connector/get-started.md)。
▢ `aco:conf:show` CLI コマンドは、実稼動Commerce Optimizer インスタンスへの接続を確認します。 組織ID、クライアント ID、取り込みURL、およびCommerce Optimizer URLが実稼動環境に一致します。
▢設定を書き出す[の同期範囲](../../aco-connector/get-started.md)は、要件に一致しています。
▢ [&#x200B; データフィードの同期ステータス &#x200B;](../../aco-connector/get-started.md)は、Cloud インスタンスからのデータ書き出しを確認します。

### Commerce Optimizerの

[!DNL Adobe Commerce Optimizer] UIでこれらのチェックを完了します。

▢ [&#x200B; データ同期ダッシュボード &#x200B;](../setup/data-sync.md)には、受信したデータが表示されます。 商品、価格、および属性がカタログサービス、商品ディスカバリー、およびレコメンデーションに表示されます。
▢ [価格表](../setup/pricebooks.md)は、クラウド上の顧客グループから自動的に作成されます。
▢ [&#x200B; カタログ ビュー](../setup/catalog-view.md)が存在し、そのIDを知っています。
▢ [&#x200B; ポリシー](../setup/policies.md)が存在し、そのIDを知っています。
▢ [&#x200B; ファセット &#x200B;](../merchandising/facets/overview.md)が設定されています。
▢ [類義語](../merchandising/synonyms/overview.md)が設定されています。
▢ [&#x200B; マーチャンダイジングルール &#x200B;](../merchandising/rules/overview.md)が設定されています。
▢ [価格ファセットと検索言語](../settings.md)は、これらの機能を使用する際の要件に一致します。
▢ [製品レコメンデーション &#x200B;](../merchandising/recommendations/create.md)が存在し、プレビューで期待どおりに動作します。
▢ [検索パフォーマンスデータ &#x200B;](../manage-results/search-performance.md)が&#x200B;*管理者*に表示されます。
▢ [推奨事項のパフォーマンスデータ &#x200B;](../manage-results/recommendation-performance.md)が&#x200B;*管理者*&#x200B;に表示されます。

## ストアフロントとクラウドの統合を確認する {#storefront-cloud-integration}

ストアフロントが正しいAdobe Commerce GraphQL エンドポイントから読み取られることを確認します。

### Adobe Commerceの

▢個のストアフロント互換性パッケージが[&#x200B; インストールされています](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility/install/)。

### ストアフロントでは

▢ ストアフロント `commerce-core-endpoint`の設定は、[Cloud GraphQL エンドポイント &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/)を指しています。
▢ Cloud GraphQLのプロキシとしてAPI Meshを使用する場合、`commerce-core-endpoint`はCloud GraphQL エンドポイントではなくAPI Mesh エンドポイントを指します。

## ストアフロントとOptimizerの統合の検証 {#storefront-optimizer-integration}

ストアフロント設定でCommerce Optimizerの設定を確認します。

▢お客様のストアフロントでは、正しい[Commerce Optimizer設定](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/)が使用されています。
▢ `adobe-commerce-optimizer`は`true`です。
▢ `commerce-endpoint`は、実稼動のCommerce Optimizer GraphQL エンドポイント、またはAPI Meshを使用する場合はAPI Mesh エンドポイントを指します。
▢ `headers.cs.AC-view-ID`には、実稼動Commerce Optimizer インスタンスのカタログ ビューIDが保持されています。

## クラウド上のサードパーティサービスの確認 {#third-party-services}

ホストコマースシステムで実行される統合を確認します（[!DNL Adobe Commerce Optimizer]ではなく）。

▢ **支払い：**&#x200B;支払いゲートウェイが公開され、テストされています（Stripe、PayPal、Adyenなど）。
▢ **配送：**&#x200B;配送API接続が機能します（UPS、FedExなど）。
▢ **配送：** フルフィルメントプラットフォームが接続され、テストされています（例：ShipStation）。
▢ **税金：**&#x200B;税計算の統合が検証されました（Avalara、TaxJarなど）。
▢ **税金：**&#x200B;会計ソフトウェアの同期が機能します（クイックブックなど）。
▢ **在庫：** PIM、ERP、または在庫管理の統合がテストされ、同期されます。
▢ **アーキテクチャ：** ホストコマースシステムは、支払い、配送、税金、在庫を処理します（[!DNL Adobe Commerce Optimizer]ではなく）。
▢ **アーキテクチャ：** API メッシュとApp Builderは、ホストコマースシステムと[!DNL Adobe Commerce Optimizer]の間で同期を維持します。
▢ **電子メール：** トランザクションの電子メール配信が機能します（注文確認、配送など）。
▢ **電子メール：**&#x200B;電子メールテンプレートがブランドに一致し、正しいリンクを使用しています。

## App BuilderとAPI Meshの検証 {#app-builder-mesh}

実稼動用の拡張性設定を確認します。

### App Builder

▢実稼動ワークスペースには、必要なすべての設定とサービスが含まれています。
▢実稼動アプリは、ビルド シナリオ間でテストに合格します。
▢製品の制限と制限は、[Adobe Developer App Builder製品の説明](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html){target="_blank"}および[App Builder システムの設定と制限](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings){target="_blank"}に基づいて確認されました。
▢実稼動アプリはApp Builder実稼動エンドポイントを使用します。
▢ カスタム *管理者* パネル拡張機能が実稼動ワークスペースにデプロイされます。

### API メッシュ

▢設定とソースは本番準備が完了しました。

### イベント

▢ Adobe I/O Eventsが設定され、サブスクリプションが確認されます。

## ストアフロント体験を最終決定 {#finalize-storefront}

コンテンツ、SEO、パフォーマンス、セキュリティ、CDNの行動をローンチ前に調査する。

### コンテンツとオーサリング

オーサリングワークフローとストアフロントコンポーネントの確認。

▢ [AEM/EDSの公開チェックリスト &#x200B;](https://www.aem.live/docs/go-live-checklist)のレビューが完了しました。
▢ オーサリングソースは、ドキュメントベースまたはユニバーサルエディター（および設定）です。
▢ コンテンツは、プレビューと公開サイクルを使用し→公開されます。
▢ コンテンツとデザイン QAが`.aem.live` ドメインで完了しました。
▢ サイトでファビコンが正しく設定され、提供されています。
▢件のda.liveと製品ビジュアルでは、[設定された](https://docs.da.live/administrators/guides/permissions)個の専用の資格情報が使用されます。
▢個のドロップイン （買い物かご、チェックアウト、PDP、PLP、認証、アカウント）は[&#x200B; カスタマイズ &#x200B;](../storefront.md)され、テストされています。
▢ ストアフロントのブランディングは、CSS デザイントークン、タイポグラフィ、およびカラーを反映しています。

### SEOとインデックス作成

メタデータ、URLを確認し、ビヘイビアーをクロールします。

▢主要ページ（特にPDPおよびPLP）に対して、ドキュメント タイトルのメタデータが存在します。 [Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/metadata/){target="_blank"} ドキュメントの&#x200B;_SEO メタデータ_を参照してください。
▢個のPDPには、[&#x200B; メタデータと構造化データ &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/metadata/){target="_blank"} （JSON-LDなど）が含まれます。
▢製品URL形式が一貫しています（例：`domain/product-name`）。
▢個のバニティ URLが正規URLにリダイレクトされます。
▢ プロジェクトには`robots.txt`が含まれており、適切な場所でインデックスを作成したり、サイトマップを参照したり、インデックスを作成しないパスをブロックしたりできます（例：`/drafts`）。
▢ [&#x200B; リダイレクト &#x200B;](https://www.aem.live/docs/redirects) ファイルは、移行からのURLの変更をカバーしています（例えば、`.html`を削除した後）。
▢個のサイトマップが存在し、必要に応じてGoogle Search Consoleに送信されます。
▢個の正規URLが`2xx`の状態を返します（`3xx`または`4xx`ではありません）。
▢多言語サイトには、サイトマップに`hreflang`個のタグが含まれています。
▢ Google Search Console カバレッジ レポートは最新です。

### プリレンダリング

有効にする場所でサーバーサイドレンダリングを確認します。

▢のプリレンダリングは、主要なページに対して有効です。 [AEM Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-prerender/){target="_blank"} ドキュメントの&#x200B;_Adobe Commerce_の事前レンダリングを参照してください。
▢個のURLは小文字を使用するため、事前レンダリングでリンクが壊れることはありません。
▢ HTML ソースには、事前レンダリングの動作を確認するメタデータと本文コンテンツが含まれています。
▢ ロケールは、該当する場合は正しい翻訳済みページを表示します。
▢追加のHTML マークアップは、必要に応じて[設定](https://www.aem.live/docs/redirects)されます。

### パフォーマンスとモニタリング

パフォーマンスのベースラインと分析の配線を確認します。

▢お客様のストアフロントは、[Adobe Commerce ストアフロント &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/performance/){target="_blank"} ドキュメントの&#x200B;_パフォーマンスのベストプラクティス_に従っています。
▢ （オプション）Google AnalyticsとGoogle Tag Managerが設定されています。
▢ [Storefront events](https://github.com/adobe/commerce-events/tree/main/examples/events/snowplow-debugger)の実装は有効で、データは[!DNL Live Search]および[!DNL Product Recommendations]のダッシュボードにAdobe Commerce *管理者*に表示されます。
▢ `environment`Commerce configuration[の](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/){target="_blank"}分析パラメーターは、開発中は`"Testing"`で、公開時は`"Production"`です。 [Analytics インストルメンテーション &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/setup/analytics/instrumentation/){target="_blank"}を参照してください。
このトピックのガイダンスに従って、▢個のLighthouse スコアが目標（主要ページの`100`など）を満たしています。

### セキュリティとアクセス

権限とシークレットを確認する。

▢適切な権限がDA コンテンツおよびEDS サイト用に設定されています。 オーサリング用の[DA.live権限](https://da.live/docs/administration/permissions)と[認証の設定](https://www.aem.live/docs/authentication-setup-authoring)を参照してください。
▢製品ビジュアル統合がプロビジョニングされます。 [AEM Cloud Service アクセスの概要](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/overview#)を参照してください。
電子メールテンプレートの▢ パスワードリセットリンクが、Edge Delivery Services設定と一致しています。 ストアフロントに関するFAQを参照してください。[Edge Delivery ServicesまたはHelixへの移行後にメールテンプレートのリンクが壊れた場合、どうすればよいですか？](https://experienceleague.adobe.com/developer/commerce/storefront/troubleshooting/faq/#what-should-i-do-if-my-email-template-links-are-broken-after-migrating-to-edge-delivery-services-or-helix){target="_blank"}。
▢統合と支払いプロバイダーの実稼動キーが配置されています。
▢ ドメインが許可リストに加えるされ、バックエンドのWebhookが機能します。

### CDNとキャッシュ

CDN、DNS、およびキャッシュの動作を確認します。

▢ CDN設定では、Sidekickの拡張機能とスクリプト （サイトマップ生成や画像インポーターなど）に実稼動のGraphQL エンドポイント （`yourproject.com/graphql`）が使用されます。
▢ Adobe Commerce Fastlyを使用する場合、CDN パージトークンが使用でき、[&#x200B; サイト設定](https://tools.aem.live/tools/cdn-setup/index.html)には`authToken`と`serviceId`が含まれます。
▢ [CDN設定](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/content-delivery-network/){target="_blank"}は、キャッシュと無効化を検証します。
▢ [&#x200B; マルチストア設定](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/indexing/#multi-store-setups){target="_blank"}の場合、カタログサービスと[!DNL Live Search]要求には、ストア固有のキャッシュバスター（クエリパラメーターやCDN ルールなど）が含まれます。
▢ プッシュ無効化はエンドツーエンドで機能します（変更を公開してから、実稼動ドメインで検証します）。
▢ DNS TTLは、カットオーバー前に十分に低くなっています。
すべてのドメインとホスト名に対して、▢個のDNS AとCNAME レコードが正しいです。
▢ SSL/TLS証明書がプロビジョニングされ、実稼動ドメイン用に検証されます。
▢ `www`およびapex リダイレクトが正しく動作します。

## セキュリティとコンプライアンス {#security-compliance}

セキュリティ対策とコンプライアンスのタスクを確認。

▢ **SSL:**&#x200B;信頼できるSSL/TLS証明書がインストールされています。
▢ **SSL:** HTTPSはサイト全体で適用されます。
▢ **アクセス：** デフォルト *管理者* パスワードが変更され、強力なパスワードポリシーが有効になっています。 [!DNL Adobe Commerce Optimizer] [&#x200B; ユーザーとIDの管理](../user-management.md)を参照してください。
▢ **アクセス：** *管理者* URLはデフォルトではありません。
▢ **アクセス：**&#x200B;すべての&#x200B;*管理者* ユーザーに対して2要素認証が有効になっています。
▢ **アクセス：**&#x200B;非アクティブまたは未使用の管理者ユーザーがプロジェクトに関連付けられていません。
▢ **ファイアウォール：** Web Application Firewall （WAF）が設定され、検証されています。
▢ **PCI:**&#x200B;実稼動環境（PCI スコープ）でのセキュリティ侵入テストが完了しました。
▢ **スキャン：** Adobe セキュリティスキャンツールが登録され、最初のスキャンが完了しました。
▢ **アクセス：** CORSでは、承認済みのオリジンのみが許可されます。
▢ **コンプライアンス：** [の](../shared-responsibility.md)共通責任モデル [!DNL Adobe Commerce Optimizer]は最新であり、Adobeとお客様の責任を明確に定義しています。
▢ **コンプライアンス：** プライバシーポリシー、Cookieの同意、GDPRまたはCCPAの要件が検証されます。

## 分析と監視 {#analytics-monitoring}

測定とベースラインの確認：

▢ **RUM:** Real User Monitoring （RUM）は、前後の比較に使用できるように実装されています。
▢ **Analytics:** Adobe Experience Platform データ収集が設定されています（該当する場合）。
▢ **Analytics:** マーテクタグが実稼動ホスト名に適用されていることを確認しました。
▢ **分析：** ベースライン分析が文書化されています。ローンチ後の変動（ページビュー、直帰率など）が予想されます。
▢ **イベント：** コンバージョンのトラッキングはエンドツーエンドで機能します（チェックアウトまたは確認のた→にカート→追加します）。

## テスト {#testing}

発売前後の品質確認。

▢ **機能：** コアフローがエンドツーエンドで動作します。参照→検索→フィルター→追加してカート→チェックアウト→アカウントの作成を行います。
▢ **機能的：**&#x200B;支払いゲートウェイは、実際のトランザクションとテスト トランザクションを受け入れます。
▢ **機能的：**&#x200B;注文処理、確認メール、注文追跡作業。
▢ **機能：**&#x200B;配送オプションと税額の計算が正確です。
▢ **機能：** クーポン、割引、ロイヤルティプログラムが期待どおりに動作します。
▢ **UAT:** ステージングと実稼動環境でのユーザー受け入れテストが完了しました。
▢ **パフォーマンス：**&#x200B;負荷と負荷のテストが完了し、Adobe CTAまたはCSEに結果が表示されます。
▢ **パフォーマンス：** ページの読み込み時間は、デスクトップとモバイルで3秒未満です。
▢ **パフォーマンス：** Lighthouse スコアは、主要ページの目標を満たします（PageSpeed Insightsなど）。
▢ **パフォーマンス：**&#x200B;画像、スクリプト、アセットが最適化されています。
▢ **互換性：** Chrome、Firefox、Safari、およびEdgeは期待どおりに動作します。
▢ **互換性：** レスポンシブレイアウトは、モバイル、タブレット、デスクトップで動作します。
▢ **互換性：** 3G、4G、およびWi-Fiでのパフォーマンスは許容されます。
▢ **アクセシビリティ：** アクセシビリティ監査が完了しました（WCAG、スクリーンリーダー、キーボードナビゲーション）。
▢ **機能：**&#x200B;起動後の404監視プランが有効です。
▢ **UAT:** ロールバックプランが存在し、起動の問題が発生した場合にテストに合格します。

## ローンチ日とローンチ後 {#launch-post-launch}

コミュニケーション、サポート、フォローアップタスクを確認する：

▢ **ローンチ調整：** Adobeにはローンチ日が確定しました。CTAには電子メールで通知されました。
▢ **サポート：** P1 ホットライン番号が記録されます：US （+1） 800-497-0335。次に、Commerceの場合は6を押します。
▢ **サポート：**&#x200B;お客様のチームは、P1 ホットラインを呼び出す&#x200B;**前**&#x200B;にサポートチケットを発行するようにトレーニングされています。
▢ **起動後：**&#x200B;実稼動ドメインのLighthouse スコアを確認します。
▢ **起動後：** インデックス作成とクロールエラーのGoogle Search Consoleを監視します。
▢ **起動後：** 404 レポートを監視し、トラフィックの多い従来のURLのリダイレクトを追加します。
▢ **開始後：**&#x200B;本番環境でのマーテクおよび分析データの確認。
▢ **ローンチ後：** CTA、CSE、またはAMに対して、SLAの高いモニタリングを有効にするように依頼します。
▢災害復旧プランが存在し、テストに合格しました。
▢ ボイラープレートと拡張パッケージを現在のバージョンに追跡してアップグレードするプロセスが準備されています。
