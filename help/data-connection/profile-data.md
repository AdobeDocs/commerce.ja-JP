---
title: Commerce Data Ingestionのプロファイルレコードスキーマの更新
description: スキーマ、データセット、データストリームを作成して、Commerce プロファイルレコードデータを収集し、Experience Platformに送信する方法を説明します。
role: Admin, Developer
feature: Personalization, Integration
exl-id: 25741837-f423-4204-8520-80b7cd9d44bd
TQID: https://experienceleague.adobe.com/I8bptw1tNdzXfCC6hFtn7fuz-BIiALXG4g6lLhga6ec
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 340
ht-degree: 0%

---

# Commerce Data Ingestionのプロファイルレコードスキーマの更新

顧客がCommerceサイトでプロファイルを作成すると、プロファイルレコードが作成され、データが取得されます。 そのプロファイルデータをExperience Platformにストリーミングする前に、そのプロファイルレコードに固有のスキーマとデータセットを作成する必要があります。

1. [&#x200B; スキーマを作成](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/resources/schemas)し、クラスを&#x200B;**個人プロファイル**&#x200B;に設定します。

1. [次のプロファイル固有のフィールドグループを](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/resources/schemas)追加します。

   - identityMap
   - デモグラフィック情報
   - 個人の連絡先詳細
   - ユーザーアカウントの詳細

1. [&#x200B; プロファイルのスキーマを有効にする](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/resources/schemas)。

   プロファイルに対してスキーマが有効になっている場合、このスキーマから作成されたすべてのデータセットがReal-Time CDPに組み込まれ、様々なソースからデータが結合され、各顧客の全体像が構築されます。

1. [作成または更新したスキーマに基づいてデータセット &#x200B;](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform)を作成します。

   データセットは、データのコレクションを格納および管理するための構成図です。通常、スキーマ（列）とフィールド（行）を含むテーブルです。 データセットには、保存するデータのさまざまな側面を説明するメタデータも含まれます。

1. 次の値を持つ[&#x200B; カスタム名前空間](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/namespaces#create-namespaces)をExperience Platformに作成します。

   - **表示名**: _Commerce Customer ID_
   - **ID シンボル**: _顧客ID_
   - **種類**: _個々のクロスデバイス ID_

   ![&#x200B; カスタム名前空間を作成](assets/custom-namespace.png){width="700" zoomable="yes"}

   **[!UICONTROL Create]**&#x200B;をクリックします。 カスタム名前空間は、統合プロファイルサービスでプロファイルフラグメントをつなぎ合わせるために使用されます。

顧客プロファイルレコードデータ用に設定されたスキーマ、データセット、カスタム名前空間を使用すると、Commerce インスタンスを[設定](connect-data.md#data-collection)して、そのデータを収集し、Experience Platformに送信できます。

行動およびバックオフィスのイベントデータのスキーマ、データセット、データストリームを作成するには、[Commerce データ取り込みの時系列イベントスキーマの更新](update-xdm.md)を参照してください。
