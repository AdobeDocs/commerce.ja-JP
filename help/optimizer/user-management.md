---
title: ユーザー管理
description: ' [!DNL Adobe Commerce Optimizer] でユーザーを管理する方法を説明します。'
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
source-git-commit: 02758aa5cc14af6d46bfc4bb7865fa37a787d4cb
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# ユーザー管理

[!DNL Adobe Commerce Optimizer] へのアクセスを有効にするには、[Adobe Admin Consoleからユーザーを追加し ](https://adminconsole.adobe.com){target="_blank"}Commerce製品にアクセスできることを確認します。

ユーザーは、次のいずれかの役割に割り当てることができます。

- **ユーザー** - ユーザーは [!DNL Adobe Commerce Optimizer] UI にアクセスして、カタログ表示とマーチャンダイジングルールを表示および管理し、パフォーマンス指標を追跡できます。

- [**開発者**](https://helpx.adobe.com/jp/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} – 開発者は、ユーザー権限とAdobe Developer Consoleへのアクセス権を持っています。 つまり、[!DNL Adobe Commerce Optimizer] API や SDK などの開発ツールを、App Builderや API メッシュなどのAdobe拡張ツールと共に使用するために、プロジェクトを作成し、資格情報を設定できます。

- **管理者** – 管理者ロールには次の 3 つのタイプがあります。
   - [ システム管理者 ](https://helpx.adobe.com/jp/enterprise/using/admin-roles.html){target="_blank"} - システム管理者は、Adobe Admin Consoleを通じて組織内のすべての製品と製品プロファイルにアクセスできます。
   - [ 製品管理者 ](#add-a-product-admin) – 製品管理者は [ 製品のユーザー、役割、権限を管理 ](#add-users-and-admins) できます。[!DNL Adobe Admin Console]
   - [ 製品プロファイル管理者 ](#add-users-developers-and-product-profile-admins) – 製品プロファイル管理者は、[!DNL Adobe Admin Console] 内の製品のユーザーを管理できます。

## 製品管理者を追加

1. [Admin Console](https://adminconsole.adobe.com) に移動し、Adobe IDを使用してログインします。

1. 組織を選択します。

1. [!UICONTROL **製品**] タブの [!UICONTROL **製品とサービス**] で、[!UICONTROL **Adobe Commerce as a Cloud Service - バックエンド**] を選択します。

   ![ 製品を選択 ](../cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. 「[!UICONTROL **管理者**]」タブを選択します。

1. [!UICONTROL **管理者を追加**] をクリックします。

1. 管理者として追加するユーザーのユーザー名またはメールアドレスを入力し、「[!UICONTROL **保存**]」をクリックします。

## ユーザー、開発者および製品プロファイル管理者の追加

>[!BEGINSHADEBOX  「前提条件」 ]
>
>ユーザー管理には、次のプロビジョニングが必要です。

- [!DNL Adobe Commerce Optimizer] 用にプロビジョニングされた IMS 組織
- システムまたは製品管理者のロールを持つ、同じ IMS 組織のAdobe Experience Cloud アカウント

>[!ENDSHADEBOX]

ユーザーと開発者を [!DNL Commerce Cloud Manager] に追加するには、次の手順を使用します。ここでは、Commerce インスタンスを管理します。

1. [Adobe Admin Console](https://adminconsole.adobe.com) に移動し、Adobe IDを使用してログインします。

1. 組織を選択します。

1. [!UICONTROL **製品**] タブの [!UICONTROL **製品とサービス**] で、[!UICONTROL **Adobe Commerce as a Cloud Service - バックエンド**] を選択します。

   ![ 製品を選択 ](../cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. [!UICONTROL **デフォルト - Cloud Manager**] 製品プロファイルをクリックします。

1. [!UICONTROL **ユーザー**]、[!UICONTROL **開発者**] または [!UICONTROL **管理者**] タブを選択して、「[!UICONTROL **ユーザーを追加**]」または「[!UICONTROL **開発者を追加**]」または「[!UICONTROL **管理者を追加**]」をクリックします。

   この画面から追加された管理者は、[ 製品プロファイル管理者 ](#understanding-roles) グループに割り当てられます。

   ![ タブ選択 ](../cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

1. 管理者として追加するユーザーのユーザー名またはメールアドレスを入力し、「[!UICONTROL **保存**]」をクリックします。

## 一括ユーザー管理

次のいずれかの方法を使用して、複数のユーザーをより効率的に追加できます。

- Adobe Admin Consoleの **CSV によるユーザーの追加** 機能を使用して、[CSV の一括アップロード ](https://helpx.adobe.com/jp/enterprise/using/bulk-upload-users.html){target="_blank"} を実行します。
- [ ユーザーグループ ](https://helpx.adobe.com/jp/enterprise/using/user-groups.html){target="_blank"} を作成して、1 つの役割に複数のユーザーを追加します。 次に、[!UICONTROL **Adobe Commerce as a Cloud Service - バックエンド**] をユーザーグループに追加します。

