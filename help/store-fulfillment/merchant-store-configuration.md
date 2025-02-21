---
title: マーチャントストアの設定
description: 拡張されたInventory management ソースをマーチャントストアとして設定します。
role: Admin
level: Experienced
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 0%

---

# マーチャントストア（Source）の設定

このソリューションは、マーチャント向けの操作指向の機能を備えたストックソースを拡張することで、Inventory managementのネイティブ機能を強化します。

- 店舗位置の地理的座標の追加
- ソースを [!DNL Store Pickup Location] として指定し、使用可能な出荷機能（出荷先店舗、出荷元店舗）を指定します。
- 集荷の詳細と指示をお客様に伝えるために、利用可能な集荷オプション （店舗またはカーブサイド）、カスタマイズされた集荷指示、およびその他の情報を指定します

_ソース_ と _マーチャントストアの場所_ という用語は同じ意味で使用されます。 すべてのレコードは在庫ソースですが、設定に応じて、ソースはマーチャントストアの場所にすることもできます。

管理者：**[!UICONTROL Stores > Inventory > Sources >  Edit Source]** からマーチャントストアの設定を管理します。

>[!NOTE]
>
>設定プロセス中は、ソースを作成または既存のソースを更新した後に、キャッシュをフラッシュする必要が生じる場合があります。

## **一般**

<table>
<tbody>
<tr>
<th>フィールド</th>
<th>説明</th>
<th>対象範囲</th>
<th>必須</th>
</tr>
<tr>
<td><strong>[!UICONTROL Latitude]</strong></br><code>Base Attribute: latitude</code></td>
<td>商店の場所の緯度の座標です。 この必須情報は、ストアフロントエクスペリエンスでの場所の検索とマップの配置で使用されます。 検証に合格するには、値がストアの正確なアドレスと一致する必要があります。</td>
<td>グローバル</td>
<td>はい</td>
</tr>
<tr>
<td><strong>[!UICONTROL Longitude]</strong></br><code>Base Attribute: Longitude</code></td>
<td>商店の場所の縦方向の座標。 この必須情報は、ストアフロントエクスペリエンスでの場所の検索とマップの配置で使用されます。 検証に合格するには、値がストアの正確なアドレスと一致する必要があります。</td>
<td>グローバル</td>
<td>はい</td>
</tr>
<tr>
<td><strong>[!UICONTROL Use as Pickup Location]</br></strong><code>Base Attribute: is_pickup_location_active</code></td>
<td>ソースを使用可能な店舗の集荷場所として指定します。 この設定は、ソースを同期して訪問者に表示するかどうかを決定します。</td>
<td>グローバル</td>
<td>不可</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship to Store]</strong><br><code>Extension Attribute: allow_ship_to_store</code></td>
<td>ソースレベルで出荷先機能を設定します。 詳しくは、[General Configuration] （enable-general.md）オプションを参照してください。<strong>[!UICONTROL Enable Ship To Store]
</tr>
<tr>
<td><strong>[!UICONTROL Latitude]</strong></br><code>Base Attribute: latitude</code></td>
<td>商店の場所の緯度の座標です。 この必須情報は、ストアフロントエクスペリエンスでの場所の検索とマップの配置で使用されます。 検証に合格するには、値がストアの正確なアドレスと一致する必要があります。</td>
<td>グローバル</td>
<td>はい</td>
</tr>
<tr>
<td><strong>[!UICONTROL Longitude]</strong></br><code>Base Attribute: Longitude</code></td>
<td>商店の場所の縦方向の座標。 この必須情報は、ストアフロントエクスペリエンスでの場所の検索とマップの配置で使用されます。 検証に合格するには、値がストアの正確なアドレスと一致する必要があります。</td>
<td>グローバル</td>
<td>はい</td>
</tr>
<tr>
<td><strong>[!UICONTROL Use as Pickup Location]</br></strong><code>Base Attribute: is_pickup_location_active</code></td>
<td>ソースを使用可能な店舗の集荷場所として指定します。 この設定は、ソースを同期して訪問者に表示するかどうかを決定します。</td>
<td>グローバル</td>
<td>不可</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship to Store]</strong></br> <code>Extension Attribute: [!DNL allow_ship_to_store]</code></td>
<td>ソースレベルで出荷先機能を設定します。 詳しくは、[General Configuration] （enable-general.md）オプション <strong>[!UICONTROL Enable Ship To Store]</strong> を参照してください。</td>
<td>グローバル</td>
<td>不可</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship From Store]</strong></br><code>Extension Attribute: [!DNL use_as_shipping_source]</code></td>
 <td>ソースレベルで店舗からの出荷機能を設定します。 詳しくは、[General Configuration] （enable-general.md）オプション [!UICONTROL Enable Ship From Store] を参照してください。</td>
