---
title: 配信見積もり拡張機能のチュートリアル
description: App Builder、Edge Delivery Services、AIを活用した開発ツールを使用して、Adobe Commerce as a Cloud Serviceの納期を見積もる拡張機能を構築する方法を説明します。
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: ba445bf33ec9334c853245fce125af12cd244367
workflow-type: tm+mt
source-wordcount: '3398'
ht-degree: 0%

---

# 配信見積もり拡張機能のチュートリアル

このチュートリアルでは、[!DNL Adobe App Builder]、[!DNL Edge Delivery Services]、およびAIを活用した開発ツールを使用して、[!DNL Adobe Commerce as a Cloud Service]の配信日の見積もり拡張機能を作成する方法について説明します。 拡張機能は、外部APIから配送時間と配送日の見積もりを取得し、ストアフロント全体に表示します。

次の2つの部分を作成します。

- **App Builder拡張機能** – 外部配信見積もりAPIをラップするバックエンドのフロントエンド（BFF）アクション、チェックアウト時の配信日で配送方法を充実させるWebhook、再展開なしで設定を管理するための管理UI設定ページ。
- **Storefrontとの統合** — [!DNL Edge Delivery Services]個のドロップインコンポーネントと共有クライアントモジュールを使用して、製品詳細ページ（PDP）、カートページ、チェックアウトページに表示される配信日の見積もり。

>[!NOTE]
>
>AI エージェントは非決定論的です。 このチュートリアルのプロンプト、質問、および出力は例です。 担当者がさまざまな質問、要件、アーキテクチャの提案を作成する場合もあります。 このチュートリアルの例を使用して、類似の結果に向けてエージェントを誘導します。

開始する前に、[前提条件](./tutorial-prerequisites.md)を完了してください。 このチュートリアルでは、**チェックアウトスターターキット**&#x200B;を使用します。 既にクローンを作成し、前提条件ページで説明されている設定手順を完了していることを確認します。

## 前提条件を確認

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

上記のコマンドのいずれかが期待される結果を返さない場合は、ガイダンスについて[前提条件](./tutorial-prerequisites.md)を参照してください。

さらに、次の点を確認します。

