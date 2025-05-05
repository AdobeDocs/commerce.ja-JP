---
title: 一般設定
description: 一般設定を構成して、ストアに対して有効  [!DNL Store Fulfillment]  します。 グローバル拡張機能の設定、ログ、データ同期およびセキュリティのためのシステム設定を構成します。 Adobe Commerceと Store Fulfillment サービスの統合を有効にするための主要なデータを提供します。
role: Admin
level: Intermediate
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '2405'
ht-degree: 0%

---

# ストア・サービスとセールス構成

拡張機能 [!DNL Store Fulfillment] 設定、ストアアシストアプリユーザーのセキュリティ設定、配信方法のオプションを設定して、[!DNL Commerce] 管理者から拡張機能を有効にします。

>[!IMPORTANT]
>
>ストアフルフィルメントサービスの設定は、Adobe Commerce インスタンスと [!DNL Store Fulfillment] アプリを接続した後にのみ適用されます。 [Connect Store Fulfillment](connect-set-up-service.md) を参照してください。

## Store Fulfillment サービス設定の管理

[!DNL Commerce Admin Store Configuration] メニューから Store Fulfillment サービスの設定を管理します。

- 拡張機能を有効にし、グローバル設定を構成し、[**[!UICONTROL Stores > Configuration > Services > Store Fulfillment by Walmart Commerce Technologies]**] を選択して Store Assist アプリのユーザー接続およびアカウントのセキュリティ オプションを指定します。

  ![ ストアフルフィルメントの管理ストアサービス設定 ](assets/store-services-admin-sf-config.png)

- **[!UICONTROL Store > Configuration > Sales > Delivery Methods > In-Store Pickup]** を選択して配信方法を設定します。

  ![Store Fulfillment の管理ストア販売設定 ](assets/store-sales-admin-sf-deliver-config.png)

## 基本設定

<table>
<thead>
<tr>
<td><strong>フィールド</strong></td>
<td><strong>説明</strong></td>
<td><strong>対象範囲</strong></td>
<td><strong>必須</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Price]</strong></td>
<td>店舗での受け取りに対して顧客に請求する価格。 デフォルトは 0 です。</td>
<td>Web サイト</td>
<td>不可</td>
</tr>
<tr>
<td><strong>[!UICONTROL Search Radius]</strong></td>
<td>買い物客がストアフロントのチェックアウトで店舗の集荷場所を検索する際に使用する半径（キロメートル単位）。 検索結果には、指定した検索半径内にあるストアのみが返されます。</td>
<td>Web サイト</td>
<td>不可</td>
</tr>
<tr>
<td><strong>[!UICONTROL Displayed error message]</strong></td>
<td>店舗での受け取りに使用できない品目に対して顧客が店舗での受け取りを選択すると表示されるメッセージ。 必要に応じて、デフォルトのテキストをカスタマイズできます。
</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
</tbody>
</table>

>[!NOTE]
>
>[!UICONTROL Search Radius] の設定は、Adobe Commerceに [ ストアの場所とマッピングの設定 ](store-location-map-provider-setup.md) を設定した場合にのみ使用されます。

## ストアフルフィルメントソリューションの有効化

[!DNL Store Fulfillment] ソリューションを有効にすると、Adobe Commerce ストアフロントのショッピングエクスペリエンスとチェックアウトエクスペリエンスに店舗内および縁側のピックアップ機能が追加されます。

<table>
<thead>
<tr>
<td><strong>フィールド</strong></td>
<td><strong>説明</strong></td>
<td><strong>対象範囲</strong></td>
<td><strong>必須</strong></td>
</tr>
 </thead>
 <tbody>
<tr>
<td><strong>[!UICONTROL Enabled]</strong></td>
<td>ソリューションを有効または無効にします。 有効化すると、ストアフルフィルメント機能を設定および使用し、Adobe Commerceストアと [!DNL Store Fulfillment] のサービスとの連携を確立します。 無効にすると、すべてのストアフルフィルメント機能が無効になり、Adobe Commerceとストアフルフィルメントサービスの間のやり取りがなくなります。 注文情報は処理または受信できません。</td>
<td>Web サイト</td>
<td>はい</td>
</tr>
</tbody>
</table>

## アカウント資格情報の追加

