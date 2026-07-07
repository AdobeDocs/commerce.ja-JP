---
title: AEM Assets統合用のIMS ユーザー権限の設定
description: IMS IDとAdmin Console プロファイルで、AEM Assets配信アクセス、アセットセレクター、自動入力されたCommerce設定フィールドを有効にする方法について説明します。
feature: CMS, Media, Configuration
source-git-commit: 94598c3cbc6b9fa84f92532e42ec5e9027c5b1fc
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# ユーザー権限とIMS

**IMS** （Adobe Identity Management System）は認証レイヤーです。 Adobe Commerce as a Cloud Serviceの場合、IMS認証は管理者でデフォルトで有効になっています。 Adobe Commerce オンクラウドまたはオンプレミスの場合、IMSはオプションです。[CommerceのIMSを有効にすると、強化された設定UI （Asset Selector、自動入力ドロップダウン）が提供されますが、**プログラム ID**&#x200B;および&#x200B;**環境ID**&#x200B;を手動で入力することで、IMSなしで統合を設定できます。](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/ims/adobe-ims-config.html?lang=ja){target=_blank}

AEM Assets統合では、IMSを使用する場合、特定の&#x200B;**Adobe Admin Console製品プロファイル**&#x200B;も必要です。 Commerce Adminで統合を設定するユーザーには、**AEM Assets DM OpenAPI Users - delivery**&#x200B;製品プロファイル、または&#x200B;**author**&#x200B;製品プロファイルがフォールバックとして必要です。 これは、ユーザーのIMS組織内のAdmin Console製品プロファイルを通じて制御され、次のことが可能になります。

* **アセットセレクター**&#x200B;を使用すると、カテゴリ画像またはページビルダーコンテンツを管理する際に、AEM Assetsから画像を選択できます。
* **自動入力された設定フィールド** （**プログラム ID**、**Environment ID**、**Domain mapping** ドロップダウンなど）。ユーザーのIMS セッションから、Admin Console製品プロファイル（配信または作成者）に基づいて値を取得します。

適切な権限がないと、アセットセレクターは使用できず、これらのフィールドは空のように見えるか、手動で入力する必要があります。
>[!BEGINSHADEBOX]

**IMSと権限の連携**

Adobe IMSは、ユーザーIDと組織のコンテキストを提供します。一方、Adobe Admin Consoleは、どの&#x200B;**製品プロファイル** （権限）を持つかを定義します。 AEM Assets統合では、IMSの詳細と割り当てられたプロファイルを使用して、設定フィールドを自動入力し、アセットセレクターを有効にできるかどうかを判断します。

>[!ENDSHADEBOX]

## 製品プロファイルが必要な理由

統合は、プロファイルにマッピングされたドメインのみを読み込むことができます。 したがって、ユーザーは次の製品プロファイルを持つことができます。

* **AEM配信製品プロファイル**。 ユーザーがオーサープロファイルと配信プロファイルの両方を持っている場合に、アセットセレクターと設定UIに必要です。 統合では、利用可能な場合はAEM配信製品プロファイルを使用します。

* **製品プロファイルの作成**。 AEM Assets UIにアクセスするために必要です。 また、ユーザーがAdmin ConsoleにAEM配信製品プロファイルを持っていない場合は、アセットセレクターと設定UIのフォールバックとしても機能します。

ドメイン（プログラム ID、環境ID、ドメインマッピングなど）は、AEM配信製品プロファイルに割り当てられます。 統合は、使用可能な場合は&#x200B;**AEM配信製品プロファイル**&#x200B;からドメインを読み込むか、ユーザーのAdmin ConsoleにAEM配信製品プロファイルが含まれていない場合は&#x200B;**オーサー製品プロファイル**&#x200B;にフォールバックします。 ユーザーは、次のいずれかのプロファイルを使用する必要があります。

* Commerce管理者設定の&#x200B;**プログラム ID**、**Environment ID**&#x200B;および&#x200B;**Domain mapping** ドロップダウンを入力します。
* AEM Assetsからアセットを参照して選択するには、アセットセレクターを使用します。

どちらのプロファイルも設定されていない場合、ユーザーは&#x200B;**プログラム ID**&#x200B;と&#x200B;**環境ID**&#x200B;を手動で入力できますが、アセットセレクターは使用できません。

## デプロイメントタイプ別の権限の付与

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

[!BADGE SaaSのみ]{type=Positive tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"}

IMS認証はデフォルトで有効になっています。 ユーザーがAdmin ConsoleにAEM Assets配信製品プロファイルを持っていない場合は、フォールバックとして、[Adobe Admin Console](https://adminconsole.adobe.com/)の&#x200B;**AEM DM OpenAPI Users - delivery**&#x200B;製品プロファイルに、または&#x200B;**author**&#x200B;製品プロファイル（例：`<environment-name> - author - <program-id> - <environment-id>`）にユーザーを追加します。

>[!NOTE]
>
> また、CommerceとAEM Assetsにユーザーを追加する必要があります。 完全な設定については、_ユーザーおよびIdentity Management_ ガイドの「[AEM Assetsまたは製品ビジュアルにユーザーを追加](https://experienceleague.adobe.com/ja/docs/commerce/cloud-service/user-management#add-a-user-to-aem-assets-or-product-visuals){target=_blank}」を参照してください。

![AEM Assets deliveryのAdmin Console製品プロファイル &#x200B;](../assets/aem-assets-delivery-product-profile.png){width="600" zoomable="yes"}

>[!TAB  クラウドまたはオンプレミスのAdobe Commerce]

[!BADGE PaaSのみ]{type=Informative tooltip="Cloud プロジェクト上のAdobe Commerce（Adobeで管理されるPaaS インフラストラクチャ）にのみ適用されます。"}

PaaSでアセットセレクターを有効にするには、**IMS クライアント ID**&#x200B;が必要です。 OpenAPIでDynamic Mediaを有効にする際にIMS クライアント IDを取得する方法など、前提条件については、[AEM Assets プロジェクト &#x200B;](configure-aem.md#prerequisites)の設定を参照してください。

アセットセレクターと自動入力された設定フィールド（プログラム ID、環境ID、ドメインマッピング）を使用するには：

1. [CommerceのAdobe IMSを有効にして、Commerce管理者がIMS認証を使用し、ユーザーのAdmin Console製品プロファイルを読み取れるようにします](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/ims/adobe-ims-config.html?lang=ja){target=_blank}。

1. [&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-cases)を開いて、アセットセレクターのカスタム IMS クライアント IDをリクエストします。

1. [Adobe Admin Console](https://adminconsole.adobe.com/)から、**AEM Assets DM OpenAPI Users - delivery**&#x200B;製品プロファイル、または&#x200B;**author**&#x200B;製品プロファイル（例：`<environment-name> - author - <program-id> - <environment-id>`）に、ユーザーがAdmin ConsoleにAEM配信製品プロファイルを持っていない場合のフォールバックとしてユーザーを追加します。

IMSを使用しない場合でも、Commerce管理者にプログラム IDと環境IDを手動で入力することで、統合を設定できます。

>[!ENDTABS]

## 関連ドキュメント

* [AEM Assets統合のIMS ユーザー権限を設定](setup-synchronization.md):CommerceをAEM Assetsに接続し、一致するルールを設定します。
* [&#x200B; アセットの手動選択](../synchronize/asset-selector-integration.md) - カテゴリ画像とページビルダーにアセットセレクターを使用します。
* [AEM AssetsまたはProduct Visuals](https://experienceleague.adobe.com/ja/docs/commerce/cloud-service/user-management#add-a-user-to-aem-assets-or-product-visuals){target=_blank}にユーザーを追加する – [!DNL Adobe Commerce as a Cloud Service]には、まずCommerceとAEM Cloud Manager（Business Owner, Deployment Manager）にユーザーを追加します。 **AEM Assets DM OpenAPI Users - delivery** プロファイル（またはフォールバックとして&#x200B;**author** プロファイル）は、アセットセレクターと自動入力機能の追加要件です。
* [AEM配信レイヤーにチームメンバーを割り当てる](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem#add-team-members){target=_blank}。 配信アクセスのAEM ドキュメント。

