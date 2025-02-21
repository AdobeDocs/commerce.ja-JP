---
title: 販売 E メール テンプレート
description: 店舗集荷注文のフルフィルメントプロセス中に、顧客および店舗管理者と通信するためのトランザクションメールテンプレートを設定します。
role: Admin
level: Intermediate
feature: Shipping/Delivery, Communications, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 1%

---


# 販売 E メール テンプレート

ストアフルフィルメントでは、注文とフルフィルメントのワークフローをサポートするために、トランザクションメールテンプレートの拡張セットを提供します。 注文ステータスの変更や店舗での受け取り注文の手順などを顧客および店舗管理者に通知するなど、チャネル間で一貫性のある自動化されたコミュニケーションとメッセージングを提供します。

ストアフルフィルメントのメールテンプレートは、デフォルトのメッセージと設定で設定されます。 Adobe Commerceのマーチャント管理者は、設定を管理および変更し、様々なシナリオで顧客と通信するためのメールテンプレートを選択できます。 管理者は、テンプレートを設定およびカスタマイズすることもできます。

Admin: **[!UICONTROL Stores > Configuration > Sales > Sales Emails]** から Sales Email テンプレートを構成します。

## メール – 一般設定

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
<td><strong>非同期送信</strong></td>
<td>販売 E メールを非同期で送信するかどうかを決定します。 Options: <br/>**'Disable'** - （デフォルト）イベントによってトリガーされたときに販売メールが送信されます。 ストアピックアップの通信時間と応答時間を最速にするには、デフォルト設定を使用します。 <br/>**'Enable'** – このオプションを有効にすると、チェックアウトおよび注文処理を行うメール通知をバックグラウンドで処理するプロセスが、事前に決められた一定の間隔で送信されるようになります。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
</tbody></table>

## 店舗での受け取り準備完了の注文

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
<td><strong>Enabled</strong></td>
<td>このメールは、店員が注文のピッキングを完了したときに顧客に送信されます。 メール通知を無効にするには、「いいえ」に設定します。 メールテンプレートが無効になっている場合でも、店舗担当者による注文のピッキングは妨げられません。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>集荷用 E メール送信者用注文の準備完了</strong></td>
<td>メール通知を送信する際に使用される送信者の ID。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>集荷準備完了の注文 E メール テンプレート</strong></td>
<td>登録済みの顧客に通知するために使用されるメールメッセージテンプレート。 統合にはデフォルトのテンプレートが用意されています。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<td><strong>集荷準備完了の注文 E メール テンプレート （ゲスト用）</strong></td>
<td>ゲスト顧客に通知するために使用されるメールメッセージテンプレート。 統合にはデフォルトのテンプレートが用意されています。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>別の集荷連絡先用の集荷準備完了の注文 E メール テンプレート</strong></td>
<td>注文で名前が付いた追加の連絡先に通知するために使用されるメールメッセージテンプレート。 統合にはデフォルトのテンプレートが用意されています。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>集荷準備完了の注文を E メール コピーで次の場所に送信</strong></td>
<td>各通知のコピーを送信するメールアドレスのコンマ区切りのリスト。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>集荷準備完了の注文を送信する E メールのコピー方法</strong></td>
<td>使用する電子メールコピー方法（カーボンコピー）。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
</tbody></table>


## 注文が店舗で受け取られました

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
<td><strong>Enabled</strong></td>
<td>このメールは、顧客がストアから注文を受け取ったことを確認する際に顧客に送信されます。 メール通知を無効にするには、「いいえ」に設定します。 メールテンプレートが無効になっている場合でも、顧客による注文の受け取りは妨げられません。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>注文が集荷されたメールの送信者</strong></td>
<td>メール通知を送信する際に使用される送信者の ID。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>注文が受け取られたメールテンプレート</strong></td>
<td>登録済みの顧客に通知するために使用されるメールメッセージテンプレート。 統合にはデフォルトのテンプレートが用意されています</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<td><strong>注文が集荷されましたゲスト向けメールテンプレート</strong></td>
<td>ゲスト顧客に通知するために使用されるメールメッセージテンプレート。 統合にはデフォルトのテンプレートが用意されています。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>送信が E メールで次の場所にコピーされました：</strong></td>
<td>各通知のコピーを送信するメールアドレスのコンマ区切りのリスト。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>送信がメールコピー方式でピックアップされました</strong></td>
<td>使用する電子メールコピー方法（カーボンコピー）。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
</tbody></table>

