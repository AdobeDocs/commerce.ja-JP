---
title: 在庫通知拡張機能のチュートリアル
description: App Builder、Edge Delivery Services、AI支援の開発ツールを使用して、Adobe Commerce as a Cloud Serviceの在庫通知拡張機能を構築する方法について説明します。
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
source-wordcount: '2693'
ht-degree: 0%

---

# 在庫通知拡張機能のチュートリアル

このチュートリアルでは、[!DNL Adobe App Builder]とAI支援の開発ツールを使用して、[!DNL Adobe Commerce as a Cloud Service]の在庫通知拡張機能を作成する方法を説明します。 この拡張機能は、買い物客が在庫切れ商品を購入し、在庫が戻ったときに通知を受け取ることができるようにします。

次の2つの部分を作成します。

- **App Builder拡張機能** — イベント駆動型およびスケジュール型の再入荷検出機能を使用して、在庫切れのサブスクリプション（作成、読み取り、削除）を管理するためのREST API。
- **Storefront統合** – 選択した製品またはバリエーションが在庫切れの場合にのみ表示される、製品詳細ページ（PDP）のサブスクリプションフォーム。

>[!NOTE]
>
>AI エージェントは非決定論的です。 このチュートリアルのプロンプト、質問、および出力は例です。 担当者がさまざまな質問、要件、アーキテクチャの提案を作成する場合もあります。 このチュートリアルの例を使用して、類似の結果に向けてエージェントを誘導します。

開始する前に、[前提条件](./tutorial-prerequisites.md)を完了してください。 このチュートリアルでは、**統合スターターキット**&#x200B;を使用します。 既にクローンを作成し、前提条件ページで説明されている設定手順を完了していることを確認します。

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

