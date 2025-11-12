---
title: Commerce用Adobe Commerce Optimizer コネクタ
description: Commerce Cloud またはオンプレミスプロジェクトからAdobe Commerce Optimizerにデータを接続する方法について説明します
feature: Personalization, Integration, Configuration
hidefromtoc: true
hide: true
source-git-commit: 5d0cfb2c389bf11f89815e7d1fbc2861a6b48962
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 0%

---


# 概要

Adobe Commerce コネクタは、クラウド上の既存の Adobe Commerce Cloud またはオンプレミスのデプロイメントとAdobe Commerce Optimizerのコンポーザブルカタログデータモデルの間でカタログと価格データを同期する統合ブリッジです。 これにより、動的な AI 検索、Recommendations、Edge Delivery Services上のAdobe Commerceのストアフロントなどの高速読み込みのヘッドレスストアフロント、リアルタイムのパフォーマンス分析などの機能が可能になります。

>[!NOTE]
>
>このドキュメントでは、製品の早期アクセス開発について説明しており、一般提供を目的とした機能のすべてを反映しているわけではありません。

## アーキテクチャとエクスペリエンス

Adobe Commerce コネクタは、Commerceのカタログ階層をAdobe Commerce Optimizer `website/store/storeview` データモデル `channel/policy/source` マッピングすることで機能します。

