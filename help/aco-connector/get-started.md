---
title: Adobe Commerce Optimizer コネクタの概要
description: コネクタのインストールと設定方法、書き出し設定のカスタマイズ方法、Adobe Commerce Optimizerへの接続方法、データ同期ステータスのモニタリング方法について説明します。
feature: Personalization, Integration, Configuration
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
source-git-commit: dc50e4d7bcd118b2b9a800779c600ade5560e0bf
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 0%

---


# 基本を学ぶ

Adobe Commerce Optimizer Connectorをインストールして設定し、Adobe Commerce カタログデータを[!DNL Adobe Commerce Optimizer]と同期してから、データ同期ステータスを監視して、ストアフロントが最新であることを確認します。

{{aco-integration-environment-alignment}}

## 統合の使用要件

* Adobe Commerce 2.4.7以降

   * PHP 8.2、8.3、または8.4
   * Composer 2.x

* プロビジョニングされたサンドボックスインスタンスを使用する[!DNL Adobe Commerce Optimizer] ライセンス。

* Composerを使用してCommerce Connector メタパッケージをダウンロードするための[認証キー](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)。

* [Adobe Commerce Optimizer サンドボックスインスタンス ](../optimizer/get-started.md)への管理者アクセス。

統合を設定するAdobe Commerce ユーザーは、次の要件を満たす必要があります。

* Adobe Commerce管理者への管理者アクセス。

* [Adobe Commerce アプリケーションサーバー](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access)へのコマンドラインアクセス。

* [!DNL Adobe Commerce Optimizer] プロジェクトがプロビジョニングされている[IMS組織](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations?)への開発者アクセス。

>[!BEGINSHADEBOX]

## 前提条件

次のいずれかの拡張機能がインストールされている場合は、Adobe Commerce Optimizer Connectorをインストールする前にアンインストールします。

* Adobe Commerce ライブサーチ （`magento/live-search`）
* Adobe Commerceの商品レコメンデーション （`magento/product-recommendations`）
* Adobe Commerce Catalog Service （`magento/catalog-service`, `magento/catalog-service-installer`）
* データ管理ダッシュボード （`magento-catalog-sync-admin`）

