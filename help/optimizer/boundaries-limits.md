---
title: 制限と境界
description: 処理能力  [!DNL Adobe Commerce Optimizer]  計画し、パフォーマンスの問題を防ぐための制限と境界を理解します。
role: Admin, Developer
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
exl-id: 58d94da9-8d48-4513-8b6a-8e8c7c27a2a5
source-git-commit: f9ac230d448f071e6e8e6368b940f0c415abb02b
workflow-type: tm+mt
source-wordcount: '1350'
ht-degree: 0%

---

# 制限と境界

[!DNL Adobe Commerce Optimizer] には、次の 2 種類の制限があります。

- **ライセンス制限** – 購入した容量に基づきます。追加パッケージを購入することで拡張できます。
- **システムの境界** - システムリソースを保護し、すべてのユーザーに対して信頼性の高いパフォーマンスを確保する固定的な制限。

使用状況はこれらの制限内に収まる必要があります。 これを超えると、待ち時間が増加し、リクエストがスロットリングされる可能性があります。

## 追加容量のリクエスト

ライセンスの上限は、[ ライセンスの上限とシステムの範囲 ](#license-limits-and-system-boundaries) の節に記載されているライセンスパッケージを購入するか、個別のユースケースに合わせてカスタムライセンスを交渉することで増やすことができます。 要件については、Adobe アカウント担当者にお問い合わせください。

システムの境界については、[Adobe サポート ](https://experienceleague.adobe.com/home?lang=en#support) にお問い合わせください。

## パフォーマンスの問題を防ぐ

次のベストプラクティスに従って、制限を超えないようにし、運用上の問題を回避します。

- **上限をレビュー** – 新しいストアフロントやキャンペーンを開始する前に [ 容量上限 ](#license-limits-and-system-boundaries) を理解します。
- **使用状況の追跡** - ビルトインの指標ダッシュボードまたは CDN ログを使用します。

## ライセンスの制限とシステムの境界

次の表は、ライセンスの制限とシステムの境界を機能領域別にまとめたもので、必要に応じて容量を拡張するためにライセンスを追加する方法に関する情報も含まれています。

### 環境の制限

| **環境** | **説明** | **基本配分** | **拡張可能** |
| --- | --- | --- | --- |
| **サンドボックス環境** | 含まれるサンドボックス環境の数 | インスタンスごとに 2 つ | はい<p>インスタンスごとに環境ライセンスを追加します</p> |
| **実稼動環境** | 含まれる実稼動環境の数 | インスタンスごとに 1 つ | ライセンス<p>インスタンスごとに環境ライセンスを追加します</p> |

{style="table-layout:auto"}

### カタログ

| **機能** | **説明** | **基本配分** | **拡張可能** |
| --- | --- | --- | --- |
| 製品取り込み率 | 作成または更新された製品の数 | 1 分あたり 1,000 回の更新<p>1 日あたり最大 100,000 回の更新</p> | はい<p>ライセンスパックを 1 つ追加します。</p><ul><li>1 分あたり 5K の更新 <br>1 日あたり最大 500,000 の更新</li> <li>1 分あたり 10,000 件の更新 <br>1 日あたり最大 100 万件の更新</li></ul><p>データ取り込みの最大容量は、1 日に 100 万回の更新です。</p> |
| 製品のペイロードサイズ | API を使用して商品情報を作成、更新または取り込む際に許可されるデータの最大量 | 200 KB | 不可 |
| カタログバリエーション | ストアフロントユーザーが使用できるカタログのビュー数、<p>（*カタログビュー数×価格台帳の数*）としてカウントされます。</p> | 100 のバリエーション | はい<p>カタログバリエーション 100 個のライセンスパックを追加</p> |
| 単一のカタログソース内の製品 | カタログでサポートされる SKU | 25 万個の SKU | はい<p>10K SKU ライセンスパックを追加</p> |
| 製品ごとのバリアント | 製品ごとに許可される製品バリアントの数（サイズ、色の組み合わせ） | 10K | 不可 |
| カタログソース | カタログデータコンテキストの数（ロケール、PIM や ERP などのデータソースなど） | 50 | 不可 |

{style="table-layout:auto"}

### 価格帳簿

| **機能** | **説明** | **基本配分** | **拡張可能** |
| --- | --- | --- | --- |
| 価格帳簿 | インスタンスごとに許可される価格帳簿の数 | [ カタログバリエーション ](#catalog) の数に基づく | はい <br> カタログのバリエーションを増やす |
| 価格レコードあたりの割引 | 1 つの価格台帳内の製品価格に適用できる割引の数 | 10 | 不可 |

{style="table-layout:auto"}

### AEM Assetsを活用した製品ビジュアル

| **機能** | **説明** | **基本配分** | **拡張可能** |
| --- | --- | --- | --- |
| 製品ビジュアルのパワーユーザー | AI ツール、Adobe Express/Firefly統合、Content Hub共有などの完全なデジタルアセット管理機能を持ち、コア DAM タスクを処理し、最適な効率を実現する高度なクラウドネイティブ機能を備えたライセンス取得済みユーザー。 | 2 | はい<p>AEM Assets ライセンスへのアップグレード</p> |
| 製品ビジュアル共同作業者ユーザー | AEM Commerce統合を通じたアセットへのアクセスと操作、Adobe ExpressとFireflyを使用したコンテンツの作成と編集、有効化されている場合はContent Hub ポータルを通じた承認済みアセットの活用が可能です。 | 2 | はい<p>AEM Assets ライセンスへのアップグレード</p> |
| 製品ビジュアルストレージ | アセットに割り当てられたストレージスペース | 1 TB ストレージ | 不可 |
| Dynamic Media の使用状況 | 次の項目を含む Dynamic Media 処理操作の手当<ul><li>画像配信</li><li>スマートイメージング</li><li>ビデオ配信</li></ul><p>詳しくは、以下の *Dynamic Media の使用状況の計算* を参照してください。 | GMV ベース<p>最小割り当て：1 か月あたり 500 万回</p> | はい<ul><li>追加操作用の購入ライセンス</li><li>AEM Assets ライセンスへのアップグレード</li></ul> |
| ビデオ配信 | ビデオ配信またはダウンロードの許可 | 300 ビデオ、ビデオあたり 1 分 | はい<p>AEM Assets ライセンスへのアップグレード</p> |
| アセットの生成 | 画像を作成するためのAdobe ExpressおよびAdobe Firefly生成 AI へのアクセス | なし | 生成 AI クレジットを別途購入 |

{style="table-layout:auto"}


>[!NOTE]
>
>**パワーユーザー** は、Adobe Expressに直接アクセスすることも、Adobe Commerce Optimizer内でアクセスすることもできます。 **共同作業者ユーザー** は、Adobe Expressアプリケーションに直接アクセスできます。 使用方法は、[Adobe ExpressとFirefly製品固有のライセンス条件 ](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/PSLT-AdobeExpressWFirefly-WW-2025v1.pdf) に準拠します。


>[!BEGINSHADEBOX  「Dynamic Media の使用状況の計算」 ]

Dynamic Media 使用状況は、Adobe Commerce Optimizer内の Product Visuals コンポーネントに入る API リクエストを追跡し、次のいずれかのアクションを容易にします。

- **画像配信は、以下が発生するたびに** Dynamic Media 操作を 1 つ消費します。
   - デジタルアセットの **基本的な画像変換** サイズ変更、拡大縮小、形式変換、圧縮、切り抜きの操作など。
   - 当該デジタルアセット又はデジタルアセットレンディション **映像でないもの）の** 静的画像配信又はダウンロード）
- **スマート画像配信は、エンドユーザーのデバイスやブラウザーに最適な画像レンディションを自動的に生成することで、単一のデジタルアセットの配信が最適化されるたびに、20 回の Dynamic Media 操作を消費します**。
- **ビデオ配信は、ビデオの単一の配信やダウンロード、またはビデオの変換済みバリアントに対して、20 個の Dynamic Media 操作を消費します**。

>[!ENDSHADEBOX]


### カタログのビューとポリシー

| **機能** | **説明** | **基本配分** | **拡張可能** |
| --- | --- | --- | --- |
| カタログビュー | マスターカタログの設定可能なサブセットの数 | [ カタログバリエーション ](#catalog) の数に基づく | はい <br> カタログのバリエーションを増やす |
| カタログビューごとのポリシー | 許可されるデータフィルターの数 | 10 | 不可 |
| ポリシーの属性値 | フィルタリング用に設定できる製品特性の数 | 100 | 不可 |

{style="table-layout:auto"}

### カタログ ストアフロント

カタログストアフロント機能のベース割り当ては、GMV 層に基づいて決定されます。 表は、各機能の最小割り当てを示します。

| **機能** | **説明** | **基本配分** | **拡張可能** |
| --- | --- | --- | --- |
| カタログ取得率 | カタログ API がシステム （ストアフロント、トランザクションシステム、ERP など）によって 1 か月あたりに呼び出され、カタログからデータが取得された回数 | GMV 層に基づく<p>最小配分：10M/月</p> | はい<p>1 か月あたり 100 万件のリクエストを追加</p> |
| コンテンツリクエスト | HTML ページビューまたは JSON API 呼び出し用のリクエストがCommerce ストアフロントに送信されます。 1 回のページビューまたは 5 回の API 呼び出しとしてカウントされます。 | GMV 層に基づく<p>最小配分：200 万/月</p> | はい<p>1 か月あたり 100 万個のライセンスパックを追加</p> |
| Storefront GenAI のバリエーション | テキストベースのコンテンツ生成の許可 | GMV 層に基づく<p>最小配分：1 か月あたり 1,000 個のバリエーション</p> | はい<p>生成 AI クレジットを別途購入</p> |

{style="table-layout:auto"}

>[!NOTE]
>
>画像生成には、Adobe Commerce Optimizerと同じ IMS 組織にプロビジョニングされたAdobe Firefly ライセンスが必要です。


### 製品の検出

| **機能** | **説明** | **基本配分** | **拡張可能** |
| --- | --- | --- | --- |
| 検索リクエストあたりの製品数 | 検索結果でページごとに返される製品の最大数 | 100 | 不可 |
| フィルタリング可能な属性 | 階層化されたナビゲーションとファセットに対して有効にできる製品特性（色、サイズ、ブランド、マテリアルなど）の数 | 200 | 不可 |
| 検索可能な属性 | 製品カタログ検索サービスで使用するように設定できる製品特性の数です | 200 | 不可 |
| ソート可能な属性 | 検索結果値の順序を決定するために設定できる製品特性の数 | 50 | 不可 |
| ページネーションの深さを検索 | ページネーションによってアクセス可能な製品の最大数（例：ページ 100 × 100 個の製品/ページ） | 10K | 不可 |
| ファセット | 買い物客が検索結果を絞り込んでカテゴリを参照できるように設定できる、フィルタリング可能な製品属性（ブランド、色、サイズ、価格など）の数 | 100<p>フィルタリング可能な属性である必要があります</p> | 不可 |
| ファセットごとのオプション | 買い物客がリストから選択できる、フィルタリング可能な製品属性値の数（色は「赤」、「青」、サイズは「小」、「Medium」など）。 | 100 | はい<p>サポートリクエストによって増加する可能性があります</p> |

{style="table-layout:auto"}

### 推奨事項

製品レコメンデーションには、次の機能を使用できます。 他のAdobe Commerce製品で利用できる機能の一部は、[!DNL Adobe Commerce Optimizer] ではサポートされていません。

| **機能** | **説明** | **基本配分** | **拡張可能** |
| --- | --- | --- | --- |
| アクティブなレコメンデーションユニット | ストアフロントにあるライブのレコメンデーションコンポーネントの数（「顧客も閲覧」や「お客様も気に入る可能性あり」） | 50 | 不可 |
| カテゴリまたは属性の包含/除外 | レコメンデーションの対象となる特定のセットに製品をフィルタリングする | サポートなし | |
| お勧めをプレビュー | 公開前に、ストアフロントでのレコメンデーションの表示方法をプレビューします | サポートなし | |

{style="table-layout:auto"}

### 拡張性

| **機能** | **説明** | **基本配分** | **拡張可能** | **備考** |
| --- | --- | --- | --- | --- |
| Adobe Developer App Builder | クラウドネイティブな拡張機能と統合を構築する機能 | GMV 層に基づく<p>最小割り当て：1 パック/年</p> | はい<p>追加パックを追加する</p> | パックごとに定義される制限については、以下を参照してください。<ul><li>パックごとに定義された制限に対する [0}App Builder製品の説明 }。](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html)</li><li>[2}App Builder Runtime Guides} の ](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings) システム設定と制限事項 *を参照してください。*</li><li>[App Builderのストレージ要件 ](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/)</li></ul> |

{style="table-layout:auto"}

<!--## How to size your solution

Ask your Adobe representative for a list of available packages to determine which most closely matches your project

To accurately size your Adobe Commerce Optimizer solution, follow these steps:

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
   * Add-On: 10 × dynamic media packs (1M each) -->
