---
title: Adobe Experience Platform Mobile SDKとCommerceの統合
description: Adobe Experience Platform Mobile SDKをヘッドレスまたはカスタムのCommerce ストアフロントで使用する方法について説明します。
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: 02d07abb-8d7f-4f0a-9f96-f42654cd79d3
TQID: https://experienceleague.adobe.com/iBxx54enSjy-vWbhCSSM-5QSjut6TjcRpWT5wWpeU2Y
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 616
ht-degree: 0%

---

# Adobe Experience Platform Mobile SDKとCommerceの統合

>[!IMPORTANT]
>
>Adobe Experience Platform Mobile SDK iOS版は、iOS 11以降をサポートしています。

[Adobe Experience Platform モバイル SDK](https://developer.adobe.com/client-sdks/home/)をCommerce モバイルアプリと統合すると、マーチャントはCommerce [ イベントデータ ](events.md)をExperience Platform エッジに送信できます。

Commerce イベントデータがエッジで利用可能な場合、他のAdobe Experience Cloud アプリケーションからアクセスできます。 例えば、データを使用してReal-Time CDPでオーディエンスを作成し、[それらのオーディエンス ](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html)を使用してCommerce モバイルアプリをパーソナライズできます。

## 設定

Adobe Experience Platform Mobile SDKとCommerceの使用を開始するには、Experience PlatformにSDKをインストールして設定します。 次に、Commerceで設定を確定します。

### Experience Platform

1. モバイルアプリの機能について詳しくは、[ モバイルアプリのAdobe Experience Cloud チュートリアル ](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html)を参照してください。

1. [Experience PlatformにSDKをインストールして設定](https://developer.adobe.com/client-sdks/documentation/getting-started/)します。

   >[!NOTE]
   >
   >Experience Platformで作成および設定するスキーマは、Commerce モバイルアプリのアプリケーションコードで使用するスキーマと同じです。

### Commerce

Experience PlatformのSDK設定を完了したら、SDK設定をCommerceに追加します。

1. Commerce イベントデータをSDK経由でExperience Platformに送信するには、アプリケーションコードにXDM スキーマを指定する必要があります。 このスキーマは、Experience PlatformのSDKのスキーマ [configured](https://developer.adobe.com/client-sdks/home/getting-started/set-up-schemas-and-datasets/)と一致する必要があります。

   次の例は、`web.webpagedetails.pageViews` イベントを追跡し、電子メールフィールドを使用して`identityMap`を設定する方法を示しています。

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

1. Commerce Cloudとの連携。

   プロジェクトのビルド設定で、Commerce GraphQL エンドポイントにURLを追加します。 例：

   - デバッグ：http://_debug_.commercesite.cloud/graphql/
   - リリース：http://_release_.commercesite.cloud/graphql/

1. Commerce GraphQL エンドポイントからデータを取得するには、まず[Apollo Code Generator](https://www.apollographql.com/docs/ios/)を使用して、プロジェクトに必要なファイルとディレクトリを生成します。

   1. プロジェクト ディレクトリから、[install](https://www.apollographql.com/docs/ios/get-started#1-install-the-apollo-frameworks) Apollo iOSをインストールします。

   1. Apollo Codegen CLIを[初期化](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#initialize)。

      これで`apollo-codegen-configuration.json` ファイルが作成されます。

   1. `apollo-codegen-configuration.json` ファイルの内容を次の内容に置き換えて、プロジェクトに必要なGraphQL ファイルとディレクトリを生成します。

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

   1. Commerce GraphQL スキーマを[取得](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#fetch-schema)します。

      Commerce GraphQL スキーマへの参照を含む`./apollo-codegen-config.json` ファイルへのパスであることを確認します。

   1. [ ソースコードを](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#generate)生成します。

      必要なファイルとディレクトリを生成するための構成情報を含む`./apollo-codegen-config.json` ファイルへのパスであることを確認します。

   1. 新しく作成した&#x200B;**GraphQLGenerated** フォルダー内で、GraphQL タイプを追加または編集します。 例えば、次の内容を含む`DynamicBlocks.graphql` タイプを追加できます。

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

   これで、Adobe Experience Platform Mobile SDKとCommerce モバイルアプリを統合しました。 アプリからExperience Platform edgeへのイベントデータフロー。

## モバイルアプリケーションから生成されたCommerce イベントの識別方法

すべての[ イベント ](events.md)には、`channel`というフィールドが含まれています。 `channel` フィールドには、`channel._id`と`channel._type`が含まれており、Luma ストアフロントの名前空間値はそれぞれ`"https://ns.adobe.com/xdm/channels/web"`と`"https://ns.adobe.com/xdm/channel-types/web"`です。 ただし、モバイルストアフロントの場合、名前空間の値はそれぞれ`"https://ns.adobe.com/xdm/channels/mobile-app"`と`"https://ns.adobe.com/xdm/channel-types/mobile"`です。

## 次のステップ

モバイル Commerce アプリからReal-Time CDP オーディエンスを取得し、カートの価格ルール、動的ブロック、および関連する商品ルールを通知する方法については、[Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html#retrieve-audiences-using-the-adobe-experience-platform-mobile-sdk)を参照してください。