これらの拡張機能に関連付けられたデータは、引き続きCommerce データベースで使用できます。 ただし、コネクタが有効になっている場合は、[!DNL Adobe Commerce Optimizer]に書き出されません。 コネクタを有効にした後、これらの拡張機能によって提供される検索およびマーチャンダイジング機能を実装するには、[[!DNL Adobe Commerce Optimizer] 管理UI](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview#quick-tour)からそれらを設定します。

>[!IMPORTANT]
>
>コネクタを有効にする前にこれらの拡張機能が削除されていない場合、接続済みサービスで拡張機能とコネクタの認証方法の競合により、同じデータがコネクタと既存の拡張機能の両方から書き出されるため、設定画面が壊れ、[!DNL Adobe Commerce Optimizer]にデータが重複し、ログに401または403のエラーが発生する可能性があります。

>[!ENDSHADEBOX]

## 設定手順

コネクタを有効にし、CommerceからAdobe Commerce Optimizer インスタンスへのデータの同期を開始するには、次の手順に従います。

1. **[Composerを使用してAdobe Commerce Optimizer Connector パッケージ](#install-the-adobe-commerce-optimizer-connector-package)**&#x200B;をインストールし、Commerce インスタンスを[!DNL Adobe Commerce Optimizer]に接続します。

1. **[管理者からデータ書き出し設定](#customize-the-commerce-scopes-export-configuration)**&#x200B;をカスタマイズします。

1. **[ [!DNL Adobe Commerce Optimizer] 統合](#enable-the-adobe-commerce-optimizer-integration)**&#x200B;を有効にします。

1. **[データ同期が機能していることを確認します](#verify-that-the-data-sync-is-working)**。


## Adobe Commerce Optimizer Connector パッケージのインストール {#install-the-adobe-commerce-optimizer-connector-package}

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
>[Cloud Infrastructure上のAdobe Commerceへの拡張機能のインストール ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[Adobe Commerce オンプレミスへの拡張機能のインストール ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)

## Commerce スコープ書き出し設定のカスタマイズ

デフォルトでは、すべてのCommerce スコープ（web サイト、カスタマーグループ、ストアビュー）でカタログデータの同期が有効になっています。 ビジネスニーズに基づいて、特定の範囲のデータのみを同期するように書き出し設定をカスタマイズできます。 例えば、同じ言語を共有する複数のストアビューがある場合、ストアビューの1つだけのデータを書き出し、[!DNL Adobe Commerce Optimizer]の複数のカタログビューの[ カタログソース ](../optimizer/setup/catalog-source.md)として使用することができます。

>[!IMPORTANT]
>
>書き出し設定を変更すると、カタログのサイズに応じて大幅な時間がかかる場合がある、完全なインデックス再作成がトリガーされます。 Adobeでは、統合を有効にして最初のデータ同期を開始する前に、Commerce スコープをCommerce Optimizerに同期するように設定することをお勧めします。


次の表に、各範囲レベルで書き出されるデータを示します。

| 範囲 | 書き出されたデータ | メモ |
|----------------------------| --------------- |-------|
| web サイトと顧客グループ | 価格と価格表 | 各価格セットは、命名規則`<website>::<SHA1 of customer group ID>`を使用して[価格表](../optimizer/setup/pricebooks.md)として書き出されます。 Web サイトのすべての顧客グループが含まれます。 |
| ストアビュー | 製品と製品属性 | 各ストアビューは、[!DNL Adobe Commerce Optimizer]に個別の[ カタログソース ](../optimizer/setup/catalog-source.md)を作成します。 |

![Commerce Optimizerの同期設定を使用したストアグリッド ](./assets/aco-connector-storeviews-list.png){width="600" zoomable="yes"}

**Web サイトまたはストアビューの設定を変更するには：**

1. Commerce Adminで、**[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL All Stores]**&#x200B;に移動します。

1. 設定するweb サイトまたはストアビューを選択します。

1. **[!DNL Adobe Commerce Optimizer]エクスポーター設定**&#x200B;で、チェックボックスを使用して、必要に応じてデータ同期を有効または無効にします。

   ![ データ同期設定の更新](./assets/aco-connector-storeview-export-settings.png){width="500" zoomable="yes"}

1. 変更を保存します。

### ビヘイビアーを有効または無効にする

| アクション | 結果 |
| -------- | -------- |
| ストアビューを無効にする | カタログ ソースは[!DNL Adobe Commerce Optimizer]に残りますが、すべてのデータは削除されます。 |
| ストアビューを無効にして再度有効にする | 同じカタログソースに、完全なデータ再同期が再入力されます。 |

## [!DNL Adobe Commerce Optimizer]統合を有効にする

>[!IMPORTANT]
>
>設定が完了するとすぐに、データ同期処理がバックグラウンドで開始されます。 カタログのサイズによっては、データ同期プロセスに数分から数時間かかる場合があります。

### 必要な接続の詳細を取得

[Adobe Developer Console](https://developer.adobe.com/console)から、[!DNL Adobe Commerce Optimizer]取り込みサービスに対して有効な新しいプロジェクトを作成し、OAuth サーバー間の資格情報を生成します。 詳細な手順については、*マーチャンダイジング開発者ガイド*&#x200B;の[IMS資格情報の取得](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials)を参照してください。

資格情報ページから次の値を保存します。

* **組織ID** （`org_id`）
* **クライアント ID** （`client_id`）
* **クライアント秘密鍵** （`client_secret`）

![資格情報の詳細を取得](assets/developer-console-project-credentials.png){width="500" zoomable="yes"}

### [!DNL Adobe Commerce Optimizer] インスタンスの詳細を取得

_テナント ID_&#x200B;を、[!DNL Adobe Commerce Optimizer] インスタンス [[!DNL Instance details]  ページ ](../optimizer/get-started.md#manage-instances)の&#x200B;_[!DNL Instance Id]_フィールドまたはインスタンスへのアクセスに使用したURLから取得します。 例：`https://experience.adobe.com/#/@<your organization>/in:<tenant ID>/commerce-optimizer-studio/home`。

1. Commerce管理者から「**[!UICONTROL Adobe Commerce Optimizer]**」を選択し、手順を含む設定ページを表示します。

   ![[!DNL Adobe Commerce Optimizer]設定ページ ](/help/aco-connector/assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. コマンドラインから、[SSH](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections)を使用してCommerce ステージング環境に接続します。

1. 次のCommerce CLI コマンドを実行して統合を設定し、プレースホルダー値をCommerce Optimizer プロジェクトの値に置き換えます。

```terminal
bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
```

1. Commerce管理者に戻り、[!UICONTROL Adobe Commerce Optimizer] オプションを選択して、接続を確認します。

   このオプションをクリックすると、新しいタブで[!DNL Adobe Commerce Optimizer] UIが開きます。

## データ同期が機能していることを確認します

管理者で利用可能な[ データフィード同期ステータス ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) ページから、同期が機能していることを監視および確認できます。

1. **Commerce管理者の同期ステータスを確認：**

   **[!UICONTROL System]** > [!UICONTROL Data Transfer] > **[!UICONTROL Data Feed Sync Status]**&#x200B;に移動します。

   ![ フィード項目のステータスがレポートされるデータフィードの同期ステータス ページ ](./assets/data-feed-sync-status.png){width="500" zoomable="yes"}

   同期を実行すると、フィード データに正常に送信されたレコードが表示されます。 フィードを選択して、詳細を表示したり、同期の問題をトラブルシューティングしたりします。

1. **データがCommerce Optimizerに到着したことを確認します：**

   [!DNL Adobe Commerce Optimizer] メニューから、**[!UICONTROL Data Sync]**&#x200B;を選択します。

   ![ データ同期](./assets/data-sync.png){width="500" zoomable="yes"}

   予想される商品、価格、属性が表示されることを確認します。

>[!TIP]
>
>データ同期に問題がある場合は、*SaaS データ書き出し* ドキュメントの[ トラブルシューティング ](/help/data-export/troubleshooting-logging.md) セクションを参照してください。

## 次のステップ

1. **カタログ ビューとポリシー[!DNL Adobe Commerce Optimizer]を設定**

   [!DNL Adobe Commerce Optimizer] UIでカタログ ビューとポリシーを作成します。 価格表は、Adobe Commerceのお客様グループから自動的に作成されることに注意してください。 手順については、*Commerce Optimizer ユーザーガイド*&#x200B;の[ カタログビュー](../optimizer/setup/catalog-view.md)および[ ポリシー](../optimizer/setup/policies.md)のドキュメントを参照してください。

1. **Edge Delivery ServicesでのCommerce ストアフロントの設定**

   [ ストアフロント設定ドキュメント ](https://experienceleague.adobe.com/developer/commerce/storefront/setup/)に従って、ストアフロントを[!DNL Adobe Commerce Optimizer] インスタンスに接続し、パーソナライズされたコマースエクスペリエンスの提供を開始します。


