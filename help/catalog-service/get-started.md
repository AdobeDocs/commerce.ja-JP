---
title: ' [!DNL Catalog Service]の基本を学ぶ'
description: ' [!DNL Catalog Service] にアクセスし、フロントエンドアプリケーションおよびサードパーティサービスと統合する方法について説明します。'
role: Admin, Developer
exl-id: ee178e67-519d-4283-8de8-2634ae1f347a
TQID: https://experienceleague.adobe.com/KBdWesEoKJu-qWsY-Ny1Om-msUkyUPfUTQWftEqSg1g
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 586
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

カタログサービス GraphQL APIの使用について詳しくは、*Adobe Commerce Developer* ドキュメントの[Adobe Commerce向けカタログサービス ガイド &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)を参照してください。

## ヘッドレスストアフロントやサードパーティサービスとの統合

ヘッドレスストアフロントと統合するには、ストアフロントと[!DNL Catalog Service]間の通信を有効にして製品およびカテゴリーデータを取得できるように、ストアフロント設定を更新する必要があります。

Edge Delivery ServicesでAdobe Commerce ストアフロントを使用している場合は、カタログサービスエンドポイントをストアフロント設定に追加します。 詳しくは、[Edge Delivery Services ドキュメント &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/#storefront-configuration)を参照してください。

その他の統合については、サービスとバックエンドのデータソース間の統合を設定する方法について詳しくは、プロジェクト設定ドキュメントを参照してください。

### ファイアウォール設定

ファイアウォール経由で[!DNL Catalog Service]を許可するには、`commerce.adobe.io`をファイアウォール許可リストに加えるに追加します。

## カタログサービスとAPI メッシュ

Adobe Developer App Builder向け[API Mesh](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/)を使用すると、開発者は、Adobe IOを使用して、プライベートまたはサードパーティのAPIやその他のインターフェイスをAdobe製品と統合できます。

インストールと設定の詳細については、[[!DNL Catalog Service] およびAPI Mesh](mesh.md)のトピックを参照してください。

## データ書き出しの監視とトラブルシューティング

Commerce管理者は、Commerceから接続されたサービスへのデータ書き出しを監視およびトラブルシューティングするためのツールを提供します。

- **[Data Management Dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)** - [!DNL Catalog Service]とAdobe Commerce インスタンス間のデータ同期を監視します。 ダッシュボードには、全体的な同期ステータスが表示され、同期済みのすべての製品が一覧表示されます。

- **[データフィードの同期ステータス ページ &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)** – すべてのデータフィードの書き出しステータスを追跡して、データの一貫性を確保します。 このページでは、書き出しプロセス中に発生した問題を警告し、迅速に解決できるようにします。 「Success」ステータスは、データが書き出され、データの同期プロセスが完了すると、接続されたCommerce サービスで使用可能であることを示します。

>[!NOTE]
>
>Data Feed Sync Status ページがCommerce Admin for Commerce on Cloudまたはオンプレミスのデプロイメントで使用できない場合は、[拡張機能のインストール手順](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status#install-the-extension)に従って有効にします。
