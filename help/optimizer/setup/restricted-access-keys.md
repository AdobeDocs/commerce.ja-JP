---
title: 制限付きアクセスキー
description: 制限付きアクセスキーで[!DNL Adobe Commerce Optimizer]のカタログビューを保護する方法について説明します。この方法は、B2B共有カタログ用に自動的に作成されるか、手動で管理されます。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよび[!DNL Adobe Commerce Optimizer]件のプロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
nudge: true
source-git-commit: f93bd673624c58050696da772ce733874ce594e5
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 0%
---
# 制限付きアクセスキー

制限付きアクセスキーを使用すると、許可されたクライアントアプリケーションは[&#x200B; プライベートカタログビュー](catalog-view.md)にアクセスできます。割り当てられたキーから有効な署名済みトークンを含むリクエストのみが、カタログデータを取得できます。 このカタログビューへのアクセスが明示的に許可されていない買い物客や、APIをプローブするスクリプトなど、その他のすべてのリクエストは拒否されます。

制限付きアクセスキーは、次の2つの方法のいずれかでプロビジョニングされます。

- [!BADGE Private Beta]{type=Caution tooltip="現在プライベートベータ版のAdobe Commerce Optimizer Connector B2B拡張機能が必要です。"} **自動的に、B2B共有カタログ**&#x200B;の場合 – [!DNL Adobe Commerce Optimizer Connector for B2B]と統合されたデプロイメントの場合、コネクタは最初のキーをプロビジョニングして割り当てます。 次に、Commerce管理者からキーとキーの割り当てを管理します。 *Commerce管理ガイド**の「[&#x200B; カタログビュー認証](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-views-manage)」を参照してください。

- **任意のカタログビューに対して手動で** – 自分でカタログビューを保護するには（パートナーポータルやプレリリースプレビューなど）、[制限付きアクセスキーの作成](#create-a-restricted-access-key)から始まるこのトピックの手順に従います。

## 制限付きアクセスキーのユースケース

[!DNL Adobe Commerce Optimizer]では、**[!UICONTROL Price Book ID]**&#x200B;はリクエストに表示される価格を決定します。これは、リクエストを実行できる担当者ではなく、価格をスコープ化します。 カタログビューのIDと価格表のIDを知っているクライアントであれば誰でも、Merchandising APIを通じてそのデータを取得できます。 制限付きアクセスキーは、別個の補完的なコントロールを追加します。各アクセスキーは、どの価格表が適用されるかにかかわらず、カタログビューにまったくアクセスできる範囲を指定します。

制限付きアクセスキーは、一般的に次の目的で使用されます。

- **契約ベースのB2B価格設定** – 交渉済み価格表にリンクされたカタログ ビューを制限して、適用される購入者のみがクエリを実行できるようにします。 その他の購買組織や一般の人は利用できません。 B2B共有カタログの場合は、これが自動的に設定されます。 [&#x200B; キーの管理とローテーション &#x200B;](#key-management-and-rotation)を参照してください。
- **パートナーおよびリセラーポータル**：カタログのサブセットを、マーチャンダイジング APIと直接統合する承認済みパートナーに制限します。
- **プレリリースプレビュー**：信頼できる内部またはパートナーのシステムが公開される前に、今後の製品をプレビューします。

## 制限付きアクセスキーの仕組み

制限付きアクセスキーは、RSA キーペアの公開コンポーネントです。 クライアントアプリケーションは、このキーを生成して使用し、プライベートカタログビューの読み取りが許可されていることを証明します。 このコンテキストでは、_クライアントアプリケーション_&#x200B;は、買い物客を認証するバックエンドシステム（例：[!DNL Adobe Commerce]のカスタムロジックやサードパーティバックエンドなど）を指します。ストアフロントフロントエンド自体は決してありません。

次の手順では、B2B共有カタログに含まれていないカタログビューについて、キーペアと署名済みトークンが作成から検証に移行する方法を説明します。

1. クライアントアプリケーションはRSA鍵ペアを生成し、秘密鍵を保持します。
1. **public** キーを[!DNL Commerce Optimizer]に制限付きアクセス キーとして登録します。
1. クライアントアプリケーションは、秘密鍵を使用してJSON Web Token （JWT）に署名し、秘密鍵を使用してプライベートカタログビューへの各リクエストに含めます。
1. [!DNL Commerce Optimizer]は、登録された公開鍵に対してトークンの署名を検証し、有効な場合は、要求されたカタログデータを返します。

## 制限付きアクセスキーの作成

>[!NOTE]
>
>このセクションとそれに続く3つのセクションでは、手動の[!DNL Adobe Commerce Optimizer] Studio フローについて説明します。 [!DNL Adobe Commerce Optimizer Connector B2B extension]でB2B共有カタログを使用する場合は、Commerce管理者からキーを管理します。 _Adobe Commerce Optimizer Connector_ ドキュメントの[制限付きアクセスキー](../../aco-connector/restricted-access-keys.md)を参照してください。

プライベートカタログビューの最初のテストでは、[!DNL OpenSSL]などのツールを使用してキーペアを生成します。 秘密鍵は秘密にしておきます。 公開鍵のみが[!DNL Commerce Optimizer]にアップロードされます。

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

アクセス制限キーは、**[!UICONTROL Catalog Protection]**&#x200B;が有効になっているカタログビューに割り当てられた後にのみアクセスを認証します。 設定手順については、[&#x200B; カタログビューの保護](private-catalog-view.md#protect-a-catalog-view)を参照してください。

## キーの削除

1. **[!UICONTROL Restricted access keys]** ページで、削除するキーを見つけて、**[!UICONTROL Delete]**&#x200B;をクリックします。

   キーが1つ以上のカタログビューに割り当てられている場合、警告は、そのキーに依存しているクライアントアプリケーションがアクセス権を失うことを説明します。 カタログビュー自体は保護されており、一般に公開されることはありません。

1. 削除を確認します。

## キー管理とローテーション

制限付きアクセスキーは、カタログ保護の使用方法に応じて、次の2つの方法のいずれかで管理されます。

- **自動的に、B2B共有カタログの場合**—[!BADGE Private Beta]{type=Caution tooltip="現在プライベートベータ版のAdobe Commerce Optimizer Connector B2B拡張機能が必要です。"} [!DNL Adobe Commerce Optimizer Connector for B2B]と統合されたデプロイメントの場合、カタログビューの作成時に、サービスは自動的に最初の制限付きアクセスキーを生成して割り当てます。 各カタログビューには、独自のキーが割り当てられます。 その後、共有カタログまたは会社アカウントページから各キーを管理できます。 また、Commerce管理者&#x200B;**制限付きアクセスキー** ページ（**システム** > **データ転送**）からキーを表示および管理することもできます。 [&#x200B; カタログビュー設定の管理](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-views-manage)を参照してください。

  共有カタログと割り当てられたストアビューの各組み合わせは、個別のカタログビューとして表示されます。 プロジェクションとは、コネクタがその組み合わせに対して[!DNL Adobe Commerce Optimizer]に書き出すカタログ ビュー、ポリシー、価格表参照、およびアクセス制限キー設定データです。 複数のストアビューに割り当てられた共有カタログは、それぞれ独自のキーを持つ複数のカタログビューを生成します。 他のカタログに影響を与えることなく、1つのカタログ ビューのキーを編集または回転します。

  キーのデフォルトは長い有効期限です。 キーを回転させる必要がある場合は、管理画面に置き換えを追加し、古いキーを削除するまで両方をアクティブのままにします。 [B2B共有カタログの変更](/help/aco-connector/get-started.md#monitor-b2b-shared-catalog-changes)を参照してください。

- **手動で、任意のカタログ ビュー**—Adobe Commerce バックエンドのB2B共有カタログに関連付けられていないカタログ ビューの場合、キー生成、トークン署名、およびローテーションは、買い物客を認証するバックエンド クライアント アプリケーションによって完全に管理されます。 [!DNL Adobe Commerce Optimizer]は、ユーザーに代わって、これらのキーを生成または回転しません。 このトピックの前の手順を使用して、キーを作成、追加、削除します。 キーを回転するには、[&#x200B; キーの回転](#rotate-a-key)を参照してください。

### キーの回転

アクセスを中断せずにキーを回転させるには、カタログビューに一度に最大3つのキーを割り当てることができます。

1. 新しいキーペアを生成し、新しい公開鍵を新しい制限付きアクセス鍵として追加します。
1. 既存のキーと並行して、新しいキーをカタログビューに割り当てます。
1. 新しい秘密鍵で新しいトークンへの署名を開始して、キーロールオーバーを完了します。
1. 新しいキーですべてのクライアントアプリケーションが確認されたら、古いキーを削除して削除します。

## 制限

[&#x200B; カタログビューとポリシー制限](../boundaries-limits.md#catalog-views-and-policies)を参照してください。

## その他

- [&#x200B; プライベートカタログビュー](private-catalog-view.md) – アクセスキーが制限されたカタログビューを保護する方法について説明します。
- [B2B共有カタログの変更](/help/aco-connector/get-started.md#monitor-b2b-shared-catalog-changes) - [!DNL Adobe Commerce Optimizer Connector]がB2B共有カタログのキー管理を自動化する方法について説明します。

