---
title: ワンタイムコードで顧客としてログイン
description: 顧客 OTC としてログイン機能を使用して、 [!DNL Adobe Commerce as a Cloud Service] で顧客認証用の 1 回限りのコードを生成する方法を説明します。
role: Admin
level: Intermediate
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
source-git-commit: 160180d9d779514f6faee3c7de46531ebf191c7d
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---

# 顧客としてログイン

{{accs-sandbox-experimental}}

顧客 OTC （ワンタイムコード）としてログイン機能を使用すると、管理者ユーザーは、顧客に対して短期間有効な単一使用のコードを生成できます。 このコードは、GraphQLを通じてカスタマーアクセストークンと交換でき、売り手が支援する買い物かごのパスワードレス **顧客としてログイン** ワークフローを有効にします。

顧客としてのログインは、次のコンポーネントで構成されています。

* **管理 UI** – 管理者は、顧客の編集ページで、顧客として直接ログインするのではなく、ワンタイムコード（OTC）をリクエストできます。
* **REST API** - OTC 生成用のプログラムによるエンドポイント。管理スクリプトやサードパーティ統合に役立ちます。
* **GraphQL API** - ストアフロントまたはヘッドレスコマースフロー用の顧客アクセストークンと OTC を交換するミューテーション。

## 管理者から 1 回限りのコードを生成

カスタマー OTC としてログインは、カスタマー編集ページの標準のカスタマーとしてログイン ボタンを [!UICONTROL **カスタマー OTC としてログイン**] ボタンに置き換えます。 生成された 1 回限りのコードは、販売者の支援を受けた買い物のためにストアフロントまたはGraphQLで使用できます。

>[!NOTE]
>
>「受注」、「請求書」、「出荷」および「クレジット・メモ」ページでは、「**顧客としてログイン**」ボタンは使用できません。

### 前提条件

顧客としてログイン機能を使用するには、次の要件を満たす必要があります。

* **管理者権限** – 顧客としてログインするには、管理者ユーザーの管理者ロールで `Magento_LoginAsCustomer::login` アクセス制御リスト （ACL）権限が有効になっている必要があります。

* **顧客の同意** – 顧客は、`login_as_customer_assistance_allowed` 拡張機能の属性を **2 に設定する必要があります**。 これは、管理者の **カスタマーを編集** ページで設定することも、カスタマーを作成または編集する際にGraphQLを通じて設定することもできます。

  ![ 顧客の編集ページの顧客同意拡張属性の設定 ](./assets/customer-consent-attribute.png){width="600" zoomable="yes"}

* **カスタマーとしてログインが有効** - カスタマーとしてログイン拡張機能が無効な場合、カスタマーとしてログイン機能は使用できません。 拡張機能が有効であることを確認するには、[!UICONTROL **ストア**]/[!UICONTROL **設定**]/[!UICONTROL **顧客**]/[!UICONTROL **顧客としてログイン**]/[!UICONTROL **拡張機能を有効にする**] に移動します。

### ワンタイムコード（OTC）のリクエスト

1. [!UICONTROL **顧客**] に移動して顧客を選択し、編集ページを開きます。

1. 顧客の編集ページで、「[!UICONTROL **顧客ログイン OTC の取得**]」をクリックします。

   ![ 顧客の編集ページの [ 顧客ログイン OTC の取得 ] ボタン ](./assets/get-customer-login-otc-button.png){width="600" zoomable="yes"}

