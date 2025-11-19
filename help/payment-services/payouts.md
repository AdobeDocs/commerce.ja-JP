---
title: 支払いレポート
description: 支払レポートを使用して、支払い金額、処理量および財務調整のトランザクションレベルに関する詳細レポートの完全な透明性を確保します。
role: User
level: Intermediate
exl-id: f3f99474-cd28-4c8f-b0ea-dca8e014b108
feature: Payments, Checkout, Paas, Saas
source-git-commit: a0f9ddbf3d0f291855cb51fd70a782c48b8efc6c
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 0%

---

# 支払いレポート

[!DNL Payment Services] for [!DNL Adobe Commerce] and [!DNL Magento Open Source] は、店舗の取引、注文、支払いを明確に把握できる包括的なレポートを提供します。

2 つの支払いレポートビューがあり、すべての支払いに関する詳細な情報を確認できます。

* **[支払いデータのビジュアライゼーションビュー](#payouts-data-visualization-view)** – 支払いサービスのホームで使用できるグラフ。支払いレポートビューから 1 日あたりの集計金額を視覚的に表現したものです。
* **[支払レポート・ビュー](#payouts-report-view)** – すべての取引の詳細な支払情報を表示する支払で使用可能なレポート

支払いビューは、包括的な支払い情報を一目で確認できるため、支払い金額、処理量、および財務調整のトランザクションレベルに関する詳細なレポートを完全に透明にすることができます。

.csv ファイル形式で [ 支払いトランザクションをダウンロード ](#download-transactions) して、既存の会計または注文管理ソフトウェアで使用できます。

>[!NOTE]
>
>支払いレポートには、キャプチャされた（支払いアクションが [`Authorize and Capture`](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/production.html#set-payment-services-as-payment-method) に設定されている）、または [`Invoiced` としてマークされている ](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice) 注文のみが表示されます。

## 支払いデータビジュアライゼーションビュー

支払いデータビジュアライゼーションビューは、支払いサービスホームで使用できます。 詳細な表形式 [ 支払いレポートビュー ](#payouts-report-view) から、1 日あたりの集計金額を視覚的に表現したものです。

_管理者_ サイドバーで、**[!UICONTROL Sales]** / **[!UICONTROL Payment Services]** に移動して、クレジットとデビットのデータビジュアライゼーショングラフおよび時間の経過に伴う移動平均を表示します。

![ 管理画面での支払いデータビジュアライゼーション ](assets/payouts-report.png){width="800" zoomable="yes"}

「**[!UICONTROL View Report]**」をクリックして、詳細な表形式 [ 支払いレポート表示 ](#payouts-report-view) に移動します。

### トランザクション期間のカスタマイズ

デフォルトでは、30 日間のトランザクションが表示されます。

支払いデータビジュアライゼーションビューで、日付範囲を選択することにより、表示する支払いトランザクションの期間をカスタマイズできます。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL Payment Services]** に移動します。 支払いデータビジュアライゼーションビューは、支払いセクションに表示されます。
1. **[!UICONTROL Range]** セレクターフィルターをクリックします。
1. 適用可能な日付範囲（30 日、15 日または 7 日）を選択します。
1. 指定した日付の取引情報を表示します。

### トランザクション情報

選択した日付範囲のトランザクション金額は、支払いデータビジュアライゼーションビューの左側に表示されます。 選択した日付範囲の日付がビューの下部に表示されます。 特定の日付に支払いがない場合、その日付は表示されません。

支払いデータビジュアライゼーションビューには、次の情報が含まれます。

| データ | 説明 |
| ------------ | -------------------- |
| [!UICONTROL Transaction amount] | 指定した時間枠でのトランザクションの金額範囲。Y 軸のデータ（左） |
| 日付範囲 | 指定した時間枠の日付範囲（X 軸のデータ）（下） |
| 貸方 | 指定した期間の支払い |
| 借方 | 指定した期間の借方（払戻） |
| 移動平均 | 指定した期間内の各日付の平均支払額を表します |
| 範囲のネット | 指定された期間（範囲）の正味支払額 |

## 支払いレポート ビュー

支払いレポート ビューは、支払いサービスの支払いビューで使用できます。 ストアの支払いに関する利用可能なすべての情報が含まれます。

_管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL Payment Services]**/_[!UICONTROL Payouts]_/**[!UICONTROL View Report]**に移動して、詳細な表形式の支払いレポートビューを表示します。

![ 管理画面での支払トランザクション ](assets/payouts-report-new.png){width="800" zoomable="yes"}

このトピックのセクションに従って、表示するデータを最も適切に表示するように、このビューを設定できます。

このレポート内のリンクされたCommerceの注文 ID と取引 ID、取引金額、1 取引あたりの支払い方法などを参照してください。

.csv ファイル形式で [ 支払いトランザクションをダウンロード ](#download-transactions) して、既存の会計または注文管理ソフトウェアで使用できます。

>[!NOTE]
>
>デフォルトでは、`DESC` を使用して、この表に示すデータが降順（`TRANS DATE`）で並べ替えられています。 `TRANS DATE` は、トランザクションが開始された日時です。

### データソースを選択

支払いレポート ビューでは、レポート結果を表示するデータ ソース （**[!UICONTROL Live]** または **[!UICONTROL Sandbox]**）を選択できます。

![ データソースの選択 ](assets/datasource.png){width="300" zoomable="yes"}

_[!UICONTROL Live]_のデータ ソースを選択した場合、本番モードでストアのレポート情報を表示できます。_[!UICONTROL Sandbox]_ が選択したデータソースの場合、サンドボックスモードでレポート情報ストアを表示できます。

データソースを選択すると、次のように機能します。

* ライブモードのストアがない場合は、データソースの選択はデフォルトで _[!UICONTROL Sandbox]_になります。
* ライブモードで 1 つまたは複数のストアがある場合、データソースの選択はデフォルトで _[!UICONTROL Live]_になります。
* レポートの書き出しでは、常にデータソースの選択に従います。

受注支払ステータス・レポートのデータ・ソースを選択する手順は、次のとおりです。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL Payment Services]**/_[!UICONTROL Payouts]_/**[!UICONTROL View Report]**に移動します。
1. 「**[!UICONTROL Data source]**」をクリックし、「**[!UICONTROL Live]**」または「**[!UICONTROL Sandbox]**」を選択します。

   レポート結果は、選択したデータソースに基づいて再生成されます。

### トランザクションの表示

デフォルトでは、30 日間のトランザクションが表示されます。

検索で返される行数、またはデフォルトの 30 日間のトランザクションで表示される行数は、支払いビューグリッドの上に、トランザクション日付カレンダーセレクターフィルターと共に表示されます。

左右にスクロールして、取引日、参照 ID、請求書番号、支払い方法の詳細など、日別レポートに [ 各支払いトランザクションの情報 ](#column-descriptions) を表示します。

#### トランザクション期間のカスタマイズ

支払レポート・ビューでは、特定の日付を入力するか、日付選択から日付範囲を選択して、表示する支払取引の期間をカスタマイズできます。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL Payment Services]**/_[!UICONTROL Payouts]_/**[!UICONTROL View Report]**に移動します。
1. _[!UICONTROL Transaction dates]_カレンダーセレクターフィルターをクリックします。
1. 該当する日付範囲を選択します。
1. 指定した日付の支払いステータスがグリッドに表示されます。

### 列の表示/非表示

デフォルトでは、支払いレポート・ビューには、利用可能な最も多くの情報列が表示されます。 ただし、レポートに表示する列をカスタマイズすることはできます。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL [!DNL Payment Services]]**/_[!UICONTROL Payouts]_/**[!UICONTROL View Report]**に移動します。
1. _列設定_ アイコン（![ 列設定アイコン ](assets/column-settings.png){width="20" zoomable="yes"}）をクリックします。
1. レポートに表示される列をカスタマイズするには、リストの列をチェックまたはチェック解除します。

   支払いレポートビューには、列設定メニューで行った変更が直ちに表示されます。 列の環境設定は保存され、レポートビューから移動しても有効になります。

### トランザクションをダウンロード

支払いビューグリッドに表示されているすべてのトランザクションを含む.csv ファイルをダウンロードできます。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL Payment Services]**/_[!UICONTROL Payouts]_/**[!UICONTROL View Report]**に移動します。
1. [ トランザクションの日付範囲の期間をカスタマイズします ](#customize-transactions-timeframe)。
1. _ダウンロード_ （![ ダウンロードアイコン ](assets/icon-download.png){width="20" zoomable="yes"}）アイコンをクリックします。

支払いトランザクションは.csv 形式でダウンロードされます。

### 列の説明

支払いレポートには、次の情報が含まれます。

| 列 | 説明 |
| ------------ | -------------------- |
| [!UICONTROL Provider] | 支払いプロバイダー |
| [!UICONTROL Provider trans] | トランザクション ID |
| [!UICONTROL Trans date] | トランザクションが開始された日時 |
| [!UICONTROL Type] | トランザクションの種類 – *[!UICONTROL PAYMENT]*、*[!UICONTROL BONUS]*、*[!UICONTROL CHARGEBACK]*、*[!UICONTROL CORRECTION]*、*[!UICONTROL CURRENCY_CONVERSATION]*、*[!UICONTROL DEPOSIT]*、*[!UICONTROL DISBURSEMENT]*、*[!UICONTROL DISPUTE]*、*[!UICONTROL FEES]*、*[!UICONTROL HOLD]*、*[!UICONTROL HOLD_RELEASE]*、*[!UICONTROL INCENTIVES]*、*[!UICONTROL OTHERS]*、*[!UICONTROL RECOUP]*、*[!UICONTROL REFUND]*、*[!UICONTROL REVERSAL]*、*[!UICONTROL WITHDRAWAL]* <br> <br> 詳しくは、[ トランザクションタイプ ](#transaction-types) を参照してください。 |
| [!UICONTROL Status] | トランザクションの現在のステータス（*[!UICONTROL SUCCESS]*、*[!UICONTROL DENIED]*、*[!UICONTROL PENDING]*） |
| [!UICONTROL Code] | 貸方（*CR*）または借方（*DR*）を示す取引コード |
| [!UICONTROL Reference ID] | このイベントが関連付けられている元のトランザクション ID |
| [!UICONTROL Invoice] | トランザクションの請求書 ID （注文ごとに 1 つ） |
| [!UICONTROL Commerce order] | Commerce注文 ID <br> <br> 関連する [ 注文情報 ](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/orders) を表示するには、ID をクリックします。 |
| [!UICONTROL Commerce trans] | Commerce トランザクション ID |
| [!UICONTROL Pay method] | クレジットカードの種類（*[!UICONTROL BANK]*、*[!UICONTROL PAYPAL]*、*[!UICONTROL CREDIT_CARD]*）および関連するカードプロバイダー（*Visa* や *MasterCard* など） |
| [!UICONTROL TRANS AMT] | トランザクションの金額 |
| [!UICONTROL CUR] | トランザクション金額の通貨単位 |
| [!UICONTROL PENDING] | 未払金額 |
| [!UICONTROL CUR] | 保留中の金額の通貨単位 |
| [!UICONTROL SELLER AMT] | 顧客との間で移動される資金の <br> 額 <br> 売り手アカウントから移動する資金には、ダッシュ（–）プレフィックスが表示されます。 |
| [!UICONTROL CUR] | 販売者金額の通貨単位 |
| [!UICONTROL PARTNER FEE] | トランザクション <br> に関連するパートナー手数料 <br> パートナー手数料アカウントから移動する資金には、ダッシュ （–） プレフィックスが表示されます。 |
| [!UICONTROL CUR] | パートナー手数料の通貨単位 |
| [!UICONTROL PROV FEES] | トランザクション <br> に関連する手数料 <br> プロバイダーの手数料アカウントから移動する資金には、ダッシュ（–）プレフィックスが表示されます。 |
| [!UICONTROL CUR] | プロバイダー手数料の通貨単位 |
| [!UICONTROL FEE %] | 手数料として請求されるトランザクション金額の割合 |
| [!UICONTROL FIXED FEE] | 固定プロバイダー手数料金額 |
| [!UICONTROL CHBK FEE] | トランザクション <br> に関連付けられたチャージバック手数料 <br> ダッシュ（–）プレフィックスは、チャージバック料金が取り消されたことを示します。 |
| [!UICONTROL CUR] | チャージバック手数料の通貨単位 |
| [!UICONTROL HOLD AMT] | 保留中または保留 <br> から解放された金額 <br> ダッシュ（–）プレフィックスは、保留中の資金がリリースされていることを示します。 |
| [!UICONTROL CUR] | 保留金額の通貨単位 |
| [!UICONTROL RECOUP AMT] | 回収勘定 <br> から回収された金額 <br> 回収勘定から移動する資金には、ダッシュ （–） プレフィックスが表示されます。 |
| [!UICONTROL CUR] | 回収金額の通貨単位 |

### トランザクションタイプ

これらの取引タイプは、支払い取引に記載される場合があります。

| 報告書 | 説明 |
| ------------ | -------------------- |
| [!UICONTROL PAYMENT] | 注文のために買い手と売り手の間で動かされるお金 |
| [!UICONTROL AUTH] | 承認および承認無効取引 |
| [!UICONTROL BONUS] | — |
| [!UICONTROL CHARGEBACK] | チャージバック手数料およびチャージバック手数料戻しトランザクション |
| [!UICONTROL CORRECTION] | — |
| [!UICONTROL CURRENCY_CONVERSION] | — |
| [!UICONTROL DEPOSIT] | — |
| [!UICONTROL DISBURSEMENT] | — |
| [!UICONTROL DISPUTE] | — |
| [!UICONTROL FEES] | パートナー手数料、支払い手数料、および手数料の取り消しトランザクション |
| [!UICONTROL HOLD] | — |
| [!UICONTROL HOLD_RELEASE] | — |
| [!UICONTROL INCENTIVES] | — |
| [!UICONTROL OTHERS] | — |
| [!UICONTROL RECOUP] | 銀行口座または損失勘定からの回収 |
| [!UICONTROL REFUND] | — |
| [!UICONTROL REVERSAL] | — |
| [!UICONTROL WITHDRAWAL] | — |
