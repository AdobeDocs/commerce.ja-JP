---
title: Adobe Experience Platform Mobile SDKとCommerceの統合
description: ヘッドレスまたはカスタムのCommerce ストアフロントでのAdobe Experience Platform Mobile SDKの使用方法について説明します。
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: 02d07abb-8d7f-4f0a-9f96-f42654cd79d3
source-git-commit: a3e19940e2a3d8a240bb17703cfdd9903df311aa
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Adobe Experience Platform Mobile SDKとCommerceの統合

>[!IMPORTANT]
>
>iOS用Adobe Experience Platform Mobile SDKは、iOS 11 以降をサポートしています。

[Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/) とCommerce モバイルアプリの統合により、マーチャントはCommerce [ イベントデータ ](events.md) をExperience Platform エッジに送信できます。

Commerce イベントデータがエッジで使用できる場合、他のAdobe Experience Cloud アプリケーションからアクセスできます。 例えば、データを使用してReal-Time CDPでオーディエンスを作成し、[ これらのオーディエンスを使用 ](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html) してCommerce モバイルアプリをパーソナライズできます。

## 設定

CommerceでのAdobe Experience Platform Mobile SDKの使用を開始するには、Experience PlatformにSDKをインストールして設定します。 次に、Commerceで設定を最終決定します。

### Experience Platform

1. モバイルアプリの機能について詳しくは、[ モバイルアプリでのAdobe Experience Cloud チュートリアル ](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html) を参照してください。

1. Experience PlatformのSDKを [ インストールして設定 ](https://developer.adobe.com/client-sdks/documentation/getting-started/) します。

   >[!NOTE]
   >
   >Experience Platformで作成および設定するスキーマは、Commerce モバイルアプリのアプリケーションコードで使用するスキーマと同じです。

### Commerce

Experience Platform のSDK設定を完了したら、SDK設定をCommerceに追加します。

1. SDKを介してCommerce イベントデータをExperience Platformに送信するには、アプリケーションコードで XDM スキーマを指定する必要があります。 このスキーマは、Experience PlatformのSDKのスキーマ [ 設定済み ](https://developer.adobe.com/client-sdks/home/getting-started/set-up-schemas-and-datasets/) と一致する必要があります。

   次の例では、`web.webpagedetails.pageViews` イベントをトラッキングし、メール フィールドを使用して `identityMap` を設定する方法を示しています。

   ```swift
   let stateName = "luma: content: ios: us: en: home"
   var xdmData: [String: Any] = [
       "eventType": "web.webpagedetails.pageViews",
       "web": [
           "webPageDetails": [
               "pageViews": [
                   "value": 1
               ],
               "name": "Home page"
           ]
       ]
   ]
   
   let experienceEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: experienceEvent)
   
   // Adobe Experience Platform - Update Identity
   
   let emailLabel = "mobileuser@example.com"
   
   let identityMap: IdentityMap = IdentityMap()
   identityMap.add(item: IdentityItem(id: emailLabel), withNamespace: "Email")
   Identity.updateIdentities(with: identityMap)
   ```

1. をCommerce Cloud環境に接続します。

   プロジェクトのビルド設定で、Commerce GraphQL エンドポイントへの URL を追加します。 例：

   - デバッグ：http://_debug_.commercesite.cloud/graphql/
   - リリース：http://_release_.commercesite.cloud/graphql/

1. Commerce GraphQL エンドポイントからデータを取得するには、まず [Apollo コードジェネレーター ](https://www.apollographql.com/docs/ios/) を使用して、プロジェクトに必要なファイルとディレクトリを生成します。

   1. プロジェクトディレクトリから、[install](https://www.apollographql.com/docs/ios/get-started#1-install-the-apollo-frameworks) Apollo iOSをインストールします。

   1. [ 初期化 ](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#initialize) Apollo Codegen CLI。

      これにより、`apollo-codegen-configuration.json` ファイルが作成されます。

   1. `apollo-codegen-configuration.json` ファイルの内容を次のように置き換えて、必要なGraphQL ファイルとディレクトリをプロジェクトに生成します。

      ```json
      {
      "schemaName" : "MagentoAPI",
      "input" : {
          "operationSearchPaths" : [
          "**/*.graphql"
          ],
          "schemaSearchPaths" : [
          "**/*.graphqls"
          ]
      },
      "output" : {
          "testMocks" : {
          "none" : {
          }
          },
          "schemaTypes" : {
          "path" : "../MagentoAPI",
          "moduleType" : {
              "swiftPackageManager" : {
              }
          }
          },
          "operations" : {
          "inSchemaModule" : {
          }
          }
      },
      "schemaDownloadConfiguration": {
          "downloadMethod": {
              "introspection": {
                  "endpointURL": "http://magento24.com/graphql/",
                  "httpMethod": {
                      "POST": {}
                  },
                  "includeDeprecatedInputValues": false,
                  "outputFormat": "SDL"
              }
          },
          "downloadTimeout": 60,
          "headers": [],
          "outputPath": "magento.graphqls"
      }
      }
      ```

   1. [ 取得 ](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#fetch-schema) Commerce GraphQL スキーマ。

      パスが `./apollo-codegen-config.json` ファイルへのパスであることを確認します。このファイルには、Commerce GraphQL スキーマへの参照が含まれています。

   1. [ 生成 ](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#generate) ソースコード。

      パスが `./apollo-codegen-config.json` ファイルへのパスであることを確認します。このファイルには、必要なファイルとディレクトリを生成するための設定情報が含まれています。

   1. 新しく作成した **GraphQLGenerated** フォルダー内で、GraphQLのタイプを追加または編集します。 例えば、次の内容を含んだ `DynamicBlocks.graphql` タイプを追加できます。

      ```graphql
      query dynamicBlocks($input: DynamicBlocksFilterInput){
          dynamicBlocks(input: $input)
          {
              items {
                  content {
                      html
                  }
              }
          }
      }
      ```

   これで、Adobe Experience Platform Mobile SDKがCommerce モバイルアプリと統合されました。 イベントデータは、アプリからExperience Platform Edge に送られます。

## モバイルアプリケーションから生成されたCommerce イベントを区別する方法

すべての [ イベント ](events.md) には、`channel` というフィールドが含まれています。 `channel` フィールドには、`channel._id` と `channel._type` が含まれ、Luma ストアフロントの名前空間の値はそれぞれ `"https://ns.adobe.com/xdm/channels/web"` と `"https://ns.adobe.com/xdm/channel-types/web"` です。 ただし、モバイルストアフロントの場合、名前空間の値はそれぞれ `"https://ns.adobe.com/xdm/channels/mobile-app"` と `"https://ns.adobe.com/xdm/channel-types/mobile"` です。

## 次の手順

モバイル Commerce アプリからReal-Time CDP オーディエンスを取得し、買い物かごの価格ルール、動的ブロック、関連する商品ルールを通知する方法については、[Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html#retrieve-audiences-using-the-adobe-experience-platform-mobile-sdk) を参照してください。
