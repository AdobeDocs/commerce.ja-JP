---
title: AEM Assets統合用の IMS ユーザー権限の設定
description: IMS ID およびAdmin Console プロファイルを使用して、AEM Assets配信アクセス、アセットセレクターおよび自動入力されたCommerce設定フィールドを有効にする方法について説明します。
feature: CMS, Media, Configuration
source-git-commit: 0fd98bf86555c914f7a5b1e177c31c37764dbf84
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---

# ユーザー権限と IMS

**IMS** （Adobe Identity Management System）は認証レイヤーです。 Adobe Commerce as a Cloud Serviceの場合、管理者では IMS 認証がデフォルトで有効になっています。 Adobe Commerce on cloud またはオンプレミスの場合、IMS はオプションです。[Commerceに対する IMS の有効化 &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/ims/adobe-ims-config.html){target=_blank} は拡張された設定 UI （アセットセレクター、自動入力されたドロップダウン）を提供しますが、**プログラム ID** および **環境 ID** を手動で入力することで、IMS なしで統合を設定できます。

IMS を使用する場合、AEM Assets統合には特定の **Adobe Admin Console製品プロファイル** も必要です。 Commerce Admin で統合を設定するユーザーには、フォールバックとして、**AEM Assets DM OpenAPI Users – 配信** 製品プロファイル、または **オーサー** 製品プロファイルが必要です。 これは、ユーザーの IMS 組織内のAdmin Console製品プロファイルを通じて制御され、次のことを可能にします。

* **アセットセレクター** を使用すると、カテゴリ画像またはページビルダーコンテンツを管理する際に、AEM Assetsから画像を選択できます。
* **プログラム ID**、**環境 ID** **、**&#x200B;**ドメインマッピング** などの自動入力された設定フィールドは、Admin Consoleの製品プロファイル（配信またはオーサー）に基づいて、ユーザーの IMS セッションから値を取り込みます。

適切な権限がないと、アセットセレクターは使用できず、これらのフィールドは空で表示されるか、手動で入力する必要があります。
>[!BEGINSHADEBOX]

**IMS と権限の連携方法**

Adobe IMSはユーザー ID と組織コンテキストを提供し、Adobe Admin Consoleはどの **製品プロファイル** （権限）を持っているかを定義します。 AEM Assets統合は、IMS の詳細と割り当てられたプロファイルを使用して、設定フィールドに自動入力できるかどうかを判断し、アセットセレクターを有効にします。

>[!ENDSHADEBOX]

## 製品プロファイルが必要な理由

統合では、プロファイルにマッピングされたドメインのみを読み込むことができます。 したがって、ユーザーは次の製品プロファイルを持つことができます。

* **AEM配信製品プロファイル**。 作成者プロファイルと配信プロファイルの両方を持つユーザーの場合、アセットセレクターおよび設定 UI で必須。 利用可能な場合、統合ではAEM配信製品プロファイルを使用します。

* **オーサー製品プロファイル**。 AEM Assets UI にアクセスするために必要です。 は、ユーザーがAdmin ConsoleにAEM配信製品プロファイルを持っていない場合、アセットセレクターと設定 UI のフォールバックとしても機能します。

ドメイン（プログラム ID、環境 ID、ドメインマッピングを含む）がAEM配信製品プロファイルに割り当てられます。 この統合は、**AEM配信製品プロファイル** が使用可能な場合はそのプロファイルからドメインを読み込みます。または、AEM配信製品プロファイルがユーザーのAdmin Consoleにない場合は **オーサー製品プロファイル** にフォールバックします。 ユーザーが次の操作を行うには、これらのプロファイルのいずれかが必要です。

* Commerce Admin 設定の **プログラム ID**、**環境 ID**、および **ドメインマッピング** ドロップダウンに入力します。
* アセットセレクターを使用して、AEM Assetsからアセットを参照して選択します。

どちらのプロファイルも設定されていない場合も、ユーザーは **プログラム ID** と **環境 ID** を手動で入力できますが、アセットセレクターは使用できません。

