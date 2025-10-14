---
title: Commerce データ取り込み用のプロファイルレコードスキーマの更新
description: スキーマ、データセット、データストリームを作成して、Commerce プロファイルレコードデータを収集し、Experience Platformに送信する方法を説明します。
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# Commerce データ取り込み用のプロファイルレコードスキーマの更新

買い物客がCommerce サイトでプロファイルを作成すると、プロファイルレコードが作成され、データが取り込まれます。 プロファイルデータをExperience Platformにストリーミングするには、そのプロファイルレコードに固有のスキーマとデータセットを作成する必要があります。

1. [&#x200B; 作成 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/ui/resources/schemas) スキーマを作成し、クラスを **個人プロファイル** に設定します。

1. [&#x200B; 追加 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/ui/resources/schemas) 次のプロファイル固有のフィールドグループ：

   - identityMap
   - 人口統計の詳細
   - 個人の連絡先の詳細
   - ユーザーアカウントの詳細

1. プロファイルのスキーマ [&#128279;](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/ui/resources/schemas) 有効 。

   スキーマがプロファイルで有効になっている場合、このスキーマから作成されたデータセットは、異なるソースのデータを結合して各顧客の全体像を構築するReal-Time CDPに関与します。

1. 作成または更新したスキーマに基づいて [&#128279;](https://experienceleague.adobe.com/ja/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform) データセットを作成  します。

   データセットは、データのコレクションのためのストレージおよび管理用の構成体で、通常は、スキーマ（列）とフィールド（行）を含むテーブルです。 データセットには、保存するデータの様々な側面を記述したメタデータも含まれます。

1. 次の値を持つ [&#x200B; カスタムネームスペース &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/features/namespaces#create-namespaces) をExperience Platformに作成します。

   - **表示名**: _Commerce顧客 ID_
   - **ID シンボル**: _CustomerId_
   - **タイプ**:_個々のクロスデバイス ID_

   ![&#x200B; カスタム名前空間の作成 &#x200B;](assets/custom-namespace.png){width="700" zoomable="yes"}

   「**[!UICONTROL Create]**」をクリックします。 カスタム名前空間は、プロファイルフラグメントをステッチして結合するために、統合プロファイルサービスで使用されます。

顧客プロファイルレコードデータ用に設定されたスキーマ、データセット、カスタムネームスペースを使用すると、Commerce インスタンスを [&#x200B; 設定 &#x200B;](connect-data.md#data-collection) し、そのデータを収集してExperience Platformに送信できます。

行動およびバックオフィスイベントデータのスキーマ、データセット、データストリームを作成するには、[Commerce データ取り込みの時系列イベントスキーマを更新 &#x200B;](update-xdm.md) を参照してください。
