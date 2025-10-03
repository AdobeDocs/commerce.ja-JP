---
title: '[!DNL Manage the Data Export extension]'
description: 拡張機能をアップグレードする方法と  [!DNL Data Export]  不要なデータ書き出しサービスを削除または無効にする方法について説明します。
role: Admin, Developer
exl-id: 94702995-d272-47b9-9560-198eee3250a6
source-git-commit: ea722d5e427e5bf536b9f2d2322f0dabb2981c77
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# SaaS データ書き出し拡張機能の管理

SaaS サービスの [[!DNL data export]  拡張機能 ](https://github.com/magento/commerce-data-export) は、Adobe Commerceと接続されたCommerce サービス間でのデータ収集と同期を可能にするモジュールの集まりです。

Adobe Commerce サービス拡張機能のメタパッケージには、次のような特定のモジュールが含まれています
[Live Search](/help/live-search/overview.md)、[Product Recommendations](/help/product-recommendations/overview.md)、および [ カタログサービス ](/help/catalog-service/overview.md) として。 これらのサービスを使用している場合、データの書き出し拡張機能を有効にするために別のインストールは必要ありません。

## Commerceのデータ書き出し機能を削除または無効にする

インストールされているコマースデータ書き出しモジュールが必要ない場合は、`magento:module:disable` CLI コマンドを使用して無効にします。

例えば、カテゴリ権限フィードデータを内部的に使用する [Categories API](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) があります。 この API を使用していない場合は、カテゴリ権限フィードのデータ書き出しを無効にできます。

```shell script
bin/magento module:disable Magento_CategoryPermissionDataExporter Magento_SaaSCategoryPermissions
```

### 特定のバージョンにモジュールを更新する

インストールされているコマースデータ書き出しモジュールは、Composer を使用して更新できます。 例えば、指定したバージョンにモジュールを更新し、必要な依存関係も更新できます。

1. Commerce アプリケーションサーバーにログインします。

1. コマンドラインから、Composer を使用してモジュールを更新します。

   ```bash
   composer require magento/module-data-exporter:103.0.4 --with-all-dependencies
   ```

Commerce インスタンスがクラウドインフラストラクチャにデプロイされている場合は、クラウドプロジェクトディレクトリから拡張機能を更新します。 [2}Cloud Infrastructure ガイドのAdobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension) 拡張機能のアップグレード _を参照してください。_
