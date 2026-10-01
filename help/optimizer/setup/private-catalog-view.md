---
title: プライベートカタログビュー
description: プライベートカタログビューでカタログデータへのアクセスを制限する方法、B2B共有カタログ用に自動的に作成する方法、カタログ保護を使用して手動で設定する方法について説明します。
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよび[!DNL Adobe Commerce Optimizer]件のプロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"
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
source-git-commit: f93bd673624c58050696da772ce733874ce594e5
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 0%
---
# プライベートカタログビュー

デフォルトでは、[ カタログビュー](catalog-view.md)はパブリックです。 カタログビューへのアクセスを制限して、有効な署名済みトークンを持つリクエストのみがデータを取得できるようにします。

カタログビューは、次の2つの方法のいずれかで非公開になります。

- [!BADGE Private Beta]{type=Caution tooltip="現在プライベートベータ版のAdobe Commerce Optimizer Connector B2B拡張機能が必要です。"} **自動的に、B2B共有カタログ**&#x200B;の場合 – [!DNL Adobe Commerce Optimizer Connector]統合とB2B拡張機能を使用するCommerce デプロイメントの場合、[!DNL Adobe Commerce]の共有カタログ設定に基づいて、プライベートカタログビューが自動的に作成および設定されます。 B2B共有カタログの[自動プライベートカタログビュー](#automatic-private-catalog-views-for-b2b-shared-catalogs)を参照してください。

