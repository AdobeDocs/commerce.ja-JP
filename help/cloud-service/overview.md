---
title: '[!DNL Adobe Commerce as a Cloud Service] の概要'
description: ' [!DNL Adobe Commerce as a Cloud Service] の主な機能とメリットについて説明します。'
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Architect, Developer, User
exl-id: 1b7e2731-4a10-4c2b-9bfc-8945729ed523
source-git-commit: 25a0d658776ea95fcae07f6390abeeb559642613
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 0%

---

# [!DNL Adobe Commerce as a Cloud Service] の概要

{{accs-early-access}}

[!DNL Adobe Commerce as a Cloud Service] は、企業がデジタルオペレーションを提供し、迅速に拡大し、イノベーションを促進できるようにすることで、柔軟性、拡張性、効率性を提供します。 Adobeのクラウドネイティブインフラストラクチャは、トラフィック、注文、カタログ管理に対するピーク時の需要に合わせてリソースを自動的に調整します。

次の図は、[!DNL Adobe Commerce as a Cloud Service] を強化する製品を示しています。

![[!DNL Adobe Commerce as a Cloud Service] 製品スタック ](./assets/product-stack.svg){align="center" zoomable="yes"}

>[!BEGINSHADEBOX]

![ 情報 ](assets/Smock_InfoOutline_18_N.svg) [!DNL Adobe Commerce as a Cloud Service] アーリーアクセス プログラムに参加するには、[ このフォーム ](https://forms.office.com/pages/responsepage.aspx?id=Wht7-jR7h0OUrtLBeN7O4WOxhjY2doZPikS2hIbfmL5URFZXTE5TUk9PMUw0OFdOWTBNNlI3UTlNMS4u&amp;route=shorturl) に入力してください。

>[!ENDSHADEBOX]

## アーキテクチャ

[!DNL Adobe Commerce as a Cloud Service] アーキテクチャの概要については、次のビデオを参照してください。 アーキテクチャを示す図をビデオの下に示します。

>[!VIDEO](https://video.tv.adobe.com/v/3443232?learn=on)

次の図は、[!DNL Adobe Commerce as a Cloud Service] とすべてのAdobe Experience Cloud ソリューション間のデータフローを示しています。

![[!DNL Adobe Commerce as a Cloud Service] アーキテクチャ図 ](./assets/data-flow.svg){zoomable="yes"}

## Commerce ストアフロント

Edge Delivery Servicesを活用したAdobeの [Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront) を使用すると、シンプルなドキュメントベースのオーサリングや Storefront ビルダーを使用したビジュアル編集で、数分で豊富なエクスペリエンスを作成できます。

Commerce ストアフロントは、GraphQL API レイヤーを通じてすべてのマーチャンダイジングサービスとデータを提供する、切り離されたアーキテクチャを備えた、完全にヘッドレスです。 このアーキテクチャにより、チームはCommerce財団とは独立してフロントエンドを開発でき、新しいテクノロジーを使用して新しいタッチポイントを構築およびテストする俊敏性が提供されます。

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service] は、Luma ストアフロントをサポートしていません。 Adobe Commerce on Cloud またはオンプレミスから移行する場合は、[ 既存のストアフロント ](https://experienceleague.adobe.com/developer/commerce/storefront/discovery/#existing-storefronts) を参照して、移行のガイダンスを確認してください。

## マーチャンダイジングサービスと支払いサービス

Adobeは、主要なビジネス目標をサポートするのに役立つ、インテリジェントで構成可能なマーチャンダイジングサービスの豊富なセットを提供します。 また、これらのサービスは、パフォーマンスを大規模に最適化するために重要な API も提供します。

- [ ライブ検索 ](../live-search/overview.md) – この AI を活用した検索ツールにより、買い物客によりスマートで迅速かつ適切な結果を提供します。
- [ 製品レコメンデーション ](../product-recommendations/overview.md) – 買い物客の行動、人気のトレンド、製品の類似性などに基づいて、AI を活用したレコメンデーションを追加します。
- [ チャネルとポリシーを活用したマーチャンダイジングサービス ](../merchandising-services/overview.md) – 柔軟なデータモデリングを使用して、大きくて複雑な製品カタログを管理し、ビジネス構造と市場戦略に沿った、高パフォーマンスで柔軟なコマースカタログを提供します。 [Commerce Optimizer](../optimizer/overview.md) との併用により、カタログのパフォーマンスを最適化し、コンバージョン率を向上させることができます。
- [ 支払いサービス ](../payment-services/overview.md)：利息なしの分割払い、支払い処理、オーダー、請求書の単一ビューなど、さまざまな支払い方法を提供することにより、顧客満足度を向上させます。

## 製品ビジュアル

Adobe Experience Managerと統合してリッチメディアコンテンツを管理する堅牢なデジタルアセット管理（DAM）システムを使用して、アセット管理をシンプル化します。 または、ネイティブのミニ DAM は、デジタルアセットを保存および管理するための基本的なアセット管理ツールを提供します。

詳しくは、[ アセット管理 ](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/aem-asset-management/aem-assets-integration) を参照してください。

## 開発者プラットフォーム

Adobeは、Commerceの基盤機能を拡張するアプリケーションを構築し、サードパーティのシステム（CRM、ERPS、PIMS など）と統合するための包括的な拡張ポイントおよびツールを開発者に提供します。 これらのツールは、次の方法でプラットフォームの総所有コストを削減します。

- **拡張性**：アプリケーションをコア・ソフトウェアとは別に拡張できるため、効率性が向上し、アップグレードが容易になります。
- **分離** – 分離された環境とは、開発者がコアリリースに頼らずに自分の裁量で拡張機能をアップグレードまたは変更できることを意味します。
- **技術的独立性** – 開発者は、ニーズに合ったテクノロジースタックとコーディング言語を選択できます。

>[!TIP]
>
>ベンダーが構築したアプリも、[Adobe Exchange](https://exchange.adobe.com/) にインストールできます。

Adobeには、統合とカスタマイズを構築するための次の開発ツールが用意されています。

- [**Adobe Developer App Builderの API メッシュ**](https://developer.adobe.com/graphql-mesh-gateway/) – 複数の API、GraphQL、REST、その他のソースを調整し、1 つのクエリ可能なGraphQL エンドポイントに組み合わせます。
- [**App Builder**](https://developer.adobe.com/app-builder/docs/overview/) - Commerce機能を拡張し、サードパーティのソリューションと統合する、セキュリティで保護されたスケーラブルな web アプリケーションを構築およびデプロイします。
- [**イベント**](https://developer.adobe.com/commerce/extensibility/events/) - カスタムイベントトリガーを使用して、その他の拡張可能な開発ツールとやり取りします。
- [**Webhook**](https://developer.adobe.com/commerce/extensibility/webhooks/) - Webhook を使用すると、Commerceとサードパーティシステム間のインタラクションを自動的にトリガーできます。
- [**管理 UI SDK**](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/) - マーチャント向けの新しいページと機能で、Commerce管理をカスタマイズおよび強化します。
- [**統合スターターキット**](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) – 参照統合、オンボーディングスクリプト、標準化されたアーキテクチャにより、バックオフィス統合を促進します。

## Commerce財団

Commerce Foundation は、クラウドネイティブな環境でCommerce アプリケーションを管理するための安全な自動ホスティングプラットフォームおよびセルフサービス機能を提供します。

主な機能は次のとおりです。

- オンボーディングの簡素化
- シームレスなアップグレード
- サードパーティの統合

### オンボーディングの簡素化

[!UICONTROL Commerce Cloud Manager] セルフサービスプロビジョニングポータルを使用すると、サンドボックスおよび実稼動インスタンスを数分で起動できます。 マーチャンダイジングサービス、ヘッドレス Commerce インスタンス、App Builderなど、必要なものはすべて自動的に設定され、インスタンスと統合されます。

Commerce インスタンスを作成および管理する方法については、[ はじめに ](getting-started.md) を参照してください。

### シームレスなアップグレード

手動のアップグレードを行わなくても、最新の機能や機能強化にアクセスできます。 新機能やアップデートが継続的に提供されるので、手動でのパッチ適用が不要になり、TCO （総所有コスト）を抑えながら最新の機能に常にアクセスできるようになります。

Cloud 上のAdobe Commerceの一般的なアップグレードプロセスは、バックアップの作成、インスタンスのクローン作成、互換性ツールの実行、コードの競合の修正を含んでいました。 それは [!DNL Adobe Commerce as a Cloud Service] にはもう必要ありません。 新機能とセキュリティアップデートがリリースされると、Adobeからアプリ内通知が送信されます。 更新が実稼動環境に自動的に適用される前に、サンドボックスインスタンスで新しい機能を評価するための期間は 30 日間です。

>[!NOTE]
>
>Adobeでは、すべての更新に対して後方互換性が保証されます。 つまり、更新が適用されても、[API ファースト拡張機能 ](https://developer.adobe.com/commerce/extensibility/) モデルに準拠する既存の機能やカスタマイズが損なわれることはありません。

### サードパーティの統合

開発者は、包括的な [GraphQLおよび REST API](https://developer.adobe.com/commerce/services/cloud/guides/) を使用して、Commerce Foundation をサードパーティシステムと統合し、Commerceの機能を拡張できます。

## Experience Cloudの統合

[!DNL Adobe Commerce as a Cloud Service] は、すべてのExperience Cloud ソリューションと統合して、[ パーソナライズされたコマースエクスペリエンスを大規模に ](https://experienceleague.adobe.com/en/docs/commerce-admin/customers/customers-menu/personalize-scale#customers-menu) 提供します。

[Data Connection](../data-connection/overview.md) を使用すると、買い物客の購買行動に関するインサイトを解き放ち、他のAdobe Digital Experience 製品と共に、すべてのチャネルにわたってパーソナライズされたショッピングエクスペリエンスを作成できます。

## 利点

以下のセクションでは、[!DNL Adobe Commerce as a Cloud Service] がビジネスおよび IT リーダーに提供するメリットについて説明します。

### ビジネスリーダー

- **収益の増加**:SEO を向上させる高性能なストアフロントでオーガニックトラフィックを推進します。 リッチデータを使用してコンバージョンを促進する、パーソナライズされたエクスペリエンスを作成します。
- **スケールオペレーション**：自動スケールサービスは、99.9% の可用性で、ビジネスのピーク時の需要を満たします。 複数のブランドと地域をロールアウトし、1 つのインスタンスから B2B と B2C をサポートします。 柔軟なデータモデリングにより、大規模で複雑な製品カタログをサポートします。
- **マーチャンダイザーの生産性の向上**:AI を活用したマーチャンダイジングサービスを使用して、コンバージョンを向上させます。 ストアフロントで直接、ネイティブに実験します。 シンプルなドキュメントベースのオーサリングまたはビジュアルエディターにより、ストアフロントのエクスペリエンスを管理して、豊富なエクスペリエンスを数分で作成できます。
- **総所有コスト（TCO）の削減とイノベーションの促進**：常に最新のサービスにより、新機能にすぐにアクセスできます。 Marketplace からアプリを簡単にインストールして、新機能をアクティブ化します。 面倒なメンテナンスからリソースを解放し、新しい機能の構築に集中します。

### 情報技術（IT）分野のリーダー

- **高速プロビジョニング**：数分でセルフサービスプロビジョニングを開始できます。 すべてのサービスは、シームレスに連携して迅速に開始できるように事前設定されています。 必要に応じて、開発者実験用のサンドボックスをプロビジョニングします。
- **低い所有コスト**：常に最新のサービスを使用して、アップグレードを行う必要がありません。 セキュリティを維持し、自動的に適用される最新のセキュリティパッチに準拠します。 最も要求の厳しいワークロードに合わせて自動的に拡張できます。
- **高パフォーマンスのストアフロント**：シンプルなドキュメントベースのオーサリングまたはビジュアルエディターを使用して、豊富なエクスペリエンスを数分で作成できます。 AI を活用したマーチャンダイジングサービスを使用して、コンバージョンを向上させます。 ストアフロントに組み込まれたネイティブ実験。
- **迅速なイノベーション**：面倒なメンテナンスからリソースを解放し、ビジネス価値をもたらす新しい機能の構築に集中します。 包括的な拡張機能および標準ベースのテクノロジー（JavaScript、HTML、CSS、ローコードツール）を使用して、差別化されたエクスペリエンスを構築します。 クリックでサードパーティアプリをインストールして、コマースプラットフォームに新しい機能を追加します。

## 新機能ソリューション

[ 管理 UI](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/guide-overview) は、バックエンドストアの運用、在庫、価格設定、プロモーション、顧客とのやり取りを管理する機能にアクセスするためのプライマリインターフェイスです。 ただし、[!DNL Adobe Commerce as a Cloud Service] では、Adobe Commerce on Cloud やオンプレミスプロジェクトで利用できる既知の機能の一部に代わる独自のソリューションを提供しています。 次の表に、[!DNL Adobe Commerce as a Cloud Service] で使用可能な機能と代替ソリューションを示します。

| 機能 | 解決策 | 対象 | 詳細 |
|---------|----------|--------------|--------|
| [ デジタルアセット管理 ](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management) | [ 製品ビジュアル ](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/aem-asset-management/aem-assets-integration) ミニ DAM | 利用可能 | Adobe Experience Managerと統合してリッチメディアコンテンツを管理する、堅牢なデジタルアセット管理（DAM）システム。 または、ミニ DAM には、デジタルアセットを保存および管理するための基本的なアセット管理ツールが用意されています。 |
| [ コンテンツ管理システム（CMS） ](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/guide-overview) | [Commerce ストアフロント ](https://www.aem.live/) | 利用可能 | 基本のCMSにより、ドキュメントベースのオーサリングを使用して、ドキュメントと web サイトのコンテンツを簡単に作成および管理できます。 または、複数のプラットフォーム間でより高度なコンテンツ管理とカスタマイズを可能にするユニバーサルエディター。 |
| [ コンテンツのステージング ](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/staging/content-staging) | [ カタログサービス ](../catalog-service/overview.md) | ロードマップ | Adobe Experience Platformと連携し、大きなカタログを管理できるカタログ管理ツール。 |
| [ ページビルダー ](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/guide-overview) | [Commerce ストアフロント ](https://www.aem.live/) | 利用可能 | 基本のCMSにより、ドキュメントベースのオーサリングを使用して、ドキュメントと web サイトのコンテンツを簡単に作成および管理できます。 または、複数のプラットフォーム間でより高度なコンテンツ管理とカスタマイズを可能にするユニバーサルエディター。 |
| [ 支給 ](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/payments/payments) | [Adobe Commerce決済等代行業 ](../payment-services/overview.md) | 利用可能 | 安全かつ効率的な取引を容易にする統合決済サービス。 |
| [ 共有カタログ ](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared) | [ 価格インデックスサービス ](../price-index/price-indexing.md) | ロードマップ | 価格データを分析し、様々な要因に基づいて製品の最適な価格戦略を提案します。 |
| [URL の書き換え ](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite) | [Commerce ストアフロント ](https://www.aem.live/) | 利用可能 | 基本のCMSにより、ドキュメントベースのオーサリングを使用して、ドキュメントと web サイトのコンテンツを簡単に作成および管理できます。 または、複数のプラットフォーム間でより高度なコンテンツ管理とカスタマイズを可能にするユニバーサルエディター。 |
| [ ビジュアルマーチャンダイザー ](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser) | [ カタログサービス ](../catalog-service/overview.md) | ロードマップ | Adobe Experience Platformと連携し、大きなカタログを管理できるカタログ管理ツール。 |