Commerce Admin からCommerce Services （Live Search と Product Recommendations）を設定および管理する代わりに、[Adobe Commerce Optimizer マーチャンダイジングツール &#x200B;](../optimizer/merchandising/overview.md) を使用して、商品の検出（Live Search）とレコメンデーション（Product Recommendations）のルール設定を管理します。  Adobe Commerce インスタンスは、カタログおよび価格データのデータオリジンになります。 Commerceでデータが更新されると、更新内容がAdobe Commerce Optimizer インスタンスに同期されます。

## ワークフロー

コネクタにより、次の主要なワークフローが可能になります。

* **Commerce カタログデータをAdobe Commerce Optimizerに書き出す** – 価格および価格台帳のデータは `website` レベルで書き出されます。 製品および製品属性データは、`store view` レベルで書き出されます。 デフォルトでは、すべてのCommerce スコープ（web サイトおよびストアビュー）でカタログデータ同期が有効になっています。

  このワークフローを有効にするには、Composer を使用して `adobe-commerce/commerce-data-export-aco-adapter` PHP 拡張機能をインストールし、Commerce プロジェクト間のコネクションを認証するための IMS 認証情報を提供します。

* **Commerce `website/store/storeview` データをマッピングしてAdobe Commerce Optimizerに書き出す**

  管理（**[!UICONTROL Stores]** -> [!UICONTROL Settings] -> **[!UICONTROL All Stores]**）のストアグリッドからエクスポーター設定を更新して、特定のスコープのデータのみを書き出すようにAdobe Commerce Optimizer エクスポーター設定をカスタマイズするオプションがあります。

* **マーチャンダイジングルールの設定と管理**

  コネクターを有効にすると、商品検出およびレコメンデーションのマーチャンダイジングルールが、Adobe Commerce Optimizer管理の [!UICONTROL Live Search] ページや [!UICONTROL Product Recommendations] ページではなく、Commerce UI から定義および管理されます。

* **Edge Delivery ServicesにCommerce ストアフロントをデプロイする**

  Adobe Commerce Optimizerとの統合を設定した後、Edge Delivery サービスにCommerce ストアフロントを設定してデプロイすると、Adobe Commerce Optimizerで利用可能なコンポーザブルな API ドリブン型アーキテクチャとモジュラーコンポーネントにより、超高速パフォーマンス、スケーラビリティ、シームレスなコンテンツオーサリング、統合されたパーソナライゼーション、運用コストの削減を実現できます。

## 統合を使用するための要件

* Adobe Commerce 2.4.5 以降

   * PHP 8.1、8.2、8.3、または 8.4
   * Composer 2.x

* プロビジョニングされたサンドボックスインスタンスを使用したAdobe Commerce Optimizer ライセンス。

* [repo.magento.com](https://repo.magento.com) にアクセスし、Composer を使用してCommerce コネクタ メタパッケージをダウンロードします。

* [Adobe Commerce Optimizer サンドボックスインスタンス &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-learn/tutorials/adobe-commerce-optimizer/create-first-instance) への管理者アクセス。

統合を設定するAdobe Commerce ユーザーには、次が必要です。

* Adobe Commerce Admin への管理者アクセス。

* [Adobe Commerce アプリケーションサーバーへのコマンドラインアクセス &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-on-cloud/user-guide/project/user-access)。

* Adobe Commerce Optimizer プロジェクトがプロビジョニングされている [IMS 組織 &#x200B;](https://experienceleague.adobe.com/ja/docs/core-services/interface/administration/organizations?) への開発者アクセス。

## はじめに

1. **統合の設定**

   1. [Commerce コネクタパッケージをインストール &#x200B;](#install-the-commerce-connector-package) します。

   1. [Commerce Optimizer接続の設定に必要な値を取得する](#get-required-values-for-configuring-the-commerce-optimizer-connection)

   1. [Adobe Commerce Optimizer統合を有効にします &#x200B;](#enable-the-adobe-commerce-optimizer-integration)。

   1. [&#x200B; データ同期が機能していることを確認 &#x200B;](#verify-that-the-data-sync-is-working)。

   1. [&#x200B; データの書き出しの設定をカスタマイズ &#x200B;](#customize-commerce-data-export-configuration) （オプション）。

1. **[Adobe Commerce Optimizer ストアの設定](#configure-adobe-commerce-optimizer-stores)**

1. **[Edge Delivery ServicesにCommerce ストアフロントを設定する](#set-up-a-commerce-storefront-on-edge-delivery-services)**

## Commerce コネクタパッケージのインストール

Adobe Commerce Connector Composer メタパッケージは、Adobe Commerce Optimizerのアクティブなライセンスを持つすべてのCommerce マーチャントが利用できます。

### インストール手順

1. Composer を使用して `adobe-commerce/commerce-data-export-aco-adapter` モジュールを追加します。

```shell
 composer require adobe-commerce/commerce-data-export-aco-adapter
```

1. 変更内容をAdobe Commerceのステージング環境にデプロイします。

変更がデプロイされると、Commerceの管理者メニューで「Commerce Optimizer Optimizer」オプションが使用できるようになります。

>[!NOTE]
>
>拡張機能のインストール手順について詳しくは、次のガイドを参照してください。
>
>[&#x200B; クラウドインフラストラクチャー上のAdobe Commerceに拡張機能をインストール &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[&#x200B; 拡張機能Adobe Commerceをオンプレミスでインストール &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/tutorials/extensions)

## Commerce Optimizer接続の設定に必要な値の取得

### API 資格情報の取得

>[!NOTE]
>
>Commerce Optimizer インスタンスがデプロイされている IMS 組織に既にApp Builder Developer プロジェクトがある場合は、必要な API 資格情報と組織 ID を、そのプロジェクトの OAUTH サーバー間資格情報から取得できます。

Adobe Developer コンソールで新しい開発者プロジェクトを作成して、Commerce インスタンスとCommerce Optimizer インスタンスの統合を設定するための API 資格情報を取得します。 手順については、開発者向けドキュメントの [App Builder プロジェクトの作成 &#x200B;](https://developer.adobe.com/commerce/extensibility/events/project-setup/) を参照してください。

プロジェクトを作成したら、OAUTH サーバー間資格情報ページから次の値を保存します。

* **組織 ID** （`org_id`）

* **IMS `client_id` と`client_secret`**

### Adobe Commerce Optimizer インスタンスの詳細を取得

Adobe Commerce Optimizer インスタンスの詳細から次の値を保存します。

* **インスタンス ID - &#x200B;** Adobe Commerce Optimizer インスタンスの一意の ID。 テナント ID とも呼ばれます。

  URL からインスタンス ID を取得して、Adobe Commerce Optimizer インスタンスにアクセスします。 例えば、URL `https://na1-sandbox.admin.commerce.adobe.com/1234567890abcdef` では、インスタンス ID は `1234567890abcdef` です。

* **地域 – &#x200B;** Adobe Commerce Optimizer サンドボックスインスタンスがホストされている地域。

  Adobe Commerce Optimizer URL からリージョンを取得します。 例えば、URL `https://na1-sandbox.admin.commerce.adobe.com/1234567890abcdef` では、領域は `na1` です。

## Adobe Commerce Optimizer統合の有効化

>[!IMPORTANT]
>
>データ同期処理は、設定コマンドを実行すると開始されます。 デフォルトでは、すべてのCommerce スコープ（web サイトおよびストアビュー）でカタログデータ同期が有効になっています。 カタログのサイズによっては、データ同期プロセスに数時間かかる場合があります。

前の手順で収集した API 資格情報とインスタンスの詳細を使用して、Commerce インスタンスとAdobe Commerce Optimizer インスタンスの統合を設定できるようになりました。

1. Commerce Admin で「**[!UICONTROL Adobe Commerce Optimizer]**」を選択すると、手順を示す設定ページが表示されます。

   ![Adobe Commerce Optimizer設定ページ &#x200B;](../assets/aco-connector-config-page.png)

1. コマンドラインから [SSH を使用して &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-on-cloud/user-guide/develop/secure-connections) Commerce ステージング環境に接続します。

1. 次のCommerce CLI コマンドを実行して統合を設定し、プレースホルダーの値をCommerce Optimizer プロジェクトの値に置き換えます。

```terminal
bin/magento aco:config:init --org_id=<<your_org_id>> --tenant_id=<<your_tenant_id>> --client_id=<<your_client_id>> --client_secret=<<your_client_secret>> --region=<<na1>> --type=sandbox
```

1. Commerce管理者に戻り、「[!UICONTROL Adobe Commerce Optimizer]」オプションを選択して、接続を確認します。

   このオプションをクリックすると、Adobe Commerce Optimizer UI が新しいタブで開きます。

## データ同期が機能していることを確認します

データ同期は、Commerce Admin とCommerce Optimizerの両方で確認できます。

* **[データフィード同期ステータス &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status.md)** ページには、CommerceからAdobe Commerce Optimizerへのカタログデータ同期の進行状況が表示されます。

* Adobe Commerce Optimizerの **[[!UICONTROL Data Sync]ページには &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/setup/data-sync)** Commerce インスタンスから転送されたカタログデータが表示されます。

1. カタログデータがCommerceからCommerce Optimizerに送られていることを確認します。

   Commerce管理者から、[!UICONTROL Data Feed Sync Status]&#x200B;**/[!UICONTROL System]/[!UICONTROL Data Transfer] を選択して &#x200B;** [!UICONTROL Data Feed Sync Status]** ページを開きます。

   ![&#x200B; フィード項目のステータスレポートを含むデータフィード同期のステータスページ &#x200B;](./assets/data-feed-sync-status.png)

   データ同期が開始された場合、フィードデータには正常に送信されたレコードが表示されます。 また、各フィードの詳細を表示して、同期の問題の表示やトラブルシューティングを行うこともできます。

1. Adobe Commerce Optimizerがカタログデータを受信していることを確認します。

   Commerce Optimizerメニューで「**[!UICONTROL Data Sync]**」を選択して、データ同期ページを開きます。

   ![&#x200B; データ同期 &#x200B;](./assets/data-sync.png)

### トラブルシューティング

データ同期が開始されていない場合は、カタログインデックスが有効であることを確認します。 インデックスが無効な場合は、Commerce CLI から次のコマンドを実行して、カタログデータのインデックスを再作成します。

```terminal
bin/magento indexer:reindex" catalog indexer re-index CLI command to start PaaS to ACO catalog data synchronization.
```

## Commerceのデータエクスポート設定のカスタマイズ

管理（**[!UICONTROL Stores]** -> [!UICONTROL Settings] -> **[!UICONTROL All Stores]**）のストアグリッドからエクスポーター設定を更新して、特定のスコープのデータのみを書き出すようにAdobe Commerce Optimizer エクスポーター設定をカスタマイズするオプションがあります。

* `website` レベルでは、エクスポーター設定を無効にすると、Adobe Commerce Optimizerへの価格と価格台帳データの書き出しは停止されます。

* エクスポーター設定を `storeview` 効にすると、エクスポーターレベルで商品と商品属性のAdobe Commerce Optimizerへの書き出しが停止します。

設定が変更されると、対応するインデックスが無効化され、影響を受けるエンティティのトリガーの再エクスポートが行われます。

## Adobe Commerce Optimizer ストアの設定

カタログビューとポリシーを作成してAdobe Commerce Optimizer ストアを設定し&#x200B;す。 Adobe Commerce Optimizer ガイドの [&#x200B; カタログビューの作成 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/setup/catalog-view) を参照してください。

価格台帳は、Adobe Commerce顧客グループから自動的に作成されます。

## Edge Delivery ServicesでのCommerce ストアフロントの設定

この節では、Commerce ストアフロントの設定に必要な手順の概要について説明します。 詳細については、[Adobe Commerce ストアフロント ] （https://experienceleague.adobe.com/developer/commerce/storefront/?lang=ja）のドキュメントサイトを参照してください。

1. [Site Creator tool](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator) を使用して、Adobe Commerceストアフロントボイラープレートのクローンを作成し、EDS にデプロイします。

1. [ローカル開発環境を設定します &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=ja#set-up-local-environment)。

1. [GraphQL Storefront 互換性パッケージのインストール &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility/install/?lang=ja)&#x200B;

1. [&#x200B; クラウド環境のCommerce インスタンスに CORS ヘッダーを設定します &#x200B;](#configure-cors-headers-for-commerce-instance)。

1. [&#x200B; ストアフロントをCommerce データソースに接続します &#x200B;](#connect-the-storefront-to-commerce-data-sources)。

### Commerce インスタンスに CORS ヘッダーを設定

GraphQL リクエストをEdge Delivery Services（EDS）ストアフロントからAdobe Commerce on cloud 環境またはオンプレミス環境で受け取れるようにするには、次のいずれかのオプションを使用して、特定のクロスオリジンリソース共有（CORS）ヘッダーをAdobe Commerce GraphQL エンドポイントに追加し&#x200B;す。

1. クロスオリジンリソース共有（CORS）ヘッダーをAdobe Commerce GraphQL エンドポイントに追加します&#x200B;

   **オプション 1:CORS ヘッダーを追加できるように、Adobe Commerce Foundation 用の PHP カスタムモジュールを実装する&#x200B;**

   **オプション 2：サードパーティのコミュニティモジュール graycore/magento2-cors&#x200B;** をインストールする – [4&rbrace;Adobe Commerce ストアフロント &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/cors-setup/?lang=ja) ドキュメントの &lbrace;CORS 設定 *を参照してください。*

1. Commerce on cloud instance `app.yaml` 環境設定ファイルに次の CORS 変数を追加します。

   * `CONFIG__DEFAULT__WEB__GRAPHQL__CORS_ALLOWED_HEADERS: *`
   * `CONFIG__DEFAULT__WEB__GRAPHQL__CORS_ALLOWED_ORIGINS: *`

### ストアフロントのCommerce データソースへの接続

ストアフロントのボイラープレートコードの GitHub リポジトリで、ストアフロントの設定ファイルを次のパラメーターを使用し `config.json` 更新します。

* `"commerce-core-endpoint": "Commerce cloud instance GraphQL endpoint"`

* `"commerce-endpoint": "Commerce Optimizer instance GraphQL endpoint"` – この値を [Commerce Optimizer インスタンスの詳細ページ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/get-started#get-instance-details)&#x200B;から取得します

* `"AC-Environment-Id": "Customer organization ID"` – この値を [Commerce クラウドプロジェクトから取得します &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-on-cloud/user-guide/project/overview#project-overview)

* `"AC-View-ID": "Catalog view ID in Commerce Optimizer Admin"` – この値は、Adobe Commerce Optimizer管理者から取得します。

* `"AC-Price-Book-ID": "base::b6589fc6ab0dc82cf12099d1c2d40ab994e8410c"` – この値は、Adobe Commerce Optimizer管理者から取得します&#x200B;。

* `"AC-Source-Locale": "Catalog source – Store View code from Commerce cloud instance"`

詳しくは、&lbrace;2[Adobe Commerce ストアフロント &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/?lang=ja) ドキュメントの &lbrace; ストアフロント設定 *を参照してください。*


