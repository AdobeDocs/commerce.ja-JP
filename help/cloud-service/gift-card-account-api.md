---
title: ギフトカードアカウントの REST エンドポイント
description: ' [!DNL Adobe Commerce as a Cloud Service] でギフトカードアカウント REST API を使用して、ギフトカードアカウントをプログラムで作成、更新、削除およびクエリする方法を説明します。'
role: Admin, Developer
level: Experienced
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
source-git-commit: 160180d9d779514f6faee3c7de46531ebf191c7d
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 0%

---

# ギフトカードアカウント API

{{accs-sandbox-experimental}}

ギフトカードアカウントの REST エンドポイントは、カートまたは見積もりレベルではなく、アカウントレベルでギフトカードアカウントをプログラム的に管理します。 この API を使用して、ギフトカードアカウントの作成、取得、更新、削除を行うか、JSON 読み込みエンドポイントを介してギフトカードアカウントを一括でプロビジョニングします。

これらのエンドポイントは、次の目的で設計されています。

* ギフトカードプログラムを管理する管理者
* サードパーティとの統合により、ERP、CRM、マーケティングプラットフォームなどの外部システムからギフトカードをプロビジョニング
* 一括ギフトカード作成の自動ワークフロー

## 認証

すべてのエンドポイントには、管理者または統合ベアラートークンが必要です。 トークンは、`Magento_GiftCardAccount::giftcardaccount` アクセス制御リスト （ACL） リソースを含む役割に関連付ける必要があります。

一括読み込み操作の場合、役割には `Magento_ImportExport::import_api` ACL リソースも含める必要があります。

## Web サイトとストアのコンテキスト

Web サイトおよびストアビューの値は、リクエスト本文ではなく、HTTP リクエストヘッダーから解決されます。 各リクエストで次のいずれかのヘッダーを渡します。

* `Store: <store_view_code>`
* `Magento-Website-Code: <website_code>`

API は、これらのヘッダーから web サイトを自動的に解決します。 REST リクエストペイロードに `website_id` を含めないでください。

>[!NOTE]
>
>一括読み込みエンドポイントは例外です。 読み込みは一括で動作し、特定の web サイトをターゲットにする可能性があるので、読み込みペイロードの各行には明示的な `website_id` 値が必要です。

## REST API リファレンス

API は、`/V1/giftcardaccounts` で以下の操作を公開します。これらの操作はすべて `Magento_GiftCardAccount::giftcardaccount` の ACL リソースによって保護されます。

| メソッド | URL | 説明 |
|--------|-----|-------------|
| POST | `/rest/V1/giftcardaccounts` | ギフトカードアカウントの作成 |
| GET | `/rest/V1/giftcardaccounts` | アカウントのリスト （searchCriteria をサポート） |
| GET | `/rest/V1/giftcardaccounts/:id` | ID でアカウントを取得 |
| GET | `/rest/V1/giftcardaccounts/code/:code` | コードによるアカウントの取得 |
| PUT | `/rest/V1/giftcardaccounts/:id` | アカウントの更新（結合セマンティクス） |
| DELETE | `/rest/V1/giftcardaccounts/:id` | アカウントを削除 |

### フィールド参照

| フィールド | タイプ | 有効な値 | REST 作成 | インポート |
|---|---|---|---|---|
| `code` | string | 最大 255 文字 | 必須 | 必須 |
| `balance` | float | >= 0 | 必須 | 必須 |
| `status` | int | `0` （無効）、`1` （有効） | （オプション、デフォルトは `1`） | （オプション、デフォルトは `1`） |
| `state` | int | `0` （使用可能）、`1` （使用中）、`2` （償還済み）、`3` （期限切れ） | （オプション、デフォルトは `0`） | （オプション、デフォルトは `0`） |
| `is_redeemable` | int | `0` 以 `1` | （オプション、デフォルトは `1`） | （オプション、デフォルトは `1`） |
| `date_expires` | string | `YYYY-MM-DD` または null | オプション | オプション |
| `date_created` | string | `YYYY-MM-DD` | 自動設定 | オプションです。省略した場合は自動設定されます |
| `website_id` | int | 有効な Web サイト ID | 許可されていません（ヘッダーから自動解決） | 必須 |

### ギフトカードアカウントの作成

重複コードの検出で新しいギフト カード アカウントを作成します。

| 項目 | 値 |
|---|---|
| **メソッド** | `POST` |
| **URL** | `/V1/giftcardaccounts` |

**リクエスト本文：**

```json
{
  "giftcardAccount": {
    "code": "GIFT-1234-ABCD",
    "balance": 100.00,
    "status": 1,
    "state": 0,
    "is_redeemable": 1,
    "date_expires": "2027-12-31"
  }
}
```

**応答（200）:**

```json
{
  "account_id": 42,
  "code": "GIFT-1234-ABCD",
  "balance": 100,
  "status": 1,
  "state": 0,
  "is_redeemable": 1,
  "date_expires": "2027-12-31",
  "date_created": "2026-03-12"
}
```

### ID によるギフトカードアカウントの取得

| 項目 | 値 |
|---|---|
| **メソッド** | `GET` |
| **URL** | `/V1/giftcardaccounts/:id` |

**応答（200）:**

1 つのギフト カード アカウント オブジェクトを返します。