<table>
<tr>
<td><strong>フィールド</strong></td>
<td><strong>説明</strong></td>
<td><strong>対象範囲</strong></td>
<td><strong>必須</strong></td>
</tr>
<tr>
<td><strong>[!UICONTROL Environment]</strong></td>
<td><i>[!UICONTROL Sandbox]</i> または <i>[!UICONTROL Production]</i><br></br> 選択すると、テスト環境 [!UICONTROL Sandbox] フルフィルメントサービスとの通信が可能になります。<br></br> 「[!UICONTROL Production]」を選択すると、ライブ環境でフルフィルメントサービスとの通信が可能になります。<br></br> 各環境に一連の資格情報が与えられ、同じインストールで両方のセットを管理できます。 <br></br> 接続を検証する前に、資格情報を保存します。</td>
<td>グローバル</td>
<td>はい</td>
</tr>
<tr>
<td><strong>[!UICONTROL API Server URL]</strong></td>
<td>Walmart Store Fulfillment API エンドポイントへの URL。 値は、オンボーディングプロセス中に提供される完全修飾 URL である必要があります。 ストアフルフィルメントの顧客は、サンドボックスと実稼動 URL の両方を受け取ります。 値を追加する場合は、末尾のスラッシュ「/」を含む完全な URL をコピーして貼り付けます。</td>
<td>グローバル</td>
<td>はい</td>
</tr>
<tr>
<td><strong>[!UICONTROL Token Auth Server URL]</strong></td>
<td>Walmart Store フルフィルメント認証エンドポイントの URL。 値は、オンボーディングプロセス中に提供される完全修飾 URL である必要があります。 サンドボックスと実稼動 URL の両方を受け取ります。 値を追加する場合は、末尾のスラッシュ「/」を含む完全な URL をコピーして貼り付けます。</td>
<td>グローバル</td>
<td>はい</td>
</tr>
<tr>
<td><strong>[!UICONTROL Merchant Id]</strong></td>
<td>オンボーディングプロセス中に提供された一意のマーチャント（テナント） ID。 この ID は、マーチャントストアが注文を確実に受け取れるように注文をルーティングするために使用されます。</td>
<td>グローバル</td>
<td>はい</td>
</tr>
<tr>
<td><strong>[!UICONTROL Consumer Id]</strong></td>
<td>オンボーディングプロセス中に提供された一意の統合 ID。 この ID は、Adobe Commerceとストアフルフィルメントサービス間のすべての通信の認証に使用されます</td>
<td>グローバル</td>
<td>はい</td>
</tr>
<tr>
<td><strong>[!UICONTROL Consumer Secret]</strong></td>
<td>オンボーディングプロセス中に提供された一意の統合キー。 このキーは、Adobe Commerceとストアフルフィルメントサービス間のすべての通信の認証に使用されます。</td>
<td>グローバル</td>
<td>はい</td>
</tr>
</table>

[!UICONTROL Account Credentials] を設定したら、「<strong>[!UICONTROL Validate Credentials]</strong>」を選択して、ストアフルフィルメントサービスへの接続を初めて検証および確立します。

## ログの設定

Store Fulfillment サービスのログは、ログ ファイル `var/log/walmart-bopis.log` で使用できます。

API 関連の例外をファイアウォールまたはキャッシュから取得できるように、例外処理を許可するように環境を設定するようにシステム管理者に依頼してください。

アプリケーション・ログ・ファイルは急速に増大する可能性があるため、必要に応じてアプリケーションのログを短時間だけ有効にします。たとえば、[!DNL Commerce] 注文のストア・フルフィルメントに関する問題のトラブルシューティングを行う場合などです。 この設定により、ログファイルのサイズが大きいことに起因する実稼動環境での応答時間の問題が回避されます。

