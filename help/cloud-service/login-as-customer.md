---
title: 1回限りのコードを使用して顧客としてログイン
description: 顧客OTCとしてログイン機能を使用して、 [!DNL Adobe Commerce as a Cloud Service]で顧客認証用の1回限りのコードを生成する方法を説明します。
role: Admin
level: Intermediate
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"
source-git-commit: 2de1006ad3cee936d114bcf1b9a98b43a54d8c76
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# 顧客としてログイン

{{accs-sandbox-experimental}}

顧客OTC （ワンタイムコード）としてログイン機能を使用すると、管理者ユーザーは顧客の短期間有効なシングルユースコードを生成できます。 このコードは、GraphQLを通じて顧客アクセストークンと交換でき、出品者が支援するショッピング シナリオのパスワードなし&#x200B;**顧客としてログイン** ワークフローを有効にします。

お客様としてのログインは、次のコンポーネントで構成されます。

* **管理者UI** – 顧客の編集ページでは、管理者は顧客として直接ログインする代わりに、1回限りのコード （OTC）をリクエストできます。
* **REST API** - OTC生成用のプログラマティック エンドポイントで、管理者スクリプトやサードパーティの統合に役立ちます。
* **GraphQL API** - OTCをストアフロントまたはヘッドレスコマースフロー用の顧客アクセストークンと交換するミューテーション。

## 管理者から1回限りのコードを生成

顧客OTCとしてログインは、顧客編集ページの顧客として標準ログイン ボタンを&#x200B;[!UICONTROL **顧客ログイン OTC**] ボタンに置き換えます。 生成された1回限りのコードは、ストアフロントまたはGraphQLで出品者が支援するショッピングに使用できます。

>[!NOTE]
>
>**顧客としてログイン** ボタンは、注文、請求書、出荷、クレジットメモの各ページでは使用できません。

### 前提条件

お客様としてログイン機能を使用する前に、次の要件を満たす必要があります。

* **管理者権限** – 管理者ユーザーが顧客としてログインするには、管理者ロールで`Magento_LoginAsCustomer::login` アクセス制御リスト （ACL）権限を有効にする必要があります。

* **顧客の同意** – 顧客は`login_as_customer_assistance_allowed`拡張機能の属性を&#x200B;**2**&#x200B;に設定する必要があります。 これは、お客様を作成または編集する際に、管理者またはGraphQLの&#x200B;**お客様を編集** ページで設定できます。

  ![顧客の編集ページでの顧客の同意拡張機能の属性設定](./assets/customer-consent-attribute.png){width="600" zoomable="yes"}

* **お客様の拡張機能としてログインが有効** – お客様の拡張機能としてログインが無効になっている場合、お客様としてログイン機能を使用できません。 拡張機能が有効になっていることを確認するには、[!UICONTROL **ストア**] > [!UICONTROL **設定**] > [!UICONTROL **顧客**] > [!UICONTROL **顧客**] > [!UICONTROL **拡張機能を有効にする**]&#x200B;に移動します。

### ワンタイムコード（OTC）のリクエスト

1. 「[!UICONTROL **お客様**]」に移動し、お客様を選択して編集ページを開きます。

1. お客様を編集ページで、[!UICONTROL **お客様のログイン情報を取得**]&#x200B;をクリックします。

   ![お客様のページの「お客様ログイン OTCを取得」ボタン ](./assets/get-customer-login-otc-button.png){width="600" zoomable="yes"}

1. [!UICONTROL **理由**] （必須）を入力し、[!UICONTROL **リクエスト**]&#x200B;をクリックします。

   理由フィールド ![を持つ](./assets/otc-reason-modal.png){width="600" zoomable="yes"}OTC リクエストモーダル

   >[!NOTE]
   >
   >**Reason** フィールドは必須です。 OTP生成フローに渡され、今後の監査およびイベントログ機能で使用するために予約されます。

1. 生成されたOTCがモーダルに表示されます。 このコードを、お客様の認証に`generateCustomerToken`または`exchangeOtpForCustomerToken`個のGraphQL変異と共に使用します。

   ![生成されたOTCがモーダルに表示されます](./assets/otc-generated-code.png){width="300" zoomable="yes"}

