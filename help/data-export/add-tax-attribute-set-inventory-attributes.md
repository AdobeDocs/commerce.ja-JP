---
title: 税区分、属性セットおよび在庫属性の追加
description: 商品フィード データを拡張して、税分類、属性セット、および高度な在庫設定の属性を含める方法について説明します
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/
TQID: https://experienceleague.adobe.com/AWc-yAn-TyiBXQONoF2ZG9SFjj2u92CKbKvAY8mEVEE
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 822
ht-degree: 0%

---

# 税区分、属性セットおよび在庫属性の追加

Adobe Commerce Extra Product Attributes モジュールは、商品データフィードを拡張します。 これには、Adobe Commerceの製品設定から追加の製品属性が含まれます。

* [税分類](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/taxes/tax-class)
* [属性セット](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-sets)
* [在庫](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/product-options#advanced-product-options)

インストールすると、モジュールは自動的に動作します。 製品の同期中に、追加の属性をキャプチャし、書き出します。 追加の設定は必要ありません。

## 主な特長

* **自動拡張**：税区分、属性セットおよび在庫属性を使用して製品フィードを強化します
* **シームレスな統合**：外部システムとサービスに必要なコンテキストを提供します
* **設定なし**: インストール直後に動作します
* **リアルタイム更新**：製品の変更と自動的に同期

## 機能と書き出された属性

このモジュールは、既存の製品データフィードに3つの追加属性を追加します。

* `ac_tax_class`
* `ac_attribute_set`
* `ac_inventory`

### &#x200B;1. 税区分の情報（`ac_tax_class`）

**目的**：各製品の税分類情報を提供します

**データ形式**：税種名を含む文字列値

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

税区分データをCommerce カタログサービスに書き出すと、このデータは次をサポートするアプリケーションで使用できるようになります。

* 税務コンプライアンスレポート
* 外部税計算サービスとの統合
* 会計システム向け製品カテゴリ

### &#x200B;2. 属性セット情報（`ac_attribute_set`）

**目的**：各製品に割り当てられている属性セットを特定します

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

属性セットデータをCommerce カタログサービスに書き出すと、外部システムで高度な製品管理機能が有効になります。 主な機能は次のとおりです。

* 製品テンプレートの特定
* カタログの管理と整理
* 属性セットコンテキストを必要とするサードパーティシステム統合

### &#x200B;3. 高度な在庫データ （`ac_inventory`）

**目的**：各製品の在庫管理設定を提供します

**データ形式**: インベントリ設定を含むJSON エンコードされた文字列

**含まれるフィールド**:

* `manageStock` （ブール値）：在庫管理が有効になっているかどうか
* `cartMinQty` （浮動小数）: ショッピングカートで許可される最小数量
* `cartMaxQty` （浮動小数）: ショッピングカートで許可される最大数量
* `backorders` （文字列）: バックオーダーポリシー。 値は次のいずれかです。
   * `"no"`：取り寄せ注文は許可されていません
   * `"allow"`：数量が0未満の場合
   * `"allow_notify"`:0未満の数量を許可し、お客様に通知
* `enableQtyIncrements` （ブール値）：数量の増分が有効かどうか
* `qtyIncrements` （浮動小数）：必要な数量の増分値

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

在庫データをCommerce カタログサービスに書き出すと、外部システムで高度な在庫管理機能が有効になります。 主な機能は次のとおりです。

* Inventory managementとの連携
* ショッピングカート検証ルール
* 注文フルフィルメントプロセスの最適化
* 顧客体験のカスタマイズ

## データ書き出しフィードの強化

製品属性の追加モジュールは、既存の製品フィードを強化します。 新しい属性データが自動的に統合されます。

* **製品フィード** （`products`）: 3つの追加属性で強化されました

   * 各製品レコードに`ac_tax_class`、`ac_attribute_set`および`ac_inventory`属性を追加します
   * 元の商品データを保持
   * 既存のフィード コンシューマーとの下位互換性を維持

* **製品属性フィード** （`productAttributes`）：新しい属性の属性メタデータで強化

   * `productAttributes` フィードに3つの新しい属性のメタデータを自動的に登録します
   * 属性設定の詳細（データタイプ、表示設定など）を提供します。
   * 外部システムが新しい属性スキーマを理解するのに役立つ

## 拡張機能のインストール

**要件**

* PHP 8.1、8.2、8.3、または8.4
* Adobe Commerce 2.4.4以降
* [Adobe Commerce Data Export拡張機能](manage-extension.md#update-a-module-to-a-specific-version)、バージョン 103.4.11以降
* [repo.magento.com](https://repo.magento.com)へのアクセス

  キーを生成し、必要な権限を取得するには、[認証キーを取得](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)するを参照してください。 クラウドインストールについては、「[Commerce on Cloud Infrastructure Guide](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/authentication-keys)」を参照してください。
* Adobe Commerce アプリケーションサーバーのコマンドラインにアクセスします。

### インストール手順

Composerを使用して`adobe-commerce/module-extra-product-attributes` モジュールを追加します。

```shell
composer require adobe-commerce/module-extra-product-attributes
```

インストール手順の詳細については、次のガイドを参照してください。

* [Adobe Commerce on Cloud Infrastructureへの拡張機能のインストール](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
* [拡張機能Adobe Commerce オンプレミスのインストール](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)

## 製品データの同期

再デプロイメント後、Adobe Commerce インスタンスは、製品の同期中に追加データを自動的に書き出します。 また、`resync` CLI コマンドを使用して、即座に同期することもできます。

```shell
# Resync the products feed (includes the new attributes)
bin/magento saas:resync --feed=products
```

```shell
# Resync the product attributes feed (includes new attribute metadata)
bin/magento saas:resync --feed=productAttributes
```

## トラブルシューティング

**追加属性が見つからない製品：**

* モジュールが適切にインストールされ、有効になっていることを確認します
* 再同期コマンドを実行して製品データを更新する
* 製品に有効な税区分と属性セットの割り当てがあることを確認します

**在庫データが正しくありません：**

* 管理画面で在庫設定が正しく設定されていることを確認します
* web サイト固有のインベントリの上書きを確認する
* [Inventory management モジュール &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/guide-overview)が正しく動作していることを確認します

詳しくは、*Inventory managementのマーチャント向けドキュメント*&#x200B;の[Adobe Commerce ガイド &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/guide-overview)を参照してください。

**パフォーマンスに関する懸念事項：**

* インストール後の書き出しプロセスのパフォーマンスを監視する
* トラフィックが少ない期間には再同期のスケジュールを検討する

### ログとデバッグ

モジュールは、エラーと警告を標準のCommerce ロギングシステムに書き出します。 製品の同期中に問題が発生した場合は、データ書き出しログを確認してください。

>[!MORELIKETHIS]
>
> * [&#x200B; ログの確認とトラブルシューティング &#x200B;](troubleshooting/logging.md)
> * [SaaS データ書き出しフィードの拡張とカスタマイズ &#x200B;](extensibility-and-customizations.md)
> * [Commerce CLIを使用してフィードを同期](data-export-cli-commands.md)