>[!TIP]
>
>Adobe Commerceのオンプレミスインストールでは、サイズを最小限に抑えるために、`var/log/walmart-bopis.log` ファイルのログローテーションを設定するようにシステム管理者に依頼してください。 Adobe Commerceのオンプレミスインストールについては、_Adobe Commerce インストールガイド [&#128279;](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html#server-settings) の  ログローテーション_ を参照してください。 クラウドインフラストラクチャプロジェクトのAdobe Commerceについては、[ ログの表示と管理 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html) を参照してください。

<table>
<thead>
<tr>
<td><strong>フィールド</strong></td>
<td><strong>説明</strong></td>
<td><strong>対象範囲</strong></td>
<td><strong>必須</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Debug Mode]</strong></td>
<td>デバッグモードは、統合内のログに記録されるアクティビティを増やすために使用します。 無効にすると、デバッグ情報はログに記録されません。 有効にすると、すべてのデバッグ情報がログに記録されます <br></br> すべてのログに記録されたデータは次のファイルにあります。 <pre>var/log/walmart-bopis.log</pre>
<td>グローバル</td>
<td>不可</td>
</tr>
</tbody>
</table>

## 注文の同期の管理

注文の同期に対するエラー処理の管理、注文ピッキング中のバーコード スキャンに使用するカタログ属性の管理、および店舗受け渡しキューの注文バッチ サイズの構成を行うための設定を構成します。

注文の同期操作に関する詳細は、管理の店舗受け渡しキュー管理ダッシュボード（
<strong>[!UICONTROL System > Tools > Store Fulfillment Queue]</strong>）に設定します。

### 同期エラー管理

<table>
<tr>
<td><strong>フィールド</strong></td>
<td><strong>説明</strong></td>
<td><strong>対象範囲</strong></td>
<td><strong>必須</strong></td>
</tr>
<tr>
<td><strong>[!UICONTROL Retry Critical Error]</strong></td>
<td>重大なエラーが発生した後のレコード同期処理の再試行を指定します。<br></br> 重要なエラーは、統合がフルフィルメントサービスから肯定的な応答を受け取れなかったときに発生します。 これらの問題は、サービスが停止している場合や、送信されている注文データにエラーがある場合に発生します。<br></br> 再試行しきい値に達した場合、項目はキューに残りますが、再処理されません。 エラーが発生したすべての項目は <strong>[!UICONTROL System > Tools > Store Fulfillment Queue]</strong> Management の Admin で表示されます。 一貫して失敗する項目のトラブルシューティングを行うには、アカウントマネージャーにお問い合わせください。</td>
<td>グローバル</td>
<td>不可</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Error Notification Email]</strong></td>
<td>注文の [!UICONTROL Retry Critical Error Threshold] に達したときにメールを受け取るためのエラー通知を有効にする。 通知には、エラーに関して使用可能な詳細が含まれます。</td>
<td>グローバル</td>
<td>不可</td>
</tr>
<tr>
<td><strong>[!UICONTROL Send Error Notification Email To]</strong></td>
<td>エラー通知用の受信者のメールアドレスのコンマ区切りリスト。</td>
<td>グローバル</td>
<td>不可</td>
</tr>
<tr>
<td><strong>[!UICONTROL Order Sync Exception Email Template]</strong></td>
<td>注文同期エラーを受信者に通知するために使用するメールテンプレートを指定します。 デフォルトのテンプレートが提供されます。 カスタマイズはサポートされていません。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
</table>

### 注文の同期

<table>
<thead>
<tr>
<td><strong>フィールド</strong></td>
<td><strong>説明</strong></td>
<td><strong>対象範囲</strong></td>
<td><strong>必須</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Barcode Source]</strong></td>
<td>マーチャントの場所にある対応する品目のスキャン可能なコードを格納するカタログ属性。<br></br> 既存のマーチャントの場所が 1 つしかない場合、UPC コードを使用している一方で、e コマースチャネルは製品を SKU で識別している可能性があります。 このシナリオでは、UPC コードを含むカタログ属性を選択します。<br></br> この設定により、正しい識別子を持つ注文が店舗リスト品目に送信されるため、店舗の担当者はピッキング プロセス中に品目を正確にスキャンできます。<br></br> 不明な場合は、出荷およびピッキング部門のフルフィルメント担当者に問い合わせて、どの属性を送信するかを決定してください。 属性が現在データベースに含まれていない場合は、Adobe Commerceの製品属性セットに属性を追加できます。</td>
<td>Web サイト</td>
<td>はい</td>
</tr>
<tr>
<td><strong>[!UICONTROL Barcode Type]</strong></td>
<td>マーチャントの場所にある対応する項目のバーコードソースを保存するカタログ属性。<br></br> この設定により、店舗に送信された注文が正しい識別子でリストされるため、店舗の担当者はピッキング プロセス中に品目を正確にスキャンできます。 オプションには、SKU、UPC、GTIN、UPCA、EAN13、UPCE0、DISA、UAB、CODABAR、Price Embedded UPC があります。<br></br> 不明な場合は、[!UICONTROL Barcode Source] 属性に含まれる値に最も近いオプションを選択します。 店舗の担当者は、選択リストから手動で項目を照合できます。</td>
<td>Web サイト</td>
<td>はい</td>
</tr>
<tr>
<td><strong>[!UICONTROL Max Number of Items]</strong></td>
<td>ストア フルフィルメント キューから一度に送信するアイテムの最大数。<br></br>BOPIS の注文は、定期的に一括でフルフィルメントサービスに送信されます。 この設定を使用すると、バッチのサイズを制御できます。<br></br> デフォルト値は 100 項目です。 ご注文の数量や容量に応じて、最大値を上下に調整できます。</td>
<td>グローバル</td>
<td>不可</td>
</tr>
</tbody>
</table>