### コードによるギフトカードアカウントの取得

| 項目 | 値 |
|---|---|
| **メソッド** | `GET` |
| **URL** | `/V1/giftcardaccounts/code/:code` |

>[!IMPORTANT]
>
>ギフトカードのコードが単なる数値（例えば `12345`）の場合、`/V1/giftcardaccounts/12345` へのリクエストは、コードルートではなく ID ルートに一致します。 コードが数値の可能性がある場合は、常に `/V1/giftcardaccounts/code/12345` を使用してコードベースの検索を行います。

**応答（200）:**

1 つのギフト カード アカウント オブジェクトを返します。

### 検索条件でギフト カード アカウントを一覧表示する

| 項目 | 値 |
|---|---|
| **メソッド** | `GET` |
| **URL** | `/V1/giftcardaccounts` |

検索条件をクエリパラメーターとして渡します。 次の例は、`status` が `1` である（有効である）ギフト カード アカウントを返します。

```text
GET /V1/giftcardaccounts?searchCriteria[filterGroups][0][filters][0][field]=status&searchCriteria[filterGroups][0][filters][0][value]=1&searchCriteria[pageSize]=10&searchCriteria[currentPage]=1
```

**応答（200）:**

```json
{
  "items": [
    {
      "account_id": 42,
      "code": "GIFT-1234-ABCD",
      "balance": 100,
      "status": 1,
      "state": 0,
      "is_redeemable": 1,
      "date_expires": "2027-12-31",
      "date_created": "2026-03-12"
    }
  ],
  "search_criteria": { ... },
  "total_count": 1
}
```

### ギフト カード アカウントの更新

結合セマンティクスを使用して既存のギフトカードアカウントを更新します。 リクエスト内の null 以外のフィールドのみが適用されます。 `code` フィールドは不変です。 別のコードを渡すと、検証エラーが返されます。

| 項目 | 値 |
|---|---|
| **メソッド** | `PUT` |
| **URL** | `/V1/giftcardaccounts/:id` |

**リクエスト本文：**

```json
{
  "giftcardAccount": {
    "balance": 75.00,
    "status": 1
  }
}
```

**応答（200）:**

更新されたギフト カード アカウント オブジェクトを返します。

### ギフト カード アカウントの削除

| 項目 | 値 |
|---|---|
| **メソッド** | `DELETE` |
| **URL** | `/V1/giftcardaccounts/:id` |

**応答（200）:**

```json
true
```

## JSON を使用した一括読み込み

ギフトカードアカウントは、エンティティタイプ `POST /V1/import/json` の `giftcardaccount` を使用して一括でプロビジョニングできます。 このエンドポイントには、ギフト カード アカウントの ACL に加えて、`Magento_ImportJsonApi::import_api` アクセス制御リスト （ACL） リソースが必要です。

### サポートされる動作

| 動作 | 説明 |
|---|---|
| `append` | 新しいギフト カード アカウントを作成します。 コードが既に存在する場合、その行は失敗し、残りの行でインポートが続行されます。 |
| `replace` | コード別にギフト カード アカウントを更新および挿入します。 コードが存在しない場合はアカウントを作成し、存在する場合は置換します。 |
| `delete` | コード別のギフト カード アカウントを削除します。 |

### リクエストの例

```json
{
  "source": {
    "entity": "giftcardaccount",
    "behavior": "append",
    "validation_strategy": "validation-stop-on-errors",
    "allowed_error_count": "10",
    "items": [
      {
        "code": "BULK-001",
        "balance": 50.00,
        "website_id": 1,
        "status": 1,
        "state": 0,
        "is_redeemable": 1,
        "date_expires": "2027-06-30"
      },
      {
        "code": "BULK-002",
        "balance": 25.00,
        "website_id": 1
      }
    ]
  }
}
```

### 動作の詳細をインポート

* リクエストヘッダーから web サイトを推測する REST エンドポイントとは異なり、インポートペイロードの各行には明示的な `website_id` が必要です。
* 各行は個別に検証されます。 無効な行は、同じバッチ内の有効な行に影響を与えずに、行ごとのエラーを生成します。
* 同じバッチ内の重複コードは、トランザクションのロールバックを引き起こすことなく、検出され、行ごとのエラーとしてレポートされます。
* 読み込みは、パフォーマンスを向上させるためにデータベースに直接書き込み、ベンダーモデルの保存ライフサイクルをバイパスします。 残高変更履歴項目は、インポート時には作成されません。
* REST 作成操作で、過去の有効期限が却下されます。 過去のデータ移行をサポートするために、読み込みは設計によって過去の有効期限を受け入れます。

## エラー処理

この API は次の標準 HTTP ステータスコードを返します。

| ステータスコード | 条件 |
|---|---|
| `400` | 検証エラー。 REST 作成に必須フィールドがない、無効な値がある、または過去の有効期限がある。 |
| `401` | ベアラートークンがないか無効です。 |
| `403` | トークンに必要な ACL リソースがありません。 |
| `404` | ギフト カード アカウントが見つかりません。 |
| `409` | ギフト カード コードを複製します。 |

入力検証では、必須フィールド、値範囲（ステータスは `0` または `1`、状態は `0` から `3`、残高は負以外）、日付形式、およびタイプの安全性が対象となります。 数値フィールドの数値以外の値は拒否されます。
