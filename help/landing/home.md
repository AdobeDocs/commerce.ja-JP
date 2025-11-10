---
title: サービスガイドのホーム
description: Commerce SaaS サービスのAdobe Commerce製品ドキュメントを参照してください。
seo-title: Services for Adobe Commerce
seo-description: Access the product documentation for hosted services that help Adobe Commerce merchants support key components of their business.
recommendations: noCatalog
exl-id: 507af1fa-9f3e-41bc-9aaf-cd89839aae0b
source-git-commit: fd3857e93dbaaf7ffce97715b77ee63e8460af16
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 0%

---

# Adobe Commerce サービスガイド

Adobe Commerce サービスは、ストアフロントの拡張、統合の効率化、データ管理の最適化を実現する強力な機能を提供します。

## Commerceはどのようにサービスに接続しますか？

すべてのCommerce サービスは、[Commerce サービスコネクタ &#x200B;](saas.md) を介してCommerce インスタンスに接続します。

Commerce サービスコネクタが設定されると、次の機能にアクセスできます。

- [&#x200B; ストアフロントサービス &#x200B;](#storefront-services) – 製品の検出、レコメンデーション、支払いに関する AI を活用した機能
- [Integration Services](#integration-services) - Adobe Experience Platform、AEM Assets、その他のAdobe ソリューションへの接続

これらのサービスは、コンバージョンを増加させ、パーソナライズされたエクスペリエンスを提供し、Adobe エコシステム全体でコマースデータをより活用するのに役立ちます。

![&#x200B; サービスレイヤー &#x200B;](./assets/services-layer.png)

>[!NOTE]
>
>Adobeでは、すべてのCommerce サービスのサポートされている最新バージョンにアップグレードすることをお勧めします。 詳しくは、[&#x200B; リリースノート &#x200B;](release-notes-all.md) を参照してください。

これらの機能に加えて、Commerce インスタンスから SaaS プラットフォームへのデータの流れをモニタリングできるツールもあります。 これらのツールは、データを自動的に同期し、パフォーマンスの最適化に役立ちます。 使用可能な [&#x200B; データツール &#x200B;](#data-tools) について詳しくは、こちらを参照してください。

## 利用可能なサービス

>[!BEGINTABS]

>[!TAB  ストアフロントサービス ]

ストアフロントサービスは、製品検出を最適化し、顧客インタラクションをパーソナライズし、支払い処理を合理化してエンゲージメントとコンバージョンを向上させる AI を活用した機能のグループです。 ストアフロントサービスを使用すると、ショッピング体験を強化し、ビジネスの成長を推進できます。

<table style="table-layout:fixed">
<tr style="border: 0;">
   <td valign="top">
      <a href="../catalog-service/overview.md">
      <img alt="接続されたサービスのカタログデータ" src="../assets/icons/DataBook.svg" width="40">
      </a>
      <div>
         <a href="../catalog-service/overview.md">
         <strong> カタログサービス </strong>
         </a>
      </div>
      <p>
         <em> 顧客に最適化された製品体験を提供すると同時に、パフォーマンスを向上させ、スケーラビリティを向上させ、コンバージョンを増やします。</em>
      </p>
   </td>
   <td valign="top">
      <a href="../live-search/overview.md">
      <img alt="検索" src="../assets/icons/Magnify.svg" width="40">
      </a>
      <div>
         <a href="../live-search/overview.md">
         <strong>[!DNL Live Search]</strong>
         </a>
      </div>
      <p>
         <em>B2C の買い物客に対して、より賢く、より速く、より関連性の高い結果を提供する、この AI を活用した検索ツールを実装します。</em>
      </p>
   </td>
   <td valign="top">
      <a href="../product-recommendations/overview.md">
      <img alt="ThumbsUp" src="../assets/icons/ThumbUp.svg" width="40">
      </a>
      <div>
         <a href="../product-recommendations/overview.md">
         <strong> 製品の推奨事項 </strong>
         </a>
      </div>
      <p>
         <em> 買い物客の行動、人気のトレンド、製品の類似性などに基づく、AI を活用したレコメンデーションを追加します </em>。
      </p>
   </td>
   <td valign="top">
      <a href="../payment-services/guide-overview.md">
      <img alt="クレジットカードによる支払い" src="../assets/icons/CreditCard.svg" width="40">
      </a>
      <div>
         <a href="../payment-services/guide-overview.md">
         <strong> 資金決済 </strong>
         </a>
      </div>
      <p>
         <em> 無利子の分割払いや、支払い処理、注文、請求書の合理化されたビューなど、多様な支払い方法で顧客満足度を高めます </em>
      </p>
   </td>
</tr>
</table>

>[!TAB  統合サービス ]

Integration Services とは、Commerce インスタンスをAdobe内の他の製品やサービスに接続する機能を指します。

<table style="table-layout:fixed">
<tr style="border: 0;">
   <td valign="top">
      <a href="../data-connection/overview.md">
      <img alt="プラットフォームにデータを転送" src="../assets/icons/TransferToPlatform.svg" width="40">
      </a>
      <div>
         <a href="../data-connection/overview.md">
         <strong>[!DNL Data Connection]</strong>
         </a>
      </div>
      <p>
         <em>Adobe CommerceとAdobe Experience Platform Edge 間の接続を活用して、Commerce データをAdobe AnalyticsやAdobe Targetなどの他のAdobe Experience Cloud製品に使用します </em>。
      </p>
   </td>
   <td valign="top">
      <a href="../aem-assets-integration/overview.md">
      <img alt="ビジュアル" src="../assets/icons/images.svg" width="40">
      </a>
      <div>
          <a href="../aem-assets-integration/overview.md">
         <strong>AEM Assetsの統合 </strong>
         </a>
      </div>
      <p>
         <em>Adobe Experience Managerと統合してリッチメディアコンテンツを管理するシステムを使用し、デジタルアセット管理を簡素化します。</em>
      </p>
   </td>
</tr>
</table>

>[!TAB  データツール ]

データツールを使用すると、Commerce インスタンスと接続されたサービスの間の情報フローを管理および最適化できます。 これらのツールは、リソースを集中的に消費するプロセスをオフロードすることで、効率的なデータ同期、同期処理の監視、パフォーマンスの向上を実現します。

<table style="table-layout:fixed">
<tr style="border: 0;">
   <td valign="top">
       <a href="../data-export/overview.md">
      <img alt="SaaS データ書き出しフィード管理" src="../assets/icons/FeedManagement.svg" width="40">
      </a>
      <div>
         <a href="../data-export/overview.md">
         <strong>[!DNL SaaS Data Export]</strong>
         </a>
      </div>
      <p>
         <em> カタログ、注文、在庫データをAdobe Commerceから接続されたサービスに自動的に同期します。 Commerce CLI コマンドまたは <strong>Data Management Dashboard</strong> を使用して、同期処理を管理します。</em>
      </p>
   </td>
   <td valign="top">
      <a href="../price-index/price-indexing.md">
      <img alt="製品価格フィード" src="../assets/icons/Feed.svg" width="40">
      </a>
      <div>
          <a href="../price-index/price-indexing.md">
         <strong>SaaS 価格インデクサー </strong>
         </a>
      </div>
      <p>
         <em> インデックス作成や価格計算など、リソースを大量に消費するタスクを、Commerce アプリケーションからAdobeのクラウドインフラストラクチャにオフロードすることで、サイトのパフォーマンスを最適化します </em>。
      </p>
   </td>
   <td valign="top">
      <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard" target="_blank">
      <img alt="データ同期の監視" src="../assets/icons/Monitoring.svg" width="40">
      </a>
      <div>
          <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard" target="_blank">
         <strong> データ管理ダッシュボード </strong>
         </a>
      </div>
      <p>
         <em>Commerce Admin の統合ダッシュボードから、Commerceのデータ同期とトリガーの再同期を簡単に追跡できます。 データの可用性に関する貴重なインサイトを取得して、買い物客にタイムリーに表示できます。</em>
      </p>
   </td>
</table>

>[!NOTE]
>
>Data Management Dashboard は、Product Recommendations v6.0.0、Live Search v4.1.0、またはアクティブなライセンスを持つカタログサービス v1.17 を使用しているCommerce マーチャントが追加費用なしで利用できます。 以前のサービスバージョンを使用しているマーチャントは、[&#x200B; カタログ同期 &#x200B;](../landing/catalog-sync.md) を使用してデータ同期を管理および追跡できます。

>[!ENDTABS]

## Commerce サービスで解決できる問題

Adobe Commerce サービスは、ビジネスの拡大、カスタマーエクスペリエンスの向上、データに基づく意思決定のいずれを目的とする場合でも、Commerceの一般的な課題に対するソリューションを提供します。

| 問題 | 課題 | 解決策 |
|---------|-----------|----------|
| 製品の検出とコンバージョンの向上 | 買い物客が探しているものが見つからず、バウンス率が高くなり、売上が減少します。 | [Live Search](../live-search/overview.md) および [Product Recommendations](../product-recommendations/overview.md) を使用すると、誤字許容値、即時の「入力時の検索」結果、動的なファセット、リアルタイムの買い物客の行動に基づいてパーソナライズされた製品レコメンデーションを備えた AI 搭載の検索を提供できます。 |
| オムニチャネルパーソナライズされたエクスペリエンスの作成 | コマースデータはサイロ化され、様々なチャネルにわたってパーソナライズされたエクスペリエンスを提供することができません。 | [&#x200B; データ接続 &#x200B;](../data-connection/overview.md) を使用すると、行動データ、トランザクションデータ、プロファイルデータをAdobe Experience Platformに送信できます。 高度な顧客セグメントを作成し、放棄された買い物かごキャンペーンを作成し、類似オーディエンスをターゲットに設定して、カスタマージャーニー全体にわたる季節的なトレンドを分析します。 |
| デジタルアセット管理の合理化 | 複数のシステムにわたる製品画像とリッチメディアの管理は、時間がかかり、エラーが発生しやすくなります。 | [AEM Assets統合 &#x200B;](../aem-assets-integration/overview.md) は、Adobe CommerceをAdobe Experience Manager Assets プロジェクトに接続し、ワークフローを簡素化し、すべてのタッチポイントで一貫したブランドエクスペリエンスを確保することで、アセット管理を一元化します。 |
| 支払い処理の最適化 | 限られた支払いオプションと不十分な支払い体験は、顧客満足度とコンバージョンを傷つけています。 | [&#x200B; 支払いサービス &#x200B;](../payment-services/guide-overview.md) では、支払い、注文、請求書を管理するための統一されたダッシュボードを使用して、利息なしの分割払いなど、複数の支払い方法を提供しています。 |
| 大規模なデータ同期の管理 | リソースを大量に消費するインデックス作成により、サイトの速度が低下し、データ同期の問題を簡単に追跡できません。 | [SaaS Data Export](../data-export/overview.md)、[SaaS Price Indexer](../price-index/price-indexing.md)、および [Data Management Dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) は、カタログ、注文、在庫データを自動的に同期し、価格計算をAdobeのクラウドインフラストラクチャにオフロードし、同期ステータスをリアルタイムに可視化します。 |
| 失われた顧客を取り戻し、収益を削減 | 高い顧客チャーンと製品の返品率は、収益性に影響を与えています。 | [&#x200B; データ接続 &#x200B;](../data-connection/overview.md) をAdobe Journey OptimizerおよびReal-Time CDPと組み合わせて、収益パターンを特定し、勝者キャンペーンを作成し、行動別に顧客をセグメント化し、パーソナライズされたリエンゲージメントキャンペーンをメールおよび SMS で送信します。 |
| データに基づくマーチャンダイジング決定を行う | プロモーションする製品やプロモーションを実行するタイミングが不明です。 | [&#x200B; ライブ検索 &#x200B;](../live-search/overview.md) では、検索パフォーマンスのインサイトとマーチャンダイジングツールを提供します。これらのツールで、主要指標にアクセスしたり、検索語句を分析したり、インテリジェントマーチャンダイジングルールを使用したりして、実際の顧客行動とビジネス目標に基づいて製品の価値を高めたり埋め込んだりできます。 |
| 機密データへのコンプライアンスを維持 | HIPAA コンプライアンスを維持しながら、機密性の高い顧客データを処理する必要があります。 | [&#x200B; データ接続 &#x200B;](../data-connection/overview.md) は HIPAA に対応しており、コンプライアンスを維持し、プライバシーリクエストを体系的に処理しながら、バックオフィスデータをExperience Platformと共有できます。 |

{{$include /help/_includes/templated/whats-new.md}}

<!-- Last updated from includes: 2025-09-26 20:42:12 -->
