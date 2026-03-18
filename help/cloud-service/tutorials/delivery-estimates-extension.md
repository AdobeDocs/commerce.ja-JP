---
title: 配信見積もり拡張のチュートリアル
description: App Builder、Edge Delivery Services、AI 支援の開発ツールを使用して、Adobe Commerce as a Cloud Serviceの配信日予測拡張機能を作成する方法を説明します。
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: 3fc8982613df7b1155cdfb08ac4b56de6d1ce4f6
workflow-type: tm+mt
source-wordcount: '3334'
ht-degree: 0%

---

# 配信予測拡張機能のチュートリアル

このチュートリアルでは、[!DNL Adobe Commerce as a Cloud Service]、[!DNL Adobe App Builder] および AI 支援の開発ツールを使用して、[!DNL Edge Delivery Services] の配信日予測拡張機能を構築する手順を説明します。 拡張機能は、外部 API から出荷時間と配信日の見積もりを取得し、ストアフロント全体に表示します。

次の 2 つのパーツを作成します。

- **App Builder拡張機能** – 外部の配信推定 API をラップするバックエンド（フロントエンド）のアクション、チェックアウト時に配信日を使用して発送方法を強化する Webhook、および再デプロイせずに設定を管理するための管理 UI 設定ページ。
- **ストアフロントの統合** – 製品詳細ページ（PDP）、買い物かごページ、チェックアウトページに、ドロップインコンポーネントと共有クライアントモジュール [!DNL Edge Delivery Services] 使用して表示される配信日予測。

>[!NOTE]
>
>AI エージェントは非決定的です。 このチュートリアルのプロンプト、質問および出力は、例です。 エージェントは、異なる質問、要件、またはアーキテクチャの提案を作成する場合があります。 このチュートリアルの例を使用して、エージェントを同様の結果に導きます。

