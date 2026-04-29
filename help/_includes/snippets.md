---
source-git-commit: 156ed7a480de9239843c96b6b6bc252585f498d6
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---
# Commerce スニペット


## Merchandising Services for Optimizer {#aco-merchandising-services}

>[!NOTE]
>
>Adobe Commerce OptimizerまたはAdobe Commerce Optimizer コネクタを使用するCommerce ソリューションの場合は、Catalog Service GraphQL APIの代わりに[Merchandising Services GraphQL API](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api/)を使用します。

## Optimizerのデータ同期チェック {#aco-data-sync-verification}

>[!NOTE]
>
>カタログデータをAdobe Commerce Optimizerに書き出すために[Adobe Commerce Optimizer Connector](../aco-connector/overview.md)をインストールした場合は、Commerce Optimizer Studioの[Data Feed Sync Status page](../optimizer/setup/data-sync.md)を使用して、Data Management ダッシュボードではなくAdobe Commerce Optimizerに正常に同期されたデータを確認します。

## ACCS早期アクセス {#accs-early-access}

>[!NOTE]
>
>このドキュメントでは、早期アクセス開発の製品について説明しており、一般的な可用性を目的とするすべての機能を反映しているわけではありません。

<!--
## Nav hack ACCS {#nav-hack-accs}

>[!BEGINSHADEBOX]

<table style="table-layout:fixed">
  <tr>
    <td style="vertical-align: middle;"><a href="https://developer.adobe.com/commerce/webapi/"><img alt="Developers" src="../assets/icons/developers.svg" /> <strong>Developers</strong></a></td>
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/?lang=ja"><img alt="Storefront" src="../assets/icons/storefront.svg" /> <strong>Storefront</strong></a></td>
    <td style="vertical-align: middle;"><a href="../cloud-service/overview.md"><img alt="Merchants" src="../assets/icons/merchants.svg" /> <strong>Merchants</strong></a></td>
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/ja/docs/commerce-learn/tutorials/getting-started/commerce-as-a-cloud-service/overview"><img alt="Videos" src="../assets/icons/videos.svg" /> <strong>Videos</strong></a></td>
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/playgrounds/commerce-services/?lang=ja"><img alt="Playgrounds" src="../assets/icons/playgrounds.svg" /> <strong>Playgrounds</strong></a></td>
  </tr>
</table>

>[!ENDSHADEBOX]
-->

## ACCS サンドボックスのみの実験的機能 {#accs-sandbox-experimental}

>[!IMPORTANT]
>
>この機能は実験的なもので、[!DNL Adobe Commerce as a Cloud Service]のサンドボックス環境でのみ使用できます。
>
>この機能は予告なく変更される場合があります。

[!BADGE &#x200B; サンドボックス &#x200B;]{type=Caution tooltip="リストされている項目は、現在サンドボックス環境でのみ使用できます。 Adobeでは、サンドボックス環境で新しいリリースを最初に使用できるようになりました。これにより、本番環境でリリースを利用できるようになる前に、今後の変更をテストする時間を確保できます。"}

## AEM Assets インスタンスのマッピング {#aem-assets-instance-mapping}

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service]を[!DNL AEM Assets]に接続する場合、[!DNL AEM Assets] ステージインスタンスはサンドボックス [!DNL Adobe Commerce as a Cloud Service] インスタンスやその他の実稼動以外の環境にマッピングされます。 [!DNL AEM Assets]実稼動インスタンスは[!DNL Adobe Commerce as a Cloud Service]実稼動インスタンスにマッピングされます。

## IMS IDとシングルサインオン情報 {#ims-identity-and-sso-config}

Adobe Commerce IDの管理と認証は、Adobe Identity Management System （IMS）によってAdobe Admin Consoleを通じて管理されます。

Adobe ID、Enterprise ID、Federated IDなどのID設定オプションと、Adobe アプリへの安全なアクセス用にシングルサインオン（SSO）を設定する手順について詳しくは、*Enterprise Admin Console* ドキュメントの[IDとシングルサインオンの設定](https://helpx.adobe.com/jp/enterprise/using/set-up-identity.html)を参照してください。

## ACCS サービスと拡張性のリリースノート {#accs-release}

### その他のリリースノート

[!DNL Adobe Commerce as a Cloud Service]には、最新バージョンのマーチャンダイジングサービス、支払いサービス、および拡張性リリースが含まれています。 以下のリンクを使用して、各リリースノートを表示します。

| サービス | 拡張機能 | ストアフロント |
| --- | --- | --- |
| <ul><li>[&#x200B; カタログ サービス &#x200B;](../catalog-service/release-notes.md)</li><li>[&#x200B; ライブサーチ &#x200B;](../live-search/release-notes.md)</li><li>[決済サービス &#x200B;](../payment-services/release-notes.md)</li><li>[商品レコメンデーション &#x200B;](../product-recommendations/release-notes.md)</li><li>[SaaS データ書き出し](../data-export/release-notes.md)</li></ul> | <ul><li>[管理者UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/release-notes/)</li><li>[API メッシュ &#x200B;](https://developer.adobe.com/graphql-mesh-gateway/mesh/release)</li><li>[&#x200B; イベント &#x200B;](https://developer.adobe.com/commerce/extensibility/events/release-notes/)</li><li>[Webhook](https://developer.adobe.com/commerce/extensibility/webhooks/release-notes/)</li></ul> | <ul><li>[&#x200B; リリース情報](https://experienceleague.adobe.com/developer/commerce/storefront/releases/?lang=ja)</li><li>[変更履歴](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/?lang=ja)</li></ul> |

## Adobe Commerce Optimizer サービスのリリースノート {#aco-release}

### その他のリリースノート

[!DNL Adobe Commerce Optimizer]は、AEM Assets統合の最新リリース、Commerce Optimizer コネクタ、および[!DNL Adobe Commerce Storefront]で動作します。 以下のリンクを使用して、各領域のリリースノートを表示します。

| サービス | ストアフロント |
| --- | --- |
| [AEM Assetsとの統合](../aem-assets-integration/release-notes.md)<br>[Commerce Optimizer コネクタ &#x200B;](../aco-connector/release-notes.md) | [&#x200B; ストアフロントのリリース情報](https://experienceleague.adobe.com/developer/commerce/storefront/releases/?lang=ja)<br>[&#x200B; ストアフロントの変更履歴](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/?lang=ja) |