>[!IMPORTANT]
>
>生成されたワンタイムコード OTCは、デフォルトで30秒間有効で、1回使用すると無効になります。 TTLは、[ サポートチケット ](https://experienceleague.adobe.com/home?support-tab=home#support)を送信することで設定できます。

ワンタイムコードが生成されたら、ストアフロントに移動し、次の資格情報を使用してログインすることで使用できます。

* **電子メール**：顧客の電子メールアドレス
* **パスワード**：生成されたワンタイムコード （OTC）

## REST APIを使用してワンタイムコードを生成する

POST `V1/customer/:customerId/otp` エンドポイントは、顧客のOTCをプログラムで生成する方法を提供します。 これは、OTC発行を一貫してトリガーする必要がある管理者UI、スクリプト、またはサードパーティ統合で便利です。

### REST契約

| 項目 | 値 |
|---|---|
| **メソッド** | 投稿する |
| **URL** | `/rest/V1/customer/:customerId/otp` |
| **認証** | 管理トークン（ベアラー）: 必須ACL: `Magento_LoginAsCustomer::login`。 |
| **リクエスト本文** | オプションの`reason` フィールドを含むJSON。 監査とログ記録に使用されます。 |
| **成功応答** | HTTP 200、JSON、`otp` （32文字の16進文字列）。 |
| **エラー応答** | 標準Web API エラー（401、403など）。 お客様の「カスタマーサポートとしてログイン」が無効になっている場合、500またはマッピングされた例外として表示される可能性があります。 |

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

## GraphQLを使用した顧客トークンの1回限りのコードの交換

OTC （管理UIまたはREST API）を生成した後、次のいずれかのGraphQLのミューテーションを使用して、顧客アクセストークンと交換します。

### `generateCustomerToken`変異

`generateCustomerToken(email, password)`の変異は顧客トークンを返します。 `password`引数は次の順序で評価されます。

1. **顧客パスワード （デフォルト）** – 顧客のアカウントパスワード。
1. **顧客リセットパスワードトークン（1回限りの使用）** - **パスワードを忘れた**&#x200B;からの有効なトークン（例：`requestPasswordResetEmail`の突然変異）。 最初の使用時に消費されます。
1. **管理者生成のOTC （1回限りのコード）** - REST APIまたは管理UIを使用して、お客様の管理者が生成したコード。 1回限りの使用、短時間（デフォルトでは30秒）。

**スキーマ：**

```graphql
type Mutation {
  generateCustomerToken(email: String!, password: String!): CustomerToken
}

type CustomerToken {
  token: String!
}
```

**例：管理者OTC**&#x200B;でログイン

```graphql
mutation GenerateCustomerToken($email: String!, $password: String!) {
  generateCustomerToken(email: $email, password: $password) {
    token
  }
}
```

変数（OTCを`password`として使用）:

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

**例：パスワード リセット トークンを使用したログイン**

お客様がパスワードのリセットを要求した後（例：`requestPasswordResetEmail`）、メールリンクを介して受信したリセットトークンは、`password`で`generateCustomerToken`として使用できます（1回限りの使用）。

```graphql
mutation GenerateCustomerToken($email: String!, $password: String!) {
  generateCustomerToken(email: $email, password: $password) {
    token
  }
}
```

変数（`password`としてリセットトークンを使用）:

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

### `exchangeOtpForCustomerToken`変異

`exchangeOtpForCustomerToken`変異は、管理者が生成したパスワード リセット トークンまたはOTPを顧客アクセス トークンと交換します。 OTPは、交換が成功した後（1回限りの使用）に無効になります。 このエンドポイントは、reCAPTCHA設定を尊重します。

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

### 突然変異の概要

| 突然変異 | ユースケース |
|---|---|
| `generateCustomerToken(email, password)` | シングルエントリポイント：顧客パスワード、パスワードリセットトークン、管理者OTC、またはOTP （パスワード/リセット後に試行）。 |
| `exchangeOtpForCustomerToken(email, otp)` | OTPまたはパスワードトークン交換のリセット。 OTP （またはパスワードトークンのリセット）は、使用後に消費されます。 |

パスワード リセット トークンと管理者OTCは、両方とも`password`引数として`generateCustomerToken`に渡されます。 レゾルバはトークンタイプを検出し、それに応じて検証します。
