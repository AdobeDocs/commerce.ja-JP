---
title: ' [!DNL Catalog Service] の基本を学ぶ'
description: にアクセスし  [!DNL Catalog Service]  フロントエンドアプリケーションやサードパーティのサービスと統合する方法について説明します。
role: Admin, Developer
source-git-commit: 3a6a81fa03f13c24ac08041c39452c553aa54f55
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# [!DNL Catalog Service] の基本を学ぶ

[!DNL Catalog Service] を有効にすると、サービスにアクセスしてそのサービスを使用し、商品やカテゴリの情報などのカタログデータをAdobe Commerce インスタンスから取得できます。 このサービスは、GraphQL Admin から、またはGraphQL クエリをサポートするフロントエンドアプリケーションからアクセスできる、Commerce API として使用できます。

## サービスへのアクセス

この [!DNL Catalog Service] は、GraphQL Admin から、またはGraphQL クエリをサポートするフロントエンドアプリケーションからアクセスできる、Commerce API として使用できます。 このサービスは、SaaS 環境と PaaS 環境の両方で利用できます。


[!BADGE PaaS のみ &#x200B;]{type=Informative url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeが管理する PaaS インフラストラクチャ）およびオンプレミスプロジェクトにのみ適用されます。"}

| 0.5511122 | エンドポイント |
|------------ | ----------: |
| **テスト** | `https://catalog-service-sandbox.adobe.io/graphql` |
| **実稼動** | `https://catalog-service.adobe.io/graphql` |

[!BADGE SaaS のみ &#x200B;]{type=Positive url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"}

| 0.5511122 | エンドポイント |
| ------------ | --------:|
| テスト | `https://na1-sandbox.api.commerce.adobe.com/{{tenant-id}}/graphql` |
| 実稼動（まだ使用できません） | `https://na1.api.commerce.adobe.com/{{tenant-id}}/graphql` |

**SaaS エンドポイントの URL 構造**

```text
https://<region>-<environment>.api.commerce.adobe.com/<tenantId>/graphql
```

- `<region>` は、インスタンスがデプロイされているクラウド地域です。
- `<environment>` は、環境タイプ（`sandbox` など）です。 環境が実稼動環境の場合、この値は省略されます。
- `<tenantId>` は、Adobe Experience Cloud内の組織固有のインスタンスの一意の ID です。

Catalog Service GraphQL API の使用について詳しくは、[Adobe Commerce Developer](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/) ドキュメントの *Adobe Commerceのカタログサービス* ガイド &rbrace; を参照してください。


## ヘッドレスストアフロントまたはサードパーティのサービスとの統合

ヘッドレスストアフロントと統合するには、ストアフロント設定を更新して、ストアフロントと [!DNL Catalog Service] 間の通信を有効にし、製品およびカテゴリデータを取得できるようにする必要があります。

Edge Delivery ServicesでAdobe Commerce ストアフロントを使用している場合は、カタログサービスエンドポイントをストアフロント設定に追加します。 詳しくは、[Edge Delivery Services ドキュメント &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/?lang=ja#storefront-configuration) を参照してください。

その他の統合については、プロジェクト設定のドキュメントで、サービスとバックエンドのデータソース間の統合を設定する方法の詳細を参照してください。


### ファイアウォール設定

ファイアウォールを通過する [!DNL Catalog Service] を許可するには、`commerce.adobe.io` を許可リストに追加します。

## カタログサービスと API メッシュ

Adobe Developer App Builderの [API メッシュ &#x200B;](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) を使用すると、デベロッパーはAdobe IO を使用して、プライベートまたはサードパーティの API およびその他のインターフェイスをAdobe製品と統合できます。

インストールと設定について詳しくは、[[!DNL Catalog Service]  および API メッシュ &#x200B;](mesh.md) に関するトピックを参照してください。

## データ管理ダッシュボードの使用

[Data Management Dashboard](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/data-transfer/data-dashboard) を使用して、[!DNL Catalog Service] とAdobe Commerce インスタンス間のデータ同期を監視します。 ダッシュボードには、データの書き出しステータスや同期された製品のリストなど、データ転送プロセスに関するインサイトが表示されます。