- **手動で、任意のカタログ ビュー**—B2C カタログ ビューを含め、パブリックになるカタログ ビューへのアクセスを制限するには、[ カタログ ビューを保護](#protect-a-catalog-view)の手順に従います。 パートナーポータルやプレリリースプレビューなどの例については、[ アクセス制限キーのユースケース ](restricted-access-keys.md#restricted-access-key-use-cases)を参照してください。

カタログ保護は、選択したカタログビューにのみ適用されます。 ビューのポリシーやレイヤーは変更されません。 ビューを単一の価格表に制限します。[ プライベートカタログビューの価格表制限](#price-book-restriction-on-private-catalog-views)を参照してください。

## 保護範囲の理解

カタログ保護は、有効になっているカタログビューにのみ適用されます。 カタログと検索リクエストを保護しますが、ビューのポリシーやレイヤーの変更、他のカタログビューの保護、カート、チェックアウト、注文操作の保護は行いません。

連続性のあるコマースのバックエンドでは、独自に購入資格を適用する必要があります。

## プライベートカタログビューに対する価格表の制限

プライベートカタログビューでは、1つの価格表のみを参照できます。 これは、複数の価格表を使用できるパブリックカタログビューとは異なります。

[!UICONTROL Catalog Protection]が有効になっている場合、カタログビューフォームの価格表セレクターは、複数選択コントロールから単一選択（ラジオボタン）コントロールに切り替わります。

![ プライベートカタログビューの価格表制限](../assets/catalog-view-private-pricebook-restrictions.png)

- 複数の価格表が割り当てられているカタログ ビューで[!UICONTROL Catalog Protection]を有効にする場合、1つの価格表を除くすべての価格表を削除するまで、ビューを保存できません。
- この制限が存在する前に、複数の価格表の割り当てがあるプライベートカタログビューを以前に保存した場合、カタログビューの設定は自動的には変更されません。 ただし、次回ビューを編集する際は、更新を保存する前に、1つを除くすべての価格表を削除する必要があります。

これらのケースのそれぞれで、[!DNL Adobe Commerce Optimizer]は次の検証メッセージを表示します：`A protected catalog view can use only one price book. Select 'Single price book only' to continue.`

パブリックカタログビューは、この制限の影響を受けず、複数の価格表を引き続き参照できます。

## B2B共有カタログの自動プライベートカタログビュー

[!BADGE Private Beta]{type=Caution tooltip="現在プライベートベータ版のAdobe Commerce Optimizer Connector B2B拡張機能が必要です。"}

共有カタログをサポートするために[!DNL Adobe Commerce Optimizer Connector for B2B]と統合されたデプロイメントの場合、拡張機能は、[!DNL Adobe Commerce]の共有カタログ設定に基づいて、プライベートカタログビューを自動的に作成および設定します。 この設定には、カタログビュー、ポリシー、初期アクセス制限キー、価格表の参照が含まれます。 この設定では、制限付きアクセスキーをCommerce管理者&#x200B;**制限付きアクセスキー** ページ （**システム** > **データ転送**）から管理します。 詳しくは、*[!DNL Adobe Commerce Optimizer Connector]統合ガイド*&#x200B;の[B2B共有カタログの変更](/help/aco-connector/get-started.md#monitor-b2b-shared-catalog-changes)を参照してください。

B2B共有カタログを使用していない場合（例えば、パートナーポータルやプレリリースプレビューのカタログビューを保護する場合など）、[ カタログビューを保護](#protect-a-catalog-view)の手順を使用して手動で設定します。

## カタログビューの保護

>[!NOTE]
>
>[!DNL Adobe Commerce Optimizer Connector for B2B]によって管理されるB2B共有カタログに関連付けられているカタログ ビューについては、この手順をスキップしてください。 B2B共有カタログの[自動プライベートカタログビュー](#automatic-private-catalog-views-for-b2b-shared-catalogs)を参照してください。

開始する前に、クライアントアプリケーションが生成する公開鍵から[制限付きアクセスキー](restricted-access-keys.md)を作成します。

1. カタログビューのフォームの作成または編集で、**[!UICONTROL Catalog Protection]**&#x200B;を&#x200B;**[!UICONTROL Enabled]**&#x200B;に切り替えます。

1. **[!UICONTROL Restricted Access Keys]**&#x200B;で、このカタログ ビューに割り当てるアクセス キー](restricted-access-keys.md)を3つまで選択してください。[

   ![ カタログ保護がカタログビュー編集フォームで有効になっており、アクセス制限キーが割り当てられている](../assets/catalog-view-protected.png){width="70%" zoomable="yes"}

1. **[!UICONTROL Save catalog view]**&#x200B;をクリックします。

   これで、カタログ ビューが保護されました。 割り当てられたキーから有効な署名されたトークンを持つリクエストのみが、そのデータを取得できます。

   >[!NOTE]
   >
   >カタログ保護の設定変更を有効にするには、最大5分かかります。

## アクセスが強制されていることを確認する

プライベートカタログビューが不正なリクエストを拒否することを確認するには、次のヘッダーを使用して、署名されたトークンの有無にかかわらず[GraphQL エンドポイント ](../get-started.md#get-instance-details)を呼び出します。

| ヘッダー | 目的 |
| --- | --- |
| `AC-View-ID` | クエリするカタログビュー。 |
| `AC-Price-Book-ID` | 適用する価格表。 |
| `AC-Catalog-View-Access-Token` | カタログビューの認証を証明する署名済みJWT。 |

有効なトークンのないリクエストは、カタログデータではなくGraphQL エラーを返します。例：

```json
{
  "errors": [
    {
      "message": "Access key validation failed: Missing token",
      "extensions": { "x-commerce-exception": "access-key-invalid" }
    }
  ]
}
```

割り当てられた、期限切れでないキーによって署名されたトークンを含むリクエストは、期待どおりにカタログデータを返します。 JWTへの署名とマーチャンダイジング APIの呼び出しについて詳しくは、[開発者ドキュメント ](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api#authentication)を参照してください。

## 制限付きアクセスキーの管理

[!UICONTROL Catalog Protection]が有効になっていて、割り当てられたすべてのキーの有効期限が切れると、カタログ ビューにアクセスできなくなります。 このカタログビューに依存するストアフロントは、このカタログビューからのデータを提供できません。 新しい期限切れでないキーを割り当てて、アクセスを復元します。 手順については、[ キーの回転](restricted-access-keys.md#rotate-a-key)を参照してください。

>[!NOTE]
>
>[!DNL Adobe Commerce Optimizer Connector for B2B]拡張機能と統合されたデプロイメントの場合、Commerce管理者&#x200B;**制限付きアクセスキー** ページ （**システム** > **データ転送**）からアクセスキーを管理します。 詳しくは、*[!DNL Adobe Commerce Optimizer Connector]統合ガイド*&#x200B;の「[制限付きアクセスキー管理](../../aco-connector/restricted-access-keys.md)」を参照してください。

## その他

- [ カタログビュー](catalog-view.md) - カタログビューが、ビジネス構造、ポリシー、価格によって商品カタログをどのように整理するかを説明します。
- [制限付きアクセス キー](restricted-access-keys.md) - カタログ保護のトークンの署名に使用するキーを作成、割り当て、回転します。