## 店舗フルフィルメント配送オプションの有効化

Adobe Commerce ストアで店舗の受け取りおよび宅配オプションを利用できるかどうかを決定するストアフルフィルメントの配送オプションを設定します。

### 出荷先店舗

<table>
<thead>
<tr>
<td><strong>フィールド</strong></td>
<td><strong>説明</strong></td>
<td><strong>対象範囲</strong></td>
<td><strong>必須</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Enable Ship To Store]</strong></td>
<td>出荷先店舗の設定は、既存の出荷先店舗機能に基づいています。 Inventory managementを使用する場合、または店舗間在庫移動により、在庫のない販売店場所で注文を受け入れて履行できる場合は、このオプションを「Yes」に設定します。<br></br>Ship-to-Store オプションをサポートできない場合、または提供を希望しない場合は、「いいえ」に設定します。 無効にすると、カタログ内の商品在庫ゼロの商品はその店舗では提供されません。また、その場所の [!DNL Out of Stock Threshold] を下回る商品は、店舗内の集荷オプションで提供されません。<br></br> この設定の値は、マーチャントの場所ごとに調整できます。</td>
<td>グローバル</td>
<td>不可</td>
</tr>
</tbody>
</table>

### 出荷元店舗

<table>
<thead>
<tr>
<td><strong>フィールド</strong></td>
<td><strong>説明</strong></td>
<td><strong>対象範囲</strong></td>
<td><strong>必須</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Enable Ship From Store]</strong></td>
<td>マーチャントストアのホーム配信オプションを有効または無効にします。 有効にすると、マーチャントストアの場所は、web サイトに関連付けられた在庫の他の割り当てられたソースと集計して考慮されます。<br></br> 標準のInventory management サービスでは、[!DNL Ship from Store] れはオプション固有のオプションであり、無効にすることはできません。 ストアフルフィルメントソリューションを使用すると、そのソリューションのオンとオフを切り替えることができます。<br></br> この設定は、マーチャントの場所と製品ごとに調整できます。</td>
<td>グローバル</td>
<td>不可</td>
</tr>
</tbody>
</table>


## Store Fulfillment App のアカウントと権限の使用の管理

Store Fulfillment App のユーザーアカウントとパスワードのセキュリティ、および二要素認証の設定を構成します。

### アプリのセキュリティ

<table>
<thead>
<tr>
<td><strong>フィールド</strong></td>
<td><strong>説明</strong></td>
<td><strong>対象範囲</strong></td>
<td><strong>必須</strong></td>
</tr>
 </thead>
 <tbody>
