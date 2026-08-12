---
title: Web サイトの別のPayPal アカウントを接続する
description: Web サイトを対象としたPayPalのオンボーディングを管理画面で完了して、別のPayPal加盟店アカウントを個々のweb サイトに接続します。
role: Admin, User
level: Intermediate
feature: Payments, Checkout, Configuration, Paas, Saas
TQID: 'https://experienceleague.adobe.com/U1zGAU6vYKjk2tc2KXnvyqnYdbA2HKTCNZSKhHdS0Vw'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
source-git-commit: d754c71e287d7d9ff297dd7d95efbaaae7ffc2fc
workflow-type: tm+mt
source-wordcount: 393
ht-degree: 0%

---

# Web サイトの別のPayPal アカウントを接続する

**複数のweb サイト**&#x200B;を持つCommerce インスタンスの場合、**異なるPayPal マーチャント アカウント**&#x200B;が必要になる場合があります。 [!DNL Payment Services]では、**グローバル**&#x200B;のオンボーディング後、**web サイト範囲**&#x200B;のPayPal オンボーディングを有効にします。

>[!NOTE]
>
> この機能は、新規アカウントの接続のみをサポートします。

## web サイトを対象としたオンボーディングの前提条件

web サイトレベルのオンボーディングは、ストアが以下の要件を満たしている場合にのみ利用可能です。

- [Commerce Services Connector](https://experienceleague.adobe.com/ja/docs/commerce/user-guides/integration-services/saas)のセットアップが完了しました。
- PayPal アカウントは、グローバル（デフォルト設定）スコープで接続されます。

これは、次のフィールドがデフォルトのスコープに入力されていることを確認することで確認できます。

- [!UICONTROL Payment Services Sandbox ID]
- [!UICONTROL Payment Services Production ID]
- [!UICONTROL PayPal Merchant ID]

これらのフィールドが空の場合は、最初に[&#x200B; グローバルオンボーディングを完了](configure-admin.md)する必要があります。 前提条件を完了するまで、**[!UICONTROL Connect different account]** ボタンは無効になります。

## web サイトレベルの接続を開始

1. _管理者_ サイドバーで、**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Sales]**&#x200B;に移動し、**[!UICONTROL Payment Methods]**&#x200B;を選択します。
1. 左上隅の範囲セレクターで、オンボーディングする&#x200B;**[!UICONTROL Default Config]**&#x200B;から&#x200B;**[!UICONTROL Website]**&#x200B;に切り替えます。
1. **[!UICONTROL Connect different account]**&#x200B;をクリックします。

   ボタンが無効になっている場合、ストアは上記の[前提条件](#prerequisites-global-scope)を満たしていません。

## オンボーディングモーダルの完了

ポップアップウィンドウが開きます。

1. ドロップダウンから&#x200B;**[!UICONTROL Country]**&#x200B;を選択します。
1. オンボーディングの種類を選択：**[!UICONTROL Basic]**&#x200B;または&#x200B;**[!UICONTROL Advanced]**。
1. **[!UICONTROL Next]**&#x200B;をクリックします。

>[!NOTE]
>
> ハンガリー、スペイン、またはオーストリアでオンボーディングする場合は、**[!UICONTROL I Accept]** ボタンをクリックする前に、利用条件リンクを開いて表示する必要があります。 このボタンは、利用条件を開くまで無効になっています。

## PayPalにログイン

PayPal ログインにリダイレクトされたら、ログインしてPayPal内のオンボーディング手順を完了します。

>[!IMPORTANT]
>
> **[!UICONTROL Confirm and Continue]**&#x200B;をクリックすると、グローバルスコープのセッションが終了し、web サイトレベルの接続が開始されます。 誤って&#x200B;**[!UICONTROL Connect different account]**&#x200B;をクリックした場合は、確認する前に&#x200B;**[!UICONTROL Cancel]**&#x200B;を選択するか、**X** アイコンをクリックしてキャンセルできます。

## 終了して管理者に戻る

1. PayPalの手順を完了したら、PayPal ウィンドウを閉じます。
1. **[!UICONTROL Finish]**、または右上隅の&#x200B;**X**&#x200B;をクリックして、オンボーディングポップアップを閉じます。
1. Commerce設定ページが自動的に更新されます。

## 結果を確認

ページが更新されたら、web サイトのスコープ設定ページで次のことを確認します。

- そのweb サイトの&#x200B;**[!UICONTROL PayPal Merchant ID]**&#x200B;が更新されました。
- オンボーディングの結果を示すステータスラベル：

| ステータス | 意味 |
| --- | --- |
| `ACTIVE` | オンボーディングが完了しました |
| `PENDING` | オンボーディングはまだ処理中です |
| `ERROR` | オンボーディングが正常に完了しませんでした |

`ERROR` ステータスが表示された場合、問題を説明するエラーメッセージが表示されます。 もう一度&#x200B;**[!UICONTROL Connect different account]**&#x200B;をクリックして、オンボーディングプロセスを再試行できます。