<td>グローバル</td>
<td>不可</td>
</tr>
<tr>
<td>グローバル</td>
<td>不可</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship From Store]</strong><code></br><code>Extension Attribute: [!DNL use_as_shipping_source]</code></td>
<td>ソースレベルで店舗からの出荷機能を設定します。 詳しくは、[General Configuration] （enable-general.md）オプション [!UICONTROL Enable Ship From Store] を参照してください。</td>
<td>グローバル</td>
<td>不可</td>
</tr>
</tbody>
</table>



| **フィールド** | **説明** | **範囲** | **必須** |
|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Latitude]**</br>`Base Attribute: latitude` | 商店の場所の緯度の座標です。 この必須情報は、ストアフロントエクスペリエンスでの場所の検索とマップの配置で使用されます。 検証に合格するには、値がストアの正確なアドレスと一致する必要があります。 | グローバル | はい |
| **[!UICONTROL Longitude]**</br>`Base Attribute: Longitude` | 商店の場所の縦方向の座標。 この必須情報は、ストアフロントエクスペリエンスでの場所の検索とマップの配置で使用されます。 検証に合格するには、値がストアの正確なアドレスと一致する必要があります。 | グローバル | はい |
| **[!UICONTROL Use as Pickup Location]**</br>`Base Attribute:[!DNL is_pickup_location_active]` | ソースを使用可能な店舗の集荷場所として指定します。 この設定は、ソースを同期して訪問者に表示するかどうかを決定します。 | グローバル | 不可 |
| **[!UICONTROL Enable Ship to Store]**</br>`Extension Attribute: [!DNL allow_ship_to_store]` | ソースレベルで出荷先機能を設定します。 詳しくは、[ 一般設定 ](enable-general.md) オプションを参照してください **[!UICONTROL Enable Ship To Store]**。 | グローバル | 不可 |
| **[!UICONTROL Enable Ship From Store]**</br>`Extension Attribute: [!DNL use_as_shipping_source]` | ソースレベルで店舗からの出荷機能を設定します。 詳しくは、「[ 一般設定 ](enable-general.md)」オプションを参照してください [!UICONTROL Enable Ship From Store] | グローバル | 不可 |

{style="table-layout:auto"}

## 集荷場所の構成

| **フィールド** | **説明** | **範囲** | **必須** |
|-----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Allow In-Store Pickup]**</br>`Extension Attribute: [!DNL store_pickup_enabled]` | 2 つのピックアップ オプションの 1 つ。 [!DNL In-Store Pickup] とは、顧客がマーチャントストアの場所に入って注文を取得できるようにする機能を指します。 </br></br> 有効にすると、チェックアウト時に顧客に提示される場合があります。 </br></br> また、このオプションは、グローバル設定を、[!UICONTROL In-store Pickup] の [!UICONTROL Delivery Method] で設定された [!UICONTROL Enable In-store Pickup] に上書きします | グローバル | 不可 |
| **店舗での受け取り指示**</br>`Extension Attribute: store_pickup_instructions` | **Order Ready For Pickup in Store** の電子メール通知で顧客に配信されるカスタマイズ可能なメッセージです。 | グローバル | 不可 |
| **縁取りを許可**</br>`Extension Attribute: curbside_enabled` | 2 つのピックアップ オプションの 1 つ。 カーブサイド配信を使用すると、顧客は商店の場所の指定された場所に車両を駐車できます。 このシナリオでは、店舗の担当者が注文を顧客に配信します。 </br></br> 有効にすると、チェックアウト時にこのオプションが顧客に表示される場合があります。 また、お客様は、チェックインの際に車両と駐車場の説明を求められる場合があります。 </br></br> また、このオプションは、**店舗内ピックアップ** に対して **配信方法** で設定された **カーブサイドピックアップを有効にする** グローバル設定を上書きします。 | グローバル | 不可 |
| **[!UICONTROL Curbside Instructions]**</br>`Extension Attribute: curbside_instructions` | [!UICONTROL Order Ready For Pickup in Store] しいメール通知で顧客に配信されるカスタマイズ可能なメッセージ。 | グローバル | 不可 |
| **[!UICONTROL Estimated Pickup Lead Time]**</br>`Extension Attribute: pickup_lead_time` | 注文を受け取り、ピッキングし、ピッキングの準備を整えるまでに必要な分数。 </br></br> この情報は、ウェブサイト上の顧客への注文受け取りの推定時間を表示するために使用されます。</br></br> このオプションの設定は、**店舗での受け取り** 設定の **配信方法** に設定された **推定ピックアップリードタイム** のグローバル設定を上書きします。 | グローバル | 不可 |
| **[!UICONTROL Estimated Pickup Time Label]**</br>`Extension Attribute: pickup_time_label` | 注文の受け取り準備が整うまでの分数を表示するラベル。</br></br> このラベルをカスタマイズするときに、コード %1 を使用して **推定ピックアップ リード タイム** を挿入できます。</br></br> このオプションを設定すると、[!UICONTROL In-store Pickup] の [!UICONTROL Delivery Method] に対して構成された [!UICONTROL Estimated Pickup Time Label] のグローバル構成が上書きされます。 | グローバル | 不可 |