- 製品データを含む[!DNL Adobe Commerce as a Cloud Service] インスタンスがあります。 [Commerce Cloud サービスインスタンス &#x200B;](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview){target="_blank"}を参照してください。
- [!DNL Commerce] インスタンスに接続されたストアフロントプロジェクトがあります。 ストアフロントがない場合は、[&#x200B; ストアフロントの作成](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/){target="_blank"}の手順に従います。
- `aem` CLIがインストールされています：

  ```bash
  npm install -g @adobe/aem-cli
  ```

## 拡張機能の開発

このセクションでは、AI支援の開発ツールを使用して、[!DNL Adobe Commerce as a Cloud Service]の在庫通知拡張機能を開発する方法を説明します。 この拡張機能は、サブスクリプション管理用のREST APIを提供し、Commerce イベントとスケジュールされたチェックを通じて商品が再入荷したときに検出します。

1. コーディングエージェントのMCP設定に移動します。

   例えば、カーソルで、**[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**&#x200B;に移動します。 エラーなしで`commerce-extensibility` ツールセットが有効になっていることを確認します。 エラーが表示された場合は、ツールセットのオンとオフを切り替えます。

   >[!NOTE]
   >
   >AI支援の開発ツールを使用する場合、エージェントによって生成されたコードと応答に自然なバリエーションが存在することを期待します。
   >コードで問題が発生した場合は、担当者にデバッグのサポートを依頼してください。

1. Cursorのコンテキストにドキュメントが追加されている場合は、そのドキュメントを無効にします。

   **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Indexing & Docs]**&#x200B;に移動し、一覧されているドキュメントをすべて削除します。

### 手順1：最初のプロンプトを入力する

AI エージェントに実装を開始するよう促します。 エージェントに停止して質問するように伝えることで、実装を早い段階で導くことができます。

担当者のチャットウィンドウに次のプロンプトを入力します。

```shell-session
Implement an Adobe Commerce as a Cloud Service extension to handle out-of-stock notifications for products.

The service should provide REST API endpoints for basic create, read, update, and delete (CRUD) operations on out-of-stock notifications, allowing storefronts to manage notifications for specific product SKUs.

Back-in-stock is detected by an inventory or product event or a scheduled action that checks Commerce API and then calls the REST API to send the notification.

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>処理を進める前にエージェントに停止して質問するように伝えることで、プロセスの早い段階で実装を誘導できます。 このプロセスにより、主要な仮定と欠けている要件が早期に特定され、このチュートリアルでガイド付きワークフローを開始するために必要になります。

### ステップ 2：担当者の質問に答える

担当者は、解決策の策定を開始する前に、必要な一連の質問を返します。 次の例は、典型的な質問と回答を示しています。 担当者は異なる質問をすることもありますが、トピックは一般的に同じです。

**エージェントの質問の例：**

1. **REST API — ホストおよびコンシューマー** — CRUD REST APIは、ストアフロントが呼び出すこのApp Builder アプリ（Adobe I/O Runtimeのweb アクションなど）に含める必要がありますか？ 誰が呼ぶのか（EDS Storefront、カスタム/ヘッドレスストアフロント、またはその両方）? CORS、公開（未認証）アクセスが必要ですか、それとも発信者はAPI キー、OAuth、またはCommerce トークンを使用しますか？
1. **データモデル** — 1つの「通知」は何を表すべきですか？ 顧客識別子（メールのみ、または顧客ID）? 商品識別子（SKUのみ、またはSKU + ストアビュー）? 同じ顧客が同じSKUを複数回購読することはできますか。または、購読を重複排除する必要がありますか？
1. **在庫再入荷の検出 – イベントとスケジュール済みの商品の比較** — イベント駆動型の検出（Commerceからの在庫/商品イベントに反応）、スケジュール済みの検出（在庫を定期的にチェックするスケジュール済みのアクション）、またはその両方を希望しますか？ 「通知を送信」とは、何を意味しますか（外部Webhookを呼び出す、メールを送信する、またはログに記録する）?
1. **在庫戻り – Commerce ソース** – 任意のイベント名を使用しますか？または、デザインでCommerceが提供する在庫/在庫更新イベントを使用する必要がありますか？ スケジュールされたチェックの場合、SKUで在庫状況を取得するためにどのAPIを使用する必要がありますか？
1. **永続性とマルチテナンシー** — `aio-lib-state`はサブスクリプションを永続化するのに適した場所ですか、それとも外部ストアを持っていますか？ デザインはマルチテナントまたはシングルテナントを前提とすべきですか？
1. **CRUD セマンティクスとライフサイクル** — 「削除」はサブスクリプションの解約を意味しますか？ 「更新」が必要ですか？ 再入荷通知を送信した後、サブスクリプションを自動的に削除するか、通知済みとしてマークする必要がありますか？
1. **非機能** – 適用するレート制限または最大サブスクリプション数はありますか？ コンプライアンスに関するニーズ（ダブルオプトイン、同意フラグ）はありますか？

**回答の例：**

```shell-session
1. The CRUD REST API should be part of thie App Builder app. It will be called by the EDS Storefront. For this implementation there is no need for API keys or security tokens.
2. For this initial implementation the customer identifier will be the email, product is identified by SKU, customer emails should not be able to subscribe to the same SKU multiple times.
3. Implement both. For now instead of sending the notification, log it so I can audit in the Adobe Developer Console.
4. Research and use what the best event to use that commerce already provides. Research the simplest way to get the stock status by SKU.
5. Use the aio-lib-state. Single tenant for now
6. Delete means cancel subscription. Skip Update, it does not apply for this service. After subscription is sent, it should be marked as notified or removed so it won't send again until the user subscribes again.
7. No limits. Implement minimal compliance requirements.
```

>[!NOTE]
>
>担当者がさまざまな質問をする場合があります。 これらの回答を、エージェントを同じ機能的な結果に導くためのガイダンスとして使用します。メールとSKUのサブスクリプションを備えたREST API、イベント駆動型およびスケジュール型の在庫戻し検出、`aio-lib-state`永続性、ログベースの通知です。

### ステップ 3：要件とアーキテクチャの見直し

担当者は、レビューする要件とアーキテクチャドキュメントを生成します。 要件が指定した回答と一致し、アーキテクチャがカバーしていることを確認します。

- サブスクリプション CRUDのREST API アクション（作成、読み取り、更新、削除）
- Commerceの在庫イベントによってトリガーされる、イベント駆動型の在庫戻しハンドラー
- フォールバックとしてのスケジュールされたチェックストックアクション
- `aio-lib-state`を使用した永続性

>[!NOTE]
>
>AI エージェントは非決定論的で、モデルとIDEによって動作が異なります。 異なる要件とアーキテクチャのセットを生成する、異なる質問のセットが表示される場合があります。 その場合は、実装がこのチュートリアルに記載されている内容と密接に一致するようにエージェントを誘導してから先に進んでください。

### 手順4：実行計画の選択

担当者は、詳細な実装計画を作成するか、直接実装を完了するかを選択できます。

- より詳細に制御して段階的に実行できるレビュー可能なプランが必要な場合は、最初のオプションを選択します。
- エージェントに最小限の介入で完全な実装を行わせたい場合は、2番目のオプションを選択します。

### 手順5：イベントのデプロイ、オンボーディング、購読

エージェントが実装を完了すると、次の手順でアプリをデプロイし、Commerce インスタンスをオンボーディングして、次のコマンドを使用してイベントをサブスクライブします。

1. 拡張機能をデプロイします。

   ```bash
   aio app deploy
   ```

1. オンボーディングスクリプトを実行して、イベントプロバイダーをCommerceに登録します。

   ```bash
   npm run onboard
   ```

1. Commerce イベントの購入：

   ```bash
   npm run commerce-event-subscribe
   ```

1. イベントのサブスクリプションを検証します。

   Commerce インスタンスに移動し、**[!UICONTROL System]** > **[!UICONTROL Event Subscriptions]**&#x200B;を開きます。

   イベントレコードのテーブルが表示されます。

   ![&#x200B; イベント購読セクションを強調表示するCommerce管理メニュー](../assets/in-stock-event-subscriptions.png){width="600" zoomable="yes"}

   ![登録済みイベントエントリを含むイベント購読テーブル &#x200B;](../assets/in-stock-event-table.png){width="600" zoomable="yes"}

### 手順6：拡張機能のテスト

担当者にテスト手順を依頼します。 これはAPI サービスなので、コマンドライン命令をリクエストできます。

```shell-session
Give me step by step instructions to test the API service from the command line.
```

エージェントが提供する手順に従います。 次に、一般的なテストコマンドの例を示します。

**SKUの購読：**

```bash
API_URL="https://<your-runtime-url>/api/v1/web/notify-out-of-stock/api"; curl -X POST "$API_URL" \
  -H "Content-Type: application/json" \
  -d '{"email":"test@example.com","sku":"ADB153"}'
```

応答は次のようになります。

```json
{
  "createdAt": "2026-03-06T22:11:00.308Z",
  "email": "test@example.com",
  "id": "b3353bf5-1007-4b10-989d-430892dd4a66",
  "sku": "ADB153"
}
```

**すべてのサブスクリプションを一覧表示：**

```bash
curl -X GET "$API_URL"
```

応答は、アクティブなすべてのサブスクリプションのリストを返します。

```json
{
  "subscriptions": [
    {
      "createdAt": "2026-03-06T22:11:00.308Z",
      "email": "test@example.com",
      "id": "b3353bf5-1007-4b10-989d-430892dd4a66",
      "sku": "ADB153"
    }
  ]
}
```

**在庫戻しフローをテストします：**

1. Commerce インスタンスから、サブスクリプションを作成した商品を編集します。
1. 商品の在庫状況を&#x200B;**[!UICONTROL Out of Stock]**&#x200B;に設定します。
1. 約1分待って、在庫状況を&#x200B;**[!UICONTROL In Stock]**&#x200B;に戻します。

   ![Commerce管理者向け商品編集ページで、在庫状況ドロップダウンと在庫切れオプションが表示されている](../assets/in-stock-product-stock-status-toggle.png){width="600" zoomable="yes"}

1. イベントがトリガーしてサービスに送信されるまで約5分待ちます。

1. [!DNL Adobe Developer Console]から、「App Builder ログ」セクションに移動します。

   ![Adobe Developer Console App Builder ログセクション &#x200B;](../assets/in-stock-developer-console-logs.png){width="600" zoomable="yes"}

1. ログで、イベントが処理されたことを確認するエントリがあり、正しい電子メールとSKUのサブスクリプションペアが識別されたことを確認します。

   ![App Builderのログエントリでバックインストックイベント処理が表示される](../assets/in-stock-log-entries.png){width="600" zoomable="yes"}

>[!TIP]
>
>エージェントにログの内容を確認して、通知アクションが正常にログに記録されたことを確認できます。 ログエントリをコピーして貼り付けて、エージェントが検証を実行できるようにすることもできます。

通知されたサブスクリプションが削除されるので、バック・イン・ストック・イベント・プロセスの後、サブスクリプションのリストを要求する場合は、1つ少ないエントリを返す必要があります。

### サービス契約の作成

サービスの実装が完了したら、担当者にストアフロント作業のサービス契約の作成を依頼します。

```shell-session
Create an API service contract for the Out of Stock notification service and its endpoints. Ensure that the service contract is clear and detailed enough for a frontend developer to implement the storefront UI integration without needing to ask additional questions about the API. Name this file OUT_OF_STOCK_NOTIFICATION_CONTRACT.md
```

このファイルをストアフロントプロジェクトにコピーし、ストアフロントエージェントが参照できるようにします。

## ストアフロントへの接続

このセクションでは、[!DNL Edge Delivery Services]とAI支援の開発ツールを使用して、在庫通知拡張機能のストアフロント部分を実装する方法について説明します。 選択した製品またはバリエーションの在庫が切れた場合にのみ表示される製品詳細ページ（PDP）に購読フォームを追加します。

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
- `OUT_OF_STOCK_NOTIFICATION_CONTRACT.md` ファイルがストアフロントプロジェクトにコピーされました

### 手順1：環境の検証

`config.json` ファイルを開き、`commerce-core-endpoint`と`commerce-endpoint`の値が[!DNL Adobe Commerce as a Cloud Service] GraphQL エンドポイントを指していることを確認します。

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### 手順2：最初のプロンプトを入力する

サービス契約が既にプロジェクトに存在する場合は、エージェントに対して、製品詳細ページでUIを作成するように促します。 エージェントで利用可能な場合は、**プラン** モードを使用して、プランなしでエージェントが続行できないようにします。

```shell-session
Analyze @OUT_OF_STOCK_NOTIFICATION_CONTRACT.md. Add a form for subscribing to a notification for when a product is back in stock. Place this form on the product details page, underneath the add to cart and wishlist button. The form only displays when a product is out of stock. 

Use the project manager skill to plan this implementation.
```

>[!TIP]
>
>段階的なワークフローをトリガーすることで、導入の早い段階を支援します。 このプロセスにより、主要な仮定と不足している要件が早期に特定され、担当者は当初のプロンプトでは提供しないと思われる詳細と要件を提示できます。

### ステップ 3：プランニングに関する質問への回答

担当者は、解決策の策定を開始する前に、回答する必要がある一連の質問を返します。 次の例は、典型的な質問と回答を示しています。 担当者は異なる質問をすることもありますが、トピックは一般的に同じです。

**エージェントの質問の例：**

1. **API ベース URL** — ストアフロントで在庫切れ通知API ベース URLを取得する方法を教えてください。 オプションには、設定ブロック（`out-of-stock-api-base-url`を含むテーブルなど）、グローバルプレースホルダーまたは環境変数、または別のアプローチを含めることができます。
1. **Copy** – 実装では、成功メッセージとエラーメッセージのプレースホルダー（ローカライゼーションなど）を使用しますか？それとも、この実装には静的英語を使用しますか？
1. **登録が成功した後** — フォームを非表示にして「登録済み」のみを表示する（A）、成功メッセージを上に表示してフォームを表示したまま無効にする（B）、または別の動作（C）を指定する必要がありますか？
1. **設定可能な製品** – 選択したバリエーションの`inStock`値に基づいてフォームの表示を行い、選択したバリエーションが在庫切れになったときにフォームを表示する必要がありますか？

**回答の例：**

```shell-session
1. Global placeholder with baseurl value of `https://<your-runtime-url>/api/v1/web/notify-out-of-stock/api`
2. Use placeholders with static English fallback
3. B
4. Use selected variant's inStock value
```

>[!NOTE]
>
>`<your-runtime-url>`を、App Builder デプロイメントの実際の[!DNL Adobe I/O Runtime] URLに置き換えます。
>
>担当者がさまざまな質問をする場合があります。 回答をガイダンスとして使用します。
>
>- API ベース URLのグローバルプレースホルダーを使用して、コードを変更せずに変更できるようにします。
>- ユーザー向けコピーにプレースホルダーを使用し、フォールバックに静的英語を使用します。
>- サブスクリプションが正常に終了した後は、フォームを表示したまま無効にし、成功メッセージを上位に表示します。
>- 設定可能な製品の場合は、選択したバリアントの`inStock`値を使用してフォームの表示を制御します。

### ステップ 4：要件とアーキテクチャの見直し

担当者は、ユーザーが確認する必要のある要件ドキュメントを更新します。 次のことを確認します。

- フォームは、商品または選択したバリエーションの在庫がない場合にのみ表示されます。
- フォームは、PDPの「カートに追加」ボタンと「ウィッシュリスト」ボタンの下に配置されます。
- API統合では、グローバルプレースホルダーのベース URLを使用します。
- 成功およびエラー状態は、契約（201、409、400、503/500）に従って処理されます。

>[!NOTE]
>
>AI エージェントは非決定論的で、モデルとIDEによって動作が異なります。 異なる要件とアーキテクチャのセットを生成する、異なる質問のセットが表示される場合があります。 その場合は、実装がこのチュートリアルに記載されている内容と密接に一致するようにエージェントを誘導してから先に進んでください。

**フェーズ 2 （アーキテクチャ プランニング）**&#x200B;中、エージェントはアーキテクチャを提案する前にドキュメントとコードベースを調査します。 エージェントには次の操作を期待します。

- PDP ドロップインコンテナ、スロット、およびイベントペイロードについて、[!DNL Commerce]のドキュメントを検索します。
- `blocks` ディレクトリと`scripts/initializers/` フォルダーをスキャンして、既存のPDP関連コードを探します。
- 使用可能なコンテナとスロットコンテキストシェイプのTypeScript定義について説明します。

その後、エージェントはアーキテクチャオプションを表示します。 プランを確認し、続行するように担当者に指示します。

### 手順5：実行計画の選択

担当者は、詳細な実装計画を作成するか、直接実装を完了するかを選択できます。

- より詳細に制御して段階的に実行できるレビュー可能なプランが必要な場合は、最初のオプションを選択します。
- エージェントに最小限の介入で完全な実装を行わせたい場合は、2番目のオプションを選択します。

**フェーズ 4 （実装）**&#x200B;中、エージェントは選択したアーキテクチャに基づいてコードを生成します。 アプローチに応じて、エージェントはいくつかの専門的なスキルを使用します。

- **コンテンツモデリング：**&#x200B;新しいブロックが必要な場合、担当者は作成者に適したコンテンツ構造を設計します。
- **ブロック開発：** エージェントは、JavaScriptのデコレーション関数、スコープ CSS スタイル、アクセシビリティ用のARIA ラベル、読み込みエラーの状態の処理など、[!DNL Edge Delivery Services]の規則に従ってブロックファイルを作成します。
- **ドロップインのカスタマイズ：** アーキテクチャでスロットのカスタマイズを使用している場合、エージェントは正しいコンテナをインポートし、製品タイトルの近くに検証済みのスロットを使用し、現在のSKUの製品データイベントを購読します。

生成されるコードを確認し、必要に応じて質問したり、担当者に連絡したりできます。

### 手順6：サーバーを起動してテストする

エージェントが実装を完了したら、開発サーバーを起動し、フォームをテストします。

1. ローカル開発サーバーを起動します。

   ```bash
   npm run start
   ```

1. ブラウザーで、在庫切れの商品ページに移動します。 例：

   ```shell-session
   http://localhost:3000/products/<out-of-stock-product-slug>/<sku>
   ```

1. サブスクリプションフォームが「カートに追加」ボタンと「ウィッシュリスト」ボタンの下に表示されていることを確認します。

手動テストを実行するか、担当者にブラウザー機能を使用してテストを依頼します。

```shell-session
Run complete browser testing. Use the following out of stock product 'http://localhost:3000/products/<out-of-stock-product-slug>/<sku>'
```

![&#x200B; カートに追加ボタンの下に入荷後通知フォームが表示されている製品詳細ページ &#x200B;](../assets/in-stock-notification-form.png){width="600" zoomable="yes"}

### ステップ 7：クリーンアップ

テストをスキップまたは完了した後、エージェントは最終的な&#x200B;**クリーンアップ** フェーズに進むよう促します。 確認すると、エージェントは実装中に作成されたすべてのドキュメントアーティファクトをアーカイブします。

## トラブルシューティング

チュートリアル中に問題が発生した場合は、次のヒントを参考にしてください。

- **API エラー：** CLIを使用して、APIにリクエストを直接送信し、動作を検証します。 例えば、`curl`を使用して、各エンドポイントを個別にテストします。
- **エージェントエラー：** エラーメッセージをエージェントチャットセッションにコピーして貼り付け、問題のデバッグに役立てます。 エージェントは、環境変数の欠落や誤った設定のアクションなど、一般的な問題を診断できます。
- **イベントパイプライン：**&#x200B;入荷イベントがトリガーしない場合は、オンボーディングとイベントのサブスクリプションの手順を完了していることを確認してください。 `workspace.json`が正しい場所にあり、Commerce Events モジュールが有効になっていることを確認してください。
- **Stock ステータス ペイロード：** Commerceは、`is_in_stock`をブール値（`true`）ではなく文字列（`"1"`）として送信できます。 後入在庫ハンドラーがトリガーされない場合は、エージェントに対して、厳密なタイプ比較のコンシューマーコードを確認し、両方の形式を処理するように更新するように依頼します。

## チュートリアルの概要

このチュートリアルで取り上げたトピックの概要を次に示します。

- **拡張機能の開発：** AI エージェントに対する新機能の説明と、[!DNL App Builder]を使用したCRUD操作を使用して動作するREST APIの生成。
- **イベント駆動型アーキテクチャ：** Commerce イベントと、商品の再入荷を検出するためのスケジュールされたアクションを設定します。
- **ローカルテストとデプロイメント：** `curl`でAPIをテストし、[!DNL Adobe I/O CLI]を使用してデプロイします。
- **サービス契約：** バックエンドの拡張機能とストアフロント実装を橋渡しするAPI契約を作成しています。
- **段階的なストアフロント統合：** AI支援のスキルを使用して、要件、アーキテクチャ、実装を進める。
- **ドロップイン統合：** [!DNL Adobe Commerce]個のドロップインコンテナとスロットを使用してPDPにサブスクリプションフォームを追加します。

## 次のステップ

在庫通知サービスを拡張するには、次の推奨事項を使用してください。

- **実際の通知を送信：** ログベースの通知を、[!DNL Adobe Campaign]などの電子メールサービスまたはサードパーティのプロバイダーに置き換えます。
- **サブスクリプション管理ページを追加：**&#x200B;買い物客がアクティブなサブスクリプションを表示およびキャンセルできるストアフロントページを作成します。
- **マルチテナントのデプロイメントをサポート：** ステート管理を拡張して、1つのApp Builder アプリで複数のCommerce テナントをサポートします。
- **レート制限を追加：**&#x200B;悪用を防ぐために、サブスクリプション APIにレート制限を実装します。
