---
title: インストールと設定
description: ' [!DNL Product Recommendations]をインストール、更新、アンインストールする方法について説明します。'
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 2e7f6454-d4cb-44bc-982f-354a179e8e59
TQID: https://experienceleague.adobe.com/z-ue-sojw9Iewuz-ZToCzkumP3qN-TCWWF3UWdpdIL0
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 10a91a91337778648e99078bcbf0c9ef25a49f86
workflow-type: tm+mt
source-wordcount: 578
ht-degree: 0%

---

# インストールと設定

[!DNL Product Recommendations]をストアフロントおよび管理者にデプロイするには、モジュールをインストールし、[Commerce Services Connector](../landing/saas.md)を設定する必要があります。 アップデートがリリースされると、インストールを最新バージョンに簡単に更新できます。

- [インストール](#install)
- [設定](#configure)
- [更新](#update)
- [アンインストール](#uninstall)

## [!DNL Product Recommendations]をインストール {#install}

[!DNL Product Recommendations] モジュールはスタンドアロンのメタパッケージであるため、更新プログラムはAdobe Commerceよりも頻繁にリリースされます。 最新のバグ修正と機能を使用して最新の状態を確認するには、[&#x200B; リリースノート &#x200B;](release-notes.md)を参照してください。

>[!IMPORTANT]
>
>商品レコメンデーションを使用するには、適切な[使用権限](../landing/saas.md#credentials)があることを確認してください。

Composerで`magento/product-recommendations` モジュールをインストールします。

```bash
composer require magento/product-recommendations
```

### ページビルダーのサポートの追加 {#pbsupport}

ページビルダーの[!DNL Product Recommendations]はオプションのモジュールであり、個別にインストールされます。 ページビルダーで[!DNL Product Recommendations]を使用するには、次のコマンドを実行してモジュールをインストールします。

```bash
composer require magento/module-page-builder-product-recommendations
```

ページビルダーで[!DNL Product Recommendations]を有効にすると、既存のアクティブな[&#x200B; レコメンデーションユニット &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/add-content/recommendations)を、ページビルダーで作成されたコンテンツ（ページ、ブロック、動的ブロックなど）に追加できます。

詳しい手順については、[&#x200B; ページビルダーコンテンツを使用した [!DNL Product Recommendations] の使用](page-builder.md)を参照してください。

### 視覚的な類似性のレコメンデーションタイプを追加 {#vissimsupport}

_視覚的な類似性_&#x200B;のレコメンデーションタイプを使用すると、表示中の製品と[視覚的に類似した](type.md#visualsim)製品を表示する製品詳細ページにレコメンデーションユニットをデプロイできます。 このレコメンデーションタイプは、商品の画像や視覚的な側面がショッピング体験の重要な部分である場合に最も役立ちます。 次のコマンドを実行して、_視覚的な類似性_&#x200B;のレコメンデーションタイプをインストールします。

```bash
composer require magento/module-visual-product-recommendations
```

## [!DNL Product Recommendations]の設定 {#configure}

1. `magento/product-recommendations` モジュールをインストールした後、API キーを指定してSaaS データスペースを選択し、[Commerce Services Connector](../landing/saas.md)を設定します。

   この接続を設定すると、Commerce インスタンス、カタログサービス、およびその他のサポートサービス間のデータ同期と通信が可能になります。 データの同期は、[SaaS データ書き出し拡張機能](../data-export/overview.md)によって処理されます。

1. カタログの書き出しを正しく実行できるようにするには、[cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) ジョブと[&#x200B; インデクサー](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers)が実行されており、`Product Feed` インデクサーが`Update by Schedule`に設定されていることを確認します。

Commerce アプリケーションをCommerce サービスに正常にリンクし、[SaaS データスペース &#x200B;](../landing/saas.md#saas-configuration)を指定すると、カタログの同期が開始されます。 その後、[&#x200B; ストアフロントに行動データが送信されていることを](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/)確認できます。

## データ同期の監視とトラブルシューティング

{{$include /help/_includes/data-export/verify-commerce-service-data-sync.md}}

{{install-data-sync-feed-status}}

## [!DNL Product Recommendations]のインストールを更新します {#update}

すべてのAdobe Commerceと同様に、[!DNL Product Recommendations]はインストールと更新にComposerを使用します。 `magento/product-recommendations` モジュールを更新するには、次のコマンドを実行します。

```bash
composer update magento/product-recommendations --with-dependencies
```

5.0から6.0などのメジャーバージョンに更新するには、プロジェクトのルート `composer.json` ファイルを編集する必要があります。 （最新バージョンについては、[&#x200B; リリースノート &#x200B;](release-notes.md)を参照してください）。 例えば、メインの`composer.json` ファイルを開き、`magento/product-recommendations` モジュールを検索します。

```json
"require": {
    ...
    "magento/product-recommendations": "^5.0",
    ...
}
```

メジャーバージョンを`5.0`から`6.0`にバンプしましょう：

```json
"require": {
    ...
    "magento/product-recommendations": "^6.0",
    ...
}
```

`composer.json` ファイルを保存して実行：

```bash
composer update magento/product-recommendations --with-dependencies
```

または、`magento/module-visual-product-recommendations`および`magento/module-page-builder-product-recommendations` モジュールをインストールした場合：

```bash
composer update --with-dependencies magento/product-recommendations magento/module-visual-product-recommendations magento/module-page-builder-product-recommendations
```

>[!NOTE]
>
> 製品レコメンデーションのバージョン 3.x.xでは、1つのAPI キーのみが必要でした。 バージョン 4.x.x以降では、サンドボックス環境と実稼動環境の両方にパブリック API キーとプライベート API キーを提供する必要があります。 両方のペアのAPI キーを指定しない場合は、管理者の製品レコメンデーション機能にアクセスできません。 しかし、データ収集はストアフロントで継続し、既存のレコメンデーションは引き続き買い物客に表示されます。

## ファイアウォール

ファイアウォールを通じて商品レコメンデーションを行うには、許可リストに`commerce.adobe.io`を追加します。

## [!DNL Product Recommendations]をアンインストール {#uninstall}

必要に応じて、product-recommendations モジュールを[&#x200B; アンインストール &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/uninstall-modules)できます。
