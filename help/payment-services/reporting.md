---
title: 報告書
description: 取引レポートを使用して、取引承認レートと取引トレンドを表示します。
role: User
level: Intermediate
exl-id: dd1d80f9-5983-4181-91aa-971522eb56fa
source-git-commit: 4482c1f93a424c73497b88c707d0ab93a694c957
workflow-type: tm+mt
source-wordcount: '1270'
ht-degree: 0%

---

# 報告書

[!DNL Payment Services] for [!DNL Adobe Commerce] and [!DNL Magento Open Source] は、店舗の取引、注文、支払いを明確に把握できる包括的なレポートを提供します。

![ 取引報告書 ](assets/transactions-report.png){width="700" zoomable="yes"}

トランザクションレポートでは、トランザクションの承認レートとマイナスのトランザクショントレンドを可視化できるため、店舗の状態を効果的に監視し、トランザクションの問題を事前に特定して対処できます。

ストアフロントで注文された注文とその支払い方法、結果、支払い応答コードなどの個々のトランザクションを参照してください。

トランザクションレポートに表示される情報は、マーチャントでの使用のみを目的としています。 この情報を顧客やその他の潜在的な詐欺師と共有しないでください。 トランザクション情報は、セキュリティチェックを回避したり、チャージバックにつながる注文を行うために使用できます。

取引レポートは.csv ファイル形式でダウンロードでき、既存の会計ソフトウェアや受注管理ソフトウェアで使用できます。