- 製品データを含む[!DNL Adobe Commerce as a Cloud Service] インスタンスがあります。 [Commerce Cloud サービスインスタンス &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/cloud-service/overview){target="_blank"}を参照してください。
- [!DNL Commerce] インスタンスに接続されたストアフロントプロジェクトがあります。 ストアフロントがない場合は、[&#x200B; ストアフロントの作成](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=ja){target="_blank"}の手順に従います。
- `aem` CLIがインストールされています：

  ```bash
  npm install -g @adobe/aem-cli
  ```

- **買い物客アカウント**&#x200B;があり、[!DNL Commerce]に登録されたお客様で、デフォルトの配送先住所が保存されています。 PDP ページとカートページでの配達見積もりは、ログインした買い物客にのみ表示されます。 チェックアウトすると、認証状況に関係なくすべての買い物客の推定値が表示されます。

>[!IMPORTANT]
>
>このチュートリアルでは、**チェックアウトスターターキット**&#x200B;を使用します（統合スターターキットは使用しません）。 Checkout Starter Kitは、支払い、配送、税金、イベントなどにWebhook ベースの拡張性を提供します。 チェックアウトキットからブートストラップを実行してください。

## モック配信見積もりAPIの設定

拡張機能は、外部配信見積もりAPIを呼び出して、出荷日と時間の見積もりを取得します。 このチュートリアルでは、モック APIを使用して、実際の通信事業者アカウントなしでフルフローを実行できるようにします。 次の2つのオプションを使用できます。

- **オプション A: Pipedream workflow** – 無料階層、クイックセットアップですが、月間呼び出し制限があります。
- **オプション B: App Builder ランタイム アクション** — バックエンドの開発手順で作成された外部依存関係はありません。

>[!TIP]
>
>開発中に、自由階層の呼び出し割り当て量に達した場合は、Pipedream （オプション A）から開始し、ランタイムアクション（オプション B）に切り替えることができます。 どちらのオプションも同じAPI コントラクトを実装します。

### API仕様

モック APIはPOST リクエストを受け入れ、配送業者、転送日、カットオフ時間、最適な見積もりで配送日の見積もりを返します。

**リクエスト本文** （モックのすべてのフィールドはオプション）:

```json
{
  "origin": { "country_code": "US", "postal_code": "90210", "city": "Beverly Hills" },
  "destination": { "country_code": "US", "postal_code": "10001", "city": "New York" },
  "ship_date": "2026-03-10",
  "carriers": ["standard", "express"],
  "service_levels": ["standard", "express"]
}
```

**応答（200 OK）:**

```json
{
  "estimates": [
    {
      "carrier_code": "standard",
      "service_code": "ground",
      "delivery_date": "2026-03-14",
      "safe_delivery_date": "2026-03-15",
      "transit_days": 4,
      "cutoff_datetime_utc": "2026-03-10T17:00:00.000Z"
    },
    {
      "carrier_code": "express",
      "service_code": "2day",
      "delivery_date": "2026-03-12",
      "safe_delivery_date": "2026-03-12",
      "transit_days": 2,
      "cutoff_datetime_utc": "2026-03-10T12:00:00.000Z"
    }
  ],
  "best_estimation": { "carrier_code": "express", "delivery_date": "2026-03-12", "transit_days": 2 }
}
```

**エラー応答：** 401 （欠落/無効なAPI キー）、400 （無効な`ship_date`形式）、503 （シミュレートされたダウンタイム）。

### モックの設定

>[!BEGINTABS]

>[!TAB Pipedream ワークフロー]

Pipedream オプションは、ベアラートークントリガーを使用し、ワークフロー認証URLへのPOST リクエストを受け入れます。

| 項目 | 説明 |
|------|-------------|
| ベース URL | 完全なPipedream ワークフロートリガー URL （例：`https://<id>.m.pipedream.net`） |
| 認証 | `Authorization: Bearer <API_KEY>` |
| メソッド | 投稿する |

{style="table-layout:auto"}

**ワークフローを作成：**

1. [Pipedream](https://pipedream.com){target="_blank"}で新しいワークフローを作成します（**[!UICONTROL Workflows]** > **[!UICONTROL New Workflow]**）。

1. POST用に設定された&#x200B;**HTTP / Webhook**&#x200B;トリガーを追加します。 PipedreamはWebhook URLを割り当てます。

1. **実行Node.js コード**&#x200B;手順を追加し、次のハンドラーコードを貼り付けます。

   ```javascript
   const DEFAULT_CARRIERS = [
     { carrier_code: "standard", service_code: "ground", transit_days: 4 },
     { carrier_code: "express", service_code: "2day", transit_days: 2 },
     { carrier_code: "priority", service_code: "overnight", transit_days: 1 },
   ];
   
   const ISO_DATE = /^\d{4}-\d{2}-\d{2}$/;
   
   function parseShipDate(shipDate) {
     if (shipDate == null || typeof shipDate !== "string") return null;
     if (!ISO_DATE.test(shipDate)) return null;
     const d = new Date(shipDate + "T12:00:00.000Z");
     if (Number.isNaN(d.getTime())) return null;
     return shipDate;
   }
   
   function addBusinessDays(isoDate, days) {
     const d = new Date(isoDate + "T12:00:00.000Z");
     let added = 0;
     while (added < days) {
       d.setUTCDate(d.getUTCDate() + 1);
       const dow = d.getUTCDay();
       if (dow !== 0 && dow !== 6) added += 1;
     }
     return d.toISOString().slice(0, 10);
   }
   
   function cutoffUtc(isoDate, hour = 17) {
     return `${isoDate}T${String(hour).padStart(2, "0")}:00:00.000Z`;
   }
   
   function getBearerToken(headers) {
     const auth = headers?.Authorization ?? headers?.authorization ?? "";
     if (typeof auth !== "string" || !auth.startsWith("Bearer ")) return null;
     return auth.slice(7).trim() || null;
   }
   
   function handleDeliveryEstimate(body) {
     const shipDate = parseShipDate(body?.ship_date);
     const baseDate = shipDate ?? new Date().toISOString().slice(0, 10);
     let carriers = DEFAULT_CARRIERS;
     if (Array.isArray(body?.carriers) && body.carriers.length > 0) {
       const set = new Set(body.carriers.map((c) => String(c).toLowerCase()));
       carriers = DEFAULT_CARRIERS.filter((c) => set.has(c.carrier_code.toLowerCase()));
     }
     if (Array.isArray(body?.service_levels) && body.service_levels.length > 0) {
       const set = new Set(body.service_levels.map((s) => String(s).toLowerCase()));
       carriers = carriers.filter(
         (c) => set.has(c.service_code.toLowerCase()) || set.has(c.carrier_code.toLowerCase())
       );
     }
     if (carriers.length === 0) {
       return { status: 200, body: { estimates: [], best_estimation: null } };
     }
     const estimates = carriers.map((c) => {
       const delivery_date = addBusinessDays(baseDate, c.transit_days);
       const safe_delivery_date = addBusinessDays(baseDate, c.transit_days + 1);
       const cutoff_datetime_utc = cutoffUtc(baseDate, 17 - c.transit_days);
       return {
         carrier_code: c.carrier_code,
         service_code: c.service_code,
         delivery_date,
         safe_delivery_date,
         transit_days: c.transit_days,
         cutoff_datetime_utc,
       };
     });
     return { status: 200, body: { estimates, best_estimation: estimates[0] } };
   }
   
   export default defineComponent({
     async run({ steps, $ }) {
       const event = steps.trigger?.event ?? steps.trigger ?? {};
       const body = event.body ?? {};
       const headers = event.headers ?? {};
       const auth = getBearerToken(headers);
       const expectedKey =
         (typeof process.env.MOCK_API_KEY === "string" && process.env.MOCK_API_KEY.trim()) || null;
       if (expectedKey && (!auth || auth !== expectedKey)) {
         await $.respond({
           immediate: true,
           status: 401,
           headers: { "Content-Type": "application/json" },
           body: { error: "unauthorized", message: "Missing or invalid API key." },
         });
         return;
       }
       if (body?.ship_date != null && !parseShipDate(body.ship_date)) {
         await $.respond({
           immediate: true,
           status: 400,
           headers: { "Content-Type": "application/json" },
           body: { error: "bad_request", message: "Invalid ship_date; use YYYY-MM-DD." },
         });
         return;
       }
       const { status, body: responseBody } = handleDeliveryEstimate(body);
       await $.respond({
         immediate: true,
         status,
         headers: { "Content-Type": "application/json" },
         body: responseBody,
       });
     },
   });
   ```

1. （オプション）ワークフロー設定に`MOCK_API_KEY`環境変数を追加して、Bearer トークン認証を強制します。 設定されていない場合は、リクエストを受け付けます。

1. ワークフローを展開します。

   エンドポイントはWebhookトリガーのURLです。

**モックをテスト：**

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer mock-api-key" \
  -d '{"destination": {"country_code": "US", "postal_code": "10001"}}' \
  "https://<your-endpoint>.m.pipedream.net"
```

>[!TAB App Builder Runtime アクション ]

App Builder Runtime アクションオプションは、モックを同じ[!DNL App Builder] プロジェクト内のランタイムアクションとしてデプロイします。 このアプローチには外部依存関係も呼び出しクォータもありません。

エージェントにモックアクションの作成を促します。

```shell-session
Add a new runtime action to this project that implements the API in @docs/PIPEDREAM_API_SPEC.md
- Add it to a separate package
- Use the code in docs/pipedream as inspiration
```

エージェントは、Pipedream オプションと同じAPI コントラクトで`actions/mock-delivery-api/index.js`を作成します。 デプロイ後、エンドポイントは次のとおりです。

```shell-session
https://<namespace>.adobeioruntime.net/api/v1/web/mock-delivery-api/delivery-estimate
```

認証は、`.env`の`MOCK_API_KEY`環境変数に対して検証されます。

>[!ENDTABS]

## 拡張機能の開発

このセクションでは、配信見積もり拡張機能の[!DNL App Builder] バックエンドの開発について説明します。 バックエンドでは、次の3つのアクションを実行できます。

| アクション | タイプ | 目的 |
|--------|------|---------|
| `delivery-estimates` | スタンドアロン web アクション | ストアフロント向けBFF — PDPとカートは配信日でこれを呼び出します |
| `shipping-methods` | Webhook アクション | チェックアウト時に`additional_data`の配達日で配送料をエンリッチします |
| `delivery-estimates-config` | 管理者バックエンドアクション | `aio-lib-state`に保存された設定のCRUD |

{style="table-layout:auto"}

1. コーディングエージェントのMCP設定から、`commerce-extensibility` ツールセットがエラーなしで有効になっていることを確認します。

   例えば、カーソルで、**[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**&#x200B;に移動します。

   エラーが表示された場合は、ツールセットのオンとオフを切り替えます。

   >[!NOTE]
   >
   >AI支援の開発ツールを使用する場合、エージェントによって生成されたコードと応答に自然なバリエーションが存在することを期待します。
   >コードで問題が発生した場合は、担当者にデバッグのサポートを依頼してください。

1. Cursorのコンテキストにドキュメントが追加されている場合は、そのドキュメントを無効にします。

   **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Indexing & Docs]**&#x200B;に移動し、一覧されているドキュメントをすべて削除します。

### 手順1：最初のプロンプトを入力する

エージェントにコンテキストの外部API仕様を指定し、開始を促します。 エージェントに停止して質問するように伝えることで、実装を早い段階で導くことができます。

担当者のチャットウィンドウに次のプロンプトを入力します。

```shell-session
I want to build an Adobe App Builder extension that extends the checkout with shipping date and time estimates taken from an external API described in @docs/API_SPEC.md.
Delivery dates for a product will be shown in the product details page and on the cart page.
Implement this feature by using the skills in this workspace for backend code, and a separate workspace with storefront skills. For this extension, focus on the backend skills and create an API_SPEC to hand work over to the storefront skills.

STOP and ask me clarifying questions about the requirements before you do any work.
```

>[!TIP]
>
>プロンプトで外部API仕様ファイル（`@docs/API_SPEC.md`）を参照すると、サードパーティ API コントラクトに関する具体的なコンテキストがエージェントに提供されます。 エージェントは、これを使用して、BFF アクション、共有HTTP クライアント、および管理者UI設定フィールドをデザインします。 担当者に対して、トリガーにガイド付きのワークフローを停止して質問し、導入を早期に進めることができるように指示します。

### ステップ 2：担当者の質問に答える

担当者は、ターゲット環境（PaaSとSaaS）、スコープ（スタンドアロンのBFF アクション、Webhookのエンリッチメント、またはその両方）、発信元アドレスソース、キャッシュ戦略、テストの環境設定などのトピックについて、一連の明確な質問を返します。 次の例は、典型的な質問と回答を示しています。 担当者は異なる質問をすることもありますが、トピックは一般的に同じです。

**エージェントの質問の例：**

1. **Target environment** — PaaS （オンプレミス）またはSaaS （Adobe Commerce as a Cloud Service）用に構築していますか？
2. **スコープ** – これは、スタンドアロンのBFF アクション（ストアフロントから直接呼び出す）、Webhook エンリッチメント（チェックアウト時に配送方法を拡張する）、またはその両方ですか？
3. **管理者の設定可能性** — API URL、API キー、発信元アドレスなどの設定は、Commerce管理者経由で設定可能にするか、`.env`に保存する必要がありますか？
4. **発信元の住所** – 発送元（倉庫）の住所はどこから来ていますか？ 静的な設定にするか、動的に解決するか？
5. **キャッシュ** – 外部APIへの呼び出しを減らすために、サーバー側で配信の見積もりをキャッシュする必要がありますか？ その場合、TTLとは？

**回答の例：**

```shell-session
Clarifications:
1. Let's build for SaaS
2. Let's do this:
(A) Can the PDP/cart call the 3rd party API directly — or are there any benefits of wrapping this call with a runtime action?
(B) Let's use the shipping-methods webhook
3. Let's use a Single-page application (SPA) that uses the Admin UI SDK to integrate with the admin. Since we are adding this config screen, let's make anything else that makes sense configurable to avoid redeployments when changing settings
4. Static configuration — origin address should be configurable in the Admin UI (e.g. warehouse address)
5. Yes, cache on the server side; suggest a TTL (e.g. 30 minutes) and make it configurable in the Admin UI
```

>[!TIP]
>
>ストアフロントがサードパーティ APIを直接呼び出すか、ランタイムアクショントリガーを介して実行するかを担当者に尋ねることは、便利なアーキテクチャに関する話し合いです。 エージェントは、BFF （Backend-for-Frontend）パターンの利点を説明します。API キーはサーバーサイドのままであり、CORSは処理され、キャッシュは一元化され、ベンダーの抽象化が行われます。 管理者UIの設定可能性を求めると、エージェントは`.env`ではなく`aio-lib-state`にすべての設定を保存するようにプッシュされ、設定を変更する際の再デプロイが不要になります。

>[!NOTE]
>
>担当者がさまざまな質問をする場合があります。 これらの回答を、エージェントを同じ機能的な結果に誘導するためのガイダンスとして使用します。ストアフロント呼び出しのBFF アクション、チェックアウトのエンリッチメントのshipping-methods webhook、設定を`aio-lib-state`に保存する管理者UI設定ページです。

### ステップ 3：要件とアーキテクチャの見直し

担当者は、レビューする要件とアーキテクチャドキュメントを生成します。 要件が指定した回答と一致し、アーキテクチャがカバーしていることを確認します。

- **BFF アクション** （`delivery-estimates`） – ストアフロントがPDP ページとカートページから呼び出すスタンドアロン web アクション。 `aio-lib-state`から設定を読み取り、外部配信見積もりAPIを呼び出し、形式の見積もりを返します。
- **Webhook アクション** （`shipping-methods`） – チェックアウト中に`additional_data`の配達日で配送料を強化します。 `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` Webhook メソッドを使用します。
- **管理者設定アクション** （`delivery-estimates-config`） — `aio-lib-state`に保存された設定用CRUD （API URL、API キー、オリジンアドレス、キャリア、キャッシュ TTL）。
- **共有ライブラリ** – 外部API用のHTTP クライアントと、`aio-lib-state`の読み取りと書き込み用の設定モジュール。

>[!NOTE]
>
>AI エージェントは非決定論的で、モデルとIDEによって動作が異なります。 異なる要件とアーキテクチャのセットを生成する、異なる質問のセットが表示される場合があります。 その場合は、実装がこのチュートリアルに記載されている内容と密接に一致するようにエージェントを誘導してから先に進んでください。

### 手順4：実行計画の選択

担当者は、詳細な実装計画を作成するか、直接実装を完了するかを選択できます。

- より詳細に制御して段階的に実行できるレビュー可能なプランが必要な場合は、最初のオプションを選択します。
- エージェントに最小限の介入で完全な実装を行わせたい場合は、2番目のオプションを選択します。

### 手順5：クリーンアップとデプロイ

エージェントが実装を完了すると、クリーンアップに進みます。 配送ドメインのみが使用されているため、エージェントは未使用の基礎モードを削除します。

- 支払いアクションと設定（`validate-payment/`、`filter-payment/`、`payment-methods.yaml`）
- 税アクションと設定（`collect-taxes/`、`collect-adjustment-taxes/`、`tax-integrations.yaml`）
- イベントのアクションと設定（`commerce-events/`、`3rd-party-events/`、`events.config.yaml`）
- 汎用の基礎モード （`generic/`）
- 他のドメイン（税関連のページやフックなど）からの管理UI SPA コンポーネント
- 未使用のスクリプト、テストファイル、環境変数

>[!TIP]
>
>担当者に、他のドメインからの残り物についてもAdmin UI SPAを確認するように依頼します。 「税務クラス」ページとそのフックは、スターターキットの基礎モードからまだ存在する可能性があり、削除する必要があります。

クリーンアップ後、次の手順&#x200B;**をこの順序**&#x200B;で使用してデプロイします。

```bash
# 1. Copy env template and fill in credentials.
cp env.dist .env

# 2. Select your App Builder workspace.
aio app use --merge

# 3. Sync OAuth credentials from workspace.
npm run sync-oauth-credentials

# 4. Deploy the extension.
aio app deploy

# 5. Register shipping carriers in Commerce.
npm run create-shipping-carriers
```

>[!IMPORTANT]
>
>手順をスキップしたり、並べ替えたりしないでください。 手順1～3は、デプロイメントの前提条件です。 資格情報が設定されていない場合、`aio app deploy` コマンドは失敗します。

### 手順6:WebhookとAdmin UIの設定

デプロイ後、出荷Webhookを設定します。 エージェントは、プログラムでサブスクライブするスクリプトを作成できます。

```bash
npm run subscribe-webhook
```

このコマンドは、次の設定で出荷Webhookを購読します。

| フィールド | 値 |
|-------|-------|
| Webhook メソッド | `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` |
| Webhook タイプ | `after` |
| 必須 | オプション（デフォルトの配送へのフォールバックが可能） |
| タイムアウト | 5000 ミリ秒 |

{style="table-layout:auto"}

>[!NOTE]
>
>SaaSの場合、Webhook メソッド名はパスから`magento.`を削除します。 PaaSのWebhook名は`plugin.magento.out_of_process_shipping_methods...`、SaaSのWebhook名は`plugin.out_of_process_shipping_methods...`です。

次に、Admin UIを設定します。

1. **管理UI SDK**&#x200B;を有効にします（**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL Adobe Services]** > **[!UICONTROL Admin UI SDK]** > **[!UICONTROL Enable]** > **[!UICONTROL Yes]**）。

1. [!DNL App Builder] ワークスペースと拡張機能を選択して、拡張機能を設定します。

1. **[!UICONTROL Refresh registrations]**&#x200B;をクリックします。

1. [!DNL Admin] サイドバーの&#x200B;**[!UICONTROL Apps]** > **[!UICONTROL Delivery Estimates]**&#x200B;に移動します。

1. 機能を有効にし、API URLとAPI キー、オリジンアドレス、デフォルトキャリア、キャッシュ TTL、キャリアコードマッピングなどの必要な設定を指定して、設定を完了します。

### 手順7：拡張機能のテスト

配信見積BFF アクションを直接テストします。

```bash
curl -s -X POST \
  -H "Content-Type: application/json" \
  -d '{"destination": {"country_code": "US", "postal_code": "10001"}}' \
  "https://<your-runtime-url>/api/v1/web/commerce-checkout-starter-kit/delivery-estimates" | jq .
```

応答は次のようになります。

```json
{
  "estimates": [
    {
      "carrier": "standard",
      "service_level": "ground",
      "delivery_date": "2026-03-12",
      "safe_delivery_date": "2026-03-13",
      "transit_days": 4,
      "cutoff_datetime_utc": "2026-03-06T18:00:00Z"
    },
    {
      "carrier": "express",
      "service_level": "2day",
      "delivery_date": "2026-03-10",
      "safe_delivery_date": "2026-03-10",
      "transit_days": 2,
      "cutoff_datetime_utc": "2026-03-06T20:00:00Z"
    }
  ],
  "best_estimation": {
    "carrier": "express",
    "delivery_date": "2026-03-10",
    "transit_days": 2
  }
}
```

### サービス契約の作成

バックエンドが完了したら、担当者にストアフロント作業のサービス契約を作成するように依頼します。

```shell-session
Produce a spec called STOREFRONT_API_SPEC that I can use in the storefront workspace with the corresponding agent. Also give me a prompt that I could use in that workspace.
```

エージェントは、完全なBFF エンドポイント契約（リクエストと応答の形式、ペイロードの例、エラー処理）と、ストアフロントワークスペース用にすぐに使用できるプロンプトを使用して`docs/STOREFRONT_API_SPEC.md`を生成します。

このファイルをストアフロント開発ステップを開始する前に、ストアフロントプロジェクトにコピーします。

>[!TIP]
>
>エージェントがサービス契約&#x200B;**と**&#x200B;の両方を生成し、他のワークスペースのプロンプトを生成することで、バックエンドとストアフロントチーム（またはエージェント）の間の明確な引き継ぎが保証されます。 ストアフロントエージェントは、APIについて質問することなく、すぐに作業を開始できます。

## ストアフロントへの接続

このセクションでは、[!DNL Edge Delivery Services]とAI支援の開発ツールを使用して、配信見積もり拡張機能のストアフロント部分を実装する方法について説明します。 PDP、カートページ、チェックアウトページに配信日の見積もりを追加します。

>[!NOTE]
>
>提供されるプロンプトは出発点です。 変更せずに使用することはできますが、エージェントと自然な会話をすることを検討してください。
>
>AI支援の開発ツールを使用する場合、エージェントによって生成されたコードと応答には常に自然なバリエーションがあります。
>
>コードで問題が発生した場合は、担当者にデバッグのサポートを依頼してください。

### ストアフロントの前提条件

ストアフロント統合を開始する前に、次の点を確認してください。

- [!DNL Commerce] インスタンスに接続されたストアフロントプロジェクト
- Commerce ストアフロント AI ツール [CLIを使用してインストール &#x200B;](./tutorial-prerequisites.md#install-the-storefront-ai-tools)
- `STOREFRONT_API_SPEC.md` ファイルがストアフロントプロジェクトの`docs/` フォルダーにコピーされました

### 手順1：環境の検証

`config.json` ファイルを開き、`commerce-core-endpoint`と`commerce-endpoint`の値が[!DNL Adobe Commerce as a Cloud Service] GraphQL エンドポイントを指していることを確認します。

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### 手順2：最初のプロンプトを入力する

サービス契約が既にプロジェクト内にある場合は、担当者にストアフロント統合の実装を促します。 エージェントで利用可能な場合は、**プラン** モードを使用して、プランなしでエージェントが続行できないようにします。

```shell-session
I need to implement delivery date estimates on the storefront for an Adobe Commerce (SaaS) store using Edge Delivery Services with storefront drop-ins. The backend is already built and deployed as an App Builder extension.

The full integration contract is in the `docs/STOREFRONT_API_SPEC.md` file— please read it first. It covers two integration points:

PDP and Cart pages — Call the delivery-estimates BFF action (HTTP POST) to fetch estimates for a destination and display the best delivery date.

Checkout shipping step — Delivery dates are already injected into each shipping method's `additional_data` by a webhook. No API call is needed. Just read `additional_data` from the shipping methods and display the delivery date next to each option.

Requirements:
- Show "Get it by [date]" on PDP using best_estimation.delivery_date
- Show a delivery date range on the cart page using delivery_date / safe_delivery_date
- Show delivery dates next to each shipping method at checkout, reading from additional_data
- Show "Order within X hours" countdown using cutoff_datetime_utc where appropriate
- Cache estimates client-side in sessionStorage to avoid redundant calls
- Never block the purchase flow — if estimates are unavailable, hide the UI silently

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>完全なAPI契約はバックエンドエージェントから既に利用可能であるため、プロンプトは詳細です。 `@docs/STOREFRONT_API_SPEC.md`を参照することで、エージェントはエンドポイント URL、リクエストと応答の形式、エラー処理を正確に把握できます。 明示的な要件リストは、エージェントがスコープを発明することを防ぎます。 具体的には、プランモードをリクエストすると、段階的なワークフローがトリガーされ、導入を早期に進めることができます。

### ステップ 3：明確な質問に答える

担当者は、認証の範囲、チェックアウトアプローチ、スタイル設定について質問を返します。 次の例は、典型的な質問と回答を示しています。

**エージェントの質問の例：**

1. **匿名ユーザーとログイン ユーザー** – すべての買い物客のPDP ページと買い物かごのページに推定が表示されるか、認証済みのページのみに表示されるか？
2. **チェックアウトアプローチ** —ShippingMethods ドロップインコンテナは`additional_data`を公開しないため、エージェントは2つのオプションを提案します。
   - **オプション A:** チェックアウト日とDOM注入日にBFFを呼び出します（シンプルで、PDP/Cartと一致）
   - **オプション B:** `overrideGQLOperations`経由でチェックアウト GraphQL フラグメントを拡張して`additional_data`を含める
3. **スタイル設定** – 絵文字と既存のデザイントークンの比較

**回答の例：**

```shell-session
1. Only for logged-in users — that way we can use the shopper's default shipping address and avoid a zip code input
2. Let's do Option A if feasible
3. Use anything that matches the current styling
```

>[!TIP]
>
>ログインした顧客に対してのみ見積もりを表示することは、現実的な選択です。 担当者は、買い物客のデフォルトの配送先住所を（GraphQL経由で）自動的に使用できるため、郵便番号の入力は必要ありません。 PDPやカートを利用している匿名の買い物客は、郵便番号を入力する必要があり、これは顧客の摩擦を招きます。 チェックアウト時には、配送先住所が既に入力されているため、すべての買い物客に配達日が表示されます。

>[!NOTE]
>
>担当者がさまざまな質問をする場合があります。 回答をガイダンスとして使用します。
>
>- ログインした買い物客に対してのみ、PDPとカートの推定値を表示します（郵便番号の入力は必要ありません）。
>- チェックアウトの場合は、オプション A （BFF呼び出し+ DOM インジェクション）を使用すると簡単になります。
>- スタイル設定に既存のデザイントークンを使用します。

### ステップ 4：要件とアーキテクチャの見直し

エージェントは、共有モジュールアーキテクチャを設計します。 次の項目をカバーしていることを確認します。

| コンポーネント | 目的 |
|-----------|---------|
| `scripts/delivery-estimates.js` | 共有モジュール — BFF クライアント、キャッシュ（sessionStorage、30分TTL）、日付書式設定、カウントダウンロジック、顧客アドレスルックアップ、キャリアマッピング |
| PDPの統合 | 価格と説明の間に任意のカウントダウンを含む「Get it by [date]」が表示されます |
| カートの統合 | 日付範囲（「3月12日（木）～3月13日（金）」を右列の注文の概要に表示 |
| チェックアウトの統合 | 出荷手順がアクティブな場合にBFFを呼び出し、DOMは`MutationObserver`を介して納期を挿入します |

{style="table-layout:auto"}

検証すべき主な設計決定：

- すべてのBFF呼び出しは非ブロッキングです。ページは最初にレンダリングされ、推定は非同期で表示されます。
- 失敗はすべてサイレントです – `console.debug`のみ。買い物客に対応するエラーはありません。
- `CARRIER_MAP`は、Commerceの通信事業者コード （DPS、Fedex）をBFFの通信事業者コード （標準、Express）にマッピングします。
- 動的`import()`は、配信モジュールをクリティカルレンダリングパスから除外します。

>[!NOTE]
>
>AI エージェントは非決定論的で、モデルとIDEによって動作が異なります。 異なる要件とアーキテクチャのセットを生成する、異なる質問のセットが表示される場合があります。 その場合は、実装がこのチュートリアルに記載されている内容と密接に一致するようにエージェントを誘導してから先に進んでください。

### 手順5：実行計画の選択

担当者は、詳細な実装計画を作成するか、直接実装を完了するかを選択できます。

- より詳細に制御して段階的に実行できるレビュー可能なプランが必要な場合は、最初のオプションを選択します。
- エージェントに最小限の介入で完全な実装を行わせたい場合は、2番目のオプションを選択します。

実装中、エージェントは次のファイルを作成および変更します。

**新しいファイル：**

- `scripts/delivery-estimates.js` — `fetchDeliveryEstimates()`、`getCustomerShippingAddress()`、`formatDeliveryDate()`、`buildCountdownText()`、`findEstimateForCarrier()`の共有モジュール

**変更されたファイル：**

- `blocks/product-details/product-details.js` + `.css` – 右側の列の配信見積もりdiv、メインレンダリング後の非同期取得
- `blocks/commerce-cart/commerce-cart.js` + `.css` – 配送見積divが注文概要を上回りました
- `blocks/commerce-checkout/commerce-checkout.js`、`containers.js`、`.css` — `MutationObserver` ベースの出荷方法ラベル用DOM インジェクション

生成されるコードを確認し、必要に応じて質問したり、担当者に連絡したりできます。

### 手順6：サーバーを起動してテストする

エージェントが実装を完了したら、開発サーバーを起動し、配信の見積もりをテストします。

1. ローカル開発サーバーを起動します。

   ```bash
   npm run start
   ```

1. ブラウザーで買い物客アカウントにログインします。

   PDPおよびカートでの配達見積もりには、デフォルトの配送先住所が保存された認証済みセッションが必要です。

1. 製品ページに移動し、次の結果を確認します。

   | ページ | 期待される結果 | 認証が必要です |
   |------|-----------------|---------------|
   | PDP | &quot;Get it by Thursday, March 12&quot; with optional countdown | はい（ログインのみ） |
   | 買い物かご | 「推定配信日：木、3月12日 – 3月13日（金）」 | はい（ログインのみ） |
   | チェックアウト | 配送方法ごとの「推定配達日：3月12日（木）」 | いいえ（チェックアウト時に入力された住所） |

   {style="table-layout:auto"}

>[!NOTE]
>
>配送業者が一致しない配送方法（定額料金など）では、見積もりは表示されません。 これは設計上のものです。`CARRIER_MAP`でマッピングされたキャリアのみが配信日を取得します。

手動テストを実行するか、担当者にブラウザー機能を使用してテストを依頼します。

```shell-session
Run complete browser testing using the following product page 'http://localhost:3000/products/<product-slug>/<sku>'
```

### ステップ 7：クリーンアップ

テストをスキップまたは完了すると、クリーンアップに進むよう求めるメッセージがエージェントから表示されます。 確認すると、エージェントは実装中に生成されたドキュメントのアーティファクトをアーカイブします。

## トラブルシューティング

チュートリアル中に問題が発生した場合は、次のヒントを参考にしてください。

### バックエンド（App Builder）

| 症状 | 原因 | 修正 |
|---------|-------|-----|
| 管理者UI設定アクションは、「要求は許可されていないパラメーター（予約済みプロパティ）を定義する」を含む`400 Bad Request`を返します | フロントエンドフックは、リクエスト本文に`__ow_method`を送信しています。 `__ow_`でプレフィックスが付いたプロパティは、OpenWhiskによって予約され、アクションに`final: true`が含まれている場合は拒否されます。 | `__ow_method`の代わりにカスタム `method` プロパティを送信します。 バックエンドアクションは最初に`params.method`を読み取り、次に`params.__ow_method`にフォールバックします（Runtimeが自動的に提供します）。 |
| `aio app deploy`が「productDependenciesにmaxVersionが必要です」で失敗する | CLIの検証には、`app.config.yaml`製品の依存関係に`minVersion`と`maxVersion`の両方が必要です。 | `app.config.yaml`の各`productDependencies` エントリに`maxVersion`値を追加します。 |
| デプロイメントコマンドが失敗する | デプロイ前に資格情報が設定されていません。 `.env`、ワークスペースの選択、およびOAuth同期を最初に行う必要があります。 | 正しい順序に従います：`cp env.dist .env` > `aio app use --merge` > `npm run sync-oauth-credentials` > `aio app deploy`。 |

{style="table-layout:auto"}

### ストアフロント（Edge Delivery Services）

| 症状 | 原因 | 修正 |
|---------|-------|-----|
| ログインした買い物客のPDP配信見積もりが表示されない | PDP ブロックは`account` ドロップインを初期化しないため、`getCustomerAddress()`はサイレントで失敗し、見積もりは取得されません。 | アカウント ドロップイン APIに依存する代わりに、`CORE_FETCH_GRAPHQL.fetchGraphQl()`を直接使用して買い物客のアドレスをクエリします。 これはどのページでも機能します。 |
| GraphQLの修正後もPDPが表示されない | メソッド名のタイプミス：`CORE_FETCH_GRAPHQL.fetchGraphQl()`ではなく`CORE_FETCH_GRAPHQL.fetch()`が使用されました。 | 正しいメソッド名を使用してください：`fetchGraphQl` （大文字Q、小文字l）。 |
| 初回読み込み時にチェックアウトの配信日が表示されない | `checkout/updated` イベントリスナーは、`checkout/initialized`が既に起動した後に登録されたため、最初のデータが失われました。 | 登録前に発行されたイベントを取得するために、`{ eager: true }`を持つ`checkout/initialized` リスナーを追加します。 後続の変更のために`checkout/updated` リスナーを保持します。 |
| 買い物かごの配送見積もりが表示されない | `block.appendChild(fragment)`はすべての子をフラグメントから削除するので、`fragment.querySelector('.cart__delivery-estimate')`はnullを返します。 | 追加操作の後に`fragment`ではなく`block`からクエリを実行します。 |
| 定額制の送料では、チェックアウト時に配達日が表示されません | デザイン別 – `CARRIER_MAP`はDPSを標準に、FedexをExpressにのみマッピングします。 Flat Rateには、外部APIに対応するキャリアがありません。 | バグではありません。 他の通信事業者の見積もりを追加するには、`scripts/delivery-estimates.js`の`CARRIER_MAP`を拡張し、バックエンド拡張機能で通信事業者を設定します。 |

{style="table-layout:auto"}

### Commerce SaaS サンドボックス

| 症状 | 原因 | 修正 |
|---------|-------|-----|
| Webhookが`429 Too Many Requests`を返します | [!DNL App Builder] ワークスペースはデバッグモードで、1分あたりのレート制限が厳しくあります。 [!DNL Commerce]は、チェックアウト中に頻繁に配送料を再計算し、割り当てを使い果たします。 | 実稼動ワークスペースにデプロイします（`aio app use`、切り替え、その後`aio app deploy`）。 実稼動ワークスペースには、デバッグ率の制限がありません。 |
| Webhook ソフトタイムアウト警告（>1000ms） | shipping-methods Webhook アクションが[!DNL Commerce] 1000 msのソフトタイムアウトよりも時間がかかりました。 | `aio-lib-state`でサーバーサイドのキャッシュをより積極的に有効にするか、[!DNL Commerce Admin]でWebhook タイムアウトを増やします（Commerce Webhook設定）。 |

{style="table-layout:auto"}

## チュートリアルの概要

このチュートリアルで取り上げたトピックの概要を次に示します。

- **モック APIの設定：** Pipedreamまたは[!DNL App Builder] Runtime アクションを使用してモック配信見積もりAPIを作成しています。
- **BFF パターン：**&#x200B;外部APIをラップし、資格情報をサーバーサイドに保持し、キャッシュを一元化するフロントエンド用バックエンドアクションを構築します。
- **Webhook エンリッチメント：** チェックアウト時に各配送オプションに配達日を挿入するように、配送方法Webhookを拡張します。
- **管理者UIの設定可能性：** [!DNL Admin UI SDK]を使用して設定ページを追加すると、再展開なしでAPI設定、発信元アドレス、およびキャリアのマッピングをマーチャントが管理できるようになります。
- **サービス契約：** バックエンドの拡張機能とストアフロント実装を橋渡しするAPI契約を作成しています。
- **Storefront統合：**&#x200B;共有クライアントモジュールを使用して、PDP （「Get it by」）、カート（日付範囲）、チェックアウト（配送方法ごとに）の配達見積もりを表示しています。
- **非ブロッキング UX:**&#x200B;配信の見積もりが購入フローをブロックしないようにします。ページが最初にレンダリングされ、見積もりが非同期で表示されます。

## 次のステップ

配信見積サービスを拡張するには、次の推奨事項を使用します。

- **実際の通信事業者APIを接続：** [!DNL Admin UI]のサービス URLとAPI キーを変更して、モックをUPS、FedEx、USPSなどのライブ配信APIに置き換えます。
- **匿名の買い物客をサポート：** PDP ページと買い物かごページに郵便番号を追加して、ログインしていない買い物客も配達見積もりを確認できるようにします。
- **配送業者マッピングを拡張：**&#x200B;配送業者コードを`CARRIER_MAP`に追加して、追加の配送方法の配送日を表示します。
- **サーバーサイド キャッシュを追加：** BFF アクションに`aio-lib-state` キャッシュを実装して、繰り返しオリジンと宛先のペアに対する外部APIへの呼び出しを減らします。
- **注文確認に見積もりを表示：**&#x200B;注文確認ページと取引電子メールに予定納期を表示します。
