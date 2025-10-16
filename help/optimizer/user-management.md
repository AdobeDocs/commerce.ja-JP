---
title: ユーザー管理
description: ユーザーを作成および管理し、 [!DNL Adobe Commerce Optimizer] のユーザーの役割を割り当てる方法について説明します。
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
exl-id: 9ab2118d-b7e3-4e2e-adac-8f3950fe1824
source-git-commit: 36a953d4fb0e1e14c7cb88a80f3b59d6fe8eb49e
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# ユーザー管理

[!DNL Adobe Commerce Optimizer] へのアクセスを有効にするには、[Adobe Admin Consoleからユーザーを追加し &#x200B;](https://adminconsole.adobe.com){target="_blank"}Commerce製品にアクセスできることを確認します。

ユーザーは、次のいずれかの役割に割り当てることができます。

- **ユーザー** - ユーザーは [!DNL Adobe Commerce Optimizer] UI にアクセスして、カタログ表示とマーチャンダイジングルールを表示および管理し、パフォーマンス指標を追跡できます。

- [**開発者**](https://helpx.adobe.com/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} – 開発者は、ユーザー権限とAdobe Developer Consoleへのアクセス権を持っています。 つまり、[!DNL Adobe Commerce Optimizer] API や SDK などの開発ツールを、App Builderや API メッシュなどのAdobe拡張ツールと共に使用するために、プロジェクトを作成し、資格情報を設定できます。

- **管理者** – 管理者ロールには次の 3 つのタイプがあります。
   - [&#x200B; システム管理者 &#x200B;](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"} - システム管理者は、Adobe Admin Consoleを通じて組織内のすべての製品と製品プロファイルにアクセスできます。
   - [&#x200B; 製品管理者 &#x200B;](#add-a-product-admin) – 製品管理者は [&#x200B; 製品のユーザー、役割、権限を管理 &#x200B;](#add-users-and-admins) できます。[!DNL Adobe Admin Console]
   - [&#x200B; 製品プロファイル管理者 &#x200B;](#add-users-developers-and-product-profile-admins) – 製品プロファイル管理者は、[!DNL Adobe Admin Console] 内の製品のユーザーを管理できます。

## 製品管理者を追加

>[!BEGINTABS]

>[!NOTE]
>
>製品管理者を製品管理者として追加する前に、製品管理者に [&#x200B; ユーザーの役割 &#x200B;](#add-users) を割り当てます。 ユーザーの役割は、Commerceの基本的な権限に必要です。

>[!TAB GA （2025 年 10 月 13 日（PT）以降にプロビジョニング） ]

1. <https://adminconsole.adobe.com> に移動し、Adobe IDを使用してログインします。

1. 組織を選択します。

1. 「[!UICONTROL **ユーザー**]」タブを選択します。

1. 「[!UICONTROL **管理者**] タブを選択します。

1. [!UICONTROL **管理者を追加**] をクリックします。

1. 管理者として追加するユーザーのユーザー名またはメールアドレスを入力し、「[!UICONTROL **次へ**]」をクリックします。

1. [!UICONTROL **製品プロファイル管理者**] の役割を選択します。

1. 「**+**」をクリックして製品を追加します。

1. 管理者を追加する既存のCommerce Optimizer インスタンスを選択します。 Commerce Optimizer インスタンスでは、`Adobe Commerce - <instance-name> - ACO - <environment-type> - <tenant-id>` のフォーマットを使用します。

1. 製品プロファイルを選択します。

1. [!UICONTROL **適用**] をクリックします。

1. [!UICONTROL **保存**] をクリックします。

>[!TAB  早期アクセス（2025 年 10 月 13 日（PT）以前にプロビジョニング） ]

1. <https://adminconsole.adobe.com> に移動し、Adobe IDを使用してログインします。

1. 組織を選択します。

1. 「[!UICONTROL **製品**]」タブの [!UICONTROL **製品とサービス**] で、[!UICONTROL **Adobe Commerce - Commerce Cloud Manager**] を選択します。

   ![&#x200B; 製品を選択 &#x200B;](/help/cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. 「[!UICONTROL **管理者**]」タブを選択します。

1. [!UICONTROL **管理者を追加**] をクリックします。

1. 管理者として追加するユーザーのユーザー名またはメールアドレスを入力し、「[!UICONTROL **保存**]」をクリックします。

>[!ENDTABS]

## ユーザーを追加

以下の手順では、[!DNL Commerce Cloud Manager] とCommerce Optimizerにユーザーを追加する方法について説明します。 [!DNL Commerce Cloud Manager] インターフェイスを使用すると、Commerce Optimizer インスタンスを作成および管理できます。 このプロセスは、開発者と管理者を含むすべてのユーザーに必要です。

>[!NOTE]
>
>製品管理者とシステム管理者のみが、ユーザーと開発者をAdobe Commerce Optimizer製品に追加できます。

>[!BEGINTABS]

>[!TAB GA （2025 年 10 月 13 日（PT）以降にプロビジョニング） ]

1. <https://adminconsole.adobe.com> に移動し、Adobe IDを使用してログインします。

1. 組織を選択します。

1. 「[!UICONTROL **製品**]」タブを選択します。

1. [!UICONTROL **Adobe Commerce**] 商品を選択します。

1. Commerce Cloud インスタンスを作成および管理できる Cloud Manager インターフェイスにユーザーを追加する場合は、Commerce Optimizer Manager 製品を選択します。または、ユーザーを追加する既存のCommerce Optimizer インスタンスを選択します。 Commerce Optimizer インスタンスでは、`Adobe Commerce - <instance-name> - ACO - <environment-type> - <tenant-id>` のフォーマットを使用します。

1. 「[!UICONTROL **ユーザー**]」タブを選択し、「[!UICONTROL **ユーザーを追加**]」をクリックします。

1. 追加するユーザーのユーザー名またはメールアドレスを入力し、「[!UICONTROL **保存**]」をクリックします。

1. 目的の製品プロファイルを選択します。

1. [!UICONTROL **適用**] をクリックします。

1. [!UICONTROL **保存**] をクリックします。

>[!TAB  早期アクセス（2025 年 10 月 13 日（PT）以前にプロビジョニング） ]

1. <https://adminconsole.adobe.com> に移動し、Adobe IDを使用してログインします。

1. 組織を選択します。

1. 「[!UICONTROL **製品**]」タブの [!UICONTROL **製品とサービス**] で、[!UICONTROL **Adobe Commerce - Commerce Cloud Manager**] を選択します。

   ![&#x200B; 製品を選択 &#x200B;](/help/cloud-service//assets/backend.png){width="600" zoomable="yes"}

1. [!UICONTROL **デフォルト - Cloud Manager**] 製品プロファイルをクリックします。

1. 「[!UICONTROL **ユーザー**]」タブを選択し、「[!UICONTROL **ユーザーを追加**]」をクリックします。

   ![&#x200B; タブ選択 &#x200B;](/help/cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

1. 追加するユーザーのユーザー名またはメールアドレスを入力し、「[!UICONTROL **保存**]」をクリックします。

>[!ENDTABS]

### 開発者と製品プロファイル管理者の追加

開発者と製品プロファイル管理者を追加するには、[&#x200B; ユーザーを追加 &#x200B;](#add-users) プロセスを繰り返しますが、「[!UICONTROL **ユーザー**] タブではなく [!UICONTROL **開発者**] または [!UICONTROL **管理者**] タブを選択します。

>[!NOTE]
>
>開発者を開発者として追加する前に、開発者にユーザーの役割を割り当てます。 ユーザーの役割は、Commerceの基本的な権限に必要です。

![&#x200B; タブ選択 &#x200B;](/help//cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

## 一括ユーザー管理

次のいずれかの方法を使用して、複数のユーザーをより効率的に追加できます。

- Adobe Admin Consoleの **CSV によるユーザーの追加** 機能を使用して、[CSV の一括アップロード &#x200B;](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"} を実行します。
- [&#x200B; ユーザーグループ &#x200B;](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"} を作成して、1 つの役割に複数のユーザーを追加します。 次に、[!UICONTROL **Adobe Commerce - Commerce Cloud Manager**] をユーザーグループに追加します。

