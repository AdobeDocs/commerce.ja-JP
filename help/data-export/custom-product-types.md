---
title: SaaS カタログデータ書き出しのカスタム製品タイプのサポート
description: Commerce Storefront MCP カタログイネーブルメントモジュールを使用して、SaaS データの書き出しが、ライブサーチおよびカタログサービスに送信されるカタログデータの単純な商品として、認識されないカスタムサードパーティの商品タイプを表す方法について説明します。
role: Admin, Developer
hide: true
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
source-git-commit: fd87417a494987f33009d386019d870b306dcf73
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%
---
# SaaS カタログデータ書き出しのカスタム製品タイプのサポート

>[!IMPORTANT]
>
>カスタム製品タイプのサポートは、現在、[!DNL Commerce Storefront MCP]の一部として&#x200B;**早期アクセス**&#x200B;で提供されています。 このモジュールは、Adobe Commerce バージョン 2.4.4以降でサポートされています。 可用性、パッケージング、およびインストールの要件は、一般提供される前に変更される場合があります。 この&#x200B;**早期アクセス**&#x200B;への招待をリクエストするには、[commerceeap@adobe.com](mailto:commerceeap@adobe.com)に電子メールを送信してください。 Adobeチームは、次のステップと適格要件で対応します。

## 概要

[!DNL SaaS Data Export]は、[ ライブサーチ ](../live-search/overview.md)や[ カタログサービス ](../catalog-service/overview.md)など、接続されたAdobe Commerce サービスのカタログデータを準備する際に、標準のCommerce製品タイプ（シンプル、設定可能、バンドルなど）を認識します。 サードパーティの拡張機能により、[!DNL SaaS Data Export]がネイティブに認識しない&#x200B;**カスタム製品タイプ**&#x200B;を導入できます。

Commerce Storefront MCP カタログイネーブルメントモジュールを使用すると、[!DNL SaaS Data Export]は、アウトバウンドカタログペイロードで&#x200B;**シンプルな商品**&#x200B;として認識されないカスタム商品タイプを表すことができるため、[!DNL Commerce Storefront MCP]を使用する買い物客は、カタログベースのサービスを通じてそれらを発見できます。

## 行動の範囲

- Commerce Storefront MCP カタログイネーブルメントモジュールでは、Adobe Commerceに保存されている商品タイプは変更されません。 カスタム製品タイプを単純な製品として表すことは、[!DNL Live Search]および[!DNL Catalog Service]に送信されたカタログデータにのみ適用されます。
- 管理者設定やランタイム設定は必要ありません。 標準の製品タイプは引き続き正常に書き出されます。
- このモジュールは、標準のCommerce製品タイプではなく、サードパーティの拡張機能によって導入されたカスタム製品タイプをターゲットにしています。

## モジュールのインストール

Commerce Storefront MCP カタログイネーブルメントモジュールを有効にするには、コマンドラインから次のコマンドを実行します。

```bash
composer require magento/module-storefront-mcp-enablement --no-update
composer update magento/module-storefront-mcp-enablement --with-dependencies
bin/magento setup:upgrade
```

## カタログデータの再同期

このモジュールをインストールしても、Adobe Commerceの基になる商品データは変更されないため、既存のカスタム商品タイプの商品が自動的に再書き出しされることはありません。 モジュールをインストールする前に既に同期されているカタログデータに新しいシンプルな製品表現を適用するには、カタログデータを手動で再同期します。 [ データを手動で再同期する](data-sync-manage.md#manually-resync-data)を参照してください。
