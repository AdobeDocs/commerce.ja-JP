---
title: '[!DNL Manage the Data Export extension]'
description: ' [!DNL Data Export] 拡張機能をアップグレードし、必要のないデータ書き出しサービスを削除または無効にする方法を説明します。'
role: Admin, Developer
exl-id: 94702995-d272-47b9-9560-198eee3250a6
TQID: https://experienceleague.adobe.com/ghrA-YFR7hurQgEnjS8PdxR7Zcx-ayLTuyBfhbCC-KI
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 256
ht-degree: 0%

---

# SaaS データ書き出し拡張機能の管理

SaaS サービスの[[!DNL data export] extension](https://github.com/magento/commerce-data-export)は、Adobe Commerceと接続されたCommerce サービス間のデータの収集と同期を可能にするモジュールのコレクションです。

Adobe Commerce サービス拡張機能のメタパッケージには、次のような特定のモジュールが含まれています
[ ライブサーチ ](/help/live-search/overview.md)、[商品レコメンデーション ](/help/product-recommendations/overview.md)、[ カタログサービス ](/help/catalog-service/overview.md)として使用できます。 これらのサービスを使用している場合、Data Export拡張機能を有効にするために個別のインストールは必要ありません。

## Commerce データ書き出し機能の削除または無効化

インストールされているコマースデータ書き出しモジュールのいずれかが必要ない場合は、`magento:module:disable` CLI コマンドを使用して無効にします。

例えば、カテゴリ権限フィード データを内部で使用する[Categories API](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/)があります。 このAPIを使用していない場合は、カテゴリ権限フィードのデータ書き出しを無効にできます。

```shell script
bin/magento module:disable Magento_CategoryPermissionDataExporter Magento_SaaSCategoryPermissions
```

### モジュールを特定のバージョンに更新する

Composerを使用すると、インストールされているコマースデータ書き出しモジュールのいずれかを更新できます。 例えば、モジュールを指定したバージョンに更新したり、必要な依存関係を更新したりできます。

1. Commerce アプリケーションサーバーにログインします。

1. コマンドラインから、Composerを使用してモジュールを更新します。

   ```bash
   composer require magento/module-data-exporter:103.0.4 --with-all-dependencies
   ```

Commerce インスタンスがクラウドインフラストラクチャにデプロイされている場合は、クラウドプロジェクトディレクトリから拡張機能を更新します。 _Adobe Commerce on Cloud Infrastructure ガイド_&#x200B;の[拡張機能のアップグレード ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension)を参照してください。
