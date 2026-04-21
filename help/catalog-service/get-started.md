---
title: ' [!DNL Catalog Service]の基本を学ぶ'
description: ' [!DNL Catalog Service] にアクセスし、フロントエンドアプリケーションおよびサードパーティサービスと統合する方法について説明します。'
role: Admin, Developer
exl-id: ee178e67-519d-4283-8de8-2634ae1f347a
source-git-commit: bf90caa5039a7d30610b18fb14efe0ba725d2cc5
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# [!DNL Catalog Service]の基本を学ぶ

[!DNL Catalog Service]を有効にした後、サービスにアクセスし、それを使用してAdobe Commerce インスタンスから商品やカテゴリ情報などのカタログデータを取得できます。 このサービスは、GraphQL APIとして利用でき、Commerce管理者またはGraphQL クエリをサポートするあらゆるフロントエンドアプリケーションからアクセスできます。

{{aco-merchandising-services}}

## サービスへのアクセス

[!DNL Catalog Service]はGraphQL APIとして利用でき、Commerce管理者またはGraphQL クエリをサポートするあらゆるフロントエンドアプリケーションからアクセスできます。 このサービスは、SaaS環境とPaaS環境の両方で利用できます。

[!BADGE PaaSのみ]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"}

| 環境 | エンドポイント |
| ------------ | ----------: |
| **テスト** | `https://catalog-service-sandbox.adobe.io/graphql` |
| **本番** | `https://catalog-service.adobe.io/graphql` |

[!BADGE SaaSのみ]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"}

| 環境 | エンドポイント |
| ----------- | --------:|
| テスト | `https://na1-sandbox.api.commerce.adobe.com/{{tenant-id}}/graphql` |
| 実稼動（まだ利用できません） | `https://na1.api.commerce.adobe.com/{{tenant-id}}/graphql` |

SaaS エンドポイントの&#x200B;**URL構造**

```text
https://<region>-<environment>.api.commerce.adobe.com/<tenantId>/graphql
```

- `<region>`は、インスタンスがデプロイされるクラウド領域です。
- `<environment>`は、`sandbox`などの環境タイプです。 環境が実稼動環境の場合、この値は省略されます。
- `<tenantId>`は、Adobe Experience Cloud内の組織の特定のインスタンスの一意のIDです。

カタログサービス GraphQL APIの使用について詳しくは、[Adobe Commerce Developer](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/) ドキュメントの&#x200B;*Adobe Commerce向けカタログサービス ガイド*&#x200B;を参照してください。

## ヘッドレスストアフロントやサードパーティサービスとの統合

ヘッドレスストアフロントと統合するには、ストアフロントと[!DNL Catalog Service]間の通信を有効にして製品およびカテゴリーデータを取得できるように、ストアフロント設定を更新する必要があります。

Edge Delivery ServicesでAdobe Commerce ストアフロントを使用している場合は、カタログサービスエンドポイントをストアフロント設定に追加します。 詳しくは、[Edge Delivery Services ドキュメント ](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/#storefront-configuration)を参照してください。

その他の統合については、サービスとバックエンドのデータソース間の統合を設定する方法について詳しくは、プロジェクト設定ドキュメントを参照してください。

### ファイアウォール設定

ファイアウォール経由で[!DNL Catalog Service]を許可するには、`commerce.adobe.io`をファイアウォール許可リストに加えるに追加します。

## カタログサービスとAPI メッシュ

Adobe Developer App Builder向け[API Mesh](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/)を使用すると、開発者は、Adobe IOを使用して、プライベートまたはサードパーティのAPIやその他のインターフェイスをAdobe製品と統合できます。

インストールと設定の詳細については、[[!DNL Catalog Service] およびAPI Mesh](mesh.md)のトピックを参照してください。

## データ管理ダッシュボードの活用

[Data Management ダッシュボード ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)を使用して、[!DNL Catalog Service]とAdobe Commerce インスタンス間のデータ同期を監視します。 ダッシュボードには、データ書き出しのステータスや同期済み製品のリストなど、データ転送プロセスに関するインサイトが表示されます。
