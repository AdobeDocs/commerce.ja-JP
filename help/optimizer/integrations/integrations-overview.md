---
title: Commerce Optimizerとの連携
description: カタログ同期、アセット管理、ストアフロントの最適化、Salesforce Commerce Cloudとの連携におけるAdobe Commerce Optimizerの統合について説明します。
solution: Commerce
feature: Integration, Catalog Management
role: Developer, Admin
level: Beginner
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="[!DNL Adobe Commerce Optimizer]件のプロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"
exl-id: 8f3a2c1b-9d4e-5f6a-bc7d-1e2f3a4b5c6d
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: ef0c45ae-6bee-4821-a65e-e1e118e8a01c
    internal-label: Commerce Optimizer
feature_v2:
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
source-git-commit: 9b3448a40c2e829e09de5e394b0972c527ee0e9b
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%
---

# [!DNL Adobe Commerce Optimizer]統合

[!DNL Adobe Commerce Optimizer]には、Adobe Commerce クラウドまたはオンプレミスからデータを同期し、アセットを管理し、ストアフロント エクスペリエンスを向上させ、外部システムを接続するための統合機能が含まれています。 以下の節では、各統合が[!DNL Adobe Commerce Optimizer]でどのように機能するかを説明します。 設定、設定、日常使用のリンクに従います。

{{aco-integration-environment-alignment}}

## AEM Assetsを使用した製品ビジュアル {#product-visuals}

Product Visualsでは、Adobe Experience Manager（AEM）Assetsを使用して商品画像を管理できます。 商品ビジュアルを有効にするには、Commerce Optimizer用AEM Assetsを設定します。 設定が完了したら、AEM Assetsを製品画像の一元的なデジタルアセット管理ソリューションとして使用し、画像をCommerce Optimizer カタログと同期させる自動アセットレビューおよび管理ワークフローを使用します。 統合は、SKUごとにアセットと製品を一致させます。 Adobeの統合サービスでアップデートを実行し、手動で再アップロードすることなくストアフロントに最新のメディアを反映。

- [AEM Assetsを使用した製品ビジュアル](../setup/product-visuals.md)

## Adobe Experience Manager Sites Optimizer {#aem-sites-optimizer}

Adobe Experience Manager Sites Optimizerは、発見、エンゲージメント、コンバージョンの向上に役立つ、AI主導の&#x200B;**[!UICONTROL Opportunities]** レコメンデーションを表面化することで、Commerce web サイトを分析し、パフォーマンスを向上させます。

>[!AVAILABILITY]
>
>この機能を使用するには、**Ultima** Adobe Sites Optimizer ライセンスが必要です。 Adobe カスタマーテクニカルアドバイザーからライセンスをリクエストできます。 アカウントのプロビジョニングが完了すると、オポチュニティ機能が[!DNL Adobe Commerce Optimizer] インターフェイスで利用できるようになり、AI主導のインサイトを使用してストアフロントとマーチャンダイジング戦略を最適化できるようになります。

- [オポチュニティ](../manage-results/opportunities.md)

## Adobe Commerce Optimizer Connector {#aco-connector}

Adobe Commerce Optimizer コネクタは、Adobe Commerce（クラウドまたはオンプレミス）と[!DNL Adobe Commerce Optimizer]の間でカタログと価格データを同期するブリッジです。 コネクタを有効にすると、Commerceは商品データの記録システムのままになり、[!DNL Adobe Commerce Optimizer]は商品の検索、レコメンデーション、マーチャンダイジングルール、分析、ヘッドレスストアフロント体験を強化します。 同期されたカタログビューのクエリを実行できるユーザーを制限するには、[&#x200B; プライベートカタログビュー](../setup/private-catalog-view.md)を参照してください。

- [Adobe Commerce Optimizer コネクタの概要](../../aco-connector/overview.md){target="_blank"}
- [コネクタの基本を学ぶ](../../aco-connector/get-started.md){target="_blank"}

## サードパーティのカートとチェックアウトの統合

Adobe Commerce Optimizerは、取引に個別のコマースプラットフォームを使用するストアフロントの商品ディスカバリーとマーチャンダイジングを強化できます。 ストアフロントでは、商品データ、検索、レコメンデーション、マーチャンダイジングにCommerce Optimizer Merchandising Services APIを使用しています。 ホストコマースプラットフォームは、買い物客アカウント、カート、チェックアウト、注文処理について引き続き責任を負います。 ホストプラットフォームとの統合は、API Mesh、App Builder、ダイレクト API、またはこれらのツールの組み合わせを使用したカスタム実装です。

Salesforce Commerce Cloud （SFCC）の場合、[Adobe Commerce Optimizer SFCC Checkout Starter Kit](https://github.com/adobe-commerce/aco-sfcc-checkout-starter-kit)には、Adobe Commerce Optimizer ストアフロントをSFCCの買い物客、買い物かご、チェックアウト機能に接続するためのEdge Delivery Services ブロックとスクリプトの例が用意されています。 これを参照実装として使用し、ストアフロントに適応させます。これは、一般的な、すぐに使えるコネクタではありません。 Next.js[&#128279;](https://github.com/adobe-commerce/aco-sfcc-storefront-next){target="_blank"}の ヘッドレスストアフロントの例も利用できます。


## Commerce Salesforce Connector {#commerce-salesforce-connector}

Commerce Salesforce Connector （Adobe App Builder上に構築）は、Salesforce Commerce Cloud B2Cのカタログと価格データを[!DNL Adobe Commerce Optimizer]に同期するため、Salesforce commerceのバックエンドを置き換えることなく、Adobe ストアフロントとマーチャンダイジング機能を使用できます。 Salesforce Commerce APIを使用して、同期のスケジュール設定、オンデマンド更新の実行、統合の拡張を行うことができます。

- [Salesforce Commerce Connector](../developer/salesforce-connector.md)

>[!MORELIKETHIS]
>
>- [Adobe Commerce Optimizer テクニカルドキュメント &#x200B;](https://developer.adobe.com/commerce/services/optimizer/){target="_blank"}
>- [Adobe Commerce Optimizerの基本を学ぶ](../get-started.md)