1. [!UICONTROL **理由**] （必須）を入力し、「[!UICONTROL **リクエスト**]」をクリックします。

   ![ 理由フィールドを含む OTC リクエストモーダル ](./assets/otc-reason-modal.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   >**理由** フィールドは必須です。 OTP 生成フローに渡され、今後の監査およびイベントログ機能で使用するために予約されています。

1. 生成された OTC がモーダルに表示されます。 このコードを `generateCustomerToken` またはGraphQL mutation と共 `exchangeOtpForCustomerToken` 使用して、お客様の承認を得ます。

   ![ 生成された OTC がモーダルに表示される ](./assets/otc-generated-code.png){width="300" zoomable="yes"}

>[!IMPORTANT]
>
>生成されたワンタイムコード OTC は、デフォルトで 30 秒間有効で、1 回使用した後に無効になります。 TTL は、`customer/otp/ttl_seconds` 設定を使用して CPS を通じて設定できます。

ワンタイムコードが生成されたら、ストアフロントに移動し、次の資格情報を使用してログインすることで、このコードを使用できます。

* **メール**：顧客のメールアドレス
* **パスワード**：生成されたワンタイムコード（OTC）

## REST API を使用した 1 回限りのコードの生成

POST `V1/customer/:customerId/otp` エンドポイントは、顧客の OTC を生成するプログラム的な方法を提供します。 これは、OTC 発行を一貫してトリガーする必要がある管理 UI、スクリプト、またはサードパーティ統合で役立ちます。

### REST 契約

| 項目 | 値 |
|---|---|
| **メソッド** | POST |
| **URL** | `/rest/V1/customer/:customerId/otp` |
| **認証** | 管理トークン（ベアラー）。 必須 ACL: `Magento_LoginAsCustomer::login`。 |
| **リクエスト本文** | オプションの `reason` フィールドを含む JSON。 監査およびログに使用します。 |
| **成功応答** | HTTP 200、`otp` を含む JSON （32 文字の 16 進文字列）。 |
| **エラー応答** | 標準 Web API エラー（401、403 など）。 お客様のカスタマーサポートとしてログインが無効になっている場合、が 500 またはマッピングされた例外として表示される場合があります。 |

### リクエストの例

```text
POST /rest/V1/customer/:customerId/otp
Content-Type: application/json
```

```json
{"reason": "Support session"}
```

### 応答の例

```json
{"otp": "a1b2c3d4e5f6789012345678abcdef01"}
```

## GraphQLを使用した 1 回限りのコードのカスタマートークンへの交換

（管理 UI または REST API から） OTC を生成した後、次のいずれかのGraphQLのミューテーションを使用して、お客様のアクセストークンと交換します。

### `generateCustomerToken` 変異

`generateCustomerToken(email, password)` のミューテーションは、顧客トークンを返します。 `password` 引数は次の順序で評価されます。

1. **顧客パスワード（デフォルト）** – 顧客のアカウントのパスワード。
1. **顧客リセットパスワードトークン（1 回限りの使用）** - **パスワードを忘れた場合** の有効なトークン（`requestPasswordResetEmail` ミューテーションなど）。 初回の使用時に使用されます。
1. **管理者生成の OTC （ワンタイムコード）** - REST API または管理 UI を使用して管理者が顧客用に生成したコード。 1 回限りの短時間のみ有効（デフォルトは 30 秒）。

**スキーマ：**

```graphql
type Mutation {
  generateCustomerToken(email: String!, password: String!): CustomerToken
}

type CustomerToken {
  token: String!
}
```

**例：管理者 OTC でログイン**

```graphql
mutation GenerateCustomerToken($email: String!, $password: String!) {
  generateCustomerToken(email: $email, password: $password) {
    token
  }
}
```

変数（OTC を `password` として使用）:

```json
{
  "email": "customer@example.com",
  "password": "<admin-generated-OTC>"
}
```

**例：パスワードを使用したログイン**

```graphql
mutation GenerateCustomerToken($email: String!, $password: String!) {
  generateCustomerToken(email: $email, password: $password) {
    token
  }
}
```

変数：

```json
{
  "email": "customer@example.com",
  "password": "CustomerPassword123"
}
```

**例：パスワードリセットトークンを使用したログイン**

顧客がパスワードリセットをリクエストした後（例：`requestPasswordResetEmail`）、メールリンクを通じて受け取ったリセットトークンを `password` で `generateCustomerToken` のように使用できます（1 回限りの使用）。

```graphql
mutation GenerateCustomerToken($email: String!, $password: String!) {
  generateCustomerToken(email: $email, password: $password) {
    token
  }
}
```

変数（リセットトークンを `password` として使用）:

```json
{
  "email": "customer@example.com",
  "password": "<reset-password-token-from-email-link>"
}
```

**応答の例：**

```json
{
  "data": {
    "generateCustomerToken": {
      "token": "<customer-access-token>"
    }
  }
}
```

### `exchangeOtpForCustomerToken` 変異

`exchangeOtpForCustomerToken` ミューテーションは、管理者が生成したパスワードリセットトークンまたは OTP を顧客アクセストークンと交換します。 OTP は、交換が成功した後（1 回限りの使用）、無効になります。 このエンドポイントは、reCAPTCHA 設定に従います。

**スキーマ：**

```graphql
type Mutation {
  exchangeOtpForCustomerToken(
    email: String!
    otp: String!
  ): CustomerToken
}

type CustomerToken {
  token: String!
}
```

**リクエストの例：**

```graphql
mutation ExchangeOtpForCustomerToken($email: String!, $otp: String!) {
  exchangeOtpForCustomerToken(email: $email, otp: $otp) {
    token
  }
}
```

変数：

```json
{
  "email": "customer@example.com",
  "otp": "<one-time-password>"
}
```

**応答の例：**

```json
{
  "data": {
    "exchangeOtpForCustomerToken": {
      "token": "<customer-access-token>"
    }
  }
}
```

### 突然変異概要

| 突然変異 | ユースケース |
|---|---|
| `generateCustomerToken(email, password)` | 単一のエントリポイント：顧客のパスワード、パスワードリセットトークン、管理者の OTC、または OTP （パスワード/リセット後に試行）。 |
| `exchangeOtpForCustomerToken(email, otp)` | OTP またはリセット パスワード トークンの交換。 OTP （またはリセットパスワードトークン）は使用後に消費されます。 |

パスワードリセットトークンと管理者 OTC はどちらも `password` 引数として `generateCustomerToken` に渡されます。 リゾルバーはトークンタイプを検出し、それに応じて検証します。
