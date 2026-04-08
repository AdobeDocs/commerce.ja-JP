---
title: Adobe Commerce Optimizer コネクタの概要
description: コネクタのインストールと設定方法、書き出し設定のカスタマイズ方法、Adobe Commerce Optimizerへの接続方法、データ同期ステータスのモニタリング方法について説明します。
feature: Personalization, Integration, Configuration
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
source-git-commit: d9ed5413d0edb23aeb4c00ee7528444b56d2a6d4
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 0%

---


# 基本を学ぶ

Commerce Optimizer Connectorをインストールして設定し、Adobe Commerce カタログデータを[!DNL Adobe Commerce Optimizer]と同期してから、データ同期ステータスを監視して、ストアフロントが最新であることを確認します。

## 統合の使用要件

* Adobe Commerce 2.4.7以降

   * PHP 8.2、8.3、または8.4
   * Composer 2.x

* プロビジョニングされたサンドボックスインスタンスを使用する[!DNL Adobe Commerce Optimizer] ライセンス。

* Composerを使用してCommerce Connector メタパッケージをダウンロードするための[認証キー](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)。

* [Adobe Commerce Optimizer サンドボックスインスタンス &#x200B;](../optimizer/get-started.md)への管理者アクセス。

統合を設定するAdobe Commerce ユーザーは、次の要件を満たす必要があります。

* Adobe Commerce管理者への管理者アクセス。

* [Adobe Commerce アプリケーションサーバー](https://experienceleague.adobe.com/ja/docs/commerce-on-cloud/user-guide/project/user-access)へのコマンドラインアクセス。

* [&#x200B; プロジェクトがプロビジョニングされている](https://experienceleague.adobe.com/ja/docs/core-services/interface/administration/organizations?)IMS組織[!DNL Adobe Commerce Optimizer]への開発者アクセス。

>[!BEGINSHADEBOX]

## 前提条件

次のいずれかの拡張機能がインストールされている場合は、Commerce Optimizer Connectorをインストールする前にアンインストールします。

* Adobe Commerce ライブサーチ （`magento/live-search`）
* Adobe Commerceの商品レコメンデーション （`magento/product-recommendations`）
* Adobe Commerce Catalog Service （`magento/catalog-service`, `magento/catalog-service-installer`）
* データ管理ダッシュボード （`magento-catalog-sync-admin`）

これらの拡張機能に関連付けられたデータは、引き続きCommerce データベースで使用できます。 ただし、コネクタが有効になっている場合は、[!DNL Adobe Commerce Optimizer]に書き出されません。 コネクタを有効にした後、これらの拡張機能によって提供される検索およびマーチャンダイジング機能を実装するには、[[!DNL Adobe Commerce Optimizer] 管理UI](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/overview#quick-tour)からそれらを設定します。

>[!ENDSHADEBOX]

## 設定手順

コネクタを有効にし、CommerceからAdobe Commerce Optimizer インスタンスへのデータの同期を開始するには、次の手順に従います。

1. **[Composerを使用してCommerce Optimizer Connector パッケージ](#install-the-commerce-connector-package)**&#x200B;をインストールし、Commerce インスタンスを[!DNL Adobe Commerce Optimizer]に接続します。

1. **[管理者からデータ書き出し設定](#customize-commerce-data-export-configuration)**&#x200B;を確認してカスタマイズします。

1. **[CommerceとCommerce Optimizer間の接続を確立するために必要なAPI資格情報を取得します](#get-required-values-for-configuring-the-commerce-optimizer-connection)**。

1. **[&#x200B; [!DNL Adobe Commerce Optimizer] 統合](#enable-the-adobe-commerce-optimizer-integration)**&#x200B;を有効にします。

1. **[データ同期が機能していることを確認します](#verify-that-the-data-sync-is-working)**。


## Commerce Optimizer Connector パッケージのインストール

Adobe Commerce Optimizer コネクタは、コンポーザーのメタパッケージとして配信され、[!DNL Adobe Commerce Optimizer]のアクティブなライセンスを持つすべてのCommerce マーチャントが利用できます。

### インストール手順

1. Composerを使用して`adobe-commerce/commerce-data-export-aco-adapter` モジュールを追加します。

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter
   ```

1. Adobe Commerce ステージング環境に変更をデプロイします。

デプロイメントが完了すると、Commerceの管理メニューから「Commerce Optimizer」オプションを使用できるようになります。 **[!UICONTROL Commerce Optimizer]**&#x200B;をクリックして、Commerce管理者から直接Commerce Optimizer インスタンスを開きます。

>[!NOTE]
>
>拡張機能のインストール手順について詳しくは、次のガイドを参照してください。
>
>[Cloud Infrastructure上のAdobe Commerceへの拡張機能のインストール &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[Adobe Commerce オンプレミスへの拡張機能のインストール &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/tutorials/extensions)

### 必要な接続の詳細を取得

Adobe Developer Consoleから、[!DNL Adobe Commerce Optimizer]取り込みサービスを有効にする開発者プロジェクトを作成し、OAuth サーバー間の資格情報を生成します。 詳細な手順については、[&#x200B; マーチャンダイジング開発者ガイド &#x200B;](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials)の&#x200B;*IMS資格情報の取得*&#x200B;を参照してください。

>[!TIP]
>
>Commerce Optimizer インスタンスと同じIMS組織でData Ingestion APIを使用して設定された開発者プロジェクトが既にある場合は、既存のOAuth サーバー間の資格情報を再利用できます。

資格情報ページから次の値を保存します。

* **組織ID** （`org_id`）
* **クライアント ID** （`client_id`）
* **クライアント秘密鍵** （`client_secret`）

### [!DNL Adobe Commerce Optimizer] インスタンスの詳細を取得

インスタンス ID （テナント IDとも呼ばれます）を[!DNL Adobe Commerce Optimizer] インスタンスから保存します。 インスタンスへのアクセスに使用されるURLで見つけることができます。 例えば、`https://experience.adobe.com/#/@<project-id>/in:TToyu73daQRn66KAYaq8YZ/commerce-optimizer-studio/home`では、インスタンス IDは`TToyu73daQRn66KAYaq8YZ`です。

## Commerce データ書き出し設定のカスタマイズ

デフォルトでは、すべてのCommerce スコープ（web サイトとストアビュー）でカタログデータの同期が有効になっています。 ビジネスニーズに基づいて、特定の範囲のデータのみを同期するように書き出し設定をカスタマイズできます。 例えば、複数のストアビューを持っていて、そのうちの1つのデータのみを書き出す場合、他のストアビューのエクスポーターを無効にすることができます。

>[!IMPORTANT]
>
>書き出し設定を変更すると、カタログのサイズに応じて大幅な時間がかかる場合がある、完全なインデックス再作成がトリガーされます。 パフォーマンスへの影響を最小限に抑えるために、トラフィックの少ない時間帯には変更を計画します。

### スコープ別データ書き出し

次の表に、各範囲レベルで書き出されるデータを示します。

| 範囲 | 書き出されたデータ | メモ |
| ------- | --------------- | ------- |
| web サイト | 価格と価格表 | 各価格セットは、命名規則[を使用して](../optimizer/setup/pricebooks.md)価格表`website::customergroupcode`として書き出されます。 Web サイトのすべての顧客グループが含まれます。 |
| ストアビュー | 製品と製品属性 | 各ストアビューは、[!DNL Adobe Commerce Optimizer]に個別のカタログソースを作成します。 |

### ビヘイビアーを有効または無効にする

| アクション | 結果 |
| -------- | -------- |
| ストアビューを無効にする | カタログ ソースは[!DNL Adobe Commerce Optimizer]に残りますが、すべてのデータは削除されます。 |
| ストアビューを無効にして再度有効にする | 同じカタログソースに、完全なデータ再同期が再入力されます。 |

### 書き出し設定の更新

Connector パッケージをインストールすると、AdminのStore グリッドにCommerce Optimizerの書き出し設定が表示されるようになりました。

![Commerce Optimizerの同期設定を使用したストアグリッド &#x200B;](./assets/aco-connector-sync-config.png){width="600" zoomable="yes"}

**Web サイトまたはストアビューの設定を変更するには：**

1. Commerce Adminで、**[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL All Stores]**&#x200B;に移動します。

1. 設定するweb サイトまたはストアビューを選択します。

1. **[!DNL Adobe Commerce Optimizer]エクスポーター設定**&#x200B;で、チェックボックスを使用して、必要に応じてデータ同期を有効または無効にします。

   ![&#x200B; データ同期設定の更新](./assets/aco-connector-store-website-export-settings.png){width="500" zoomable="yes"}

1. 変更を保存します。

## [!DNL Adobe Commerce Optimizer]統合を有効にする

>[!IMPORTANT]
>
>データ同期処理は、設定コマンドを実行するとすぐに開始されます。 デフォルトでは、すべてのCommerce スコープ（web サイトとストアビュー）でカタログデータの同期が有効になっています。 カタログのサイズによっては、データ同期プロセスに数分から数時間かかる場合があります。

前の手順で収集したAPI資格情報とインスタンスの詳細を使用して、Commerceと[!DNL Adobe Commerce Optimizer] インスタンスの統合を設定できるようになりました。

1. Commerce管理者から「**[!UICONTROL Adobe Commerce Optimizer]**」を選択し、手順を含む設定ページを表示します。

   ![[!DNL Adobe Commerce Optimizer]設定ページ &#x200B;](/help/aco-connector/assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. コマンドラインから、[SSH](https://experienceleague.adobe.com/ja/docs/commerce-on-cloud/user-guide/develop/secure-connections)を使用してCommerce ステージング環境に接続します。

1. 次のCommerce CLI コマンドを実行して統合を設定し、プレースホルダー値をCommerce Optimizer プロジェクトの値に置き換えます。

```terminal
bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
```

1. Commerce管理者に戻り、[!UICONTROL Adobe Commerce Optimizer] オプションを選択して、接続を確認します。

   このオプションをクリックすると、新しいタブで[!DNL Adobe Commerce Optimizer] UIが開きます。

## データ同期が機能していることを確認します

統合を有効にすると、データの同期が自動的に開始されます。 カタログサイズによっては、最初の同期に数分から数時間かかる場合があります。

1. **Commerce管理者の同期ステータスを確認：**

   **[!UICONTROL System]** > [!UICONTROL Data Transfer] > **[!UICONTROL Data Feed Sync Status]**&#x200B;に移動します。

   ![&#x200B; フィード項目のステータスがレポートされるデータフィードの同期ステータス ページ &#x200B;](./assets/data-feed-sync-status.png){width="500" zoomable="yes"}

   同期を実行すると、フィード データに正常に送信されたレコードが表示されます。 フィードを選択して、詳細を表示したり、同期の問題をトラブルシューティングしたりします。

1. **データがCommerce Optimizerに到着したことを確認します：**

   [!DNL Adobe Commerce Optimizer] メニューから、**[!UICONTROL Data Sync]**&#x200B;を選択します。

   ![&#x200B; データ同期](./assets/data-sync.png){width="500" zoomable="yes"}

   予想される商品、価格、属性が表示されることを確認します。

>[!TIP]
>
>データ同期に問題がある場合は、[SaaS データ書き出し](/help/data-export/troubleshooting-logging.md) ドキュメントの&#x200B;*トラブルシューティング* セクションを参照してください。

## 次のステップ

1. **[カタログ ビューとポリシー [!DNL Adobe Commerce Optimizer] の設定](#configure-adobe-commerce-optimizer-stores)**

   カタログ ビューとポリシーを[!DNL Adobe Commerce Optimizer] ガイドで作成します。 価格表は、Adobe Commerceのお客様グループから自動的に作成されることに注意してください。

1. **[Edge Delivery ServicesでのCommerce ストアフロントの設定](#set-up-a-commerce-storefront-on-edge-delivery-services)**

   [&#x200B; ストアフロント設定ドキュメント &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/setup/?lang=ja)に従って、ストアフロントを[!DNL Adobe Commerce Optimizer] インスタンスに接続し、パーソナライズされたコマースエクスペリエンスの提供を開始します。


