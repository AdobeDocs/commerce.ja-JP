---
title: ストアフロントの設定
description: 基礎モード ツールを実行して [!DNL Adobe Commerce as a Cloud Service]  ストアフロントを設定する方法を説明します。
feature: Storefront
role: Developer
level: Beginner
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"
autotag-review: '2026-06-18T16:05:19.363Z'
TQID: 'https://experienceleague.adobe.com/LoeNTJ-evBJB-TaJV0mEQpD2G2MwxHX7cYHx67kP0cA'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2: id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: bcc5edb5-84c3-4940-9f84-ed88b6c16274
source-git-commit: 15a99ce130efaf3a35968cfc01747fe1b6ab93c9
workflow-type: tm+mt
source-wordcount: 300
ht-degree: 0%

---

# ストアフロントの設定

[!DNL Adobe Commerce as a Cloud Service] （SaaS）用に[!DNL Edge Delivery Services]を利用した[!DNL Adobe Commerce Storefront]を設定するには、次の手順を実行します。

よりカスタマイズ可能で詳細なチュートリアルについては、[ ストアフロントのドキュメント ](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/)を参照してください。

1. [ サイト作成ツール ](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)を開きます。

1. **[!UICONTROL Create New Site (Code & Content)]**&#x200B;を選択します。

1. ストアフロントコードリポジトリを作成する&#x200B;**[!UICONTROL Github Organization/Username]**&#x200B;を入力します。

1. **[!UICONTROL Site Name]**&#x200B;を入力します。

1. **[!UICONTROL Commerce GraphQL Endpoint (optional)]** フィールドに[!DNL Adobe Commerce as a Cloud Service] （SaaS） GraphQL エンドポイントを入力します。このエンドポイントには、[ インスタンスを作成した後にCommerce Cloud Managerでアクセスできます](./getting-started.md#create-an-instance)。

   または、[[!DNL API Mesh]](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic)を使用している場合は、[!DNL API Mesh] GraphQL エンドポイントを&#x200B;**[!UICONTROL Commerce GraphQL Endpoint (optional)]** フィールドに入力します。 詳しくは、[ メッシュの作成](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh)を参照してください。

1. **[!UICONTROL Create Site]**&#x200B;をクリックします。 画面の指示に従って、GitHub リポジトリへのアクセスを承認します。

プロセスが完了したら、次の方法でストアフロントをカスタマイズできます。

* コードをカスタマイズ：`https://github.com/<username or org>/<repo name>`
* コンテンツを編集：`https://da.live/#/<username or org>/<repo name>`
* 設定を管理：`https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
* ストアフロントのプレビュー：`https://main--<repo name>--<username or org>.aem.page/`

## 次のステップ

詳しくは、次の記事を参照してください。

* [ ストアフロントコンテンツの更新](./use-cases.md#update-storefront-content) - ストアフロントでコンテンツとデータを管理および表示します。
* [ コンテクスト実験](./use-cases.md#contextual-experimentation) - ストアフロントで実験を作成および管理します。
* [ バリエーションの生成](./use-cases.md#generate-variations) – 生成AIを使用して、高品質なコンテンツ生成を自動化します。
* [Adobe Commerce Storefront ドキュメント ](https://experienceleague.adobe.com/developer/commerce/storefront/) - サイトコンテンツの更新と、Commerce フロントエンドコンポーネントおよびバックエンドデータとの統合について詳しく説明します。
* [設定サービス ](https://www.aem.live/docs/config-service-setup) - ストアフロント設定を`config.json`から移行して、再帰設定やオーバーレイなどの高度なユースケースをサポートする設定サービスを使用する方法について説明します。
