---
title: プライベートカタログビュー
description: カタログ保護を有効にして、有効な署名済みトークンを持つリクエストのみが製品と価格データを取得できるように、プライベートカタログビューを作成する方法を説明します。
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよび [!DNL Adobe Commerce Optimizer]  プロジェクトにのみ適用されます（Adobeで管理されるSaaS インフラストラクチャ）。"
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
source-git-commit: 16e3405e1500dfd39603b1e300f4625e5a57cf02
workflow-type: tm+mt
source-wordcount: 642
ht-degree: 0%

---

# プライベートカタログビュー

デフォルトでは、[&#x200B; カタログビュー](catalog-view.md)はパブリックです。 カタログビューでカタログ保護を有効にして、有効な署名済みトークンを含むリクエストへのアクセスを制限します。

カタログ保護は、選択したカタログビューにのみ適用されます。 ビューのポリシーやレイヤーは変更されません。 ビューを単一の価格表に制限します。[&#x200B; プライベートカタログビューの価格表制限](#price-book-restriction-on-private-catalog-views)を参照してください。

カタログビューを保護するタイミングの例については、[&#x200B; アクセス制限キーの使用例](restricted-access-keys.md#restricted-access-key-use-cases)を参照してください。

## 保護範囲の理解

カタログ保護は、有効になっているカタログビューにのみ適用されます。 カタログと検索リクエストを保護しますが、ビューのポリシーやレイヤーの変更、他のカタログビューの保護、カート、チェックアウト、注文操作の保護は行いません。

連続性のあるコマースのバックエンドでは、独自に購入資格を適用する必要があります。

## プライベートカタログビューに対する価格表の制限

プライベートカタログビューでは、1つの価格表のみを参照できます。 これは、複数の価格表を使用できるパブリックカタログビューとは異なります。

[!UICONTROL Catalog Protection]が有効になっている場合、カタログビューフォームの価格表セレクターは、複数選択コントロールから単一選択（ラジオボタン）コントロールに切り替わります。

![&#x200B; プライベートカタログビューの価格表制限](../assets/catalog-view-private-pricebook-restrictions.png)

- 複数の価格表が割り当てられているカタログ ビューで[!UICONTROL Catalog Protection]を有効にする場合、1つの価格表を除くすべての価格表を削除するまで、ビューを保存できません。
- この制限が存在する前に、複数の価格表の割り当てがあるプライベートカタログビューを以前に保存した場合、カタログビューの設定は自動的には変更されません。 ただし、次回ビューを編集する際は、更新を保存する前に、1つを除くすべての価格表を削除する必要があります。

これらのケースのそれぞれで、[!DNL Adobe Commerce Optimizer]は次の検証メッセージを表示します：`A protected catalog view can use only one price book. Select 'Single price book only' to continue.`

パブリックカタログビューは、この制限の影響を受けず、複数の価格表を引き続き参照できます。

## カタログビューの保護

開始する前に、クライアントアプリケーションが生成する公開鍵から[制限付きアクセスキー](restricted-access-keys.md)を作成します。

1. カタログビューのフォームの作成または編集で、**[!UICONTROL Catalog Protection]**&#x200B;を&#x200B;**[!UICONTROL Enabled]**&#x200B;に切り替えます。

1. **[!UICONTROL Restricted Access Keys]**&#x200B;で、このカタログ ビューに割り当てるアクセス キー[&#128279;](restricted-access-keys.md)を3つまで選択してください。

   ![&#x200B; カタログ保護がカタログビュー編集フォームで有効になっており、アクセス制限キーが割り当てられている](../assets/catalog-view-protected.png){width="70%" zoomable="yes"}

1. **[!UICONTROL Save catalog view]**&#x200B;をクリックします。

   これで、カタログ ビューが保護されました。 割り当てられたキーから有効な署名されたトークンを持つリクエストのみが、そのデータを取得できます。

   >[!NOTE]
   >
   >カタログ保護の設定変更を有効にするには、最大5分かかります。

## アクセスが強制されていることを確認する

プライベートカタログビューが不正なリクエストを拒否することを確認するには、次のヘッダーを使用して、署名されたトークンの有無にかかわらず[GraphQL エンドポイント &#x200B;](../get-started.md#get-instance-details)を呼び出します。

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

割り当てられた、期限切れでないキーによって署名されたトークンを含むリクエストは、期待どおりにカタログデータを返します。 JWTへの署名とマーチャンダイジング APIの呼び出しについて詳しくは、[開発者ドキュメント &#x200B;](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api#authentication)を参照してください。

## 制限付きアクセスキーの管理

[!UICONTROL Catalog Protection]が有効になっていて、割り当てられたすべてのキーの有効期限が切れると、カタログビューにアクセスできなくなります。このカタログビューに依存するストアフロントは、そのカタログビューからデータを提供できません。 新しい期限切れでないキーを割り当てて、アクセスを復元します。 手順については、[&#x200B; キーの回転](restricted-access-keys.md#rotate-a-key)を参照してください。

>[!IMPORTANT]
>
>Adobe CommerceおよびAdobe Commerce Optimizer コネクタによるキーの自動作成と管理はまだ利用できません。

## その他

- [&#x200B; カタログビュー](catalog-view.md) - カタログビューが、ビジネス構造、ポリシー、価格によって商品カタログをどのように整理するかを説明します。
- [制限付きアクセス キー](restricted-access-keys.md) - カタログ保護のトークンの署名に使用するキーを作成、割り当て、回転します。
