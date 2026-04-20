---
title: ユーザーとIdentity Management
description: ' [!DNL Adobe Commerce Optimizer]のユーザーを作成および管理し、ユーザーの役割を割り当てる方法について説明します。'
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよび [!DNL Adobe Commerce Optimizer]  プロジェクトにのみ適用されます（Adobeで管理されるSaaS インフラストラクチャ）。"
exl-id: 9ab2118d-b7e3-4e2e-adac-8f3950fe1824
source-git-commit: 14c4178338859d55a7391139033d51d1aa6f7678
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 0%

---

# ユーザー管理

[!DNL Adobe Commerce Optimizer]へのアクセスを有効にするには、[Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"}からユーザーを追加し、ユーザーがCommerce製品にアクセスできることを確認します。

ユーザーは、次のいずれかの役割に割り当てることができます。

- **ユーザー**— ユーザーは[!DNL Adobe Commerce Optimizer] UIにアクセスして、カタログビューとマーチャンダイジングルールを表示および管理し、パフォーマンス指標を追跡できます。

- [**Developer**](https://helpx.adobe.com/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} – 開発者には、ユーザー権限とAdobe Developer Consoleへのアクセス権があります。 つまり、[!DNL Adobe Commerce Optimizer] APIやSDKなどの開発者ツールと、App BuilderやAPI MeshなどのAdobe拡張性ツールを使用して、プロジェクトを作成し、資格情報を設定することができます。

- **管理者** – 管理者ロールには3つの異なるタイプがあります。
   - [&#x200B; システム管理者](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"} - システム管理者は、Adobe Admin Consoleを通じて、組織内のすべての製品および製品プロファイルにアクセスできます。
   - [製品管理者](#add-a-product-admin) – 製品管理者は、[の](#add-users)製品のユーザー、役割、権限を[!DNL Adobe Admin Console]管理できます。
   - [製品プロファイル管理者](#add-developers-and-product-profile-admins) – 製品プロファイル管理者は[!DNL Adobe Admin Console]の製品のユーザーを管理できます。

## 製品管理者の追加

>[!BEGINTABS]

>[!NOTE]
>
>製品管理者として追加する前に、製品管理者に[&#x200B; ユーザーの役割](#add-users)を割り当てます。 Commerceの基本権限には、ユーザーロールが必要です。

組織がプロビジョニングされた時点に基づいて、製品管理者ユーザーを[!DNL Adobe Commerce Optimizer]に追加するには、2つの異なる方法があります。 早期アクセス組織では、製品管理者の役割を割り当てられた各ユーザーに、組織内のすべてのインスタンスを管理する権限が付与されます。 2025年10月13日以降にプロビジョニングされた一般提供（GA）組織では、特定のインスタンスの製品管理者としてユーザーを割り当てることができます。 製品管理者ユーザーがログインすると、管理する権限を持つインスタンスのみが表示されます。

>[!TAB GA （2025年10月13日（PT）以降にプロビジョニング） ]

1. <https://adminconsole.adobe.com>に移動し、Adobe IDでログインします。

1. 組織の選択。

1. 「[!UICONTROL **ユーザー**]」タブを選択します。

1. 「[!UICONTROL **管理者**]」タブを選択します。

1. 「[!UICONTROL **管理者を追加**]」をクリックします。

1. 管理者として追加するユーザーのユーザー名またはメールアドレスを入力し、[!UICONTROL **次へ**]&#x200B;をクリックします。

1. [!UICONTROL **製品プロファイル管理者**]&#x200B;の役割を選択します。

1. **+**&#x200B;をクリックして製品を追加します。

1. 管理者を追加する既存のCommerce Optimizer インスタンスを選択します。 Commerce Optimizer インスタンスでは、次のフォーマットが使用されます：`Adobe Commerce - <instance-name> - ACO - <environment-type> - <tenant-id>`。

1. 製品プロファイルを選択します。

1. 「[!UICONTROL **適用**]」をクリックします。

1. [!UICONTROL **保存**]&#x200B;をクリックします。

>[!TAB 早期アクセス （2025年10月13日より前にプロビジョニング） ]

1. <https://adminconsole.adobe.com>に移動し、Adobe IDでログインします。

1. 組織の選択。

1. [!UICONTROL **製品**] タブの&#x200B;[!UICONTROL **製品とサービス**]&#x200B;で、[!UICONTROL **Adobe Commerce - Commerce Cloud Manager**]&#x200B;製品を選択します。

   ![製品を選択](/help/cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. 「[!UICONTROL **管理者**]」タブを選択します。

1. 「[!UICONTROL **管理者を追加**]」をクリックします。

1. 管理者として追加するユーザーのユーザー名またはメールアドレスを入力し、[!UICONTROL **保存**]&#x200B;をクリックします。

>[!ENDTABS]

## ユーザーを追加

次の手順では、[!DNL Commerce Cloud Manager]とCommerce Optimizerにユーザーを追加する方法について説明します。 [!DNL Commerce Cloud Manager] インターフェイスでは、Commerce Optimizer インスタンスを作成および管理できます。 このプロセスは、開発者と管理者を含むすべてのユーザーに必要です。

>[!NOTE]
>
>[!DNL Adobe Commerce Optimizer]製品にユーザーと開発者を追加できるのは、製品管理者とシステム管理者のみです。

>[!BEGINTABS]

>[!TAB GA （2025年10月13日（PT）以降にプロビジョニング） ]

1. <https://adminconsole.adobe.com>に移動し、Adobe IDでログインします。

1. 組織の選択。

1. 「[!UICONTROL **製品**]」タブを選択します。

1. 「[!UICONTROL **Adobe Commerce**]」商品を選択します。

1. Commerce Cloud インスタンスを作成および管理できるcloud manager インターフェイスにユーザーを追加する場合は、Commerce Optimizer Manager製品を選択するか、ユーザーを追加する既存のCommerce Optimizer インスタンスを選択します。 Commerce Optimizer インスタンスでは、次のフォーマットが使用されます：`Adobe Commerce - <instance-name> - ACO - <environment-type> - <tenant-id>`。

1. 「[!UICONTROL **ユーザー**]」タブを選択し、「[!UICONTROL **ユーザーを追加**]」をクリックします。

1. 追加するユーザーのユーザー名またはメールアドレスを入力し、[!UICONTROL **保存**]&#x200B;をクリックします。

1. 必要な製品プロファイルを選択します。

1. 「[!UICONTROL **適用**]」をクリックします。

1. [!UICONTROL **保存**]&#x200B;をクリックします。

>[!TAB 早期アクセス （2025年10月13日より前にプロビジョニング） ]

1. <https://adminconsole.adobe.com>に移動し、Adobe IDでログインします。

1. 組織の選択。

1. [!UICONTROL **製品**] タブの&#x200B;[!UICONTROL **製品とサービス**]&#x200B;で、[!UICONTROL **Adobe Commerce - Commerce Cloud Manager**]&#x200B;製品を選択します。

   ![製品を選択](/help/cloud-service//assets/backend.png){width="600" zoomable="yes"}

1. 「[!UICONTROL **Default - Cloud Manager**] product profile」をクリックします。

1. 「[!UICONTROL **ユーザー**]」タブを選択し、「[!UICONTROL **ユーザーを追加**]」をクリックします。

   ![&#x200B; タブ選択](/help/cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

1. 追加するユーザーのユーザー名またはメールアドレスを入力し、[!UICONTROL **保存**]&#x200B;をクリックします。

>[!ENDTABS]

### 開発者と製品プロファイル管理者の追加

開発者と製品プロファイル管理者を追加するには、[&#x200B; ユーザーを追加](#add-users) プロセスを繰り返しますが、[!UICONTROL **ユーザー**] タブの代わりに&#x200B;[!UICONTROL **開発者**]&#x200B;または&#x200B;[!UICONTROL **管理者**] タブを選択します。

>[!NOTE]
>
>開発者として追加する前に、開発者にユーザーの役割を割り当てます。 Commerceの基本権限には、ユーザーロールが必要です。

![&#x200B; タブ選択](/help//cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

## バルクユーザー管理

次のいずれかの方法を使用すると、複数のユーザーをより効率的に追加できます。

- Adobe Admin Consoleの&#x200B;**Add Users by CSV**&#x200B;機能を使用して、[一括CSV アップロード &#x200B;](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}を実行します。
- [&#x200B; ユーザーグループ &#x200B;](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}を作成して、役割に複数のユーザーを追加します。 次に、適切な商品をユーザーグループに追加します。

## ID管理とシングルサインオン設定

{{ims-identity-and-sso-config}}
