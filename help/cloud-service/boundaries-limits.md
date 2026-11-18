---
title: Adobe Commerce as a Cloud Serviceの制限と境界
description: Adobe Commerce as a Cloud Serviceのライセンス制限とシステムの制限について説明します。 キャパシティを計画し、使用状況を追跡し、制限を超えた場合の待ち時間とスロットリングを回避します。
role: Admin, Developer
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよび[!DNL Adobe Commerce as a Cloud Service]件のプロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"
nudge: true
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: a13aaee57732f27b51a2d2acdd0ca3de364ee6ab
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 1%
---
# 制限と境界

[!DNL Adobe Commerce as a Cloud Service]は、プロジェクトで使用できるキャパシティを定義する&#x200B;**ライセンス制限**&#x200B;および&#x200B;**システム境界**&#x200B;を適用します。

- **ライセンス制限**&#x200B;は、購入済みの容量に基づいており、追加のパッケージを購入することで拡張できます。
- **システムの境界**&#x200B;は、システム リソースを保護し、すべてのユーザーに信頼性の高いパフォーマンスを確保するための固定の制限です。

>[!IMPORTANT]
>
> 使用は、これらの制限内に収まる必要があります。 これらを超えると、待ち時間が増加し、スロットリングが要求される可能性があります。

## 追加能力を求める

