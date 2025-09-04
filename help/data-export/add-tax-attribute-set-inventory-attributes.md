---
title: 税区分、属性セットおよび在庫属性の追加
description: 製品フィードデータを拡張して、税分類、属性セット、高度な在庫設定の属性を含める方法について説明します
role: Admin, Developer
badgePaas: label="PaaS のみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/
source-git-commit: 6abfeca68ab67fb11493f78440e09408479e1535
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# 税区分、属性セットおよび在庫属性の追加

Adobe Commerceの追加製品属性モジュールは、製品データフィードを拡張します。 これには、Adobe Commerce製品コンフィギュレーションからの追加の製品属性が含まれます。

* [ 税分 ](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/taxes/tax-class)
* [ 属性セット ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-sets)
* [ 在庫 ](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/product-options#advanced-product-options)

インストールが完了すると、モジュールは自動的に動作します。 製品の同期中に、追加の属性を取得して書き出します。 追加の設定は必要ありません。

## 主なメリット

* **自動拡張**：税金区分、属性セットおよび在庫属性で製品フィードを強化します
* **シームレスな統合**：外部のシステムやサービスに不可欠なコンテキストを提供します
* **ゼロ設定**：インストール直後に動作
* **リアルタイムの更新**：製品の変更を自動的に同期します

## 機能と書き出された属性

モジュールでは、既存の製品データフィードに次の 3 つの属性を追加します。

* `ac_tax_class`
* `ac_attribute_set`
* `ac_inventory`

### 1.税クラス情報（`ac_tax_class`）

**目的**：各製品の税分類情報を提供します

**データ形式**：税金区分名を含む文字列値

**出力例**:

```json
{
  "attributes": [
    {
      "code": "ac_tax_class",
      "values": ["Taxable Goods"]
    }
  ]
}
```

**ユースケース**:

Commerce カタログサービスに税クラスデータを書き出すと、次の項目をサポートするアプリケーションでこのデータを使用できるようになります。

* 税務コンプライアンスレポート
* 外部税計算サービスとの統合
* 会計システムの製品分類

### 2.属性セット情報（`ac_attribute_set`）

**目的**：各製品に割り当てる属性セットを識別します

**データ形式**：属性セット名を含む文字列値

**出力例**:

```json
{
  "attributes": [
    {
      "code": "ac_attribute_set",
      "values": [
        "Default"
      ]
    }
  ]
}
```

**ユースケース**:

属性セットデータをCommerce カタログサービスに書き出すと、外部システムでの高度な商品管理機能が有効になります。 次のような機能があります。

* 製品テンプレートの識別
* カタログの管理と編成
* 属性セットコンテキストが必要なサードパーティシステム統合

### 3.事前在庫データ（`ac_inventory`）

**目的**：各製品の在庫管理設定を提供します

**データ形式**：インベントリ設定を含む、JSON エンコードされた文字列

**含まれるフィールド**:

* `manageStock` （ブール値）：在庫管理が有効かどうか
* `cartMinQty` （フロート）：買い物かごで許可される最小数量
* `cartMaxQty` （浮動小数）：買い物かごで許可される最大数量
* `backorders` （string）：バックオーダーポリシー。 値は次のいずれかです。
   * `"no"`: バックオーダーは許可されていません
   * `"allow"`：数量が 0 未満の許可
   * `"allow_notify"`: 0 未満の数量を許可し、お客様に通知します
* `enableQtyIncrements` （ブール値）：数量の増分を有効にするかどうかを指定します
* `qtyIncrements` （浮動小数）：必要な増分値

**出力例**:

```json
{
  "attributes": [
    {
      "code": "ac_inventory",
      "values": [
        "{\"manageStock\":true,\"cartMinQty\":2,\"cartMaxQty\":42,\"backorders\":\"no\",\"enableQtyIncrements\":false,\"qtyIncrements\":2}"
      ]
    }
  ]
}
```

**ユースケース**:

在庫データをCommerce カタログサービスに書き出すと、外部システムの高度な在庫管理機能が有効になります。 次のような機能があります。

* Inventory management システムの統合
* 買い物かご検証ルール
* 注文フルフィルメントプロセスの最適化
* 顧客体験のカスタマイズ

## データエクスポートフィードの機能強化

追加製品属性モジュールは、既存の製品フィードを強化します。 新しい属性データが自動的に統合されます。

* **製品フィード** （`products`）:3 つの追加属性で強化されました

   * 各製品レコードに `ac_tax_class`、`ac_attribute_set`、`ac_inventory` 属性を追加します
   * 元の製品データは変更されません
   * 既存のフィードコンシューマーとの下位互換性を維持します

* **製品属性フィード** （`productAttributes`）：新しい属性の属性メタデータで強化されました

   * `productAttributes` フィードの 3 つの新しい属性のメタデータを自動的に登録します
   * 属性設定の詳細（データタイプ、表示設定など）を提供します
   * 外部システムが新しい属性スキーマを理解するのに役立ちます

## 拡張機能のインストール

**要件**

* PHP 8.1、8.2、8.3、または 8.4
* Adobe Commerce 2.4.4 以降
* [Adobe Commerce Data Export extension](manage-extension.md#update-a-module-to-a-specific-version)、バージョン 103.4.11 以降
* [repo.magento.com](https://repo.magento.com) へのアクセス

  キーを生成し必要な権限を取得するには、[ 認証キーの取得 ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) を参照してください。 クラウドインストールについては、[Commerce on Cloud Infrastructure ガイド ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/authentication-keys) を参照してください。
* Adobe Commerce アプリケーションサーバーのコマンドラインにアクセスします。

### インストール手順

Composer を使用して `adobe-commerce/module-extra-product-attributes` モジュールを追加します。

```shell
composer require adobe-commerce/module-extra-product-attributes
```

インストール手順について詳しくは、次のガイドを参照してください。

* [ クラウドインフラストラクチャー上のAdobe Commerceに拡張機能をインストール ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
* [ 拡張機能Adobe Commerceをオンプレミスでインストール ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extension)

## 製品データの同期

再デプロイメント後、Adobe Commerce インスタンスは、製品の同期中に追加のデータを自動的に書き出します。 `resync` の CLI コマンドを使用して、即座に同期することもできます。

```shell
# Resync the products feed (includes the new attributes)
bin/magento saas:resync --feed=products
```

```shell
# Resync the product attributes feed (includes new attribute metadata)
bin/magento saas:resync --feed=productAttributes
```

## トラブルシューティング

**製品に追加属性がありません：**

* モジュールが正しくインストールされ、有効になっていることを確認します
* 製品データを更新するには、再同期コマンドを実行します
* 製品に有効な税区分と属性セットの割り当てがあることを確認します

**インベントリデータが正しく表示されない：**

* 管理画面でインベントリ設定が正しく構成されていることを確認します
* Web サイト固有のインベントリの上書きを確認する
* [Inventory management モジュール ](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/guide-overview) が正しく動作していることを確認します

詳しくは、[Adobe Commerce マーチャントドキュメント ](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/guide-overview)*Inventory managementガイド* を参照してください。

**パフォーマンス上の問題：**

* インストール後のエクスポートプロセスのパフォーマンスの監視
* 低トラフィックの期間には再同期のスケジュールを検討する

### ログとデバッグ

モジュールログでは、標準のCommerce ログシステムにエラーと警告が書き出されます。 製品の同期中に問題が発生した場合は、データの書き出しログを確認します。

詳しくは、[ ログの確認とトラブルシューティング ](troubleshooting-logging.md) を参照してください。