### **開館時間**

| **フィールド** | **説明** | **範囲** | **必須** |
|------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Location Timezone]**</br>`Extension Attribute: timezone` | マーチャントストアの場所のタイムゾーン。 毎日、開始時刻と終了時刻を設定します。</br></br> これらの設定は、推定受け取り時間の最適化と、フルフィルメントサービスのレポートで使用されます。 | グローバル | はい |
| **[!UICONTROL Opening Hours]**</br>`Internal Attribute: inventory_source_opening_hours_dynamic_rows` | 販売店所在地の営業時間。 </br></br> この情報は、推定集荷時間の最適化や、フルフィルメントサービスのレポート作成に使用できます。 | グローバル | はい |

### チェックインエクスペリエンスインターフェイスオプションの設定



| **フィールド** | **説明** | **範囲** | **必須** |
|---------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Use Parking Spots]**</br>`Extension Attribute: parking_spots_enabled` | 加盟店の場所にカーブサイド集荷の指定駐車場があるかどうかを指定します。 </br></br> 有効にすると、利用可能な駐車場を設定できます。 | グローバル | 不可 |
| **[!UICONTROL Is Parking Spot a Mandatory Field?]**</br>`Extension Attribute: parking_spot_mandatory` | 買い物エクスペリエンス中に、顧客の駐車場の識別が必須かどうかを指定します。</br></br> 有効にすると、お客様は到着時に駐車場を指定するように求められます。 無効にした場合、ユーザーはこの入力をスキップできます。 | グローバル | 不可 |
| **[!UICONTROL Parking Spots List]**</br> `Internal Attribute: inventory_source_parking_spot_dynamic_rows` | この加盟店の場所で利用可能な駐車場は、カーブサイドで受け取ることができます。 提供されたインターフェイスを使用して、各スポットに名前を付けます。</br></br> すべての駐車場に名前を付ける必要はなく、縁石に指定された場所にのみ名前を付けます。 例えば、駐車場の行 A～G が使用可能な場合でも、行 A の最初の 8 つのスポットのみが縁側ピックアップ用に指定されます。 このシナリオでは、A1、A2、A3 などの 8 つのスポットを定義できます。 | グローバル | 不可 |
| **[!UICONTROL Allow "Other" Parking Spot Field]**</br>`Extension Attribute: custom_parking_spot_enabled` | この設定を有効にすると、お客様はチェックイン時に駐車場を説明できるようになります。 | グローバル | 不可 |
| **[!UICONTROL Use Car Color]**</br>`Extension Attribute: use_car_color` | チェックイン時に顧客からの車両カラーの収集をサポートするかどうかを指定します。 </br></br> [!UICONTROL Car Color] で使用可能な選択項目は、管理者 [ チェックインエクスペリエンスのシステム設定 ](check-in-experience-setup.md) で設定されます。 | グローバル | 不可 |
| **[!UICONTROL Is Car Color a Mandatory Field?]**</br>`Extension Attribute: car_color_mandatory` | チェックイン時にお客様が車両の色を識別する必要があるかどうかを指定します。</br></br> 有効にすると、お客様は到着時に車両の色を指定するように求められます。 無効にした場合、ユーザーはこの入力をスキップできます。 | グローバル | 不可 |
| **[!UICONTROL Use Car Make]** </br>`Extension Attribute: use_car_make` | チェックイン時に顧客からの車種の回収をサポートするかどうかを指定します。</br></br> [!UICONTROL Car Make] で使用可能な選択項目は、管理者 [ チェックインエクスペリエンスのシステム設定 ](check-in-experience-setup.md) で設定されます。 | グローバル | 不可 |
| **[!UICONTROL Is Car Make a Mandatory Field?]**</br>`Extension Attribute: car_make_mandatory` | チェックイン時に顧客の車両確認 ID が必須かどうかを指定します。</br></br> 有効にすると、お客様は到着時に車両の車種を指定するように求められます。 無効にした場合、ユーザーはこの入力をスキップできます。 | グローバル | 不可 |
| **[!UICONTROL Use Additional Information]**</br> `Extension Attribute: use_additional_information` | チェックイン時に顧客からの追加情報の収集をサポートするかどうかを指定します。 | グローバル | 不可 |
| **[!UICONTROL Is Additional Information a Mandatory Field?]**</br>`Extension Attribute: additional_information_mandatory` | チェックイン時に顧客に追加情報が必要かどうかを指定します。 </br></br> 有効にすると、お客様は到着時に追加情報の入力を求められます。 無効にした場合、ユーザーはこの入力をスキップできます。 | グローバル | 不可 |
