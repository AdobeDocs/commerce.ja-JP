---
title: ストアフロントの設定
description: 基礎モードツールを実行してストアフロントを設定する方法  [!DNL Adobe Commerce as a Cloud Service]  説明します。
feature: Storefront
role: Developer
level: Beginner
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
source-git-commit: 0cd9749574460374a8fe875f1eff54f2a4a8d614
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# ストアフロントの設定

[!DNL Adobe Commerce Storefront] for [!DNL Edge Delivery Services] （SaaS）を使用した [!DNL Adobe Commerce as a Cloud Service] を設定するには、次の手順を実行します。

カスタマイズ可能で詳細なチュートリアルについては、[ ストアフロントのドキュメント ](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) を参照してください。

1. [ サイト作成ツール ](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator) を開きます。

1. 「**[!UICONTROL Create New Site (Code & Content)]**」を選択します。

1. ストアフロントのコードリポジトリを作成する **[!UICONTROL Github Organization/Username]** を入力します。

1. **[!UICONTROL Site Name]** を入力します。

1. 「**[!UICONTROL Commerce GraphQL Endpoint (optional)]**」フィールドに、[!DNL Adobe Commerce as a Cloud Service] （SaaS）GraphQL エンドポイントを入力します。このエンドポイントは、（インスタンスを作成 [ した後、Commerce Cloud Manager でアクセスでき ](./getting-started.md#create-an-instance) す。

   または、[[!DNL API Mesh]](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic) を使用している場合は、[!DNL API Mesh] GraphQL エンドポイントを「**[!UICONTROL Commerce GraphQL Endpoint (optional)]**」フィールドに入力します。 詳細については、[ メッシュの作成 ](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh) を参照してください。

1. 「**[!UICONTROL Create Site]**」をクリックします。 画面の指示に従って、GitHub リポジトリへのアクセスを認証します。

プロセスが完了したら、次の方法でストアフロントをカスタマイズできます。

* コードのカスタマイズ：`https://github.com/<username or org>/<repo name>`
* コンテンツを編集：`https://da.live/#/<username or org>/<repo name>`
* 設定を管理：`https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
* ストアフロントのプレビュー：`https://main--<repo name>--<username or org>.aem.page/`

## 次の手順

詳しくは、次の記事を参照してください。

* [ ストアフロントコンテンツの更新 ](./use-cases.md#update-storefront-content) - ストアフロントのコンテンツとデータを管理および表示します。
* [ コンテキスト実験 ](./use-cases.md#contextual-experimentation) - ストアフロントで実験を作成および管理します。
* [ バリエーションを生成 ](./use-cases.md#generate-variations) – 生成 AI を使用して、高品質のコンテンツ生成を自動化します。
* [Adobe Commerce ストアフロントのドキュメント ](https://experienceleague.adobe.com/developer/commerce/storefront/) - サイトコンテンツの更新と、Commerceのフロントエンドコンポーネントおよびバックエンドデータとの統合に関する詳細情報を説明します。
* [ 設定サービス ](https://www.aem.live/docs/config-service-setup) - `config.json` からストアフロント設定を移行して、リポジトリ設定やオーバーレイなどの高度なユースケースをサポートする設定サービスを使用する方法について説明します。
