---
title: ストアフロントの設定
description: 基礎ツールを実行してストアフロントを設定する方法  [!DNL Adobe Commerce as a Cloud Service]  説明します。
role: Developer
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
source-git-commit: b0d492ffab2dcf5742772d02bed026e241ac43cd
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# ストアフロントの設定

Edge Delivery Services for Adobe Commerce as a Cloud Service（SaaS）を利用したAdobe Commerce ストアフロントを設定するには、次の手順を使用します。

よりカスタマイズ可能で詳細なチュートリアルについては、[ ストアフロントのドキュメント ](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=ja) を参照してください。

1. [ サイト作成ツール ](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator) を開きます。

1. 「**新しいサイトを作成（コードとコンテンツ）**」を選択します。

1. ストアフロントコードリポジトリを作成する **Github 組織/ユーザー名** を入力します。

1. **サイト名** を入力します。

1. 「**Commerce GraphQL エンドポイント（オプション）**」フィールドに、Adobe Commerce as a Cloud Service（SaaS）GraphQL エンドポイントを入力します。このエンドポイントには、（インスタンスの作成 [ 後にCommerce Cloud Manager でアクセスでき ](./getting-started.md#create-an-instance) す。

   または、[API メッシュ ](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic) を使用している場合は、API メッシュ GraphQL エンドポイントを **Commerce GraphQL エンドポイント（オプション）** フィールドに入力します。 詳細については、[ メッシュの作成 ](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh) を参照してください。

1. **サイトを作成** をクリックします。 画面の指示に従って、Github リポジトリへのアクセスを認証します。

プロセスが完了したら、次の方法でストアフロントをカスタマイズできます。

* コードのカスタマイズ：`https://github.com/<username or org>/<repo name>`
* コンテンツを編集：`https://da.live/#/<username or org>/<repo name>`
* 設定を管理：`https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
* ストアフロントのプレビュー：`https://main--<repo name>--<username or org>.aem.page/`

## 次の手順

詳しくは、次の記事を参照してください。

* ストアフロントでのコンテンツとデータの管理と表示について詳しくは、[ ストアフロントコンテンツの更新 ](./use-cases.md#update-storefront-content) を参照してください。
* コンテキスト実験機能について詳しくは、「[ コンテキスト実験 ](./use-cases.md#contextual-experimentation)」を参照してください。
* ジェネレーティブ AI を使用して高品質のコンテンツ生成を自動化する方法について詳しくは、[ バリエーションの生成 ](./use-cases.md#generate-variations) を参照してください。
* サイトコンテンツの更新、Commerce フロントエンドコンポーネントおよびバックエンドデータとの統合について詳しくは、[Adobe Commerce ストアフロントのドキュメント ](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=ja) を参照してください。
