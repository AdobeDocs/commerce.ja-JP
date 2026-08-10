---
title: 制限付きアクセスキー
description: 署名済みトークン認証を使用して [!DNL Adobe Commerce Optimizer] でカタログ ビューを保護するために、制限付きアクセス キーを作成、割り当て、回転する方法について説明します。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよび [!DNL Adobe Commerce Optimizer]  プロジェクトにのみ適用されます（Adobeで管理されるSaaS インフラストラクチャ）。"
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
nudge: true
source-git-commit: 688bc6e28a4c5a94b1fe55c84f7c05401dd651bc
workflow-type: tm+mt
source-wordcount: 791
ht-degree: 0%

---

# 制限付きアクセスキー

制限付きアクセスキーを使用すると、許可されたクライアントアプリケーションは[&#x200B; プライベートカタログビュー](catalog-view.md)にアクセスできます。割り当てられたキーから有効な署名済みトークンを含むリクエストのみが、カタログデータを取得できます。 匿名の買い物客、このカタログビューへのアクセスが明示的に許可されていない買い物客、APIを調査するスクリプトなど、その他のすべてのリクエストは拒否されます。

## 制限付きアクセスキーのユースケース

[!DNL Adobe Commerce Optimizer]では、**[!UICONTROL Price Book ID]**&#x200B;はリクエストに表示される価格を決定します。これは、リクエストを実行できる担当者ではなく、価格をスコープ化します。 カタログビューのIDと価格表のIDを知っているクライアントであれば誰でも、Merchandising APIを通じてそのデータを取得できます。 制限付きアクセスキーは、別個の補完的なコントロールを追加します。各アクセスキーは、どの価格表が適用されるかにかかわらず、カタログビューにまったくアクセスできる範囲を指定します。

制限付きアクセスキーは、一般的に次の目的で使用されます。

- **契約ベースのB2B価格設定** – 交渉済み価格表にリンクされたカタログ ビューを制限して、適用される購入者のみがクエリを実行できるようにします。 その他の購買組織や一般の人は利用できません。
- **パートナーおよびリセラーポータル**：カタログのサブセットを、マーチャンダイジング APIと直接統合する承認済みパートナーに制限します。
- **プレリリースプレビュー**：信頼できる内部またはパートナーのシステムが公開される前に、今後の製品をプレビューします。

>[!IMPORTANT]
>
>キーの生成、トークンの署名、ローテーションは、現在、買い物客を認証するバックエンドクライアントアプリケーションですべて管理されています。 [!DNL Adobe Commerce Optimizer]は、ユーザーに代わって、これらのキーを生成または回転しません。

## 制限付きアクセスキーの仕組み

制限付きアクセスキーは、RSA キーペアの公開コンポーネントです。 クライアントアプリケーションは、このキーを生成して使用し、プライベートカタログビューの読み取りが許可されていることを証明します。 このコンテキストでは、「クライアントアプリケーション」とは、買い物客を認証するバックエンドシステム（例えば、[!DNL Adobe Commerce]やサードパーティバックエンドのカスタムロジック）を意味します。ストアフロントフロントエンド自体は決してありません。

次の手順では、キーペアと署名済みトークンが作成から検証に移動する方法について説明します。

1. クライアントアプリケーションはRSA鍵ペアを生成し、秘密鍵を保持します。
1. **public** キーを[!DNL Commerce Optimizer]に制限付きアクセス キーとして登録します。
1. クライアントアプリケーションは、秘密鍵を使用してJSON Web Token （JWT）に署名し、秘密鍵を使用してプライベートカタログビューへの各リクエストに含めます。
1. [!DNL Commerce Optimizer]は、登録された公開鍵に対してトークンの署名を検証し、有効な場合は、要求されたカタログデータを返します。

## 制限付きアクセスキーの作成

プライベートカタログビューの最初のテストでは、[!DNL OpenSSL]などのツールを使用してキーペアを生成します。 秘密鍵を秘密にしてください。公開鍵のみが[!DNL Commerce Optimizer]にアップロードされます。

```bash
openssl genrsa -out private-key.pem 2048
openssl rsa -in private-key.pem -pubout -out public-key.pem
```

キーサイズは、2048 ビットから8192 ビットの間である必要があります。 `public-key.pem`には、下の&#x200B;**[!UICONTROL Public key]** フィールドに貼り付けた値が含まれています。

## 制限付きアクセスキーを[!DNL Commerce Optimizer]に追加

1. [!DNL Adobe Commerce Optimizer Studio]の左側のメニューから、**[!UICONTROL Store setup]**&#x200B;に移動し、**[!UICONTROL Restricted access keys]**&#x200B;をクリックします。

   ![制限付きアクセスキーのリスト、制限付きアクセスキーを追加ボタン &#x200B;](../assets/restricted-access-keys.png){width="70%" zoomable="yes"}

1. **[!UICONTROL Add Restricted Access Key]**&#x200B;をクリックします。

1. キーの詳細を入力します。

   ![&#x200B; タイトル、有効期限、および公開鍵フィールドを含む制限付きアクセスキー形式を追加](../assets/restricted-access-keys-add.png){width="70%" zoomable="yes"}

   - **[!UICONTROL Title]** - キーを識別するためのラベル。キーリストおよびカタログ表示のキーピッカー（例：`ACME Corp wholesale portal — Tier 1 pricing`）に表示されます。
   - **[!UICONTROL Expiration date]** – 有効期限がまだ切れていないトークンの場合でも、キーの処理が停止する日時（UTC）。
   - **[!UICONTROL Public key]** - `-----BEGIN PUBLIC KEY-----`および`-----END PUBLIC KEY-----` マーカーを含む、PEMでエンコードされたRSA公開鍵をSubject Public Key Info （SPKI）形式で指定します。 環境全体で一意である必要があります。

1. **[!UICONTROL Save]**&#x200B;をクリックします。

キーは作成後に不変になります。 値を変更するには、キーを削除して新しいキーを作成します。 アクセスの中断なしでキー[&#128279;](#rotate-a-key)を回転する方法については、を参照してください。

## カタログビューへのキーの割り当て

制限付きアクセスキーは、**[!UICONTROL Catalog Protection]**&#x200B;が有効になっているカタログビューに割り当てられた後にのみアクセスを制限します。 設定手順については、[&#x200B; カタログビューの保護](private-catalog-view.md#protect-a-catalog-view)を参照してください。

## キーの削除

1. **[!UICONTROL Restricted access keys]** ページで、削除するキーを見つけて、**[!UICONTROL Delete]**&#x200B;をクリックします。

   キーが1つ以上のカタログビューに割り当てられている場合、警告は、そのキーに依存しているクライアントアプリケーションがアクセス権を失うことを説明します。 カタログビュー自体は保護されており、一般に公開されることはありません。

1. 削除を確認します。

## キーの回転

アクセスを中断せずにキーを回転させるには、カタログビューに一度に最大3つのキーを割り当てることができます。

1. 新しいキーペアを生成し、新しい公開鍵を新しい制限付きアクセス鍵として追加します。
1. 既存のキーと並行して、新しいキーをカタログビューに割り当てます。
1. 新しい秘密鍵で新しいトークンへの署名を開始して、キーロールオーバーを完了します。
1. 新しいキーですべてのクライアントアプリケーションが確認されたら、古いキーを削除して削除します。

## 制限

[&#x200B; カタログビューとポリシー制限](../boundaries-limits.md#catalog-views-and-policies)を参照してください。

## その他

- [&#x200B; プライベートカタログビュー](private-catalog-view.md) – アクセスキーが制限されたカタログビューを保護する方法について説明します。

