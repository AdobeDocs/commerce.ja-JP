---
title: 発送方法拡張のチュートリアル
description: App Builder、チェックアウトスターターキット、AI アシスト開発ツールを使用して、Adobe Commerce as a Cloud Service用に設定可能な発送方法拡張機能を作成する方法について説明します。
feature: App Builder, Cloud
role: Developer
level: Intermediate
source-git-commit: e55bc4db196d3d973b981bb2484be950dcd6b7c3
workflow-type: tm+mt
source-wordcount: '1849'
ht-degree: 0%

---

# 発送方法拡張のチュートリアル

このチュートリアルでは、[!DNL Adobe Commerce as a Cloud Service]、[!DNL Adobe App Builder] チェックアウトスターターキット [、AI アシスト開発ツールを使用して、](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/){target="_blank"} ーザー向けの発送方法の拡張機能を構築する手順を説明します。

この拡張機能により、チェックアウト時に設定可能な配送方法が追加されます。この方法では、料金は外部のモック配送料サービスから取得されます。 マーチャントは、管理 UI でサービス URL、API キー、ウェアハウス（出荷元）アドレスを設定し、チェックアウト時に、拡張機能がそのサービスに対するレートをリクエストし、返されたオプションを顧客に表示します。

開始する前に、[&#x200B; 前提条件 &#x200B;](./tutorial-prerequisites.md) を完了してください。

## 前提条件を確認 {#tutorial-verify-prerequisites}

次の前提条件がインストールされていることを確認します。

```bash
# Check Node.js version (should be 22.x.x)
node --version

# Check npm version (should be 9.0.0 or higher)
npm --version

# Check Git installation
git --version

# Check Bash shell installation
bash --version
```

上記のコマンドのいずれかで期待される結果が返されない場合は、[&#x200B; 前提条件 &#x200B;](./tutorial-prerequisites.md) を参照してガイダンスを確認してください。

## モック配送料 API の作成

[&#x200B; 前提条件 &#x200B;](./tutorial-prerequisites.md) を完了したら、モック配送料 API を作成して、サー [!DNL Commerce Admin] スで拡張機能を設定する際にサービス URL と API キーの準備を整えます。 拡張機能は外部配送料 API を呼び出します。 このチュートリアルでは、モック API を使用して、実際の通信事業者アカウントなしでフローを実行できます。 [Pipedream](https://pipedream.com) （無料アカウントが必要）を使用してモック API を作成します。 モック API では、通常の実際の配送料 API に似たリクエスト/応答契約を使用するので、後でこの拡張機能を実際のプロバイダーに接続するのは簡単です。

モック API を作成するには、[&#x200B; モックレート API 仕様ファイル &#x200B;](../assets/mock-rates-api-spec.zip) をダウンロードして開き、`.md` ファイルをプロジェクトに追加します（例：`docs/mock-rates-api-spec.md`）。

**時間：** モック API の作成には約 **5～10 分かかります**。

### ワークフローと HTTP トリガーの作成

1. [pipedream.com](https://pipedream.com) に移動し、新規登録するかログインします。
1. **新規ワークフロー** （または **ワークフローを追加**）をクリックします。
1. トリガーには、「**HTTP/Webhook**」を選択します。
1. トリガーの設定で、「**HTTP 応答**」を「**ワークフローからカスタム応答を返す** に設定します。 これにより、コードステップで JSON 応答のモックを送信できます。
1. Pipedream は、**などの一意の** HTTP エンドポイント URL`https://123456.m.pipedream.net` を表示します。
1. Commerce Admin で拡張機能を設定する際には、**この URL をコピー** して、**サービス URL** として使用します。

   ![HTTP/Webhook トリガーとエンドポイント URL が表示された Pipedream ワークフロー &#x200B;](../assets/mock-api-trigger.png){width="600" zoomable="yes"}

トリガーに **Authorization** を設定する必要はありません。モック API は、コードステップの `API-Key` ヘッダーを検証します。

### コードステップの追加

1. **+** アイコンをクリックしてステップを追加します。
1. 「**Node.js コードを実行**」（コードステップ）を選択します。
1. デフォルトのコードを次のJavaScriptに **置き換え** ます。

   ```javascript
   export default defineComponent({
   async run({ steps, $ }) {
      const event = steps.trigger.event;
      const body = event.body ?? {};
      const headers = event.headers ?? {};
      const apiKey = headers["api-key"] ?? body.api_key ?? "";
   
      if (!apiKey || String(apiKey).trim() === "") {
         await $.respond({
         immediate: true,
         status: 401,
         headers: { "Content-Type": "application/json" },
         body: { error: "Missing or invalid API-Key header" },
         });
         return;
      }
   
      const shipment = body.shipment;
      if (!shipment || typeof shipment !== "object") {
         await $.respond({
         immediate: true,
         status: 400,
         headers: { "Content-Type": "application/json" },
         body: { error: "Missing or invalid shipment" },
         });
         return;
      }
   
      const rates = [
         {
         service_code: "mock_standard",
         service_name: "Mock Standard",
         carrier_friendly_name: "Mock Carrier",
         shipping_amount: { amount: 5.99 },
         shipment_cost: 5.99,
         cost: 5.99,
         },
         {
         service_code: "mock_express",
         service_name: "Mock Express",
         carrier_friendly_name: "Mock Carrier",
         shipping_amount: { amount: 12.99 },
         shipment_cost: 12.99,
         cost: 12.99,
         },
      ];
   
      await $.respond({
         immediate: true,
         status: 200,
         headers: { "Content-Type": "application/json" },
         body: { rates },
      });
   },
   });
   ```

1. **デプロイ** をクリックします。

   ![&#x200B; モック配送料スクリプトを使用した Pipedream コードステップ &#x200B;](../assets/mock-api-code-step.png){width="600" zoomable="yes"}

モックは、空でない `API-Key` ヘッダーと `shipment` オブジェクトを含む有効なリクエストに対して、2 つの評価オプション（モックスタンダードとモックエクスプレス）を返します。 API キーの設定は、このチュートリアルの後半の [!DNL Commerce Admin] で行います。 また、同じ設定画面で Pipedream ワークフローの URL を指定するので、メモしておきます。

## 拡張機能の開発

このセクションでは、[!DNL Adobe Commerce as a Cloud Service] チェックアウトスターターキット [&#x200B; と AI アシスト開発ツールを使用して、](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/){target="_blank"} の配送方法の拡張機能を開発する手順を説明します。

1. コーディングエージェントの MCP 設定に移動します。 例えば、カーソルでは、**[!UICONTROL Cursor]**/**[!UICONTROL Settings]**/**[!UICONTROL Cursor Settings]**/**[!UICONTROL Tools & MCP]** に移動します。 `commerce-extensibility` ツールセットがエラーなく有効になっていることを確認します。 エラーが表示された場合は、ツールセットのオン/オフを切り替えます。

   ![MCP コマース拡張ツールセットが有効になっていることを示すカーソル IDE 設定 &#x200B;](../assets/cursor-settings-shipping.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   >AI 支援による開発ツールを使用する場合、エージェントによって生成されるコードと応答に自然なバリエーションが生じることを期待してください。
   >
   >コードで問題が発生した場合は、いつでもエージェントにデバッグの支援を求めることができます。

1. カーソルのコンテキストにドキュメントを追加した場合は、無効にします。 [!UICONTROL **カーソル**]/[!UICONTROL **設定**]/[!UICONTROL **カーソル設定**]/[!UICONTROL **インデックスとドキュメント**] に移動し、一覧表示されているドキュメントを削除します。

   ![&#x200B; ドキュメントリストが空のカーソルインデックス作成とドキュメント設定 &#x200B;](../assets/disable-documentation.png){width="600" zoomable="yes"}

1. エージェントにモック率 API 仕様へのアクセス権を付与して、クライアントを正しく実装できるようにします。 まだ行っていない場合は、[&#x200B; モックリレート API 仕様ファイル &#x200B;](../assets/mock-rates-api-spec.zip) をダウンロードして開き、`.md` ファイルをプロジェクト（例：`docs/mock-rates-api-spec.md`）に追加してから、プロンプトでそのファイルを参照します。

1. 発送方法拡張機能を生成します。

   - エージェントのチャットウィンドウで、**プラン** モードを選択します（使用可能な場合）。 これにより、エージェントが計画なしで続行するのを防ぎます。
   - 次のプロンプトを入力します。

   ```shell-session
   Build an Adobe Commerce extension that adds a shipping method at checkout. The rates come from an external mock shipping rates service: the merchant configures the service's URL and API key in Admin, and at checkout the extension asks that service for rates and shows the returned options to the customer.
   
   External service (mock shipping rates API):
   - The service endpoint URL is configurable by the merchant (for example https://123456.m.pipedream.net).
   - The API is specified in ./docs/mock-rates-api-spec.md.
   
   The merchant must be able to configure the following in the Adobe Commerce Admin UI. Use the Adobe Commerce Admin UI SDK (or equivalent App Builder extensibility options for the Admin) to add a configuration screen where the merchant can set:
   - The service URL (where the extension sends rate requests).
   - An API key the service expects (any non-empty value for the mock). The API key is sensitive data: it must be stored securely and must never appear in logs, error messages, or in the UI in full (e.g. mask in the UI).
   - The warehouse (ship-from) address: name, phone, street, city, state, postal code, country. This is the origin used when requesting rates.
   ```

   >[!NOTE]
   >
   >エージェントがドキュメントの検索を要求した場合は、許可します。

   ![Shipping extension プロンプトが入力されたエージェントモードのカーソルチャットウィンドウ &#x200B;](../assets/enter-prompt-shipping.png){width="600" zoomable="yes"}

1. エージェントが最適なコードを生成できるように、エージェントの質問に正確に答えます。 使用するキットまたはテンプレートを尋ねられた場合は、出荷先ドメインと管理者 UI SDK拡張機能を使用して [&#x200B; チェックアウトスターターキット &#x200B;](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/){target="_blank"} に送ります。これにより、出荷 Webhook とマーチャント設定画面の両方が実装されます。

   エージェントは、実装の信頼できる情報源として機能する `requirements.md` （または同等の）ファイルを作成できます。

1. `requirements.md` （または同等の）ファイルを確認し、計画を検証します。 すべてが正しいと思われる場合は、アーキテクチャ計画（またはフェーズ 2 **に移行するようエージェントに指示し** す。 次のことを確認します。

   - **shipping-methods** アクション（または同等の）がCommerce Webhook を処理し、外部レート API を呼び出します。
   - **shipping-config** （または同等の）アクションは、GET（読み取り設定、API キーがマスクされた）および SET （保存サービス URL、API キー、ウェアハウスアドレス）をサポートします。設定は Runtime State などに安全に保存されます。
   - 管理 UI には、サービス URL、API キー（パスワード/マスク）、ウェアハウスのアドレスのフィールドを持つ **モック出荷** （または同様の）タブが含まれています。

   ![AI エージェントによって作成された要件ファイルに出荷拡張機能の実装の詳細が含まれている &#x200B;](../assets/requirements-file-shipping.png){width="600" zoomable="yes"}

1. エージェントがアーキテクチャプランを提供したら、レビューします。

   ![&#x200B; モック配送料延長に対応する AI エージェント実装計画 &#x200B;](../assets/implementation-plan-shipping.png){width="600" zoomable="yes"}

1. コードの生成を続行するようにエージェントに指示します。 エージェントは、Commerceが返されたメソッドを受け入れ、Webhook メソッドの **（Webhook タイプ** after`plugin.magento.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates`、必須 **オプション**）を使用できるように、配送先設定に **モック** 配送業者を追加する必要があります。

   このエージェントは、必要なコードを生成し、次の手順（依存関係のインストール、モックキャリアの登録、Commerce Webhook の設定、デプロイなど）に関する詳細な概要を提供します。

   ![&#x200B; 生成されたコードの概要と出荷拡張機能の実装 &#x200B;](../assets/code-generation-summary-shipping.png){width="600" zoomable="yes"}

   ![AI エージェントは、Webhook のインストール、設定および出荷用拡張機能のデプロイに関する次の手順を実行します &#x200B;](../assets/next-steps-shipping.png){width="600" zoomable="yes"}

### デプロイ前のクリーンアップ

デプロイする前に、アプリケーションで必要のないコードを削除します。 チェックアウトスターターキットには、未使用のドメイン（支払い、税金、イベントなど）や基礎モードが含まれる場合があります。 次のようなプロンプトを使用して、担当者にそれらを削除させ、出荷パーツと [!DNL Admin UI] 品パーツのみを保持させます。

```shell-session
Proceed with Phase 5 cleanup.
```

エージェントがクリーンアップレポートを生成し、未使用のアクション、設定およびスクリプトを削除して、プロジェクトを更新します。 デプロイする前に、この手順を完了してください。

![&#x200B; 削除および保持されたコンポーネントを示す AI エージェントフェーズ 5 クリーンアップレポート &#x200B;](../assets/cleanup-report-shipping.png){width="600" zoomable="yes"}

### 拡張機能のデプロイ

1. 生成されたコードを検証した後、次のプロンプトを使用して拡張機能をデプロイします。

   ```shell-session
   Deploy the app.
   ```

   エージェントは、デプロイメント前の準備状況を評価します（例えば、管理 UI またはCommerce API が使用されている場合、`.env`、`COMMERCE_WEBHOOKS_PUBLIC_KEY` および OAuth/IMS 変数に関する `COMMERCE_BASE_URL` を確認します）。

   ![&#x200B; モック出荷の拡張機能に対する AI エージェントのデプロイ前準備とデプロイ手順 &#x200B;](../assets/pre-deployment-assessment-shipping.png){width="600" zoomable="yes"}

1. 評価結果に自信がある場合は、エージェントにデプロイメントを続行するように指示します。 エージェントは、MCP ツールキットを使用して、検証、ビルド、およびデプロイを自動的に行います。

   ![&#x200B; デプロイされたパッケージと出荷用の Webhook URL を含む MCP ツールキットのデプロイメント出力 &#x200B;](../assets/deployment-process-shipping.png){width="600" zoomable="yes"}

### デプロイメント後

デプロイ後、次の手順を実行してモックキャリアを登録し、Webhook と [!DNL Admin UI] を設定し、チェックアウト時に拡張機能を検証します。

1. **Commerceへのモックキャリアの登録** （デプロイ後に 1 回実行）:

   ```bash
   npm run create-shipping-carriers
   ```

   `.env` に `COMMERCE_BASE_URL` と有効な OAuth/IMS 認証情報が設定されていることを確認し、スクリプトで通信事業者を登録できるようにします。

1. **[!DNL Commerce Admin] での配送 Webhook の設定：**

   - **ストア**/設定/**設定**/**Adobe サービス**/**Commerce Webhook** に移動します。
   - Webhook を追加します。
      - **Webhook メソッド：** `plugin.magento.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates`
      - **Webhook タイプ：** **after**
      - **URL:** デプロイされた **shipping-methods** web アクション URL （デプロイ出力または [!DNL Adobe Developer Console] から）。
      - **必須：**&#x200B;**オプション** – 外部 API がレートを返さない場合でも、チェックアウトを引き続き機能させることができます。

   ![&#x200B; モック配送料のCommerce管理 Webhook 設定 &#x200B;](../assets/admin-webhook-shipping.png){width="600" zoomable="yes"}

1. **[!DNL Admin UI SDK] 拡張機能を設定します。**

   - [!DNL Commerce Admin] で、**ストア**/設定/**設定** に移動します。
   - **Adobe サービス** / **管理 UI SDK** を開きます。
   - **管理 UI SDKを有効にする** を **はい** に設定し、**設定を保存** をクリックします（まだ有効になっていない場合）。
   - 「**拡張機能を設定**」をクリックし、アプリのデプロイ先のワークスペースを選択して、「**適用**」をクリックします。 また、「**カスタム**」オプションを選択して、ワークスペース名を入力することもできます。
   - リストで [!DNL App Builder] アプリを選択して保存します。 アプリが表示されない場合は、「**登録を更新**」をクリックして、もう一度試してください。

   ![&#x200B; 管理 UI SDK ワークスペースと拡張機能の選択を使用して拡張機能モーダルを設定する &#x200B;](../assets/admin-ui-configure-extensions.png){width="600" zoomable="yes"}

1. **Adobe Commerce管理 UI でのモック出荷方法の設定：**
   - **アプリ** を開き、アプリを選択します。
   - 「**モック出荷**」タブ（または同等のタブ）を開きます。
   - 次の詳細を入力します。
      - **サービス URL:** コピーした Pipedream ワークフローの URL （例：`https://123456.m.pipedream.net`）。
      - **API キー：** モック用の空でない値（例：`tutorial-key`）。
      - **倉庫（発送元）住所：** 名、電話、住所、市区町村、都道府県、郵便番号、国。
   - **保存** をクリックします。 設定はランタイム状態に保存され、shipping-methods アクションで使用されます。

   ![&#x200B; サービス URL、API キーおよびウェアハウスのアドレスを含んだモック出荷設定フォーム &#x200B;](../assets/admin-ui-mock-shipping.png){width="600" zoomable="yes"}

1. **チェックアウト時に確認：** 買い物かごに商品を追加し、チェックアウトに移動して、配送先住所を入力します。 例えば **Mock Standard** や **Mock Express** などのモック配送オプションが表示されます。

   ![&#x200B; 外部レート API からのモック配送オプションを示すチェックアウトページ &#x200B;](../assets/checkout-mock-shipping.png){width="600" zoomable="yes"}

### トラブルシューティング

- **管理 UI で設定が保存されません：** 「応答が有効な「message/http」ではない」または保存後に値が更新されない場合は、次のようなコマンドを使用して、config アクションのランタイムアクティベーションログを確認します。

  ```bash
  aio app logs --action CustomMenu/shipping-config --limit 20
  ```

  一般的な原因としては、ゲートウェイが特定の応答形式（例：文字列本文と `Content-Type: application/json`）を要求しているか、ステートライブラリが文字列値を要求している場合が考えられます。アクションが config を文字列として格納し、読み取り時に解析し、shipping-methods アクションが同じ解析を使用します。 エージェントのチャットまたはログで、正確な原因と修正方法を確認します。

- **「応答には少なくとも 1 つの操作が含まれている必要があります」** （Webhook ログ内）:Commerceでは、少なくとも 1 つの操作を返すように出荷用 Webhook が必要です。 エージェントに、shipping-methods アクションが空の操作配列を返さないように依頼します（例えば、外部 API が率を返さない場合にフォールバック率を返します）。

- **チェックアウト時に配送料はかかりません：** Webhook の URL とメソッドが正しく、モック通信事業者が登録され（`npm run create-shipping-carriers`）、[!DNL Admin UI] にモック配送設定が設定されていることを確認します。 ランタイムログで、shipping-methods アクションの API または検証エラーを確認し、アクションが少なくとも 1 つの操作を返すよう [!DNL Commerce] し、「応答には少なくとも 1 つの操作が含まれている必要があります」と表示されないようにします。

### チュートリアルの概要

このチュートリアルで扱うトピックの概要は次のとおりです。

- **前提条件と設定：** ツールの検証とモック配送料 API の作成。
- **エージェント主導型開発：** コマース拡張ツールセットを使用して、出荷 Webhook と管理 UI 用の要件、実装計画およびコードを生成します。
- **フェーズ 5 クリーンアップ：** 未使用のチェックアウトスターターキットドメインと基礎モードをデプロイ前に削除します。
- **導入：** 導入前評価および MCP ツールキットの導入
- **デプロイメント後の設定：** モック通信事業者の登録、[!DNL Commerce] Webhook の設定、[!DNL Admin UI SDK] 拡張機能の有効化、[!DNL Admin UI] でのモック出荷（サービス URL、API キー、ウェアハウス）の設定。
- **検証：** モック配送オプションの確認がチェックアウト時に表示されます。

### 次の手順

このチュートリアルの詳細な実験では、次の点を考慮してください。

- [!DNL Commerce] にモックキャリアを登録し、各デプロイメント後に出荷 Webhook を設定するフックを使用して、デプロイ後の設定を自動化します。
- 拡張機能のサービス URL と API キーを変更して、実際の配送料 API を指 [!DNL Admin UI] します。
- [!DNL Admin UI] を拡張して、通信事業者のステータスを表示するか、レートサービスへの接続をテストします。