## デプロイメントタイプ別の権限の付与

>[!BEGINTABS]

>[!TAB Adobe Commerceas a Cloud Service]

[!BADGE SaaS のみ &#x200B;]{type=Positive tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"}

IMS 認証はデフォルトで有効になっています。 ユーザーを **AEM Assets DM OpenAPI ユーザー – 配信**&#x200B;[Adobe Admin Console](https://adminconsole.adobe.com/) の製品プロファイル、またはユーザーがAdmin ConsoleにAEM配信製品プロファイルを持っていない場合は、フォールバックとして **オーサー** 製品プロファイル（例：`<environment-name> - author - <program-id> - <environment-id>`）に追加します。

>[!NOTE]
>
> また、ユーザーはCommerceとAEM Assetsにも追加する必要があります。 完全な設定については、『 [&#x200B; ユーザーとIdentity Management](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/user-management#add-a-user-to-aem-assets-or-product-visuals){target=_blank} ガイドの _AEM Assetsまたは製品ビジュアルへのユーザーの追加_ を参照してください。

![AEM Assets配信用のAdmin Console製品プロファイル &#x200B;](../assets/aem-assets-delivery-product-profile.png){width="600" zoomable="yes"}

>[!TAB  クラウドまたはオンプレミスのAdobe Commerce]

[!BADGE PaaS のみ &#x200B;]{type=Informative tooltip="クラウドプロジェクト上のAdobe Commerceにのみ適用されます（Adobeが管理する PaaS インフラストラクチャ）。"}

**IMS クライアント ID** は、PaaS でアセットセレクターを有効にするために必要です。 OpenAPI で Dynamic Media を有効にする際に IMS クライアント ID を取得する方法など、前提条件については、[AEM Assets プロジェクトの設定 &#x200B;](configure-aem.md#prerequisites) を参照してください。

アセットセレクターと自動入力された設定フィールド（プログラム ID、環境 ID、ドメインマッピング）を使用するには：

1. [CommerceのAdobe IMSを有効にする &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/ims/adobe-ims-config.html){target=_blank} これにより、Commerce管理者が IMS 認証を使用し、ユーザーのAdmin Console製品プロファイルを読み取ることができます。

1. [&#x200B; サポートチケットを開く &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-cases) アセットセレクターのカスタム IMS クライアント ID をリクエストします。

1. [Adobe Admin Console](https://adminconsole.adobe.com/) から、**AEM Assets DM OpenAPI Users – 配信** 製品プロファイル、またはAdmin ConsoleにAEM配信製品プロファイルがない場合のフォールバックとして **オーサー** 製品プロファイル （例：`<environment-name> - author - <program-id> - <environment-id>`）にユーザーを追加します。

IMS がインストールされていない場合でも、Commerce Admin でプログラム ID と環境 ID を手動で入力することで、統合を設定できます。

>[!ENDTABS]

## 関連ドキュメント

* [AEM Assets統合の IMS ユーザー権限の設定 &#x200B;](setup-synchronization.md) - CommerceをAEM Assetsに接続して、マッチングルールを設定します。
* [&#x200B; 手動のアセット選択 &#x200B;](../synchronize/asset-selector-integration.md) - カテゴリ画像とページビルダーにアセットセレクターを使用します。
* [AEM Assetsまたは製品ビジュアルへのユーザーの追加 &#x200B;](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/user-management#add-a-user-to-aem-assets-or-product-visuals){target=_blank} - ACCS の場合、最初にCommerceおよびAEM Cloud Manager（ビジネスオーナー、デプロイメントマネージャー）にユーザーを追加します。 **AEM Assets DM OpenAPI Users – 配信** プロファイル（またはフォールバックとして **作成者** プロファイル）は、アセットセレクターおよび自動入力機能のその他の要件です。
* [&#x200B; チームメンバーをAEM配信レイヤーに割り当てる &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem#add-team-members){target=_blank}。 配信アクセスに関するAEM ドキュメント。