開始する前に、[&#x200B; 前提条件 &#x200B;](./tutorial-prerequisites.md) を完了してください。 このチュートリアルでは、**チェックアウトスターターキット** を使用します。 クローンが既に作成されていて、前提条件ページに記載されている設定手順を完了していることを確認します。

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

上記のコマンドのいずれかで期待される結果が返されない場合は、[&#x200B; 前提条件 &#x200B;](./tutorial-prerequisites.md) を参照してガイダンスを確認してください。

さらに、次の点も確認してください。

- 製品データを含む [!DNL Adobe Commerce as a Cloud Service] インスタンスがあります。 [Commerce Cloud サービスインスタンス &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/cloud-service/overview){target="_blank"} を参照してください。
- [!DNL Commerce] インスタンスに接続されたストアフロントプロジェクトがある。 ストアフロントがない場合は、[&#x200B; ストアフロントの作成 &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=ja){target="_blank"} の手順に従ってください。
- `aem` CLI がインストールされます。

  ```bash
  npm install -g @adobe/aem-cli
  ```

- **買い物客アカウント** があり、保存されたデフォルトの配送先住所を持つ、[!DNL Commerce] に登録された顧客。 PDP および買い物かごページに関する配信予測は、ログインした買い物客にのみ表示されます。 チェックアウトには、認証ステータスに関係なく、すべての買い物客の予測値が表示されます。

>[!IMPORTANT]
>
>このチュートリアルでは、（統合スターターキットではなく） **チェックアウトスターターキット** を使用します。 チェックアウトスターターキットは、支払い、送料、税金、イベントに Webhook ベースの拡張機能を提供します。 チェックアウトキットから Bootstrap を入手してください。

## モック配信推定 API の設定

拡張機能は、外部配信推定 API を呼び出して、発送日時の推定を取得します。 このチュートリアルでは、モック API を使用して、実際の通信事業者アカウントがなくても完全なフローを実行できるようにします。 次の 2 つのオプションを使用できます。

- **オプション A:Pipedream ワークフロー** – 無料層、クイックセットアップですが、月間の呼び出し制限があります。
- **オプション B:App Builder Runtime アクション** — バックエンドの開発手順で作成された、外部の依存関係がない。

>[!TIP]
>
>開発時に、Pipedream （オプション A）から開始し、自由層呼び出し割り当てを達成した場合はランタイムアクション（オプション B）に切り替えることができます。 どちらのオプションも同じ API コントラクトを実装します。

### API の仕様

モック API は POST リクエストを受け入れ、配送業者、輸送日数、締め切り時間、最適な見積もりを使用して、配信日の見積もりを返します。

**リクエスト本文** （モックの場合、すべてのフィールドはオプションです）:

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

**エラー応答：** 401 （API キーがない/無効）、400 （無効な `ship_date` 形式）、503 （ダウンタイムをシミュレート）。

### モックの設定

>[!BEGINTABS]

>[!TAB Pipedream ワークフロー ]

Pipedream オプションは、ベアラートークン認証を使用し、ワークフロートリガー URL への POST リクエストを受け入れます。

| 項目 | 説明 |
|------|-------------|
| ベース URL | 完全な Pipedream ワークフロートリガー URL （例：`https://<id>.m.pipedream.net`） |
| 認証 | `Authorization: Bearer <API_KEY>` |
| メソッド | POST |

{style="table-layout:auto"}

**ワークフローの作成：**

1. [Pipedream](https://pipedream.com){target="_blank"} （**[!UICONTROL Workflows]** > **[!UICONTROL New Workflow]**）で新しいワークフローを作成します。

1. POST 用に設定された **HTTP/Webhook**&#x200B;トリガーを追加します。 Pipedream が Webhook の URL を割り当てます。

1. **Node.js コードを実行** 手順を追加し、次のハンドラーコードを貼り付けます。

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

1. （オプション）ワークフロー設定に `MOCK_API_KEY` 環境変数を追加して、ベアラートークン認証を適用します。 設定されていない場合、任意のリクエストが受け入れられます。

1. ワークフローをデプロイします。

   お使いのエンドポイントは Webhook トリガー URL です。

**モックのテスト：**

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer mock-api-key" \
  -d '{"destination": {"country_code": "US", "postal_code": "10001"}}' \
  "https://<your-endpoint>.m.pipedream.net"
```

>[!TAB App Builder Runtime アクション ]

「App Builder ランタイムアクション」オプションを使用すると、同じ [!DNL App Builder] プロジェクト内でランタイムアクションとしてモックをデプロイできます。 このアプローチには、外部の依存関係や呼び出しクォータはありません。

エージェントに対して、モックアクションを作成するように求めます。

```shell-session
Add a new runtime action to this project that implements the API in @docs/PIPEDREAM_API_SPEC.md
- Add it to a separate package
- Use the code in docs/pipedream as inspiration
```

エージェントは、Pipedream オプションと同じ API 契約で `actions/mock-delivery-api/index.js` を作成します。 デプロイ後、エンドポイントは次のようになります。

```shell-session
https://<namespace>.adobeioruntime.net/api/v1/web/mock-delivery-api/delivery-estimate
```

認証は、`MOCK_API_KEY` の `.env` 環境変数に対して検証されます。

>[!ENDTABS]

## 拡張機能の開発

このセクションでは、配信予測拡張機能の [!DNL App Builder] バックエンドの開発について説明します。 バックエンドには次の 3 つのアクションがあります。

| アクション | タイプ | 目的 |
|--------|------|---------|
| `delivery-estimates` | スタンドアロン Web アクション | ストアフロントの BFF — PDP と買い物かごでは、配信日についてこれを呼び出します |
| `shipping-methods` | Webhook アクション | チェックアウト時に配送日を使用して配送料 `additional_data` 強化 |
| `delivery-estimates-config` | 管理バックエンドアクション | `aio-lib-state` に保存されている設定用の CRUD |

{style="table-layout:auto"}

1. コーディングエージェントの MCP 設定で、`commerce-extensibility` ツールセットがエラーなく有効になっていることを確認します。

   例えば、カーソルでは、**[!UICONTROL Cursor]**/**[!UICONTROL Settings]**/**[!UICONTROL Cursor Settings]**/**[!UICONTROL Tools & MCP]** に移動します。

   エラーが表示された場合は、ツールセットのオン/オフを切り替えます。

   >[!NOTE]
   >
   >AI 支援による開発ツールを使用する場合、エージェントによって生成されるコードと応答に自然なバリエーションが生じることを期待してください。
   >コードで問題が発生した場合は、デバッグの支援をエージェントに依頼します。

1. カーソルのコンテキストにドキュメントを追加した場合は、無効にします。

   **[!UICONTROL Cursor]**/**[!UICONTROL Settings]**/**[!UICONTROL Cursor Settings]**/**[!UICONTROL Indexing & Docs]** に移動し、一覧表示されているドキュメントをすべて削除します。

### 手順 1：最初のプロンプトを指定する

エージェントにコンテキストの外部 API 仕様を指定し、開始を促します。 エージェントに停止して質問するように伝えることで、実装を早期に導くのに役立ちます。

エージェントのチャットウィンドウに次のプロンプトを入力します。

```shell-session
I want to build an Adobe App Builder extension that extends the checkout with shipping date and time estimates taken from an external API described in @docs/API_SPEC.md.
Delivery dates for a product will be shown in the product details page and on the cart page.
Implement this feature by using the skills in this workspace for backend code, and a separate workspace with storefront skills. For this extension, focus on the backend skills and create an API_SPEC to hand work over to the storefront skills.

STOP and ask me clarifying questions about the requirements before you do any work.
```

>[!TIP]
>
>プロンプトで外部 API 仕様ファイル（`@docs/API_SPEC.md`）を参照すると、サードパーティの API 契約に関する具体的なコンテキストがエージェントに提供されます。 エージェントはこれを使用して、BFF アクション、共有 HTTP クライアント、管理 UI 設定の各フィールドをデザインします。 エージェントに停止して質問するように指示すると、ガイド付きワークフローがトリガーに表示され、実装を早期に導くことができます。

### 手順 2：エージェントの質問に回答する

エージェントは、ターゲット環境（PaaS と SaaS）、範囲（スタンドアロン BFF アクション、Webhook エンリッチメント、またはその両方）、接触チャネルアドレスソース、キャッシュ戦略、テスト環境設定などのトピックをカバーする一連の明確な質問を返します。 次の例は、一般的な質問と回答を示しています。 エージェントが異なる質問をする場合がありますが、トピックは一般的に同じです。

**エージェントの質問の例：**

1. **対象環境** - PaaS （オンプレミス）または SaaS （Adobe Commerce as a Cloud Service）用に構築していますか？
2. **範囲** – これは、スタンドアロンの BFF アクション（ストアフロントによって直接呼び出される）、Webhook エンリッチメント（チェックアウト時に配送方法を拡張）またはその両方にする必要がありますか？
3. **管理者の設定可能性** - API URL、API キー、接触チャネルアドレスなどの設定は、Commerce管理者で設定できるか、`.env` に保存できるか？
4. **出荷元住所**：出荷元（倉庫）住所の送信元はどこですか？ 静的な設定にするか、動的に解決する必要がありますか？
5. **キャッシュ** – 外部 API への呼び出しを減らすために、配信予測をサーバーサイドでキャッシュする必要がありますか？ その場合、TTL はどれくらいですか？

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
>ストアフロントがサードパーティ API を直接呼び出すか、ランタイムアクションを実行するかをエージェントに確認すると、アーキテクチャに関する便利なトリガーが表示されます。 このエージェントは、BFF （Backend-for-Frontend）パターンのメリットを説明しています。API キーがサーバーサイドのままであり、CORS が処理され、キャッシュが一元化され、ベンダーの抽象化が実現します。 管理 UI 設定を要求すると、エージェントは `aio-lib-state` ではなく `.env` にすべての設定を保存するようにプッシュされるので、設定を変更する際の再展開が不要になります。

>[!NOTE]
>
>あなたのエージェントは異なる質問をする可能性があります。 これらの回答は、エージェントを同じ機能結果に導くためのガイダンスとして使用します。例えば、ストアフロント呼び出しの BFF アクション、チェックアウトエンリッチメントの発送方法 Webhook、`aio-lib-state` で設定を保存する管理 UI 設定ページです。

### 手順 3：要件とアーキテクチャのレビュー

エージェントは、確認する要件およびアーキテクチャ文書を生成します。 要件が提供した回答と一致し、アーキテクチャが次の内容をカバーしていることを確認します。

- **BFF アクション** （`delivery-estimates`） – ストアフロントが PDP および買い物かごページから呼び出すスタンドアロン web アクション。 `aio-lib-state` から設定を読み取り、外部配信推定 API を呼び出して、フォーマットされた推定を返します。
- **webhook アクション** （`shipping-methods`） – チェックアウト時に `additional_data` で配送日を使用して配送料を強化します。 `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` Webhook メソッドを使用します。
- **管理設定アクション** （`delivery-estimates-config`） - `aio-lib-state` に保存されている設定（API URL、API キー、接触チャネル アドレス、キャリア、キャッシュ TTL）の CRUD。
- **共有ライブラリ** – 外部 API 用の HTTP クライアントと、`aio-lib-state` ータの読み取りおよび書き込み用の設定モジュール。

>[!NOTE]
>
>AI エージェントは非決定的で、その動作はモデルや IDE によって異なります。 異なる要件やアーキテクチャを生み出す異なる質問セットが得られる場合があります。 その場合は、続行する前に、このチュートリアルで示している内容に厳密に一致する実装を使用するように、エージェントを設定してください。

### 手順 4：実装計画の選択

エージェントでは、詳細な導入計画を作成するか、直接導入を完了するかを選択できます。

- より詳細な制御を行いながら段階的に実行できる表示可能なプランが必要な場合は、最初のオプションを選択します。
- エージェントが最小限の介入で完全な実装を行う場合は、2 番目のオプションを選択します。

### 手順 5：クリーンアップとデプロイ

エージェントは、実装が完了すると、クリーンアップに進みます。 出荷ドメインのみが使用されているため、エージェントは未使用の基礎モードを削除します。

- 支払いアクションと設定（`validate-payment/`、`filter-payment/`、`payment-methods.yaml`）
- 税務アクションおよび設定（`collect-taxes/`、`collect-adjustment-taxes/`、`tax-integrations.yaml`）
- イベントのアクションと設定（`commerce-events/`、`3rd-party-events/`、`events.config.yaml`）
- 汎用基礎モード （`generic/`）
- 他のドメインの管理 UI SPA コンポーネント（税金関連のページやフックなど）
- 未使用のスクリプト、テストファイル、環境変数

>[!TIP]
>
>他のドメインからの残りの情報についても、管理 UI SPA で確認するようにエージェントに依頼します。 税クラス ページとそのフックは、スターターキットの基礎モードから引き続き存在する場合があり、削除する必要があります。

クリーンアップ後、次の手順を使用してデプロイします **この順序で**。

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
>手順をスキップまたは並べ替えないでください。 デプロイメントの前提条件は、手順 1 ～ 3 です。 資格情報が設定されていない場合、`aio app deploy` コマンドは失敗します。

### 手順 6:Webhook と管理 UI の設定

デプロイ後、出荷 Webhook を設定します。 エージェントは、プログラムで登録するスクリプトを作成できます。

```bash
npm run subscribe-webhook
```

このコマンドは、次の設定で配送 Webhook を登録します。

| フィールド | 値 |
|-------|-------|
| Webhook メソッド | `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` |
| Webhook タイプ | `after` |
| 必須 | 任意（デフォルトの配送へのフォールバックを許可） |
| タイムアウト | 5000 ミリ秒 |

{style="table-layout:auto"}

>[!NOTE]
>
>SaaS の場合、Webhook メソッド名はパスから `magento.` をドロップします。 PaaS の Webhook 名は `plugin.magento.out_of_process_shipping_methods...` で、SaaS の Webhook 名は `plugin.out_of_process_shipping_methods...` です。

次に、管理 UI を設定します。

1. **管理 UI SDK** を有効にします（**[!UICONTROL Stores]**/**[!UICONTROL Settings]**/**[!UICONTROL Configuration]**/**[!UICONTROL Adobe Services]**/**[!UICONTROL Admin UI SDK]**/**[!UICONTROL Enable]**/**[!UICONTROL Yes]**）。

1. [!DNL App Builder] ワークスペースと拡張機能を選択して拡張機能を設定します。

1. 「**[!UICONTROL Refresh registrations]**」をクリックします。

1. **[!UICONTROL Apps]** サイドバーの **[!UICONTROL Delivery Estimates]**/[!DNL Admin] に移動します。

1. 機能を有効にし、API URL と API キー、発信元アドレス、デフォルトのキャリア、キャッシュ TTL、キャリア コード マッピングなどの必要な設定を指定して、設定を完了します。

### 手順 7：拡張機能をテストする

配信推定 BFF アクションを直接テストします。

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

バックエンドが完了したので、エージェントにストアフロント作業用のサービス契約を作成するよう依頼します。

```shell-session
Produce a spec called STOREFRONT_API_SPEC that I can use in the storefront workspace with the corresponding agent. Also give me a prompt that I could use in that workspace.
```

エージェントは、完全な BFF エンドポイント契約（リクエストと応答の形式、例えばペイロード、エラー処理）と、ストアフロントワークスペースのすぐに使用できるプロンプトを含んだ `docs/STOREFRONT_API_SPEC.md` ールを生成します。

ストアフロントの開発手順を開始する前に、このファイルをストアフロントプロジェクトにコピーします。

>[!TIP]
>
>エージェントがサービス契約 **および** もう一方のワークスペースのプロンプトの両方を生成することで、バックエンドチームとストアフロントチーム（またはエージェント）の間でクリーンなハンドオフが保証されます。 ストアフロントエージェントは、API について質問しなくても、すぐに作業を開始できます。

## ストアフロントに接続

このセクションでは、[!DNL Edge Delivery Services] および AI を利用した開発ツールを使用して、配信予測拡張機能のストアフロント部分を実装する手順を説明します。 PDP、買い物かごページ、チェックアウトページに配信日予測を追加します。

>[!NOTE]
>
>表示されるプロンプトは開始点です。 変更せずに使用できますが、エージェントと自然に会話することを検討してください。
>
>AI 支援開発ツールを使用する場合、エージェントによって生成されるコードと応答には常に自然なバリエーションがあります。
>
>コードで問題が発生した場合は、デバッグの支援をエージェントに依頼します。

### ストアフロントの前提条件

ストアフロントの統合を開始する前に、次の点を確認してください。

- [!DNL Commerce] インスタンスに接続されたストアフロントプロジェクト
- Commerce ストアフロントの AI ツール [CLI を使用してインストール &#x200B;](./tutorial-prerequisites.md#install-the-storefront-ai-tools)
- ストアフロントプロジェクトの `STOREFRONT_API_SPEC.md` フォルダーにコピーされた `docs/` ファイル

### 手順 1：環境を検証する

`config.json` ファイルを開き、`commerce-core-endpoint` と `commerce-endpoint` の値が [!DNL Adobe Commerce as a Cloud Service] GraphQL エンドポイントを指していることを確認します。

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### 手順 2：最初のプロンプトを指定する

サービス契約がプロジェクトに既に存在する場合は、エージェントに対して、ストアフロント統合を実装するように促します。 エージェントで **プラン** モードが使用可能な場合は、そのモードを使用して、エージェントがプランなしで進行しないようにします。

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
>バックエンドエージェントから完全な API 契約が既に使用可能になっているので、プロンプトが詳細になります。 `@docs/STOREFRONT_API_SPEC.md` を参照することで、エージェントはエンドポイントの正確な URL、リクエストと応答の形式、エラー処理を把握します。 明示的な要件リストにより、エージェントはスコープを発明できません。 特に、プランモードをリクエストすると、実装を早期に進めるのに役立つ段階的なワークフローがトリガーされます。

### 手順 3：明確な質問に回答する

エージェントは、認証範囲、チェックアウトアプローチおよびスタイル設定に関する質問を返します。 次の例は、一般的な質問と回答を示しています。

**エージェントの質問の例：**

1. **匿名ユーザーとログインユーザー** – すべての買い物客について、または認証済みの買い物客についてのみ、PDP および買い物かごページに表示される予測値を指定できます。
2. **チェックアウトアプローチ** - ShippingMethods ドロップインコンテナは `additional_data` を公開しないので、エージェントは次の 2 つのオプションを提案します。
   - **オプション A:** チェックアウト時に BFF を呼び出して、配信日を DOM 挿入する（よりシンプルで、PDP/買い物かごと一致）
   - **オプション B:** `overrideGQLOperations` を使用してチェックアウトGraphQL フラグメントを拡張し、`additional_data` を含めます
3. **スタイル設定** – 絵文字と既存のデザイントークン

**回答の例：**

```shell-session
1. Only for logged-in users — that way we can use the shopper's default shipping address and avoid a zip code input
2. Let's do Option A if feasible
3. Use anything that matches the current styling
```

>[!TIP]
>
>ログインした買い物客に対してのみ見積もりを表示することは、実用的な選択です。 エージェントは、買い物客のデフォルトの配送先住所を（GraphQL経由で）自動的に使用できるので、郵便番号を入力する必要はありません。 PDP や買い物かごでの匿名の買い物客は、郵便番号の入力が必要になり、摩擦が生じます。 配送先住所が既に入力されているため、チェックアウト時にすべての買い物客に配送日が表示されます。

>[!NOTE]
>
>あなたのエージェントは異なる質問をする可能性があります。 次の回答をガイダンスとして使用します。
>
>- ログインした買い物客に対してのみ PDP と買い物かごの見積りを表示します（郵便番号の入力は不要）。
>- チェックアウトについては、わかりやすくするためにオプション A （BFF 呼び出し+ DOM 挿入）を使用します。
>- スタイル設定に既存のデザイントークンを使用します。

### 手順 4：要件とアーキテクチャのレビュー

エージェントは、共有モジュールアーキテクチャを設計します。 次の内容が含まれていることを確認します。

| コンポーネント | 目的 |
|-----------|---------|
| `scripts/delivery-estimates.js` | 共有モジュール：BFF クライアント、キャッシュ（sessionStorage、30 分 TTL）、日付フォーマット、カウントダウン・ロジック、顧客アドレス・ルックアップ、通信事業者マッピング |
| PDP 統合 | 価格と説明の間のオプションのカウントダウンを使用して、「[ 日付 ] で取得」を表示します |
| 買い物かごの統合 | 日付範囲（「3 月 12 日（木）～3 月 13 日（金）」）を注文概要の右側の列に表示します |
| チェックアウトの統合 | 配送ステップがアクティブなときに BFF を呼び出し、DOM が `MutationObserver` を介して配信日を挿入する |

{style="table-layout:auto"}

検証すべき主な設計上の決定：

- すべての BFF 呼び出しはノンブロッキングです。ページが最初にレンダリングされると、見積もりは非同期で表示されます。
- すべてのエラーはサイレント型で、買い物客 `console.debug` 直面するエラーはありません。
- `CARRIER_MAP` は、Commerceの通信事業者コード（DPS、Fedex）を BFF の通信事業者コード（標準、高速）にマッピングします。
- Dynamic `import()` は、配信モジュールを重要なレンダリングパスから除外します。

>[!NOTE]
>
>AI エージェントは非決定的で、その動作はモデルや IDE によって異なります。 異なる要件やアーキテクチャを生み出す異なる質問セットが得られる場合があります。 その場合は、続行する前に、このチュートリアルで示している内容に厳密に一致する実装を使用するように、エージェントを設定してください。

### 手順 5：実装計画の選択

エージェントでは、詳細な導入計画を作成するか、直接導入を完了するかを選択できます。

- より詳細な制御を行いながら段階的に実行できる表示可能なプランが必要な場合は、最初のオプションを選択します。
- エージェントが最小限の介入で完全な実装を行う場合は、2 番目のオプションを選択します。

実装時に、エージェントは以下のファイルを作成および変更します。

**新しいファイル：**

- `scripts/delivery-estimates.js` - `fetchDeliveryEstimates()`、`getCustomerShippingAddress()`、`formatDeliveryDate()`、`buildCountdownText()`、`findEstimateForCarrier()` との共有モジュール

**変更されたファイル：**

- `blocks/product-details/product-details.js` + `.css` – 右側の列にある配信推定 div、メインレンダリング後の非同期取得
- `blocks/commerce-cart/commerce-cart.js` + `.css` – 上記の注文概要の配信見積り div
- `blocks/commerce-checkout/commerce-checkout.js`、`containers.js`、`.css` – 発送方法ラベル用の `MutationObserver` ベースの DOM 挿入

生成されるコードを監視し、必要に応じて質問したり、エージェントをリダイレクトしたりできます。

### 手順 6：サーバーを起動してテストする

エージェントによる実装が完了したら、開発サーバーを起動して、配信の見積もりをテストします。

1. ローカル開発サーバーを起動します。

   ```bash
   npm run start
   ```

1. ブラウザーで、買い物客アカウントにログインします。

   PDP と買い物かごに関する配信の予測には、保存されたデフォルトの配送先住所を使用した、認証済みセッションが必要です。

1. 製品ページに移動して、次の結果を確認します。

   | ページ | 期待される結果 | 認証が必要 |
   |------|-----------------|---------------|
   | PDP | 「3 月 12 日（木）までに入手」とカウントダウン（オプション） | はい（ログインのみ） |
   | カート | 「納品予定日：3 月 12 日（木）～3 月 13 日（金）」 | はい（ログインのみ） |
   | チェックアウト | 発送方法ごとの「推定配送：3 月 12 日木曜日（PT）」 | いいえ（チェックアウト時に入力された住所） |

   {style="table-layout:auto"}

>[!NOTE]
>
>一致する配送業者のない配送方法（定額料金など）では、見積もりは表示されません。 これは意図的なもので、`CARRIER_MAP` にマッピングされた通信事業者のみが配信日を取得します。

手動でテストを実行することも、エージェントに対してブラウザー機能を使用してテストを実行するように依頼することもできます。

```shell-session
Run complete browser testing using the following product page 'http://localhost:3000/products/<product-slug>/<sku>'
```

### 手順 7：クリーンアップ

テストをスキップまたは完了すると、クリーンアップに進むように求められます。 確認後、エージェントは実装時に生成されたドキュメントアーティファクトをアーカイブします。

## トラブルシューティング

チュートリアル中に問題が発生した場合は、次のヒントを参考にしてください。

### バックエンド（App Builder）

| 症状 | 原因： | 修正 |
|---------|-------|-----|
| 管理 UI 設定アクションで、「リクエストが、許可されていないパラメーターを定義する（予約済みのプロパティ）」を含む `400 Bad Request` が返される | フロントエンドフックがリクエスト本文で `__ow_method` を送信しています。 先頭に `__ow_` が付いたプロパティは、OpenWhisk によって予約され、アクションが `final: true` 了すると拒否されます。 | `method` の代わりにカスタム `__ow_method` プロパティを送信します。 バックエンドアクションは、最初に `params.method` を読み取り、次に `params.__ow_method` （Runtime が自動的に提供する）にフォールバックします。 |
| `aio app deploy` が失敗し、「productDependencies に maxVersion が必要です」と表示される | CLI の検証では、製品の依存関係に `minVersion` と `maxVersion` の両方 `app.config.yaml` 必要です。 | `maxVersion` の各 `productDependencies` エントリに `app.config.yaml` 値を追加します。 |
| 展開コマンドが失敗する | デプロイ前に資格情報が設定されていません。 `.env`、ワークスペースの選択、OAuth 同期が最初に行われる必要があります。 | 正しい順序（`cp env.dist .env`/`aio app use --merge`/`npm run sync-oauth-credentials`/`aio app deploy`）に従います。 |

{style="table-layout:auto"}

### ストアフロント（Edge Delivery Services）

| 症状 | 原因： | 修正 |
|---------|-------|-----|
| ログインした買い物客に対して PDP 配信予測が表示されない | PDP ブロックは `account` のドロップインを初期化しないので、`getCustomerAddress()` はサイレントに失敗し、見積もりは取得されません。 | `CORE_FETCH_GRAPHQL.fetchGraphQl()` を使用すると、アカウントのドロップダウン API を使用する代わりに、買い物客アドレスを直接クエリできます。 これは、どのページでも機能します。 |
| GraphQLの修正後、PDP がまだ表示されない | メソッド名に入力された誤字：`CORE_FETCH_GRAPHQL.fetch()` の代わりに `CORE_FETCH_GRAPHQL.fetchGraphQl()` が使用されました。 | 正しいメソッド名 `fetchGraphQl` （大文字 Q、小文字 l）を使用します。 |
| チェックアウトの配信日が最初の読み込みに表示されない | `checkout/updated` イベントリスナーは `checkout/initialized` が既に実行された後に登録されたので、最初のデータが欠落していました。 | 登録前に発行されたイベントを取得する `checkout/initialized` を持つ `{ eager: true }` リスナーを追加します。 後続の変更に対して `checkout/updated` リスナーを保持します。 |
| 買い物かごの配信予測が表示されない | `block.appendChild(fragment)` はすべての子をフラグメントから移動するので、`fragment.querySelector('.cart__delivery-estimate')` は null を返します。 | 追加操作の後に、`block` ではなく `fragment` からクエリします。 |
| 定率配送でチェックアウト時に配送日が表示されない | 設計上 – `CARRIER_MAP` は DPS を標準に、Fedex を表現にマッピングするだけです。 外部 API に対応する通信事業者がありません。 | バグではありません。 他の通信事業者の見積もりを追加するには、`CARRIER_MAP` で `scripts/delivery-estimates.js` を拡張し、バックエンド拡張機能で通信事業者を設定します。 |

{style="table-layout:auto"}

### Commerce SaaS サンドボックス

| 症状 | 原因： | 修正 |
|---------|-------|-----|
| Webhook は `429 Too Many Requests` を返します | [!DNL App Builder] workspace はデバッグモードになっています。このモードでは、1 分あたりのレートに厳密な制限があります。 [!DNL Commerce] では、チェックアウト時に頻繁に配送料を再計算して、割り当て量を使い果たします。 | 実稼動ワークスペースにデプロイします（切り替える `aio app use`、切り替える `aio app deploy`）。 実稼動ワークスペースには、デバッグレートの制限がありません。 |
| Webhook ソフトタイムアウト警告（>1000ms） | 発送方法の Webhook アクションが、[!DNL Commerce] 1000 ms のソフトタイムアウトよりも時間がかかりました。 | `aio-lib-state` でサーバーサイドキャッシュをより積極的に有効にするか、[!DNL Commerce Admin] で Webhook タイムアウトを増やします（Commerce Webhook 設定）。 |

{style="table-layout:auto"}

## チュートリアルの概要

このチュートリアルで扱うトピックの概要は次のとおりです。

- **モック API の設定：** Pipedream または [!DNL App Builder] Runtime アクションを使用して、モック配信見積もり API を作成します。
- **BFF パターン：** 外部 API をラップし、認証情報をサーバーサイドに保持し、キャッシュを一元化するバックエンドを使用したフロントエンドアクションを作成します。
- **Webhook の強化：** 配送方法 Webhook を拡張して、チェックアウト時に各配送オプションに配送日を挿入します。
- **管理 UI の設定機能：** [!DNL Admin UI SDK] を使用して設定ページを追加し、マーチャントが再デプロイメントなしで API 設定、接触チャネルアドレスおよび通信事業者マッピングを管理できるようにします。
- **サービス契約：** バックエンドの拡張機能とストアフロントの実装を橋渡しする API コントラクトを作成しています。
- **ストアフロントの統合：** 共有クライアントモジュールを使用して、PDP （「入手」）、買い物かご（日付範囲）、チェックアウト（出荷方法ごと）に関する配信の推定を表示します。
- **ノンブロッキング UX:** 配信予測が購入フローをブロックしないことを確認します。ページが最初にレンダリングされ、予測が非同期で表示されます。

## 次の手順

次の推奨事項を使用して、配信予測サービスを拡張します。

- **実際の通信事業者 API に接続：** [!DNL Admin UI] のサービス URL と API キーを変更して、モックを UPS、FedEx、USPS などのライブ配送 API に置き換えます。
- **匿名の買い物客をサポート：** PDP および買い物かごページへの郵便番号の入力を追加して、ログインしていない買い物客が配信の見積もりを表示できるようにします。
- **配送業者マッピングの拡張：** 配送業者に配送業者コードを追加して、追加の配送方法の配送日を表示で `CARRIER_MAP` ます。
- **サーバーサイドのキャッシュを追加：** BFF アクションに `aio-lib-state` ーバーサイドのキャッシュを実装して、繰り返しオリジンと宛先のペアに対する外部 API への呼び出しを減らします。
- **注文確認に見積もりを表示：** 注文確認ページとトランザクションメールに推定配信日を表示します。
