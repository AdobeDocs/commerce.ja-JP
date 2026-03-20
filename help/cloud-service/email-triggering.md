---
title: REST によるメールのトリガー
description: ' [!DNL Adobe Commerce as a Cloud Service] のテンプレート ID、受信者のメールおよびテンプレート変数を指定し、REST API を使用してオンデマンドでトランザクションメールをトリガーにする方法を説明します。'
role: Admin
level: Experienced
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
source-git-commit: 9661e368f7a0dc85edcd3e52a67ae2a98355d8b5
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# REST API を使用したメールのトリガー

以前は、顧客登録や注文購入時など、イベントがトリガーされた場合にのみメールを送信できました。 ま [!DNL Adobe Commerce as a Cloud Service]、テンプレート ID、受信者のメールおよびテンプレート変数を指定して、REST API を通じてオンデマンドでメールを送信できます。

>[!NOTE]
>
>現在、新しく作成されたカスタムテンプレートのみを送信できます。 定義済みのおよびシステムテンプレートはサポートされていません。

`V1/custom-email/send` エンドポイントを使用すると、統合や外部サービスなどの **サードパーティシステム** が、次のように指定して、オンデマンドでメールを送信できます。

- **テンプレート ID** - メールテンプレート ID。
- **受信者のメール** – このリクエストのターゲットメールアドレス。
- **変数** - （任意） `customer_name` や `order_id` など、テンプレートに挿入するカスタム定義のキーと値のペア。

>[!NOTE]
>
>メールは、現在のストア範囲と、デフォルトの **送信元** メールアドレスまたはテンプレート用に定義されたメールアドレスを使用して、同期的に送信されます。

## REST 契約

次の節では、REST API を使用してトランザクションメールをオンデマンドで送信する方法について説明します。

### エンドポイント

- **URL** - `POST /rest/V1/custom-email/send`
- **認証** - **サービス間 IMS 認証** のみがサポートされています。 呼び出し元は、**API を使用してカスタムメールを送信** （`Magento_CustomEmailSend::send_custom_email`）リソースにアクセスできる必要があります。 詳しくは、[REST 認証 &#x200B;](https://developer.adobe.com/commerce/webapi/rest/authentication/) を参照してください。
- **非同期使用** （推奨） – このエンドポイントは同期的に実装されますが、リクエストがコンシューマーによってキューに入れられ処理されるように、**非同期 REST API** を使用して呼び出すことをお勧めします。これにより、長期間有効な HTTP 接続を回避できます。 [!DNL Adobe Commerce as a Cloud Service] では、`/async` の後に `V1` を使用してルートを使用できます。例：`POST https://<server>.api.commerce.adobe.com/<tenant-id>/V1/async/custom-email/send`。

  詳しくは、[&#x200B; 非同期 Web エンドポイント（SaaS） &#x200B;](https://developer.adobe.com/commerce/webapi/rest/use-rest/asynchronous-web-endpoints/) を参照してください。

### リクエスト本文

- **templateId** （インターガー、必須） – [!UICONTROL **マーケティング**]/[!UICONTROL _通信_]/[!UICONTROL **メールテンプレート**] の下の管理者で定義されたメールテンプレート ID。

- **recipientEmail** （文字列、必須） – ターゲットのメールアドレス。 有効なメールフォーマットを指定する必要があります。 値が見つからないか空の場合、検証エラーがトリガーします。
- **variables** （オブジェクト、オプション） – `UnstructuredArray` としてテンプレートに挿入されるキー値マップ。

  変数を使用しない場合は、空のオブジェクトを渡すか省略します。 メールテンプレートの本文と件名では、変数の構文を使用して変数を参照します（例：`var order_id`）。 また、サブジェクトは、[&#x200B; サポートされるテンプレートシナリオ &#x200B;](#supported-template-scenarios) で説明したのと同じカスタム変数および構文をサポートします。

### 成功応答（HTTP 200）

この API は、送信に成功すると HTTP 200 を返します。

### エラーの応答

- **HTTP 400 – 検証エラー**

  統合では、リクエストごとに有効な `templateId` と `recipientEmail` を指定する必要があります。

   - `"message": "Invalid recipient email format"` – 受信者アドレスが無効または正しくありません
   - `"message": "Recipient email is required."` - `recipientEmail` が見つからないか空です
   - `"message": "Template ID must be a positive integer."` - `templateId` が見つからない、ゼロまたは無効

- **HTTP 404 - テンプレートが見つかりません**

  例：`"message": "Email template with ID \"999\" does not exist."`

## サポートされるテンプレートシナリオ

次のテンプレート機能は、**メール本文** と **テンプレートの件名** の両方でサポートされています。

>[!NOTE]
>
>テンプレートの件名は、カスタム変数もサポートしています。 次の節で説明するように、`var variableName` やその他の構文を使用します。

- **ディレクティブを含める** - メールヘッダーなど、他の設計テンプレートを含めます。

  ```javascript
  {{template config_path="design/email/header_template"}}
  ```

- **単純な変数** - `var variableName` を使用します（例：`var order_id` または `var g`）。

  ```javascript
  {{var order.test}}
  {{var g}}
  {{var order_id}}
  ```

- **ネスト/ドット表記** - リクエストフ `variables` ールドで渡されるネストされたキーの場合、翻訳では、`$order_data.customer_name`、`$order.increment_id`、`$order_data.frontend_status_label` などのドル記号の付いた名前を使用します。

  ```javascript
  {{trans "%name," name=$order_data.customer_name}}
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **翻訳（trans）** - パラメーター化されたテキスト、複数のプレースホルダーとHTML タグを持つ複数行の翻訳。

  ```javascript
  {{trans "%name," name=$order_data.customer_name}}
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **Raw 出力** – 翻訳済みまたは可変コンテンツにHTMLが含まれている場合に `|raw` フィルターを使用します（例：`<strong>` または `<a>`）。

  ```javascript
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **URL ヘルパー** – 翻訳内のストア URL の場合。

  ```javascript
  {{trans 'You can check the status of your order by [logging into your account](%account_url).' account_url=$this.getUrl($store,'customer/account/',[_nosid:1]) |raw}}
  ```