>[!NOTE]
>
>[!DNL Payment Services] に対して [ オンボーディングおよびアクティブ化されたライブモード ](production.md#enable-live-payments) を持っていない場合は、財務報告書を表示できません。

## トランザクションレポートの表示

取引レポート・ビューは、Payment Services の「取引」ビューで使用できます。 ストアのトランザクションに関して使用可能なすべての情報が含まれます。

_管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL Payment Services]**/_[!UICONTROL Transactions]_/**[!UICONTROL View Report]**&#x200B;に移動して、詳細な表形式のトランザクションレポート表示を表示します。

![ トランザクションレポートの表示 ](assets/transactions-report-view.png){width="800" zoomable="yes"}

このトピックのセクションに従って、表示するデータを最も適切に表示するように、このビューを設定できます。

このレポート内のリンクされたCommerceの注文と PayPal の取引 ID、取引額、1 取引あたりの支払い方法などを参照してください。

すべての支払い方法が同じ精度の情報を提供するわけではありません。 例えば、クレジットカードの取引では、応答、AVS および CCV コードが提供され、取引レポートではカードの最後の 4 桁が提供されますが、PayPal の支払いボタンは提供されません。

既存の会計または注文管理ソフトウェアで使用するために、.csv ファイル形式で [ トランザクションをダウンロード ](#download-transactions) できます。

>[!WARNING]
>
> トランザクション レポートには、[!DNL Payment Services] 外で作成されたキャプチャは含まれません。

### データソースを選択

「トランザクション」レポート・ビューでは、レポート結果を表示するデータ・ソース（**[!UICONTROL Live]** または **[!UICONTROL Sandbox]**）を選択できます。

![ データソースの選択 ](assets/datasource.png){width="300" zoomable="yes"}

_[!UICONTROL Live]_&#x200B;が選択されているデータソースの場合、実稼動モードで [!DNL Payment Services] を使用しているストアのレポート情報を表示できます。_[!UICONTROL Sandbox]_ が選択したデータソースの場合、サンドボックスモードのレポート情報を表示できます。

データソースを選択すると、次のように機能します。

* 実稼働モードで [!DNL Payment Services] を使用するストアがない場合、データソースの選択はデフォルトで _[!UICONTROL Sandbox]_&#x200B;になります。
* 実稼動モードで [!DNL Payment Services] を使用するストア（1 つまたは複数）がある場合、データソースの選択はデフォルトで _[!UICONTROL Live]_&#x200B;になります。
* レポートの書き出しでは、常にデータソースの選択に従います。

[!UICONTROL Transactions] レポートのデータソースを選択するには：

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL [!DNL Payment Services]]**/_[!UICONTROL Transactions]_/**[!UICONTROL View Report]**&#x200B;に移動します。
1. 「**[!UICONTROL Data source]**」をクリックし、「**[!UICONTROL Live]**」または「**[!UICONTROL Sandbox]**」を選択します。

   レポート結果は、選択したデータソースに基づいて再生成されます。

### 日付の期間のカスタマイズ

取引レポート表示から、特定の日付を選択して、表示する取引の期間をカスタマイズできます。 デフォルトでは、30 日間のトランザクションがグリッドに表示されます。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL [!DNL Payment Services]]**/_[!UICONTROL Transactions]_/**[!UICONTROL View Report]**&#x200B;に移動します。
1. **[!UICONTROL Transaction dates]** カレンダーセレクターフィルターをクリックします。
1. 該当する日付範囲を選択します。
1. 指定した日付のトランザクションをグリッドに表示します。

### レポート情報をフィルター

取引レポート・ビューで、フィルタ条件を選択して、表示するステータス結果をフィルタできます。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL [!DNL Payment Services]]**/_[!UICONTROL Transactions]_/**[!UICONTROL View Report]**&#x200B;に移動します。
1. **[!UICONTROL Filter]** セレクターをクリックします。
1. _[!UICONTROL Transaction Result]_&#x200B;のオプションを切り替えて、選択した注文トランザクションのみのレポート結果を表示します。
1. _[!UICONTROL Payment Method]_&#x200B;のオプションを切り替えて、トランザクションに使用された支払いタイプのレポート結果を表示します。
1. _[!UICONTROL Payment Detail]_&#x200B;のオプションを切り替えて、使用する支払いタイプの追加情報を表示します（使用可能な場合）。
1. _最小オーダー金額_ または _最大オーダー金額_ を入力して、そのオーダー金額範囲内のレポート結果を表示します。
1. 特定のトランザクションを検索する _[!UICONTROL Order ID]_&#x200B;を入力します。
1. 特定のクレジット カードまたはデビット カードを検索する _[!UICONTROL Card Last Four]_&#x200B;を紹介します。
1. 特定の顧客のすべてのトランザクションを表示する _[!UICONTROL Customer ID]_&#x200B;を入力します。
1. その電子メールのトランザクションをフィルター処理する _[!UICONTROL Customer Email]_&#x200B;を入力します。
1. 「**[!UICONTROL Hide filters]**」をクリックすると、フィルターが非表示になります。

### 列の表示/非表示

取引レポートには、デフォルトで使用可能なすべての情報列が表示されます。 ただし、レポートに表示する列をカスタマイズすることはできます。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL [!DNL Payment Services]]**/_[!UICONTROL Transactions]_/**[!UICONTROL View Report]**&#x200B;に移動します。
1. **[!UICONTROL Column settings]** アイコン ![ 列設定アイコン ](assets/column-settings.png){width="20" zoomable="yes"} をクリックします。
1. レポートに表示される列をカスタマイズするには、リストの列をチェックまたはチェック解除します。

   取引報告書には、列設定メニューで行った変更が直ちに表示されます。 レポートビューから移動すると、列の環境設定は保存され、有効なままになります。

### レポートデータを更新

トランザクションレポート表示には、レポート情報が最後に更新された時刻を示す _[!UICONTROL Last updated]_&#x200B;タイムスタンプが表示されます。 デフォルトでは、トランザクションレポートデータは 3 時間ごとに自動更新されます。

また、レポートデータを手動で強制的に更新して、最新のレポート情報を表示することもできます。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL [!DNL Payment Services]]**/_[!UICONTROL Transactions]_/**[!UICONTROL View Report]**&#x200B;に移動します。
1. _更新_ アイコン（![ 更新アイコン ](assets/refresh-button-med.png){width="20" zoomable="yes"}）をクリックします。

   トランザクションレポートデータが更新され、*[!UICONTROL Update complete]* の確認が表示され、最新の情報がグリッドに表示されます。

### トランザクションをダウンロード

デフォルトの 30 日間のトランザクションを表示している場合でも、カスタマイズされた期間を表示している場合でも、すべてのトランザクションがトランザクションビューグリッドに表示されている.csv ファイルをダウンロードできます。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL [!DNL Payment Services]]**/**[!UICONTROL Transactions]** に移動します。
1. 過去 30 日以外の期間のトランザクションを表示する場合は、[ ステータスの日付範囲の期間をカスタマイズ ](#customize-dates-timeframe) します。
1. _ダウンロード_![ ダウンロードアイコン ](assets/icon-download.png){width="20" zoomable="yes"} アイコンをクリックします。

トランザクションは.csv 形式でダウンロードされます。

### 列の説明

取引レポートには次の情報が含まれます。

| 列 | 説明 |
| ------------ | -------------------- |
| [!UICONTROL Order ID] | Commerce注文 ID （成功した取引の値のみを含み、却下された取引の値は空） <br> <br> 関連する [ 注文情報 ](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/order-management/orders/orders){target="_blank"} を表示するには、ID をクリックします。 |
| [!UICONTROL PayPal Transaction ID] | 支払いプロバイダーから提供されたトランザクション ID。成功したトランザクションの値のみを含み、却下されたトランザクションのダッシュを含みます。 この ID をクリックすると、PayPal の取引詳細ページにアクセスできます。 |
| [!UICONTROL Customer ID] | 注文のCommerce顧客 ID<br> <br> 詳しくは、[customer info](https://experienceleague.adobe.com/ja/docs/commerce-admin/customers/customer-accounts/account-create){target="_blank"} を参照してください。 |
| [!UICONTROL Transaction Date] | トランザクション日タイムスタンプ |
| [!UICONTROL Payment Method] | ブランドおよびカードのタイプに関する情報を使用して、トランザクションに使用する支払のタイプ。 詳しくは、[ カードタイプ ](https://developer.paypal.com/docs/api/orders/v2/#definition-card_type) を参照してください。支払いサービス バージョン 1.6.0 以降で使用できます。 |
| [!UICONTROL Payment Detail] | トランザクションに使用される支払いタイプに関する追加情報を提供します（利用可能な場合）。 |
| [!UICONTROL Card Last Four] | 取引に使用するクレジット カードまたはデビット カードの最後の 4 桁 |
| [!UICONTROL Result] | トランザクションの結果 – *[!UICONTROL OK]* （成功したトランザクション）、*[!UICONTROL Rejected by Payment Provider]* （PayPal によって却下）、*[!UICONTROL Rejected by Bank]* （カードを発行した銀行によって却下） |
| [!UICONTROL Response Code] | 支払いプロバイダーまたは銀行から拒否の理由を提供するエラーコード。[&#128279;](https://developer.paypal.com/api/rest/reference/orders/v2/errors/)`Rejected by Bank` の状態および [`Rejected by Payment Provider` の状態については ](https://developer.paypal.com/docs/api/orders/v2/#definition-processor_response) 考えられる応答コードと説明の一覧を参照してください  |
| [!UICONTROL AVS Code] | 住所確認サービスコード。支払いリクエストに対するプロセッサー応答情報です。 詳しくは、[ 使用可能なコードと説明のリスト ](https://developer.paypal.com/docs/api/orders/v2/#definition-processor_response) を参照してください。 |
| [!UICONTROL CVV Code] | クレジットカードおよびデビットカードのカード検証値コード。詳しくは、[ 使用可能なコードと説明のリスト ](https://developer.paypal.com/docs/api/orders/v2/#definition-processor_response) を参照してください。 |
| [!UICONTROL Amount] | トランザクションの注文金額 |
| [!UICONTROL Currency] | トランザクションでの注文に使用する通貨 |
| [!UICONTROL Type] | 取引に対する [ 支払 ](../payment-services/production.md#set-payment-services-as-payment-method) の訴え – `Authorize` 又は `Authorize and Capture` |

### エラー応答コード

_応答コード_ 列には、トランザクションに関連する特定のエラーまたは成功コードが表示されます。 表示される一般的なエラーコードを次に示します。

* `PAYMENT_DENIED` – 不正の疑いがあるため、PayPal によって取引が拒否されました。
* `INTERNAL_SERVER_ERROR` - トランザクションが PayPal によって却下され、PayPal サーバーエラーが発生しました。 トランザクションは再試行できます。
* `INSTRUMENT_DECLINED` – 選択した支払い方法に従って、PayPal によって顧客が拒否されました。 トランザクションは、別の支払い方法で再試行できます。
* `9500` – 不正の疑いがあるため、関連する銀行によって取引が拒否されました。
* `5120` – 顧客が支払に十分な資金を持っていなかったため、関連銀行によって取引が却下されました。
* `5650`：銀行は強力な顧客認証を必要とするため、関連する銀行によってトランザクションが拒否されました（[3DS](security.md#3ds)）。

失敗したトランザクションの詳細なエラー応答コードは、2023 年 6 月 1 日（PT）以降のトランザクションで使用できます。 2023 年 6 月 1 日（PT）より前に発生した取引については、部分的なレポートデータが表示されます。
