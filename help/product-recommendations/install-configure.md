---
title: インストールと設定
description: ' [!DNL Product Recommendations] をインストール、更新、アンインストールする方法を説明します。'
role: Admin, Developer
exl-id: 2e7f6454-d4cb-44bc-982f-354a179e8e59
badgePaas: label="PaaS のみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeが管理する PaaS インフラストラクチャ）およびオンプレミスプロジェクトにのみ適用されます。"
source-git-commit: 7d5e3faeef2fb16779d1558027a0b76ff3fe3a38
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---

# インストールと設定

[!DNL Product Recommendations] をストアフロントおよび管理者にデプロイするには、モジュールをインストールして [1&rbrace;Commerce サービスコネクタ &rbrace; を設定する必要があります。 ](../landing/saas.md)アップデートがリリースされると、インストールを最新バージョンに簡単にアップデートできます。

- [インストール](#install)
- [設定](#configure)
- [更新](#update)
- [Uninstall](#uninstall)

## [!DNL Product Recommendations] のインストール {#install}

[!DNL Product Recommendations] モジュールはスタンドアロンメタパッケージなので、アップデートはAdobe Commerceよりも頻繁にリリースされます。 最新のバグ修正と機能を確認するには、[ リリースノート ](release-notes.md) を参照してください。

>[!IMPORTANT]
>
>Product Recommendations を使用するための正しい [ 使用権限 ](../landing/saas.md#credentials) があることを確認します。

Composer を使用して `magento/product-recommendations` モジュールをインストールします。

```bash
composer require magento/product-recommendations
```

### ページビルダーのサポートの追加 {#pbsupport}

ページビルダーの [!DNL Product Recommendations] はオプションのモジュールで、個別にインストールされます。 ページビルダーで [!DNL Product Recommendations] を使用するには、次のコマンドを実行してモジュールをインストールします。

```bash
composer require magento/module-page-builder-product-recommendations
```

ページビルダーで [!DNL Product Recommendations] を有効にすると、ページ、ブロック、動的ブロックなど、ページビルダーで作成した任意のコンテンツに既存のアクティブな [ レコメンデーションユニット ](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/add-content/recommendations) を追加できます。

詳しくは [ ページビルダーコンテンツの使用  [!DNL Product Recommendations]  を参照 ](page-builder.md) てください。

### 視覚的類似性レコメンデーションタイプを追加 {#vissimsupport}

_視覚的類似性_ レコメンデーションタイプを使用すると、表示している製品に [ 視覚的に類似 ](type.md#visualsim) している製品を表示するレコメンデーションユニットを製品の詳細ページにデプロイできます。 このレコメンデーションタイプは、商品の画像や視覚的側面がショッピング体験の重要な部分である場合に最も役立ちます。 次のコマンドを実行して、「_ビジュアルな類似性_」レコメンデーションタイプをインストールします。

```bash
composer require magento/module-visual-product-recommendations
```

## [!DNL Product Recommendations] の設定 {#configure}

1. `magento/product-recommendations` モジュールをインストールしたら、API キーを指定して SaaS Data Space を選択し [&#128279;](../landing/saas.md)Commerce サービスコネクタを設定します。

   この接続を設定すると、Commerce インスタンス、カタログサービス、その他のサポートサービス間のデータ同期と通信が可能になります。 データ同期は、[SaaS データ書き出し拡張機能 ](../data-export/overview.md) で処理されます。

1. カタログの書き出しを正しく実行できるようにするには、[cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) ジョブと [ インデクサー ](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers) が実行中で、`Product Feed` インデクサーが `Update by Schedule` に設定されていることを確認します。

Commerce アプリケーションをCommerce サービスに正常にリンクし、[SaaS Data Space](../landing/saas.md#saas-configuration) を指定すると、カタログの同期が開始されます。 その後、行動データがストアフロントに送信されていることを [ 確認 ](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/) できます。

## データ同期の監視とトラブルシューティング

Commerce Admin から、[Data Management Dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard) を使用して同期プロセスを監視できます。 [Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting) とログを使用して、プロセスの管理とトラブルシューティングを行います。

その後、行動データがストアフロントに送信されていることを [ 確認 ](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/) できます。

## [!DNL Product Recommendations] インストールの更新 {#update}

他のすべてのAdobe Commerceと同様に、[!DNL Product Recommendations] はインストールとアップデートに Composer を使用します。 `magento/product-recommendations` モジュールを更新するには、次の手順を実行します。

```bash
composer update magento/product-recommendations --with-dependencies
```

5.0 から 6.0 などのメジャーバージョンにアップデートするには、プロジェクトのルート `composer.json` ファイルを編集する必要があります。 （最新のバージョンについて詳しくは、[ リリースノート ](release-notes.md) を参照してください）。 例えば、メインの `composer.json` ファイルを開いて、`magento/product-recommendations` モジュールを検索します。

```json
"require": {
    ...
    "magento/product-recommendations": "^5.0",
    ...
}
```

メジャーバージョンを `5.0` から `6.0` に変更しましょう。

```json
"require": {
    ...
    "magento/product-recommendations": "^6.0",
    ...
}
```

`composer.json` ファイルを保存し、次を実行します。

```bash
composer update magento/product-recommendations --with-dependencies
```

または、`magento/module-visual-product-recommendations` モジュールと `magento/module-page-builder-product-recommendations` モジュールがインストールされている場合は、次の手順を実行します。

```bash
composer update --with-dependencies magento/product-recommendations magento/module-visual-product-recommendations magento/module-page-builder-product-recommendations
```

>[!NOTE]
>
> Product Recommendations のバージョン 3.x.x では、必要な API キーは 1 つだけです。 バージョン 4.x.x 以降では、サンドボックス環境と実稼動環境の両方に公開および秘密 API キーを指定する必要があります。 API キーの両方のペアを指定しない場合は、管理者の Product Recommendations 機能にアクセスできません。 ただし、データ収集はストアフロントで引き続き行われ、既存のお勧めは引き続き買い物客に表示されます。

## ファイアウォール

ファイアウォールを介して Product Recommendations を許可するには、許可リストに `commerce.adobe.io` を追加します。

## [!DNL Product Recommendations] のアンインストール {#uninstall}

必要に応じて、製品レコメンデーションモジュールを [ アンインストール ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/uninstall-modules) できます。
