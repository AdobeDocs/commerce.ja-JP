---
title: ストアの場所とマッピングシステムの設定
description: ストアフロント UI でのストアの場所のマッピングをサポートするように、距離プロバイダーを設定します。 店舗フルフィルメントソリューションでは、エンドツーエンドのフルフィルメントワークフローのために、小売店の検索やその他のマッピングおよびスケジュール機能を有効にするための距離プロバイダーが必要です。
role: Admin
level: Intermediate
feature: Shipping/Delivery, Integration, Tools and External Services, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# ストアの場所とマッピング設定

[ 距離プロバイダー ](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/distance-priority-algorithm) を設定して小売店の場所を検索することで、店舗配送の場所とマッピング機能を有効にします。

**要件**

設定プロセス中に、Google マッププラットフォームのGoogle API キーを指定します。 まだ存在しない場合は、[Google Maps プラットフォームから 1 つ生成します ](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/distance-priority-algorithm#configure-google-maps)。

距離プロバイダを設定するには：

1. 管理の **[!UICONTROL Stores > General]** 設定から、マップコンテンツタイプのGoogle マップ統合を追加します。

   - **[!UICONTROL Stores > Configuration  > General > Content Management]** に移動します。

   - Google API キーをフィールドに追加 **[!UICONTROL Google Maps API Key]** ます。

1. Admin の **[!UICONTROL Stores > Inventory]** 設定から、Store Fulfillment の距離プロバイダーを選択します。

   - **[!UICONTROL Stores > Configuration > Catalog > Inventory]** に移動します。

   - 「**[!UICONTROL Distance Provider for Distance Based SSA]**」セクションを展開します。

   - **Provider** を **Google Map** に設定します。

1. **[!UICONTROL Google Distance Provider]** の設定を指定します。

   - **Google API キー** を追加します。

   - **[!UICONTROL Computation Mode]** を `Driving` に、**[!UICONTROL Value]** を `Distance` に設定します
