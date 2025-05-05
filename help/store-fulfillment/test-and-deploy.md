---
title: ストアフルフィルメントのテストとデプロイ
description: テスト計画を実行して、ストアフルフィルメント機能を検証します。 テストでは、在庫同期 API、キャンセルされた注文のエンドツーエンドのフルフィルメントワークフロー、ストアフルフィルメントアプリのユーザー管理、顧客のチェックインエクスペリエンスについて説明します。
role: User, Admin
level: Intermediate
feature: Shipping/Delivery, User Account, Roles/Permissions
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '2661'
ht-degree: 0%

---

# Adobe Commerceのストアフルフィルメントのテストとデプロイ

開発環境でのオンボーディングプロセスを完了したら、ストアフルフィルメントソリューションをテストし、実稼動環境にデプロイするプロセスを開始できます。

**前提条件**

情報、ストア、オーダーをテストまたは同期する前に、次のタスクを完了していることを確認してください。

- Store Fulfillment サービスの [ 一般構成 ](enable-general.md) を完了しました。

- [サンドボックス環境と実稼動環境のアカウント資格情報と接続詳細を追加し、検証します。](connect-set-up-service.md#configure-store-fulfillment-account-credentials)

- ストアフルフィルメントソリューションの [&#128279;](connect-set-up-service.md#configure-store-fulfillment-account-credentials)0&rbrace;Adobe Commerce統合 &rbrace; が使用可能で承認されていることを確認します。

## テストの準備

テストオーダーを作成したり、統合テストを実行したりするには、接続設定を完了する必要があります。 テストする前に、ストアデータが同期されていることも確認する必要があります。

1. ストアフルフィルメントソースを同期します。

   - **[!UICONTROL Stores > Sources]** に移動します。

   - 「**[!UICONTROL Synchronize Store Fulfillment Sources]**」を選択します。

1. ストアグリッドから、テストオーダーを作成する前に、ストアが `Synced` としてマークされていることを確認します。

## サンプルテスト計画

小売業者は、デプロイメントの設定およびテストフェーズで、ストアフルフィルメントソリューションの基本機能を検証します。 このサンプルテストプランは、テストの出発点となります。 必要に応じて、シナリオを追加します。

>[!NOTE]
>
>ストアフルフィルメントソリューションの最初のオンボーディングを完了するか、既存のインストールを更新した後、実稼動環境にデプロイする前に、常に実稼動以外の環境でアプリケーションをテストします。

このサンプルテスト計画は、次の機能領域をカバーしています。

| 機能領域 | 関数 | 役割 |
|-------------------------------------|------------------------------------------|----------------------------------|
| 在庫と注文の同期 | 在庫 API 同期 | Adobe Commerce管理者 |
| エンドツーエンド | 注文キャンセルワークフロー | 顧客、管理者、店員 |
| Admin | Store Fulfillment App の権限 | Admin |
| Adobe Commerce フロントエンド | 製品タイプ | 顧客、管理者 |
| フロントエンドのチェックアウ </br> フォーム | チェックイン操作 | 顧客、管理者 |
| ストアシストアプリ | Order</br>Pick</br>Stage</br>and Handoff | ストアの関連付け |

### Inventory API の同期

テスト計画のこのセクションでは、在庫と注文の同期について説明し、集荷ソースと在庫の更新がAdobe Commerceと Store Fulfillment ソリューションの間で正しく同期されることを確認します。

**機能領域**：在庫と注文の同期 </br>
**役割：** Admin</br>
**テストタイプ：** すべて陽性

<table>
<thead>
<tr>
<th>関数</th>
<th>シナリオをテスト</th>
<th>期待される結果</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>集荷在庫ソースの追加</strong></td>
<td>新しい集荷在庫ソースを保存します。</td>
<td>リアルタイム同期により、ソースの詳細が 5 分以内にウォルマートGIFサービスに送信されます。</td>
</tr>
<tr>
<td><strong>既存の集荷在庫ソースの更新</strong></td>
<td>既存の集荷在庫ソースの更新を保存します。</td>
<td>リアルタイム同期処理により、詳細が 5 分以内にウォルマートGIFに送信されます</td>
</tr>
<tr>
<td><strong>集荷在庫ソース </br><code>Is Synced</code> 状態</strong></td>
<td>既存の集荷在庫ソースの更新を保存します。</td>
<td>操作が成功すると、Sourceの管理ページの「<code>Is Synced</code>」列が <code>No</code> から <code>Yes</code> に更新されます。</td>
</tr>
<tr>
<td><strong>変更された在庫予約プロセス</strong></td>
<td>商品の新しい注文を作成して送信します。</td>
<td>それに応じて、商品の売り上げ可能数量が減少します。</td>
</tr>
<tr>
<td><strong>新しい注文のプッシュ、API 同期：顧客の注文</strong></td>
<td>顧客が店舗の受け取り注文を送信します。</td>
<td><ul><li>管理者の注文表示で、<strong>Adobe Commerce管理者ユーザーに注文の同期ステータスが次のように更新されたことを </strong> 知らせします。 <code>Sent</code></li><li>注文の詳細ログには、メッセージが含まれます <code>Order was sent to BOPIS solution for sync, it's not yet acknowledged yet.</code></li></ul></td>
</tr>
<tr>
<td><strong>新しい注文のプッシュ、API 同期 – 管理者が注文を送信</strong></td>
<td>Adobe Commerce<strong> 管理者 </strong> が集荷注文を送信します。</td>
<td><ul><li>管理者の注文表示で、注文同期のステータスが <code>Sent</code> に更新されます。</li><li>注文の詳細ログには、メッセージが含まれます <code>Order was sent to BOPIS solution for sync, it's not yet acknowledged yet.</code></li></ul></td>
</tr>
<tr>
<td><strong>新規受注プッシュ、例外キュー<strong></td>
<td>フルフィルメントサービス（FaaS）とのやり取りを必要とせずにAdobe Commerceを通じてフルフィルメントできる、Adobe Commerce Admin のバーチャルおよびダウンロード可能な商品をいくつか特定します。</td>
<td>ダウンストリームでの FaaS との競合を防ぐために、これらの製品は、書き出しで適切に削除またはフラグ付けされます。</td>
</tr>
</tbody>
</table>

### 注文キャンセルワークフロー

テスト計画のこのセクションには、Adobe Commerceを通じてキャンセルされた注文のエンドツーエンドのワークフローをテストするシナリオが含まれます。

**機能領域：** Adobe Commerce管理者 </br>
**役割：** エンドツーエンド（管理者、ストアの関連付け、顧客） </br>
**テスト結果のタイプ：** すべてのシナリオでプラス

<table style="table-layout:fixed">
<tr>
<th>関数</th>
<th>シナリオ</th>
<th>期待される結果</th>
</tr>
<tr>
<td><strong>完全な注文のキャンセル</strong></td>
<td><ol>
<li>注文する。</li>
<li>注文が同期されるまで待ちます。</li>
<li>請求書の作成を検証します（承認してキャプチャする場合）。請求書の E メールの受信。</li>
<li>請求書ビューで、すべての受注製品を使用してクレジット・メモを作成します。</li>
</ol>
</td>
<td>
<ul>
<li><code>We refunded $X online. Transaction ID: transactionID</code> とで注文履歴が更新されました <code>Received Cancel acknowledgment from the BOPIS solution.</code></li>
<li>注文ステータスは <code>Closed</code> です。 （支払いレビューを設定しました。）</li>
<li>Adobe Commerceで作成されたクレジットメモ。 （cron が動作するまで待ちます。</li>
<li>すべてのアイテムが選択された場合、[ 集荷の準備完了 ] E メール <code>DISPLAY COMMENT HISTORY</code> に <code>Order is ready for pickup</code> と表示されます（<code>CUSTOMER NOTIFIED</code> フラグは <code>true</code> です）。</li>
<li>すべての項目が選択されていない場合は、キャンセルメールおよびコメント履歴を表示 <code>Order has been canceled - all items were not available</code></li>
<li><code>CUSTOMER NOTIFIED</code> フラグは <code>true</code>）。</li>
</ul>
</td>
</tr>
<tr><td><strong>一部注文のキャンセル<strong></td>
<td>
<ol>
<li>少なくとも 2 つの製品で注文します。</li>
<li>注文が同期されるまで待ちます。</li>
<li>請求書が作成され（承認してキャプチャする場合）、請求書の電子メールが受信されたことを確認します。</li>
<li>トランザクションの決済まで 2 時間待ちます。</li>
<li>請求書ビューから受注製品の一部のみを使用してクレジット・メモを作成します。</li>
</td>
<td>
<ul>
<li>注文履歴の更新： <code>We refunded $X online. Transaction ID: transactionID</code></li>
<li>注文履歴の更新： <code>Order notified as partly canceled at: Date and Hour</code></li>
<li>注文の払い戻しメールの受信： <code>$x amount was refunded</code></li>
<li>注文ステータスは <code>Processing</code> です。</li>
<li>Adobe Commerceで作成されたクレジットメモ （cron が機能するまで待つ）。</li>
<li>一部の商品が選択されていない場合は、nil の選択または払い戻しセクションが記載された [!UICONTROL Ready for Pickup] ールメールが表示されていることを確認します。 <code>DISPLAY COMMENT HISTORY</code> は <code>Order is ready for pickup, but some items not available.</code> を示す。</li>
<li><code>CUSTOMER NOTIFIED</code> フラグは <code>true</code> です。</li>
</ul>
</td>
</tr>
<td><strong>集荷の準備完了 </br></br> 完全キャンセル </br> （すべての製品は数量 0 の集荷として設定されます）</strong></td>
<td>
<ol>
<li>注文します。</li>
<li>注文が同期されるまで待ちます。</li>
<li>請求書が作成され（承認してキャプチャする場合）、請求書の電子メールが受信されたことを確認します。</li>
<li>Postmanに移動し、<code>0 qty</code> で <code>picked</code> 定されたすべての商品を含む Ready for Pickup リクエストを実行します。</li>
</ol>
</td>
<td>
<ul>
<li>注文履歴が更新されました： <code>We refunded $X offline</code></li>
<li>注文ステータスは「<code>CLOSED</code>」です。
<li>クレジット・メモが作成されます。 （cron が動作するまで待ちます。</li>
<li>返金処理の電子メールが届きました： <code>$x amount was refunded</code></li>
<li>注文のキャンセル用メールが送信されました。</li>
</ul>
</td>
</tr>
<tr>
<td><strong> 集荷の準備完了 – 一部キャンセル </strong></br></br><strong> （一部の商品は集荷され、一部は <code>0 qty</code> で集荷される） </strong>
</td>
<td>
<ol>
<li>注文します。</li>
<li>注文が同期されるまで待ちます。</li>
<li>請求書が作成され（承認してキャプチャする場合）、請求書の電子メールが受信されたことを確認します。</li>
<li>Postmanに移動し、一部の商品が 0 数量でピッキング済みとしてセットされ、残りの商品がピッキング済みになっている状態で、Ready for Pickup リクエストを実行します。</li>
</ol>
</td>
<td>
<ul>
<li><code>Your order is ready for pickup</code> [!UICONTROL Ready for Pickup Items] テーブルと [!UICONTROL Canceled Items] テーブルを使用します。 </li>
<li>注文ステータスが集荷準備の状態です。 </li>
<li>注文履歴が更新されました：<code>We refunded $X offline.</code>
<li>注文履歴が更新されました：<code>Order notified as partly canceled at: Date and hour</code>
<li>返金処理の電子メールが届きました：<code>$x amount was refunded</code>
<li>クレジット メモが作成されます。 （cron が動作するまで待ちます。</li>
</ul>
</td>
</tr>
<tr>
<td><strong> 集荷準備完了 – 一部取消 </br></br> 一部の商品は集荷され、一部の商品は <code>0 qty</code> で集荷されます） </strong>
</td>
<td><ol>
<li>注文します。</li>
<li>注文が同期されるまで待ちます。</li>
<li>請求書が作成され（承認してキャプチャする場合）、請求書の電子メールが受信されたことを確認します。</li>
<li>Postmanに移動し、一部の商品が 0 数量でピッキング済みとしてセットされ、残りの商品がピッキング済みになっている状態で、Ready for Pickup リクエストを実行します。</li>
</ol>
</td>
<td><ul>
<li><code>Your order is ready for pickup</code> [!UICONTROL Ready for Pickup Items] テーブルと [!UICONTROL Canceled Items] テーブルを使用します。 </li>
<li>注文ステータスが集荷準備の状態です。 </li>
<li>注文履歴が更新されました：<code>We refunded $X offline.</code>
<li>注文履歴が更新されました：<code>Order notified as partly canceled at: Date and hour</code>
<li>返金処理の電子メールが届きました：<code>$x amount was refunded</code>
<li>クレジット メモが作成されます。 （cron が動作するまで待ちます。</li>
</ul>
</td>
</tr>
<tr>
<td><strong> 調剤（調剤中） </br></br> フルキャンセル（全商品が拒否に設定） </strong>
</td>
<td>
<ol>
<li>注文します。</li>
<li>注文が同期されるまで待ちます。</li>
<li>請求書が作成され（承認してキャプチャする場合）、請求書の電子メールが受信されたことを確認します。</li>
<li>Postmanに移動し、すべての商品がピッキング済みとして設定された状態で Ready for Pickup リクエストを実行します。</li>
<li>メールボックスを開き、Ready for Pickup のメールを見つけます。 次に、「**[!UICONTROL Confirm Arrival]**」をクリックします。</li>
<li>チェックインします。</li>
<li>Postmanに移動し、拒否されたとおりにすべての商品を指定して「調剤」リクエストを実行します。</li>
</ol>
<td><ul>
<li>注文履歴が更新されました： <code>We refunded $X offline.</code></li>
<li>返金処理の電子メールが届きました： <code>$x amount was refunded</code></li>
<li>状態が <code>CLOSED</code> に設定されました。</li>
<li>作成されたクレジット メモ。 （cron が動作するまで待ちます。</li>
</ul>
</td>
</tr>
<tr>
<td><strong> 調剤済み（調剤中） </br></br> 一部解除 </br> （調剤済み、不合格の製品あり） </strong>
</td>
<td>
<ol>
<li>注文します。</li>
<li>注文が同期されるまで待ちます。</li>
<li>請求書が作成され（承認してキャプチャする場合）、請求書の電子メールが受信されたことを確認します。</li>
<li>Postmanに移動し、すべての商品がピッキング済みとして設定された状態で Ready for Pickup リクエストを実行します。</li>
<li>メールボックスを開きます。 Ready for Pickup の電子メールを探し、<code>Confirm Arrival</code> を選択します。</li>
<li>チェックインします。</li>
<li>Postmanに移動し、調剤された商品と拒否された商品を含む調剤リクエストを実行します</li>
</ol>
</td>
<td>
<li>注文履歴が更新されました： <code>We refunded $X offline</code></li>
<li><code>Order notified as partly canceled at: Date and Hour</code>
<li>返金処理の電子メールが届きました：<code>$x amount was refunded</code>
<li>注文ステータスを <code>Ready for pickup Dispensed</code> に設定
<li>作成されたクレジット メモ。 （cron が動作するまで待ちます。</li>
</td>
</tr>
<tr>
<td> <strong> 返品後の新しい RMA （完全） </strong>
</td>
<td>
<ol>
<li>注文します。</li>
<li>注文が同期されるまで待ちます。</li>
<li>承認して取り込みオプションが設定されている場合は、請求書が作成され、お客様が請求書メールを受け取ったことを確認します。</li>
<li>Postmanですべての商品を選択します。</li>
<li>チェックインします。</li>
<li>調剤をしなさい。</li>
<li>order に移動し、select<strong>[!UICONTROL Create returns]=
<li>RMA を作成します。</li>
</ol>
</td>
<td>
<ul>
<li>RMA が作成され、[Order] ビューの [<strong>[!UICONTROL Returns]</b>] タブの下に表示されます。</li>
<li>顧客は RMA 確認メールを受信しました。</li>
</ul>
</td>
</tr>
<tr>
<td><strong> 再来訪後の新規 RMA – 一部 </strong>
</td>
<td>
<ol>
<li>注文します。</li>
<li>注文が同期されるまで待ちます。</li>
<li>請求書が作成され（承認してキャプチャする場合）、請求書の電子メールが受信されたことを確認します。</li>
<li>Postmanですべての商品を選択します。</li>
<li>チェックインします。</li>
<li>調剤をしなさい。</li>
<li>注文に進み、を選択します。  <strong>[!UICONTROL Create returns]</strong></li>
<li>注文した製品の一部を使用して RMA を作成します。</li>
</ol>
<td>
<ul>
<li>RMA が作成され、[Order] ビューの [<strong>[!UICONTROL Returns]</strong>] タブの下に表示されます。</li>
<li>顧客は RMA 確認メールを受け取った。</li>
<li>RMA を作成したら、RMA 認証を取得します。管理者から、<strong>[!UICONTROL Sales > Returns]</strong> に移動します。 作成した RMA を選択し、承認します。</li>
<li>お客様が RMA 認証確認メールを受信したことを確認します。</li>
<li>返金がトランザクションおよび注文履歴に追加されたことを確認します。</li>
</ul>
</td>
</tr>
</table>


### Store Fulfillment App の権限

テストプランのこのセクションでは、Store Fulfillment App ユーザーのアカウント管理について説明します。

- Store Associate が、Adobe Commerce管理者から作成された新しいユーザーアカウントを使用して認証できることを確認します。
- 既存のアカウントに対する更新が正常に適用されていることを確認します。

**機能領域：** Adobe Commerce管理者 </br>
**役割：** 管理者、ストアの関連付け </br>
**テストタイプ：** すべて陽性

<table style="table-layout:auto">
<tr>
<th>関数</th>
<th>シナリオ</th>
<th>期待される結果</th>
</tr>
<tr>
<td><strong> ユーザーアカウント管理 – アカウントの作成 </strong></br></br>
</td>
<td>
<ol>
<li><strong>Admin</strong> — Adobe Commerce Admin にログインします。</li>
<li><strong>[!UICONTROL System] / Store Fulfillment App Permissions / All Store Fulfillment App Users に移動します </strong></li>
<li><strong>新しいユーザーを追加します。</strong></li>
</ol>
<td>
<ul>
<li>アカウントが正常に作成されました。</li>
<li>新しいユーザーアカウントが [!UICONTROL Store Fulfillment Users] ダッシュボードに表示されます。</li>
<li><strong> ストア関連付け </strong> 新しいユーザーアカウントでストアアシストアプリにログインします。</li>
</ul>
</td>
</tr>
<tr>
<td><strong> ユーザーアカウント管理 – 既存のユーザーアカウントを更新 </strong>
</td>
<td>
<ol>
<li>管理者ユーザーアカウントでAdobe Commerce管理者にログインします。</li>
<li><strong>[!UICONTROL System] / Store Fulfillment App Permissions / All Store Fulfillment App Users</strong> に移動します。</li>
<li>ユーザーアカウント リストで、既存のアクティブなユーザーアカウントを選択して開 <strong>[!UICONTROL Edit]</strong> ます。
<li><strong>[!UICONTROL Is Active]</strong> を <strong> いいえ </strong> に変更して、アカウントを無効にします。</li>
</ol>
</td>
<td>
<ul>
<li><strong>[!UICONTROL Store Fulfillment App Users]</strong> ダッシュボードで、更新されたアカウントのステータスが <strong>[!UICONTROL Inactive]</strong> に変更されました。</li>
<li>ストアの関連付けは、非アクティブなアカウント資格情報ではストアアシストアプリにログインできません。</li>
</ul>
</td>
</tr>
</table>

## Adobe Commerceの製品タイプ

Adobe Commerce商品タイプのテストシナリオでは、様々な商品タイプに対して正しい商品、在庫、配信方法が顧客に表示されることを確認します。

- [!UICONTROL Configurable]
- [!UICONTROL Grouped]
- [!UICONTROL Virtual]
- Adobe Commerceのストアフロントに [!UICONTROL Bundle products] ります。

**機能領域：** Adobe Commerce フロントエンド </br>
**役割：** ストアシストアプリユーザー（ストアアソシエイト） </br>
**テストタイプ：** すべて陽性

<table style="table-layout:auto">
<tr>
<th>関数</th>
<th>シナリオ</th>
<th>コメント</th>
</tr>
<tr>
<td><strong> 設定可能な製品 </strong>
</td>
<td>
<ul>
<li>ユーザーが設定可能なオプション（有効なソース、在庫の割り当て済み）のみを表示できること、および在庫に一部の品目があることを確認します。子製品をチェックします。</li>
<li>別のストアを選択する際に、使用できないオプションが取り消し線で表示されていることを確認します。</li>
<li>ユーザーが別のストアを選択すると、設定可能なオプションの選択が解除されることを確認します。</li>
<li>設定可能な商品が既に買い物かごに入っていて、ユーザーが別のストアを選択した場合、その商品は在庫切れとして表示されることを確認します。</li>
</ul>
</td>
<td></td>
</td>
</tr>
<tr>
<td><strong> グループ化された製品 </strong>
</td>
<td>
<ul>
<li>すべての子製品に次の機能がある場合は、顧客の「配信方法と [!UICONTROL Add to cart]」ボタンが無効になっていることを確認します
<code>qty</code> を <code>0</code> に設定します。</li>
<li>少なくとも 1 つの子製品がに設定されている場合、顧客に対して配信方法が有効 <code>qty</code> なっていることを確認します <code>0.</code></li>
<li>メソッドが、有効になっ [!UICONTROL Store Pickup Delivery] いる製品に対してのみ表示され、アクティブで [!UICONTROL Available for Store Pickup] ることを確認します。 （子の製品を確認してください。）</li>
</ul>
</td>
<td></td>
</tr>
<tr>
<td><strong> バーチャル製品 </strong>
</td>
<td>
仮想製品が [!UICONTROL In-store Pickup] の配信方法を提供していないことを確認します。
<td></td>
</td>
</tr>
<tr>
<td><strong> バンドル製品 </strong>
</td>
<td>
<ul>
<li>少なくとも 1 つの子製品が無効になってい [!UICONTROL Available for Store Pickup] 場合、顧客が店舗での受け取り配信オプションを使用できないことを確認します。</li>
<li>少なくとも 1 つの子製品が無効になっ [!UICONTROL Available for Home Delivery] いる場合、顧客がホーム配信オプションを使用できないことを確認します。</li>
<li>バンドル内の子製品の少なくとも 1 つが在庫切れであるかどうかを確認します。バンドル（親製品）も表示されます
[!UICONTROL Out of stock] の通りです。</li>
</ul>
</td>
<td></td>
</tr>
<tbody>
</table>

## チェックイン操作

テスト計画のこのセクションでは、次の機能のストア ピックアップ注文のチェックイン エクスペリエンスについて説明します。

- 代替ピックアップ担当 – [!UICONTROL Alternate Pickup Contact] ータを追加し、ストア・ピックアップ受注の [!UICONTROL Preferred Contact] を選択するワークフローを検証します。

- チェックイン フォーム – ストアの集荷注文に対してチェックイン要求を送信するワークフローを確認します。

**機能領域：** 買い物かごのチェックアウト、店舗の受け取り注文のチェックインフォーム </br>
**役割：** 管理者、顧客、ストアの関連付け </br>
**テストタイプ：** すべて陽性

### 代替ピックアップ連絡先


**機能領域：** 買い物かごチェックアウト </br>
**役割：** 顧客 </br>
**テストタイプ：** すべて陽性

<table style="table-layout:auto">
<tr>
<th>関数</th>
<th>シナリオ</th>
<th>期待される結果</th>
</tr>
<tr>
<td><strong>代替ピックアップ連絡先 </br>
チェックイン<strong>
</td>
<td>
顧客が店舗内受け取りオプションを使用して注文を送信します。</td>
<td>チェックアウトプロセス中に、顧客は [!UICONTROL Alternate Pickup Contact] のオプションを出荷手順で確認できます。
</td>
</tr>
<tr>
<td><strong> 代替ピックアップ優先連絡先、チェックイン </strong>
<td>
顧客が店舗内受け取りオプションを使用して注文を送信します。 チェックアウト時に、顧客は [!UICONTROL Alternate Pickup Contact] を追加します。</td>
<td>チェックアウトプロセス中に、お客様には配送手順に [!UICONTROL Preferred Contact] のオプションが表示されます。</td>
</td>
</tr>
<tr>
<td><strong> 代替集荷連絡先詳細、チェックイン </strong>
</td>
<td>
顧客が店舗内受け取りオプションを使用して注文を送信します。 チェックアウト時に、顧客は出荷手順で [!UICONTROL Alternate Pickup Contact] を選択します。
</td>
<td>顧客には、連絡先の詳細（[!UICONTROL First name]、[!UICONTROL Last name]、[!UICONTROL Phone]、[!UICONTROL Email]）を入力するための入力オプションが表示されます。</td>
</tr>
<tr>
<td><strong> 代替受け取り、E メールでチェックイン </strong>
</td>
<td>顧客が店舗内受け取りオプションを使用して注文を送信します。 チェックアウト時に、顧客は出荷手順で [!UICONTROL Alternate Pickup Contact] を選択し、連絡先の詳細を追加して、注文を送信します。</td>
<td>顧客と代替担当者の両方が、注文のチェックイン E メールを受け取ります。</td>
</tr>
<td><strong>代替ピックアップ、オーダー詳細</strong></td>
<td>顧客が店舗内受け取りオプションを使用して注文を送信します。 チェックアウト時に、顧客は出荷手順で [!UICONTROL Alternate Pickup Contact] を選択し、連絡先の詳細を追加して、注文を送信します。</td>
<td>管理者には、保存された注文に関する追加の連絡先情報が表示されます。</td>
</tr>
<tr>
<td><strong> 代替集荷連絡先、店舗の関連付け注文ビュー </strong>
</td>
<td>顧客が店舗内受け取りオプションを使用して注文を送信します。 チェックアウト時に、顧客は出荷手順で [!UICONTROL Alternate Pickup Contact] を選択し、連絡先の詳細を追加して、注文を送信します。</td>
<td>Store Associate は、注文に関する追加の連絡先情報を FaaS/ChaS で確認できます。</td>
</td>
</tr>
</tbody>
</table>

### チェックインフォーム


**機能領域：** チェックインフォーム </br>
**役割：** 顧客 </br>
**テストタイプ：** すべて陽性

<table style="table-layout:auto">
<tr>
<th>関数</th>
<th>シナリオ</th>
<th>期待される結果</th>
</tr>
<tr>
<td><strong> チェックイン処理 – 要求の送信 </strong>
</td>
<td>チェックインフォームで、顧客はすべての必須フィールドに入力し、リクエストを送信します。</td>
<td>顧客が成功応答を受信します。</td>
</tr>
<tr>
<td><strong>「チェックイン」アクション – リクエストの詳細を表示します</strong></td>
<td>顧客がチェックイン要求を正常に送信した。</td>
<td>FaaS システムで注文ステータスが更新され、ストアの関連付け担当者は FaaS でチェックイン要求の詳細を確認できます。
</td>
</tr>
<tr>
<td><strong>「チェックイン」アクション – リクエストを 1 回だけ送信します。</strong></td>
<td>注文のチェックイン要求を送信した後、顧客は再度チェックインするリンクを選択します。</td>
<td>チェックインフォームには、フォームを編集または再送信するオプションは表示されません。</td>
</tr>
<tr>
<td><strong>チェックイン動作 – 到着を確認</strong></td>
<td>FaaS では、店頭での集荷注文は集荷準備完了としてマークされます。 顧客は Ready for Pickup のメールを受け取り、[!UICONTROL Confirm Arrival] を選択します。</td>
<td>顧客には、注文のチェックインフォームが表示されます。</td>
</tr>
</tbody>
</table>

## ストアシストアプリ

テスト計画のこの節では、ストアアシストアプリで注文、選択、およびハンドオフのワークフローをテストするシナリオについて説明します。

**機能領域：** ストアシストアプリ </br>
**役割：** ストアの関連付け </br>
**テストタイプ：** すべて陽性

<table style="table-layout:auto">
<tr>
<th>関数</th>
<th>シナリオ</th>
<th>期待される結果</th>
</tr>
<tr>
<td>
<strong>1 回の注文でピッキングする – Happy Path、Curbside Picking</strong></td>
<td>単一数量および複数数量の品目をピックします。 ニルの選択および縁側の選択は行われません（ステージングを使用）。
</td>
<td>
</td>
</tr>
<tr>
<td><strong>複数注文のピッキング – ハッピーパス、カーブサイドのピックアップ</strong></td>
<td>単一および複数数量の品目 ニル・ピックおよび縁側ピックなし（ステージング時）</td>
<td></td>
</tr>
<tr>
<td><strong>1 回の注文で商品を受け取る</strong></td>
<td>単一および複数数量の品目 ニルの選択および店舗でのピックアップは行われません（ステージングを使用）</td>
<td>
</td>
</tr>
<tr>
<td><strong>複数注文のピッキング – ハッピーパス、店舗でのピックアップ</strong></td>
<td>単一数量および複数数量の品目をピックします。 ニルの選択および縁側の選択は行われません（ステージングを使用）。</td>
<td></td>
</tr>
<tr>
<td><strong>1 回の注文ピッキング – 満足できないパス、店舗での受け取り</strong></td>
<td>部分ピッキングおよびピッキングと店舗内集荷による単一品目および複数数量品目のピック（ステージングを使用）</td>
</td>
<td></td>
</tr>
<td><strong>複数注文のピッキング – 満足できないパスカーブサイドのピックアップ</strong></td>
<td>部分ピッキングおよびピッキングと店舗内集荷による単一品目および複数数量品目のピック（ステージングを使用）</td>
<td></td>
</tr>
<td><strong>1 回の注文でピッキングする – 満足できないパス、カーブサイドのピックアップ</strong></td>
<td>部分取り出しおよび非点弧取り出しを使用した単一品目および複数数量品目のピック（ステージングを使用）</strong></td>
</td>
<td></td>
</tr>
<tr><td><strong>注文 – ピッキング前にキャンセル</strong></td>
<td></td>
<td></td>
</tr>
<tr>
<td><strong>注文 – ハンドオフ前にキャンセル</strong></td>
<td></td>
<td></td>
</tr>
<tr>
<td><strong>注文 – 注文モジュールを検索</strong></td>
<td></td>
<td></td>
</tr>
<tr><td><strong>注文 – 検索とハンドオフのための手動チェックイン</strong></td>
<td></td>
<td></td>
</tr>
<tr><td><strong>注文済み – すべての品目が選択されているか、ピッカーによってマークされていない</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>バンドル品目で発注 – ピッキングおよびハンドオフ</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>注文が行われました – 拒否を含む受け渡し</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>注文 – すべての品目を拒否して引き渡します</strong></td>
<td></td>
<td></td></tr>
</tbody>
</table>

## デプロイ

ソリューションが設定され、仕様に合わせてテストされたことを確認したら、ステージング環境から実稼動環境にデプロイする準備が整います。

デプロイメントとテストは、インフラストラクチャと機能によって異なります。

>[!TIP]
>
>クラウドインフラストラクチャプロジェクトでのAdobe Commerceのデプロイメントのガイドライン、チェックリスト、ベストプラクティスについては、Adobe Commerce開発者向けドキュメントの [ ストアのデプロイ ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/deploy/staging-production) を参照してください。
