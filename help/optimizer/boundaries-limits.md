---
title: 制限と境界
description: キャパシティを計画し、パフォーマンスの問題を防ぐため、 [!DNL Adobe Commerce Optimizer] 制限と境界について理解します。
role: Admin, Developer
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよび [!DNL Adobe Commerce Optimizer]  プロジェクトにのみ適用されます（Adobeで管理されるSaaS インフラストラクチャ）。"
exl-id: 58d94da9-8d48-4513-8b6a-8e8c7c27a2a5
source-git-commit: ba445bf33ec9334c853245fce125af12cd244367
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 0%

---

# 制限と境界

[!DNL Adobe Commerce Optimizer]には、次の2種類の制限があります。

- **ライセンス制限** – 購入済みの容量に基づいて、追加のパッケージを購入することで拡張できます。
- **システムの境界** - システム リソースを保護し、すべてのユーザーに信頼性の高いパフォーマンスを確保するための制限を修正しました。

使用は、これらの制限内に収まる必要があります。 これらを超えると、待ち時間が増加し、スロットリングが要求される可能性があります。

## 追加能力を求める

ライセンス制限は、[&#x200B; ライセンス制限とシステム境界](#license-limits-and-system-boundaries) セクションに記載されているライセンスパッケージを購入するか、独自のユースケースに対するカスタムライセンスを交渉することで増やすことができます。 お客様の要件については、Adobeの担当者にお問い合わせください。

システムの境界について質問がある場合は、[Adobe サポート &#x200B;](https://experienceleague.adobe.com/home?lang=en#support)にお問い合わせください。

## パフォーマンスの問題を防止

制限内に収め、運用上の問題を回避するには、次のベストプラクティスに従ってください。

- **上限を確認する** – 新しいストアフロントやキャンペーンを開始する前に、[上限を把握する](#license-limits-and-system-boundaries)。
- **使用状況を追跡** – 組み込みの指標ダッシュボードまたはCDN ログを使用します。

## ライセンス制限とシステム境界

次の表は、機能領域ごとのライセンス制限とシステム境界をまとめたもので、必要に応じて容量を拡張するために追加のライセンスを追加する方法に関する情報が含まれています。

### 環境の制限

| **環境** | **説明** | **基本配分** | **拡張可能ですか？** |
| --- | --- | --- | --- |
| **サンドボックス環境** | 含まれているサンドボックス環境の数 | 2/インスタンス | はい<p>インスタンスごとに環境ライセンスを追加</p> |
| **実稼動環境** | 含まれる実稼動環境の数 | 1/インスタンス | ライセンス<p>インスタンスごとに環境ライセンスを追加</p> |

{style="table-layout:auto"}

### カタログ

| **機能** | **説明** | **基本配分** | **拡張可能ですか？** |
| --- | --- | --- | --- |
| 製品取り込み率 | 作成または更新された製品数 | 1分あたり1,000件の更新<p>1日あたり最大10万アップデート</p> | はい<p>1つのライセンスパックを追加：</p><ul><li>1分あたり5,000件の更新<br>1日あたり最大50,000件の更新</li> <li>1分あたり10,000件の更新<br>1日あたり最大1,000万件の更新</li></ul><p>データ取り込み最大容量は1日あたり100万件です。</p> |
| 製品ペイロードサイズ | APIを使用して製品情報を作成、更新、または取り込む際に許可されるデータの最大量 | 200 KB | いいえ |
| カタログのバリエーション | ストアフロントユーザーが利用できるカタログのビュー数を，<p>（*カタログ閲覧数×価格書籍数*）としてカウントされます</p> | 100のバリエーション | はい<p>100種類のカタログのバリエーションの追加ライセンスパック</p> |
| 単一のカタログソースの製品 | カタログでサポートされているSKU | 25万SKU | はい<p>100,000 SKU ライセンス パックを追加</p> |
| 製品ごとのバリエーション | 製品ごとに許可される製品バリエーションの数（サイズ、色の組み合わせ） | 10K | いいえ |
| カタログソース | カタログデータコンテキストの数（ロケール、PIMやERPなどのデータソースなど） | 50 | いいえ |

{style="table-layout:auto"}

### プライスブック

| **機能** | **説明** | **基本配分** | **拡張可能ですか？** |
| --- | --- | --- | --- |
| プライスブック | インスタンスごとに許可される価格台帳の数 | [&#x200B; カタログのバリエーション数](#catalog)に基づく | はい<br> カタログのバリエーションを増やす |
| 価格記録ごとの割引 | 1つの価格表に適用できる割引数 | 10 | いいえ |

{style="table-layout:auto"}

### AEM Assetsを活用した商品ビジュアル

| **機能** | **説明** | **基本配分** | **拡張可能ですか？** |
| --- | --- | --- | --- |
| 製品ビジュアルがユーザーを動かす | AI ツール、Adobe ExpressとFireflyの統合、Content Hubとの共有など、包括的なデジタルアセット管理機能を備えたライセンスユーザーは、主要なDAM タスクと高度なクラウドネイティブ機能を処理して、効率を最大化できます。 | 2 | はい<p>AEM Assets ライセンスへのアップグレード</p> |
| Product Visuals Collaborator ユーザー | AEM Commerceとの連携によるアセットへのアクセスと作業、Adobe ExpressとFireflyを使用したコンテンツの制作と編集、および有効な場合はContent Hub ポータルを介した承認済みアセットの活用。 | 2 | はい<p>AEM Assets ライセンスへのアップグレード</p> |
| 製品ビジュアルのストレージ | アセットに割り当てられたストレージ容量 | 1 TB ストレージ | いいえ |
| Dynamic Mediaの使用状況 | 以下を含むダイナミックメディア処理操作の許可<ul><li>画像配信</li><li>スマートイメージング</li><li>動画配信</li></ul><p>詳しくは、以下の「*Dynamic Mediaの使用状況の計算*」を参照してください。 | GMVによる<p>最小配分：5M オペレーション/月</p> | はい<ul><li>追加操作の購入ライセンス</li><li>AEM Assets ライセンスへのアップグレード</li></ul> |
| 動画配信 | ビデオ配信またはダウンロードの許可 | 300本、1分/ビデオ | はい<p>AEM Assets ライセンスへのアップグレード</p> |
| アセット生成 | 画像を作成するためのAdobe ExpressとAdobe Fireflyの生成AIへのアクセス | なし | 生成AI クレジットは別途購入する |

{style="table-layout:auto"}


>[!NOTE]
>
>**パワーユーザー**&#x200B;は、直接または[!DNL Adobe Commerce Optimizer]内でAdobe Expressにアクセスできます。 **共同作業者ユーザー**&#x200B;は、Adobe Express アプリケーションに直接アクセスできます。 利用方法は、[Adobe Express with Firefly Product Specific Licensing Terms](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/PSLT-AdobeExpressWFirefly-WW-2025v1.pdf)に準拠します。


>[!BEGINSHADEBOX &quot;Dynamic Mediaの使用状況の計算&quot;]

Dynamic Mediaの使用状況は、[!DNL Adobe Commerce Optimizer]内の製品ビジュアルコンポーネントに入ってくるAPI リクエストを追跡して、次のいずれかのアクションを容易にします。

- **画像配信では、次の項目が発生するたびに1つの動的メディア操作**&#x200B;が使用されます。
   - デジタルアセットの&#x200B;**基本的な画像変換** （サイズ変更、スケール、フォーマット変換、圧縮、切り抜き操作など）。
   - デジタルアセットまたはデジタルアセットのレンディション（ビデオ以外）の&#x200B;**静的画像配信またはダウンロード**
- **スマート画像配信では、エンドユーザーのデバイスとブラウザーに最適な画像レンディションを自動的に生成することで、単一のデジタルアセットの最適化された配信ごとに20のDynamic Media操作**&#x200B;を使用します。
- **ビデオ配信は、ビデオの1回の配信またはダウンロード、またはビデオの変換されたバリエーションに対して、20のDynamic Media操作**&#x200B;を使用します。

>[!ENDSHADEBOX]


### カタログビューとポリシー

| **機能** | **説明** | **基本配分** | **拡張可能ですか？** |
| --- | --- | --- | --- |
| カタログビュー | マスターカタログの設定可能なサブセットの数 | [&#x200B; カタログのバリエーション数](#catalog)に基づく | はい<br> カタログのバリエーションを増やす |
| カタログビューごとのポリシー | 許可されるデータフィルターの数 | 10 | いいえ |
| ポリシーの属性値 | フィルタリング用に設定できる製品特性の数 | 100 | いいえ |

{style="table-layout:auto"}

### Catalog storefront

カタログストアフロント機能のベース配分は、GMV層に基づいて決定されます。 The table indicates the minimum allocation for each capability.

| **機能** | **説明** | **基本配分** | **拡張可能ですか？** |
| --- | --- | --- | --- |
| Catalog retrieval rate | Number of times a catalog API is called per month by a system (storefront, transaction system, ERP, or other) to retrieve data from the catalog | Based on GMV tier<p>Minimum allocation: 10M/month</p> | はい<p>Add 1M requests per month license packs</p> |
| Content requests | Requests to Commerce Storefront for HTML page views or JSON API calls. Counted as 1 page view or 5 API calls. | Based on GMV tier<p>Minimum allocation: 2M/month</p> | はい<p>Add 1M per month license pack</p> |
| Storefront GenAI variations | Allowance for text-based content generation | Based on GMV tier<p>Minimum allocation: 1K variations/month</p> | はい<p>生成AI クレジットは別途購入する</p> |

{style="table-layout:auto"}

>[!NOTE]
>
>画像を生成するには、[!DNL Adobe Commerce Optimizer]と同じIMS組織にプロビジョニングされたAdobe Firefly ライセンスが必要です。


### 製品の発見

| **機能** | **説明** | **基本配分** | **拡張可能ですか？** |
| --- | --- | --- | --- |
| 検索リクエストあたりの商品 | 検索結果でページごとに返される製品の最大数 | 100 | いいえ |
| フィルター可能な属性 | 階層化されたナビゲーションとファセットで有効にできる製品特性（色、サイズ、ブランド、素材など）の数 | 200 | いいえ |
| 検索可能な属性 | 製品カタログ検索サービスで使用するように設定できる製品特性の数 | 200 | いいえ |
| ソート可能な属性 | 検索結果の値の順序を決定するために設定できる製品特性の数 | 50 | いいえ |
| 検索ページの深さ | ページ分割を通じてアクセスできる製品の最大数（例：100 ページ× 100 ページの製品/ページ） | 10K | いいえ |
| ファセット | 買い物客が検索結果を絞り込み、カテゴリーを閲覧するのに役立つ、フィルター可能な商品属性（ブランド、色、サイズ、価格など）の数 | 100<p>フィルター可能な属性である必要があります</p> | いいえ |
| ファセットごとのオプション | 買い物客がリストから選択できるフィルター可能な商品属性値の数（例：色の場合は「赤」、「青」、サイズの場合は「小」、「Medium」） | 100 | はい<p>サポートリクエストで増加する可能性があります</p> |

{style="table-layout:auto"}

### 推奨事項

商品レコメンデーションでは、次の機能を利用できます。 他のAdobe Commerce製品で利用できる一部の機能は、[!DNL Adobe Commerce Optimizer]ではサポートされていません。

| **機能** | **説明** | **基本配分** | **拡張可能ですか？** |
| --- | --- | --- | --- |
| アクティブなレコメンデーションユニット | ストアフロント上のライブレコメンデーションコンポーネントの数（「顧客も閲覧した」または「気に入ったかもしれない」など） | 50 | いいえ |
| カテゴリまたは属性のインクルード/除外 | レコメンデーションの対象となる特定のセットに商品をフィルタリング | サポートされていません | |

{style="table-layout:auto"}

### 拡張機能

| **機能** | **説明** | **基本配分** | **拡張可能ですか？** | **メモ** |
| --- | --- | --- | --- | --- |
| Adobe Developer App Builder | クラウドネイティブな拡張機能や統合機能の構築能力 | GMV層に基づく<p>最小配分：1 パック/年</p> | はい<p>追加パックを追加</p> | パックごとに定義される制限については、次を参照してください。<ul><li>パックごとに定義された制限の[App Builder製品説明](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html)。</li><li>*App Builder Runtime Guides*&#x200B;の[&#x200B; システム設定と制限](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings)。</li><li>[App Builder ストレージの要件](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/)</li></ul> |

{style="table-layout:auto"}

<!--
## How to size your solution

Ask your Adobe representative for a list of available packages to determine which most closely matches your project

To accurately size your [!DNL Adobe Commerce Optimizer] solution, follow these steps:

1. Review the available packages, and start with a package that most closely matches your requirements.
1. Review the capabilities and metrics to ensure they align with your business requirements.
1. Purchase add-on packages for any metrics where you require additional capacity.

This approach ensures your solution is accurately sized for your business needs.

### Example use cases

1. **Seasonal Catalog Expansion**

   * Need: +20K SKUs
   * Add-On: 2 × SKU Packs (10K each)

1. **High Traffic Surge**

   * Need: +3M content requests/month
   * Add-On: 3 × content request packs (1M each)

1. **Global Presence**

   * Need: Additional environments for testing
   * Add-On: +1 Production, +2 Sandbox instances

1. **GenAI or Media Needs**

   * Need: +10M dynamic media ops/month
   * Add-On: 10 × dynamic media packs (1M each) 
-->
