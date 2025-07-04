---
title: ユーザー管理
description: ' [!DNL Adobe Commerce as a Cloud Service] でユーザーを管理する方法を説明します。'
exl-id: 9bc80fe6-6dfd-4bb3-8dc5-d5efd8a8d90c
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
role: Admin
source-git-commit: a06d64566fda76c0527aabfa9e8fdf27e7c149ca
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---

# ユーザー管理

ユーザーに [!DNL Adobe Commerce as a Cloud Service] の管理者へのアクセスを許可する場合は、ユーザーを組織内のユーザーとして追加し、[Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"} のCloud Service製品へのアクセス権を持っている必要があります。

このプロセスを実行するには、[!DNL Adobe Commerce as a Cloud Service] へのアクセス権を持つ IMS 組織が必要です。 これらのプロセスを実行できるのは、組織のシステム管理者または製品管理者のみです。

>[!TIP]
>
>複数のユーザーを同時に追加するには、[CSV の一括アップロード ](https://helpx.adobe.com/jp/enterprise/using/bulk-upload-users.html){target="_blank"} を実行します。
> 
> [ ユーザーグループ ](https://helpx.adobe.com/jp/enterprise/using/user-groups.html){target="_blank"} を作成して、1 つの役割に複数のユーザーを追加することもできます。 次に、[!UICONTROL **Adobe Commerce as a Cloud Service - バックエンド**] 製品をユーザーグループに追加できます。

## 役割について

[!DNL Adobe Commerce as a Cloud Service] では、次の役割を使用できます。 これらのロールを表示または編集するには、Commerce管理者で **システム**/**権限**/**ユーザーロール** に移動します。

* **ユーザー** - ユーザーは、Commerce管理者に管理者アクセス権を持っていますが、Admin Consoleで製品レベルのアクセス権を管理することはできません。 ユーザーは、クレジットを使用して [!DNL Commerce Cloud Manager] で [ インスタンスを作成 ](./getting-started.md#create-an-instance) することもできます。

* [**開発者**](https://helpx.adobe.com/jp/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} 開発者はユーザー権限を持ち、開発者ユーザーとしてCommerce インスタンスに追加されます。 つまり、[ 管理 UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/){target="_blank"}、[ イベントの設定 ](https://developer.adobe.com/commerce/extensibility/events/){target="_blank"}、[Webhook の作成 ](https://developer.adobe.com/commerce/extensibility/webhooks/){target="_blank"} を使用できます。

* 管理者 – 管理者には次の 3 つのタイプがあります。
   * [ システム管理者 ](https://helpx.adobe.com/jp/enterprise/using/admin-roles.html){target="_blank"} - システム管理者は、Admin Consoleを通じて組織内のすべての製品と製品プロファイルにアクセスできます。
   * [ 製品管理者 ](#add-a-product-admin) – 製品管理者は [ 製品のユーザー、役割、権限を管理 ](#add-users-and-admins) [!DNL Adobe Admin Console] で、[Commerce管理者でユーザーを管理 ](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/user-accounts/permissions-users-all#create-a-user){target="_blank"} できます。
   * [ 製品プロファイル管理者 ](#add-users-developers-and-product-profile-admins) – 製品プロファイル管理者は、Adobe Commerce管理者へのアクセス権を持っていませんが、[!DNL Adobe Admin Console] 内の製品のユーザーを管理できます。

Adobe Commerce内の各ロールに付与される権限について詳しくは、[ ユーザー権限 ](#user-permissions) を参照してください。

## 製品管理者を追加

1. https://adminconsole.adobe.comに移動し、Adobe IDでログインします。

1. 組織を選択します。

1. [!UICONTROL **製品**] タブの [!UICONTROL **製品とサービス**] で、[!UICONTROL **Adobe Commerce as a Cloud Service - バックエンド**] を選択します。

   ![ 製品を選択 ](./assets/backend.png){width="600" zoomable="yes"}

1. 「[!UICONTROL **管理者**]」タブを選択します。

1. [!UICONTROL **管理者を追加**] をクリックします。

1. 管理者として追加するユーザーのユーザー名またはメールアドレスを入力し、「[!UICONTROL **保存**]」をクリックします。

## ユーザー、開発者および製品プロファイル管理者の追加

以下の手順では、[!DNL Commerce Cloud Manager] とCommerce管理者にユーザーと開発者を追加する方法について説明します。 [!DNL Commerce Cloud Manager] インターフェイスを使用すると、Commerce インスタンスを作成および管理できます。

>[!NOTE]
>
>製品管理者とシステム管理者のみが、ユーザーと開発者をAdobe Commerce as a Cloud Service製品に追加できます。

1. https://adminconsole.adobe.comに移動し、Adobe IDでログインします。

1. 組織を選択します。

1. [!UICONTROL **製品**] タブの [!UICONTROL **製品とサービス**] で、[!UICONTROL **Adobe Commerce as a Cloud Service - バックエンド**] を選択します。

   ![ 製品を選択 ](./assets/backend.png){width="600" zoomable="yes"}

1. [!UICONTROL **デフォルト - Cloud Manager**] 製品プロファイルをクリックします。

1. [!UICONTROL **ユーザー**]、[!UICONTROL **開発者**] または [!UICONTROL **管理者**] タブを選択して、「[!UICONTROL **ユーザーを追加**]」または「[!UICONTROL **開発者を追加**]」または「[!UICONTROL **管理者を追加**]」をクリックします。

   >[!NOTE]
   >
   >この画面から追加された管理者は [ 製品プロファイル管理者 ](#understanding-roles) であり、Commerce管理者へのアクセス権がありません。

   ![ タブ選択 ](./assets/tab-select.png){width=600 zoomable="yes"}

1. 管理者として追加するユーザーのユーザー名またはメールアドレスを入力し、「[!UICONTROL **保存**]」をクリックします。

## 役割リソース

次のリストは、デフォルトロールがAdobe Commerce管理内でアクセスする権限を持つリソースを示しています。 各役割のデフォルトの権限を変更するには、Commerce管理で **システム**/**権限**/**ユーザーの役割** に移動します。

**ユーザー**

* カタログ
   * 在庫
      * 製品
         * 製品価格の読み取り

**開発者**

* カタログ
   * 在庫
      * 製品
         * 製品価格の読み取り
* システム
   * データ転送
      * 履歴の読み込み
* Adobe IO イベントの設定
   * 設定チェック
   * イベント プロバイダーの作成
   * 設定の更新
   * イベントの同期
   * イベント プロバイダーリストの取得
* イベント フレームワーク
   * イベントリスト
   * 送信接続のテスト
   * イベントの購読
   * イベントの登録解除
   * イベントステータス
   * イベント購読を取得するための API
   * イベント購読管理 UI の表示
   * イベント購読管理 UI の作成
   * 新しいイベント管理 UI をリクエスト
* Webhook
   * Webhook デジタル署名
      * Webhook デジタル署名設定
      * Webhook デジタル署名によるキーの生成
   * Webhook 管理
      * Webhook グリッド
      * Webhook 編集
      * Webhook のテスト
      * Webhook の API 購読
      * Webhook からの API 購読解除
      * Webhook リスト
      * 新しい Webhook をリクエスト
      * Webhook ログ
      * Webhook のリストを取得

**管理者**

管理者は、すべての権限にアクセスできます。
