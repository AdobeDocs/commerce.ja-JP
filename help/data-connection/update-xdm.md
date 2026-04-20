---
title: Commerce Data Ingestionの時系列イベントスキーマの更新
description: Commerce データ取り込み用に時系列イベントデータを収集して送信するスキーマ、データセットおよびデータストリームを作成する方法について説明します。
role: Admin, Developer
feature: Personalization, Integration
exl-id: c933a1bc-3d6f-4f80-944f-8c3e212aaeb6
source-git-commit: 14c4178338859d55a7391139033d51d1aa6f7678
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 0%

---

# Commerce Data Ingestionの時系列イベントスキーマの更新

[拡張機能を使用するための](overview.md#onboarding-steps) オンボーディング手順[!DNL Data Connection]の1つは、データストリームワークスペースにアクセスし、[Adobe Commerce固有のデータストリーム &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=ja)を作成することです。 そのデータストリームを作成する場合は、取り込むデータを説明するスキーマも選択する必要があります。 このスキーマには、コマース固有のフィールドグループを含める必要があります。

この記事では、Adobe Commerce イベントによって提供される次の時系列データを正常に収集するために、スキーマに含める必要があるフィールドグループについて説明します。

- [行動](events.md) - ストアフロント、プロファイル、検索、B2B イベントが含まれます。
- [&#x200B; バックオフィス &#x200B;](events-backoffice.md) – 注文状況とプロファイルイベントが含まれます。

[時系列データ &#x200B;](data-ingestion.md)について詳しく見る。

スキーマ構成[の](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=ja)基本事項について詳しく説明します。

## 時系列行動データとバックオフィスイベントデータでスキーマを更新する

この節では、既存のスキーマを更新する方法や、行動データとバックオフィスのイベントデータを含めるスキーマを作成する方法について説明します。

>[!NOTE]
>
>プロファイル固有のフィールドを追加する方法については、[時系列プロファイルイベントデータ &#x200B;](#time-series-profile-event-data)を参照してください。

1. まだスキーマがない場合は、クラスが[Experience Event](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=ja#create)に設定された&#x200B;**create**&#x200B;を作成します。

1. [次のCommerce固有のフィールドグループを](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=ja#add-field-groups)追加します（または、既存のスキーマを編集してこれらのフィールドグループを追加します）。

   - サイト検索
   - Web ページを見る
   - ユーザーログインプロセス
   - リファレンスキー
   - 個人の連絡先詳細
   - チャネル詳細
   - Commerceの詳細
   - Adobe Analytics ExperienceEvent Commerce（Adobe Analyticsにデータを送信する場合）

   >[!NOTE]
   >
   > Commerce固有のフィールドグループを`Primary identity`として設定しないでください。 これにより、フィールドが必要に応じて識別され、Experience Platformはすべてのイベントでそのフィールドを想定します。 このフィールドが存在しない場合、データの取り込みは失敗します。

   スキーマにCommerce固有のフィールドグループが含まれるようになり、Commerce [行動](events.md)および[&#x200B; バックオフィス &#x200B;](events-backoffice.md) イベントから収集された時系列データがスキーマで表されるようになりました。

1. [&#x200B; プロファイルのスキーマを有効にする](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=ja#profile)。

   プロファイルに対してスキーマが有効になっている場合、このスキーマから作成されたすべてのデータセットがReal-Time CDPに組み込まれ、様々なソースからデータが結合され、各顧客の全体像が構築されます。

1. [作成または更新したスキーマに基づいてデータセット &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=ja#create-a-dataset)を作成します。

   データセットは、データのコレクションを格納および管理するための構成図です。通常、スキーマ（列）とフィールド（行）を含むテーブルです。 データセットには、保存するデータのさまざまな側面を説明するメタデータも含まれます。

1. [&#x200B; データストリーム &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=ja)を作成し、Commerce固有のフィールドグループと対応するデータセットを含むスキーマを選択します。

   データストリームは、収集したデータをデータセットに転送します。 選択したスキーマに基づいて、データセットにデータが表示されます。

行動データとバックオフィスデータ用に設定されたスキーマ、データセット、データストリームを使用すると、Commerce インスタンスを[configure](connect-data.md#data-collection)して、そのデータを収集し、Experience Platformに送信できます。

買い物客のプロファイル情報を含めるには、[時系列プロファイルイベントデータ &#x200B;](#time-series-profile-event-data)を参照してください。

## 時系列プロファイルイベントデータ

時系列プロファイルイベントデータは、次のイベントから生成されます。

- [&#39;accountCreated&#39;](events-backoffice.md#accountcreated)
- [&#39;accountUpdated&#39;](events-backoffice.md#accountupdated)
- [&#39;accountDeleted&#39;](events-backoffice.md#accountdeleted)

お客様のプロファイルイベントデータをExperience Platformに取り込む場合は、既存のCommerce スキーマを更新して、既に設定されているのと同じデータストリームを使用するか、プロファイル固有のデータストリームとスキーマを作成できます。 それは、自社のデータガバナンスにもとづいて決定されます。 次の2つのセクションでは、どちらのケースでも順を追って説明します。

### 既存のデータストリームを使用して、時系列プロファイルイベントデータをExperience Platformに送信します

時系列[&#x200B; サーバーサイドのプロファイルイベントデータ &#x200B;](events-backoffice.md#customer-profile-events)を既存のCommerce データストリームに追加する場合は、`Demographic Details` フィールドグループをスキーマに追加します。 スキーマに、次のCommerce固有のフィールドグループが含まれるようになりました。

- サイト検索
- Web ページを見る
- ユーザーログインプロセス
- リファレンスキー
- 個人の連絡先詳細
- チャネル詳細
- Commerceの詳細
- Adobe Analytics ExperienceEvent Commerce（Adobe Analyticsにデータを送信する場合）
- 新規：**デモグラフィックの詳細**

既存のCommerce スキーマに`Demographic Details` フィールドグループを追加すると、Commerce スキーマに既に関連付けられているデータセットとデータストリームがこの時系列プロファイルデータに使用されます。

### 時系列プロファイルイベントデータを別のデータストリームでExperience Platformに送信する

[&#x200B; サーバーサイドのプロファイルイベントデータ &#x200B;](events-backoffice.md#customer-profile-events)を新しいプロファイル固有のデータストリームとスキーマに追加する場合は、次の手順を実行します。

1. [&#x200B; スキーマを作成](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=ja#create)し、クラスを&#x200B;**エクスペリエンスイベント**&#x200B;に設定します。

1. [次のプロファイル固有のフィールドグループを](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=ja#add-field-groups)追加します。

   - デモグラフィック情報
   - 個人の連絡先詳細
   - チャネル詳細
   - Commerceの詳細

1. [&#x200B; プロファイルのスキーマを有効にする](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=ja#profile)。

   プロファイルに対してスキーマが有効になっている場合、このスキーマから作成されたすべてのデータセットがReal-Time CDPに組み込まれ、様々なソースからデータが結合され、各顧客の全体像が構築されます。

1. [作成したスキーマに基づいてデータセット &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=ja#create-a-dataset)を作成します。

   データセットは、データのコレクションを格納および管理するための構成図です。通常、スキーマ（列）とフィールド（行）を含むテーブルです。 データセットには、保存するデータのさまざまな側面を説明するメタデータも含まれます。

1. [&#x200B; データストリーム &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=ja)を作成し、Commerce固有のフィールドグループと対応するデータセットを含むXDM スキーマを選択します。

   データストリームは、収集したデータをデータセットに転送します。 選択したスキーマに基づいて、データセットにデータが表示されます。

顧客プロファイルデータ用に設定されたスキーマ、データセット、データストリームを使用して、Commerce インスタンスを[設定](connect-data.md#data-collection)し、そのデータを収集してExperience Platformに送信できます。

プロファイルレコードデータのスキーマ、データセットおよびデータストリームを作成するには、[&#x200B; プロファイルレコードデータをExperience Platform](profile-data.md)に送信するを参照してください。