<tr>
<td><strong>[!UICONTROL User Session Lifetime]</strong></td>
<td>ストア関連付けユーザーセッションが自動ログアウトの前にアクティブのままである期間（秒）。 有効な値の範囲は 60 ～ 31536000 です。</td>
<td>グローバル</td>
<td>不可</td>
</tr>
<tr>
<td><strong>[!UICONTROL Maximum Login Failures to Lockout Account]</strong></td>
<td>ストアの関連付けがユーザーのアカウントからロックアウトされるまで、許可されるログインの失敗回数を指定します。<br></br> アカウントのロックアウトを無効にするには、値を 0 に設定します。</td>
<td>グローバル</td>
<td>不可</td>
</tr>
<tr>
<td><strong>[!UICONTROL Lockout Time (minutes)]</strong></td>
<td>ログインに失敗した後、アカウントをロックする時間（分）。</td>
<td>グローバル</td>
<td>不可</td>
</tr>
<tr>
<td><strong>[!UICONTROL Force Password Change]</strong></td>
<td><em>[!UICONTROL Yes]</em>：アカウントの設定後にパスワードの変更をユーザーに要求します。<br></br><em>[!UICONTROL No]</em>: アカウントの設定後にパスワードを変更することをお勧めします。</td>
<td>グローバル</td>
<td>不可</td>
</tr>
<tr>
<td><strong>[!UICONTROL Password Lifetime]</strong></td>
<td>必要なパスワードが変更されるまでパスワードが有効である日数。 このオプションを無効にするには、空のままにします。</td>
<td>グローバル</td>
<td>不可</td>
</tr>
</tbody>
</table>

## 配信方法

ストアフルフィルメントは、Adobe Commerceのネイティブな [!DNL In-Store Delivery] 機能を拡張することで機能します。 拡張機能をインストールしたら、管理者に追加される次の拡張設定を使用して、ストア内配信方法を設定できます。

- **店舗での受け取り** - チェックアウトプロセス中の店舗内配信のオファーオプション
これらの設定は、BOPI 注文の最も一般的な配信シナリオを設定します。

- 顧客が店舗の場所に駐車して、店員によって注文を配達するための **[!UICONTROL Curbside pick up]** ートオファーオプション。

<strong>[!UICONTROL Stores > Configuration > Sales > Delivery Methods > In-Store Pickup]</strong> を選択して、管理者からこれらの設定を構成します。

>[!NOTE]
>
>ストア内配信オプションの設定について詳しくは、&lbrace;2[Adobe Commerce ユーザーガイド ](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/delivery/basic-methods/shipping-in-store-delivery) ストア内配信 _を参照してください。_


### 配信方法の設定

店舗内配送方式では、お客様はチェックアウト時に集荷場所として使用するソースを選択できます。

<table>
<thead>
<tr>
<td><strong>フィールド</strong></td>
<td><strong>説明</strong></td>
<td><strong>対象範囲</strong></td>
<td><strong>必須</strong></td>
</tr>
 </thead>
 <tbody>
<tr>
<td><strong>[!UICONTROL Enable In-Store Pickup]</strong></td>
<td>店舗の受け取りを選択する顧客のチェックアウト時に使用できる店舗の受け取りオプションを有効または無効にします。 店舗での受け取りが無効になっている場合、このオプションは表示されません。<br></br> このグローバル設定は、すべての小売店の場所に適用されます。 有効にすると、小売店の場所で選択的に無効にすることができます。</td>
<td>Web サイト</td>
<td>不可</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Curbside Pickup]</strong></td>
<td>店舗の集荷を選択する顧客のチェックアウト プロセス中にカーブサイドの集荷オプションを有効または無効にします。<br></br> このグローバル設定は、すべての小売店の場所に適用されます。 有効にすると、小売店の場所で選択的に無効にすることができます。</td>
<td>Web サイト</td>
<td>不可</td>
</tr>
</tbody>
</table>

### 配信方法のタイトルの設定

