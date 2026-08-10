---
title: プライベートカタログビュー
description: カタログ保護を有効にして、有効な署名済みトークンを持つリクエストのみが製品と価格データを取得できるように、プライベートカタログビューを作成する方法を説明します。
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよび [!DNL Adobe Commerce Optimizer]  プロジェクトにのみ適用されます（Adobeで管理されるSaaS インフラストラクチャ）。"
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 38fa0734562a631fdcdd7510580571c5d37cb598
workflow-type: tm+mt
source-wordcount: 467
ht-degree: 0%

---

# プライベートカタログビュー

デフォルトでは、[ カタログビュー](catalog-view.md)はパブリックです。 カタログビューでカタログ保護を有効にして、有効な署名済みトークンを含むリクエストへのアクセスを制限します。

カタログ保護は、選択したカタログビューにのみ適用されます。 ビューのポリシー、レイヤー、価格表は変更されません。

カタログビューを保護するタイミングの例については、[ アクセス制限キーの使用例](restricted-access-keys.md#restricted-access-key-use-cases)を参照してください。

## 保護範囲の理解

カタログ保護は、有効になっているカタログビューにのみ適用されます。 カタログと検索リクエストを保護しますが、ビューのポリシーや価格表の変更、他のカタログビューの保護、カート、チェックアウト、注文操作の保護は行いません。

連続性のあるコマースのバックエンドでは、独自に購入資格を適用する必要があります。

## カタログビューの保護

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

[!UICONTROL Catalog Protection]が有効になっていて、割り当てられたすべてのキーの有効期限が切れると、カタログビューにアクセスできなくなります。このカタログビューに依存するストアフロントは、そのカタログビューからデータを提供できません。 新しい期限切れでないキーを割り当てて、アクセスを復元します。 手順については、[ キーの回転](restricted-access-keys.md#rotate-a-key)を参照してください。

>[!IMPORTANT]
>
>Adobe CommerceおよびAdobe Commerce Optimizer コネクタによるキーの自動作成と管理はまだ利用できません。

## その他

- [ カタログビュー](catalog-view.md) - カタログビューが、ビジネス構造、ポリシー、価格によって商品カタログをどのように整理するかを説明します。
- [制限付きアクセス キー](restricted-access-keys.md) - カタログ保護のトークンの署名に使用するキーを作成、割り当て、回転します。
