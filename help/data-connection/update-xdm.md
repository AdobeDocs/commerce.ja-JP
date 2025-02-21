---
title: Commerceのデータ取り込みに対する時系列イベントスキーマの更新
description: スキーマ、データセット、データストリームを作成して、Commerceのデータ取り込み用に時系列イベントデータを収集して送信する方法を説明します。
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 0%

---

# Commerceのデータ取り込みに対する時系列イベントスキーマの更新

[!DNL Data Connection] 拡張機能を使用するための [ オンボーディング手順 ](overview.md#onboarding-steps) の 1 つは、データストリームワークスペースにアクセスし、Adobe Commerceに固有の [ データストリームを作成 ](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html) することです。 そのデータストリームを作成する際は、取り込む予定のデータを記述したスキーマも選択する必要があります。 このスキーマには、コマース固有のフィールドグループを含める必要があります。

この記事では、Adobe Commerce イベントで提供される次の時系列データを正常に収集するために、スキーマに含める必要があるフィールドグループについて説明します。

- [ 行動 ](events.md) - ストアフロント、プロファイル、検索、B2B イベントが含まれます。
- [ バックオフィス ](events-backoffice.md) – 注文ステータスとプロファイルイベントが含まれます。

詳しくは、[ 時系列データ ](data-ingestion.md) を参照してください。

詳しくは、[ スキーマ構成の基本 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html) を参照してください。

## 時系列の行動およびバックオフィスイベントデータを使用したスキーマの更新

この節では、既存のスキーマを更新する方法や、行動およびバックオフィスイベントデータを含むスキーマを作成する方法について説明します。

>[!NOTE]
>
>プロファイル固有のフィールドを追加する方法については、[ 時系列プロファイルイベントデータ ](#time-series-profile-event-data) を参照してください。

1. スキーマがまだない場合は、[Experience Event](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#create) に設定されたクラスを持つ **create** スキーマを使用します。

1. 次のCommerce固有のフィールドグループを [ 追加 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#add-field-groups) します（または、既存のスキーマを編集して、これらのフィールドグループを追加します）。

   - サイト検索
   - Web ページを訪問
   - ユーザーログインプロセス
   - 参照キー
   - 個人の連絡先の詳細
   - チャネルの詳細
   - Commerceの詳細
   - Adobe Analytics ExperienceEvent Commerce（Adobe Analyticsにデータを送信する場合）

   >[!NOTE]
   >
   > Commerce固有のフィールドグループを `Primary identity` のように設定しないでください。 これにより、フィールドが必須として特定され、Experience Platformは各イベントでそのフィールドを使用することを想定します。 このフィールドが存在しない場合、データ取り込みは失敗します。

   Commerce[ 行動 ](events.md) および [ バックオフィス ](events-backoffice.md) イベントから収集された時系列データがスキーマに表されるように、スキーマにCommerce固有のフィールドグループが含まれるようになりました。

1. プロファイルのスキーマ ](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#profile) 有効 [。

   スキーマがプロファイルで有効になっている場合、このスキーマから作成されたデータセットは、異なるソースのデータを結合して各顧客の全体像を構築するReal-Time CDPに関与します。

1. 作成または更新したスキーマに基づいて [ データセットを作成 ](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset) します。

   データセットは、データのコレクションのためのストレージおよび管理用の構成体で、通常は、スキーマ（列）とフィールド（行）を含むテーブルです。 データセットには、保存するデータの様々な側面を記述したメタデータも含まれます。

1. [ データストリームを作成 ](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html) し、Commerce固有のフィールドグループと対応するデータセットを含むスキーマを選択します。

   データストリームは、収集したデータをデータセットに転送します。 データは、選択したスキーマに基づいてデータセット内で表されます。

行動データやバックオフィスデータ用に設定されたスキーマ、データセット、データストリームを使用すると、データを収集してExperience Platformに送信するようにCommerce インスタンスを [ 設定 ](connect-data.md#data-collection) できます。

買い物客のプロファイル情報を含めるには、[ 時系列プロファイルイベントデータ ](#time-series-profile-event-data) を参照してください。

## 時系列プロファイルイベントデータ

時系列プロファイルイベントデータは、次のイベントから生成されます。

- [&#39;accountCreated&#39;](events-backoffice.md#accountcreated)
- [&#39;accountUpdated&#39;](events-backoffice.md#accountupdated)
- [&#39;accountDeleted&#39;](events-backoffice.md#accountdeleted)

顧客のプロファイルイベントデータをExperience Platformに取り込む場合は、既存のCommerce スキーマを更新し、設定済みの同じデータストリームを使用するか、プロファイル固有のデータストリームとスキーマを作成できます。 この決定は、会社のデータガバナンスに基づいています。 次の 2 つの節では、どちらの場合についても説明します。

### 既存のデータストリームを使用して、時系列プロファイルイベントデータをExperience Platformに送信する

時系列 [ サーバーサイドのプロファイルイベントデータ ](events-backoffice.md#customer-profile-events-server-side) を既存のCommerce データストリームに追加する場合は、スキーマに `Demographic Details` フィールドグループを追加します。 スキーマには、次のCommerce固有のフィールドグループが含まれるようになりました。

- サイト検索
- Web ページを訪問
- ユーザーログインプロセス
- 参照キー
- 個人の連絡先の詳細
- チャネルの詳細
- Commerceの詳細
- Adobe Analytics ExperienceEvent Commerce（Adobe Analyticsにデータを送信する場合）
- 新規：**人口統計の詳細**

既存のCommerce スキーマに `Demographic Details` フィールドグループを追加すると、この時系列プロファイルデータには、Commerce スキーマに既に関連付けられているデータセットとデータストリームが使用されます。

### 時系列プロファイルイベントデータを別のデータストリームでExperience Platformに送信する

[ サーバーサイドのプロファイルイベントデータ ](events-backoffice.md#customer-profile-events-server-side) を新しいプロファイル固有のデータストリームおよびスキーマに追加する場合は、次の手順を実行します。

1. [ 作成 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#create) スキーマを作成し、クラスを **エクスペリエンスイベント** に設定します。

1. [ 追加 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#add-field-groups) 次のプロファイル固有のフィールドグループ：

   - 人口統計の詳細
   - 個人の連絡先の詳細
   - チャネルの詳細
   - Commerceの詳細

1. プロファイルのスキーマ ](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#profile) 有効 [。

   スキーマがプロファイルで有効になっている場合、このスキーマから作成されたデータセットは、異なるソースのデータを結合して各顧客の全体像を構築するReal-Time CDPに関与します。

1. 作成したスキーマに基づいて [ データセットを作成 ](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset) します。

   データセットは、データのコレクションのためのストレージおよび管理用の構成体で、通常は、スキーマ（列）とフィールド（行）を含むテーブルです。 データセットには、保存するデータの様々な側面を記述したメタデータも含まれます。

1. [ データストリームを作成 ](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html) し、Commerce固有のフィールドグループと対応するデータセットを含む XDM スキーマを選択します。

   データストリームは、収集したデータをデータセットに転送します。 データは、選択したスキーマに基づいてデータセット内で表されます。

顧客プロファイルデータ用に設定されたスキーマ、データセット、データストリームを使用すると、データを収集してExperience Platformに送信するようにCommerce インスタンスを [ 設定 ](connect-data.md#data-collection) できます。

プロファイルレコードデータのスキーマ、データセット、データストリームを作成するには [Experience Platformへのプロファイルレコードデータの送信 ](profile-data.md) を参照してください。