<table>
<thead>
<tr>
<th><strong>フィールド</strong></th>
<th><strong>説明</strong></th>
<th><strong>対象範囲</strong></th>
<th><strong>必須</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>ホーム配信タイトル</strong></td>
<td>製品、買い物かご、チェックアウトの各エリアのホーム配信オプションに表示するタイトルを指定します。 宅配とは、Adobe Commerceの標準的な配送機能を指します。倉庫から、配送業者によって、またはお客様が指定した配送先住所に直接お届けします。 </br></br> このラベルは、選択した配送業者の配送方法ラベルには影響しません。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>ホーム配信の説明</strong></td>
<td>顧客にホーム配信のタイトルが表示されるたびに表示されるオプションの説明です。 ほとんどの場合、説明は、配信のプロミスを伝えるための静的メッセージです。 次に例を示します。</br><code>Same-day shipping on orders by 4</code></br></br><code>Ships within 2 business days</code></td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>店舗の集荷タイトル</strong></td>
<td>顧客に配信オプションが表示され、店舗での受け取りが可能な場合、このラベルが表示されます。 </br></br> このラベルは、製品、買い物かご、チェックアウトの各エリアに表示されるようにカスタマイズできます。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<td><strong>店舗の受け取りの説明</strong></td>
<td>ストア ピックアップ タイトルが表示される場所に関わらず、説明を任意で含めることができます。 この静的メッセージは、ストアの受け取りエクスペリエンスに関連する顧客コミュニケーションを改善するのに役立ちます。 次に例を示します。</br></br><code>Get it today for free!</code></br></br><code>Ready for pickup in an hour!</code></td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>店舗内集荷タイトル</strong></td>
<td>店舗での受け取りが有効になっている場合、このタイトルは、店舗での受け取り配信オプションとして顧客に表示されます。 ラベルをカスタマイズできます。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<tr>
<td><strong>カーブサイド ピックアップ タイトル</strong></td>
<td>カーブサイドの受け取りを有効にすると、このオプションは、店舗の受け取り配信オプションのタイプとして顧客に表示されます。 ここでラベルをカスタマイズできます。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>店舗での受け取り手順</strong></td>
<td>小売店で注文を受け取る準備が整うと、顧客にメールで通知されます。 お客様がチェックアウト時に [!DNL In-Store Pickup] を選択した場合は、ここでピックアップ手順をカスタマイズできます。 </br></br> これらの手順はグローバルに設定され、すべての小売店の場所に適用されます。 小売店の場所レベルで指示をカスタマイズすることもできます。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>カーブサイドの受け取り手順</strong></td>
<td>カーブサイドの集荷注文に関する顧客の電子メール通知に含める、カスタマイズされた注文集荷指示を指定します。 </br></br> これらの手順はグローバルに設定され、すべての小売店の場所に適用されます。 小売店の場所レベルで指示をカスタマイズすることもできます。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>推定集荷リード タイム</strong></td>
<td>注文を受け取り、履行し、受け取る準備が整うまでに必要な分数。 この情報は、店舗ピックアップ配信オプションの小売店舗の場所を選択する際に顧客に表示されます。 この設定は、すべての小売店舗の場所に適用されます。 小売店の場所レベルでリードタイムをカスタマイズすることもできます。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>推定ピックアップ時間ラベル</strong></td>
<td>顧客の集荷に対する注文が利用可能になるまでの推定時間を表示します。 この情報は、顧客が [!DNL In-Store Pickup] 配信オプションで小売店の場所を選択した場合に表示されます。 </br></br> このラベルをカスタマイズする場合、コード <code>%1</code> を使用して <strong> 推定ピックアップリードタイム </strong> を挿入できます。 例：</br></br><code>Ready for Pickup in %1 minutes.</code></br></br> この設定は、すべての小売店の場所に適用されます。 小売店の場所レベルでリードタイムをカスタマイズすることもできます。</td>
<td>ストア表示</td>
<td>不可</td>
<tr>
<td><strong>集荷時間の免責事項</strong></td>
<td>時間、休日、予期しない閉鎖などを一覧表示するツールヒントの製品ページに表示されるコンテンツ</td>
<td>ストア表示
</td>
<td>不可
</td>
</tr>
</tbody></table>

### 在庫の可用性タイトルの設定

<table>
<thead>
<tr>
<th><strong>フィールド</strong></th>
<th><strong>説明</strong></th>
<th><strong>対象範囲</strong></th>
<th><strong>必須</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>在庫</strong></td>
<td>顧客が小売店舗保管棚を使用している場合、現在の品目の在庫可用性が事業所ごとに表示されます。 </br></br> ここで <em>[!UICONTROL in-stock]</em> ステータスラベルをカスタマイズできます。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>在庫切れ</strong></td>
<td>顧客が小売店舗保管棚を使用している場合、現在品目の在庫可用性が各事業所に表示されます。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>一部在庫あり</strong></td>
<td>顧客が小売店舗保管棚を使用している場合、現在品目の在庫可用性が各事業所に表示されます。 </br></br> ここで <em>[!UICONTROL partially in-stock]</em> ステータスラベルをカスタマイズできます。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
</tbody></table>

