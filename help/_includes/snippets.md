---
source-git-commit: 25e92d9418c5b0ac331e8aab2e13330f52ca85bb
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---
# Commerce スニペット

## ACCS 早期アクセス {#accs-early-access}

>[!NOTE]
>
>このドキュメントでは、製品の早期アクセス開発について説明しており、一般提供を目的とした機能のすべてを反映しているわけではありません。

<!--
## Nav hack ACCS {#nav-hack-accs}

>[!BEGINSHADEBOX]

<table style="table-layout:fixed">
  <tr>
    <td style="vertical-align: middle;"><a href="https://developer.adobe.com/commerce/webapi/"><img alt="Developers" src="../assets/icons/developers.svg" /> <strong>Developers</strong></a></td>
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/"><img alt="Storefront" src="../assets/icons/storefront.svg" /> <strong>Storefront</strong></a></td>
    <td style="vertical-align: middle;"><a href="../cloud-service/overview.md"><img alt="Merchants" src="../assets/icons/merchants.svg" /> <strong>Merchants</strong></a></td>
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/getting-started/commerce-as-a-cloud-service/overview"><img alt="Videos" src="../assets/icons/videos.svg" /> <strong>Videos</strong></a></td>
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/playgrounds/commerce-services/"><img alt="Playgrounds" src="../assets/icons/playgrounds.svg" /> <strong>Playgrounds</strong></a></td>
  </tr>
</table>

>[!ENDSHADEBOX]
-->

## ACCS サンドボックスのみの実験的機能 {#accs-sandbox-experimental}

>[!IMPORTANT]
>
>この機能は試験的で、[!DNL Adobe Commerce as a Cloud Service] のサンドボックス環境でのみ使用できます。
>
>この機能は予告なく変更される場合があります。

[!BADGE  サンドボックス ]{type=Caution tooltip="リストされた項目は、現在、サンドボックス環境でのみ使用できます。 Adobeでは、最初にサンドボックス環境で新しいリリースを使用できるようにして、リリースが実稼動環境で使用できるようになる前に、今後の変更をテストするための時間を確保します。"}

## AEM Assets インスタンスのマッピング {#aem-assets-instance-mapping}

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service] を [!DNL AEM Assets] に接続すると、[!DNL AEM Assets] ステージインスタンスがサンドボックス [!DNL Adobe Commerce as a Cloud Service] インスタンスおよびその他の実稼動以外の環境にマッピングされます。 お使いの [!DNL AEM Assets] 実稼動インスタンスが、[!DNL Adobe Commerce as a Cloud Service] 実稼動インスタンスにマッピングされます。

## IMS ID とシングルサインオン情報 {#ims-identity-and-sso-config}

Adobe Commerceの ID 管理および認証は、Adobe Admin Consoleを通じて、Adobe Identity Management System （IMS）で管理されます。

Adobe ID、Enterprise ID、Federated IDなどの ID 設定オプション、およびAdobe アプリに安全にアクセスするためのシングルサインオン（SSO）を設定する手順については、[Enterprise Admin Console](https://helpx.adobe.com/enterprise/using/set-up-identity.html) ドキュメントの *ID とシングルサインオンの設定* を参照してください。

## ACCS サービスと拡張リリースノート {#accs-release}

### その他のリリースノート

[!DNL Adobe Commerce as a Cloud Service] には、最新バージョンのマーチャンダイジングサービス、支払いサービスおよび拡張リリースが含まれています。 次のリンクを使用して、それぞれのリリースノートを表示します。

| サービス | 拡張性 | ストアフロント |
| --- | --- | --- |
| <ul><li>[ カタログサービス ](../catalog-service/release-notes.md)</li><li>[Live Search](../live-search/release-notes.md)</li><li>[ 資金決済 ](../payment-services/release-notes.md)</li><li>[ 製品の推奨事項 ](../product-recommendations/release-notes.md)</li><li>[SaaS データのエクスポート ](../data-export/release-notes.md)</li></ul> | <ul><li>[ 管理 UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/release-notes/)</li><li>[API メッシュ ](https://developer.adobe.com/graphql-mesh-gateway/mesh/release)</li><li>[ イベント ](https://developer.adobe.com/commerce/extensibility/events/release-notes/)</li><li>[Webhook](https://developer.adobe.com/commerce/extensibility/webhooks/release-notes/)</li></ul> | <ul><li>[ リリース情報 ](https://experienceleague.adobe.com/developer/commerce/storefront/releases/)</li><li>[ 変更ログ ](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/)</li></ul> |