## 注文の遅延

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
<td><strong>Enabled</strong></td>
<td>このメールは、マーチャントストアでの注文の処理またはピッキングの遅延を通知するために顧客に送信されます。 メール通知を無効にするには、「いいえ」に設定します。 メールテンプレートが無効な場合、この機能を使用しても注文の遅延は回避できません。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>注文の遅延メール送信者
</strong></td>
<td>メール通知を送信する際に使用される送信者の ID。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>注文遅延メールテンプレート</strong></td>
<td>登録済みの顧客に通知するために使用されるメールメッセージテンプレート。 統合にはデフォルトのテンプレートが用意されています。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<td><strong>ゲスト用の注文遅延メールテンプレート</strong></td>
<td>ゲスト顧客に通知するために使用されるメールメッセージテンプレート。 統合にはデフォルトのテンプレートが用意されています。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>注文遅延 E メールコピーの送信先</strong></td>
<td>各通知のコピーを送信するメールアドレスのコンマ区切りのリスト。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>注文遅延コピーの送信方法</strong></td>
<td>使用する電子メールコピー方法（カーボンコピー）。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
</tbody></table>



## キャンセル済みの注文

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
<td><strong>Enabled</strong></td>
<td>このメールは、マーチャントストアでの注文がキャンセルされたことを通知するために顧客に送信されます。 <code>No</code> に設定すると、メール通知が無効になります。 メールテンプレートが無効になっている場合、この機能を使用しても注文がキャンセルされることはありません。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>注文をキャンセルしたメールの送信者
</strong></td>
<td>メール通知を送信する際に使用される送信者の ID。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>注文がキャンセルされたメールテンプレート</strong></td>
<td>登録済みの顧客に通知するために使用されるメールメッセージテンプレート。 統合にはデフォルトのテンプレートが用意されています。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<td><strong>ゲストの注文がキャンセルされました</strong></td>
<td>ゲスト顧客に通知するために使用されるメールメッセージテンプレート。 統合にはデフォルトのテンプレートが用意されています。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>注文のキャンセル済み E メールのコピーの送信先</strong></td>
<td>各通知のコピーを送信するメールアドレスのコンマ区切りのリスト。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>Send Order Cancelled Copy メソッド</strong></td>
<td>使用する電子メールコピー方法（カーボンコピー）。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
</tbody></table>


## オーダーが一部取り消されました

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
<td><strong>Enabled</strong></td>
<td>このメールは、注文の一部がマーチャントストアでキャンセルされたことを通知するために顧客に送信されます。 <code>No</code> に設定すると、メール通知が無効になります。 メールテンプレートが無効になっている場合でも、注文が部分的にキャンセルされます。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>注文が部分的にキャンセルされたメール送信者
</strong></td>
<td>メール通知を送信する際に使用される送信者の ID。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>注文が部分的にキャンセルされたメールテンプレート</strong></td>
<td>登録済みの顧客に通知するために使用されるメールメッセージテンプレート。 統合にはデフォルトのテンプレートが用意されています。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<td><strong>代替集荷連絡先用の注文の一部取り消し E メール テンプレート</strong></td>
<td>注文で名前が付いた追加の連絡先に通知するために使用されるメールメッセージテンプレート。 統合にはデフォルトのテンプレートが用意されています。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>ゲストの注文が一部取り消されました</strong></td>
<td>ゲスト顧客に通知するために使用されるメールメッセージテンプレート。 統合にはデフォルトのテンプレートが用意されています。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>注文の一部がキャンセルされた E メールのコピーの送信先</strong></td>
<td>各通知のコピーを送信するメールアドレスのコンマ区切りのリスト。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>注文の一部がキャンセルされたコピー方法の送信</strong></td>
<td>使用する電子メールコピー方法（カーボンコピー）。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
</tbody></table>

## 出荷先店舗

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
<td><strong>注文に出荷先商品のメール送信者がある</strong></td>
<td>在庫が使用可能になるまで商店でピッキングできないすべてのオープン注文の集計レポートとして、指定した販売員に送信される E メール。 </br></br> マーチャントはこのレポートを使用して、店舗間の在庫移動または補充を開始および管理できます。 </br></br> この通知は、[!DNL Ship-to-Store] 機能が有効な場合にのみ適用されます。
</br></br> このラベルは、選択した配送業者や使用可能な配送方法のラベルには影響しません。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>出荷先店舗の E メール受信者</strong></td>
<td>各通知のコピーを送信するメールアドレスのコンマ区切りのリスト。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
<tr>
<td><strong>E メール テンプレート</strong></td>
<td>受信者への通知に使用するメールメッセージテンプレート。 統合にはデフォルトのテンプレートが用意されています。</td>
<td>ストア表示</td>
<td>不可</td>
</tr>
</tbody></table>

>[!NOTE]
>
>バックオーダーを許可する場合は、これらのオーダーに関する通知を受信するための管理者メールアドレスを指定する必要があります。 住所を次の設定に追加します。[ 注文遅延 ](#order-delayed) テンプレートの **[!UICONTROL Send Order Delayed Email Copy To]**、および [ 出荷先店舗 ](#ship-to-store) テンプレートの [!UICONTROL Ship To Store Email Recipients]。