[&#x200B; ライセンス制限とシステム境界](#license-limits-and-system-boundaries)に記載されているライセンスパッケージを購入するか、独自のユースケースに対するカスタムライセンスを交渉することで、ライセンス制限を増やすことができます。 お客様の要件については、Adobeの担当者にお問い合わせください。

システムの境界について質問がある場合は、[Adobe サポート &#x200B;](https://experienceleague.adobe.com/home?lang=en#support)にお問い合わせください。

## パフォーマンスの問題を防止

制限内に収め、運用上の問題を回避するには、次のベストプラクティスに従ってください。

- **上限を確認する** – 新しいストアフロントやキャンペーンを開始する前に、[上限を把握する](#license-limits-and-system-boundaries)。
- **使用状況を追跡** – 組み込みの指標ダッシュボードまたはCDN ログを使用します。

## ライセンス制限とシステム境界

次の表は、機能領域ごとのライセンス制限とシステム境界をまとめたもので、必要に応じて追加ライセンスを使用して容量を拡張する方法に関する情報が含まれています。

### 環境の制限

| **環境** | **説明** | **基本配分** | **拡張可能ですか？** |
| --- | --- | --- | --- |
| **サンドボックス環境** | 含まれているサンドボックス環境の数 | 2/インスタンス | はい<p>インスタンスごとに環境ライセンスを追加</p> |
| **実稼動環境** | 含まれる実稼動環境の数 | 1/インスタンス | はい<p>インスタンスごとに環境ライセンスを追加</p> |

{style="table-layout:auto"}

### カタログ

| **機能** | **説明** | **基本配分** | **拡張可能ですか？** |
| --- | --- | --- | --- |
| 製品取り込み率 | 作成または更新された製品数 | 1分あたり1,000件の更新<p>1日あたり最大10万アップデート</p> | はい<p>1つのライセンスパックを追加：</p><ul><li>1分あたり5,000件の更新<br>1日あたり最大50,000件の更新</li><li>1分あたり10,000件の更新<br>1日あたり最大1,000万件の更新</li></ul><p>データ取り込み最大容量は1日あたり100万件です。</p> |
| 製品ペイロードサイズ | APIを使用して製品情報を作成、更新、または取り込む際に許可されるデータの最大量 | 200 KB | いいえ |
| カテゴリ | 製品がグループ化できるカテゴリの数 | 6,000 | いいえ |
| 製品数 | カタログでサポートされているSKUの数 | 25万SKU | はい<p>100,000 SKU ライセンス パックを追加</p> |
| 製品ごとのバリエーション | 製品ごとに許可される製品バリエーションの数（サイズ、色の組み合わせ） | 10K | いいえ |
| ストアビュー | ストアビューコンテキストの数（ロケールなど） | 50 | いいえ |
| 検索に表示される製品アップデートのSLA | ストアフロント検索に商品の作成/更新が表示される時間 | 10～15分 | いいえ |

{style="table-layout:auto"}

### チェックアウト

| **機能** | **説明** | **基本配分** | **拡張可能ですか？** |
| --- | --- | --- | --- |
| 買い物かご内の商品 | 買い物かごごとに許可される商品数 | 650 | いいえ |
| アカウントごとの顧客アドレス | アカウントごとに許可される顧客アドレスの数 | 2,000 | いいえ |
| カートの価格ルール | 一連の条件に基づいて、ショッピングカート内の商品に割引を適用するカート価格ルールの数 | 100,000 | いいえ |
| クーポン | カート価格ルールで使用されるクーポンコードの数 | 1,000,000 | いいえ |

{style="table-layout:auto"}

<!--
# Price books

# | **Capability** | **Description** | **Base allocation** | **Expandable?** |
# | --- | --- | --- | --- |
# | Price books | The number of price books allowed per instance | Based on the number of [Catalog variations](#catalog) | Yes<br>Increase catalog variations |
# | Discounts per price record | The number of discounts that can be applied to a product price within a single price book | 10 | No |

{style="table-layout:auto"}
-->

### [!DNL Product Visuals]個の制限

| **機能** | **説明** | **基本配分** | **拡張可能ですか？** |
| --- | --- | --- | --- |
| 製品ビジュアルがユーザーを動かす | AI ツール、[!DNL Adobe Express]/[!DNL Firefly]との統合、Content Hubの共有など、包括的なデジタルアセット管理機能を備えたライセンスユーザーが、主要なDAM タスクと高度なクラウドネイティブ機能を処理して、効率を最適化しています。 | 2 | はい<p>[!DNL AEM Assets] ライセンスへのアップグレード</p> |
| Product Visuals Collaborator ユーザー | AEM Commerceとの連携によるアセットへのアクセスと操作、[!DNL Adobe Express]と[!DNL Firefly]を使用したコンテンツの制作と編集、および有効な場合はContent Hub ポータルを介した承認済みアセットの活用。 | 2 | はい<p>[!DNL AEM Assets] ライセンスへのアップグレード</p> |
| 製品ビジュアルのストレージ | アセットに割り当てられたストレージ容量 | 1 TB ストレージ | いいえ |
| Dynamic Mediaの使用状況 | 以下を含むダイナミックメディア処理操作の許可<ul><li>画像配信</li><li>スマートイメージング</li><li>動画配信</li></ul><p>詳しくは、以下の「*Dynamic Mediaの使用状況の計算*」を参照してください。 | GMV （グロス・マーチャンダイジング・バリュー）ベース<p>最小配分：5M オペレーション/月</p> | はい<ul><li>追加操作の購入ライセンス</li><li>[!DNL AEM Assets] ライセンスへのアップグレード</li></ul> |
| 動画配信 | ビデオ配信またはダウンロードの許可 | 300本、1分/ビデオ | はい<p>[!DNL AEM Assets] ライセンスへのアップグレード</p> |
| アセット生成 | 画像を作成するための[!DNL Adobe Express]および[!DNL Adobe Firefly]生成AIへのアクセス | なし | 生成AI クレジットは別途購入する |

{style="table-layout:auto"}

>[!NOTE]
>
>**パワーユーザー**&#x200B;は[!DNL Adobe Express]に直接または[!DNL Adobe Commerce as a Cloud Service]内でアクセスできます。
>
>**共同作業者ユーザー**&#x200B;は[!DNL Adobe Express] アプリケーションに直接アクセスできます。 利用方法は、[Adobe Express with Firefly Product Specific Licensing Terms](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/PSLT-AdobeExpressWFirefly-WW-2025v1.pdf)に準拠します。

>[!BEGINSHADEBOX &quot;Dynamic Mediaの使用状況の計算&quot;]

Dynamic Mediaの使用状況は、[!DNL Adobe Commerce as a Cloud Service]内の製品ビジュアルコンポーネントに入ってくるAPI リクエストを追跡して、次のいずれかのアクションを容易にします。

- **画像配信では、次の項目が発生するたびに1つの動的メディア操作**&#x200B;が使用されます。
  - デジタルアセットの&#x200B;**基本的な画像変換** （サイズ変更、スケール、フォーマット変換、圧縮、切り抜き操作など）。
  - デジタルアセットまたはデジタルアセットのレンディション（ビデオ以外）の&#x200B;**静的な画像配信またはダウンロード**。
- **スマート画像配信では、エンドユーザーのデバイスとブラウザーに最適な画像レンディションを自動的に生成することで、単一のデジタルアセットの最適化された配信ごとに20のDynamic Media操作**&#x200B;を使用します。
- **ビデオ配信は、ビデオの1回の配信またはダウンロード、またはビデオの変換されたバリエーションに対して、20のDynamic Media操作**&#x200B;を使用します。

>[!ENDSHADEBOX]

>[!NOTE]
>
>上記の制限は、容量と使用割り当てをカバーします。 製品ビジュアル機能の概要と機能的な制約については、[製品ビジュアルとAEM Assets](../optimizer/setup/product-visuals.md)を参照してください。

<!--
### Catalog views and policies

| **Capability** | **Description** | **Base allocation** | **Expandable?** |
| --- | --- | --- | --- |
| Catalog views | Number of configurable subsets of your master catalog | Based on the number of [Catalog variations](#catalog) | Yes<br>Increase catalog variations |
| Policies per catalog view | Number of data filters allowed | 10 | No |
| Attribute values in a policy | Number of product characteristics that can be configured for filtering | 100 | No |
| [Restricted access key assignment](setup/private-catalog-view.md) | Number of restricted access keys that can be assigned to a single catalog view | 3 | No |
| RSA key size (restricted access keys) | Minimum and maximum key strength accepted for a restricted access key | 2048-bit minimum, 8192-bit maximum | No |
| Restricted access keys | Key revocation propagation delay | Up to 5 minutes, due to caching. Tokens signed by a removed key are denied once the delay elapses. | Not applicable |

{style="table-layout:auto"}
-->

### カタログストアフロント

カタログストアフロント能力の基本配分は、GMV （商品総価値）層に基づいて決定されます。 この表は、各機能の最小割り当てを示しています。

| **機能** | **説明** | **基本配分** | **拡張可能ですか？** |
| --- | --- | --- | --- |
| カタログ検索率 | カタログ APIが、カタログからデータを取得するためにシステム（ストアフロント、トランザクションシステム、ERPなど）によって1か月に呼び出される回数 | GMV層に基づく<p>最小配分：10M/月</p> | はい<p>1か月あたり100万リクエストのライセンスパックを追加</p> |
| コンテンツリクエスト | HTML ページビューまたはJSON API呼び出しのストアフロントへのリクエスト。 1 ページビューまたは5回のAPI呼び出しとしてカウント。 | GMV層に基づく<p>最小配分：月額2M</p> | はい<p>1か月あたり1 Mのライセンスパックを追加</p> |
| バリエーション | テキストベースのコンテンツ生成の許可 | GMV層に基づく<p>最小配分：1K バリエーション/月</p> | はい<p>生成AI クレジットは別途購入する</p> |

{style="table-layout:auto"}

>[!NOTE]
>
>画像の生成には、[!DNL Adobe Commerce as a Cloud Service]と同じIMS組織にプロビジョニングされた[!DNL Adobe Firefly] ライセンスが必要です。

### 製品の発見

ストアフロントの商品検索、リスト、マーチャンダイジング設定には、次の制限が適用されます。

| **機能** | **説明** | **基本配分** | **拡張可能ですか？** |
| --- | --- | --- |---------------------------------------------------|
| 商品検索 | `products`、`productSearch`、`refineProduct`、`variants`で商品データを取得する際の[!DNL Catalog Service] GraphQL リクエストあたりの最大SKU数。 複数の呼び出しに対して、大きなリクエストを分割します。 | 100 | いいえ |
| フィルター可能な属性 | 階層化されたナビゲーションとファセットで有効にできる製品特性（色、サイズ、ブランド、素材など）の数 | 200 | いいえ |
| 検索可能な属性 | カタログ検索でインデックスを作成できる製品特性の数 | 200 | いいえ |
| ソート可能な属性 | 検索ページとカテゴリーページの並べ替えオプションとして使用できる製品特性の数。 | 50 | いいえ |
| 検索ページの深さ | 検索ページネーションを通じて到達できる最大の商品（例：100 ページ× 100 ページの商品/ページ） | 10K | いいえ |
| ファセット | 買い物客が検索結果を絞り込み、カテゴリーを閲覧するのに役立つ、フィルター可能な商品属性（ブランド、色、サイズ、価格など）の数 | 100<p>フィルター可能な属性である必要があります</p> | はい<p>サポートリクエストで500に増やすことができます</p> |
| ファセットごとのオプション | 買い物客がファセット内で選択できるフィルター可能な商品属性値の数（例：色の場合は「赤」、「青」、サイズの場合は「小」、「Medium」） | 100 | はい<p>サポートリクエストで増加する可能性があります</p> |

{style="table-layout:auto"}

### 推奨事項

商品レコメンデーションでは、次の機能を利用できます。 他のAdobe Commerce製品で利用できる一部の機能は、[!DNL Adobe Commerce as a Cloud Service]ではサポートされていません。

| **機能** | **説明** | **基本配分** | **拡張可能ですか？** |
| --- | --- | --- | --- |
| アクティブなレコメンデーションユニット | ストアフロント上のライブレコメンデーションコンポーネントの数（「顧客も閲覧した」または「気に入ったかもしれない」など） | 商品レコメンデーション用に、ページタイプごとに50個のアクティブなユニットを作成し、必要に応じてカタログモデルの範囲を明示的に指定 | いいえ |

{style="table-layout:auto"}
<!-- Talos complained about this even thought it was copied directly from the ACO version of this page. Commenting out for now, | Category or attribute inclusions/exclusions | Filter products to a specific set that qualifies for recommendations | Not supported | — | -->

### 拡張機能

| **機能** | **説明** | **基本配分** | **拡張可能ですか？** | **メモ** |
| --- | --- | --- | --- | --- |
| Adobe Developer App Builder | クラウドネイティブな拡張機能や統合機能の構築能力 | GMV層に基づく<p>最小配分：1 パック/年</p> | はい<p>追加パックを追加</p> | パックごとに定義される制限については、次を参照してください。<ul><li>[App Builder製品の説明](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html)。</li><li>*App Builder Runtime Guides*&#x200B;の[&#x200B; システム設定と制限](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings)。</li><li>[App Builder ストレージの要件](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/)</li></ul> |

{style="table-layout:auto"}

<!--
## How to size your solution

Ask your Adobe representative for a list of available packages to determine which most closely matches your project

To accurately size your [!DNL Adobe Commerce as a Cloud Service] solution, follow these steps:

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
