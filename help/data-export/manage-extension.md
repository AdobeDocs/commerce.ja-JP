---
title: '[!DNL Manage the Data Export extension]'
description: ' [!DNL Data Export] 拡張機能をアップグレードし、必要のないデータ書き出しサービスを削除または無効にする方法を説明します。'
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 94702995-d272-47b9-9560-198eee3250a6
TQID: https://experienceleague.adobe.com/ghrA-YFR7hurQgEnjS8PdxR7Zcx-ayLTuyBfhbCC-KI
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: d3cdead0-685a-4489-9250-4bb709942f66
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 312
ht-degree: 0%

---

# SaaS データ書き出し拡張機能の管理

SaaS サービスの[[!DNL data export] extension](https://github.com/magento/commerce-data-export)は、Adobe Commerceと接続されたCommerce サービス間のデータの収集と同期を可能にするモジュールのコレクションです。

Adobe Commerce サービス拡張機能のメタパッケージには、次のような特定のモジュールが含まれています
[&#x200B; ライブサーチ &#x200B;](/help/live-search/overview.md)、[商品レコメンデーション &#x200B;](/help/product-recommendations/overview.md)、[&#x200B; カタログサービス &#x200B;](/help/catalog-service/overview.md)、および[[!DNL Adobe Commerce Optimizer Connector]](/help/aco-connector/overview.md)として使用できます。 これらのサービスを使用している場合、Data Export拡張機能を有効にするために個別のインストールは必要ありません。

## Commerce データ書き出し機能の削除または無効化

インストールされているコマースデータ書き出しモジュールのいずれかが必要ない場合は、`magento:module:disable` CLI コマンドを使用して無効にします。

例えば、カテゴリ権限フィード データを内部で使用する[Categories API](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/)があります。 このAPIを使用していない場合は、カテゴリ権限フィードのデータ書き出しを無効にできます。

```shell
bin/magento module:disable Magento_CategoryPermissionDataExporter Magento_SaaSCategoryPermissions
```

### モジュールを特定のバージョンに更新する

Composerを使用すると、インストールされているコマースデータ書き出しモジュールのいずれかを更新できます。 [&#x200B; リリースノート &#x200B;](release-notes.md)を確認して、必要な修正が利用可能かどうかを判断し、その特定のバージョンと必要な依存関係にアップグレードします。

>[!NOTE]
>
>最新バージョンの[&#x200B; ライブサーチ &#x200B;](/help/live-search/overview.md)、[&#x200B; カタログサービス &#x200B;](/help/catalog-service/overview.md)、[製品レコメンデーション &#x200B;](/help/product-recommendations/overview.md)、または[[!DNL Adobe Commerce Optimizer Connector]](/help/aco-connector/overview.md)に更新すると、最新バージョンのデータ書き出し拡張機能も取得できます。 データ書き出しメタパッケージは、これらのサービスのComposer パッケージの依存関係です。

1. Commerce アプリケーションサーバーにログインします。

1. コマンドラインから、Composerを使用してモジュールを更新します。

   ```bash
   composer require magento/module-data-exporter:103.0.4 --with-all-dependencies
   ```

Commerce インスタンスがクラウドインフラストラクチャにデプロイされている場合は、クラウドプロジェクトディレクトリから拡張機能を更新します。 _Adobe Commerce on Cloud Infrastructure ガイド_&#x200B;の[拡張機能のアップグレード &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension)を参照してください。

>[!MORELIKETHIS]
>
> - [&#x200B; リリースノート &#x200B;](release-notes.md)
> - [SaaS データ書き出しモジュール &#x200B;](reference/data-export-modules.md)
> - [&#x200B; ガイドの概要](overview.md)
