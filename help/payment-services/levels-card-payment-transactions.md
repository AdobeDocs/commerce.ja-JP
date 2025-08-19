---
title: レベル 2 およびレベル 3 の処理
description: トランザクション内のカード支払  [!DNL Payment Services]  処理レベル。
role: Admin
feature: Payments, Paas, Saas
exl-id: db8993fe-dd6f-48b5-9e7b-69a0f2e08552
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# レベル 2 およびレベル 3 の処理

[!DNL Payment Services] は、マーチャントが支払いトランザクションを最適化し、交換手数料を削減するのに役立つ高度なカード処理機能を提供します。 カード処理には 3 つのレベルがあり、それぞれトランザクションデータの要件が異なります。

>[!CAUTION]
>
> [Fastlane](payments-options.md#fastlane-button) 注文には、レベル 2/レベル 3 のデータ、品目、金額の内訳は含まれません。

## 処理レベルごとのデータ要件

![ 取引報告書 ](assets/level-processing-details.png){width="500" zoomable="yes"}

[!DNL Payment Services] はこのデータを収集し、支払いトランザクションの詳細なレポートを提供します。

## カードネットワーク別の利用可能な処理レベル

![ カードの詳細 ](assets/cards-details-level-processing.png){width="500" zoomable="yes"}

詳しくは、PayPal Developer ドキュメントの [ 支払い処理 ](https://developer.paypal.com/docs/checkout/advanced/processing/){target=_blank} を参照してください。

### 第一級

レベル 1 は最も一般的であり、必要な情報は少ないため、一般に、レベル 2 またはレベル 3 のデータで処理される取引（通常は企業のクレジットカードやクレジットカードの購入に関連する取引）と比べて、高い交換手数料が発生します。

### レベル 2 およびレベル 3

Interchange Plus （IC++）の [!DNL Payment Services] マーチャントは、カード ネットワークに追加のトランザクションの詳細を提供し、特定の認定基準を満たす場合、レベル 2/レベル 3 の処理の対象となる可能性があります。 これらのレベルは、大幅なコスト削減につながる可能性があるため、大量の購入や名刺を扱うマーチャントにとって特に有益です。 詳細なレベル 2 またはレベル 3 のデータを提供すると、次のことが可能です。

* 処理手数料の削減と全体的なコストの最適化
* 不正の防止、プロセッサ・リスクの軽減
* トランザクションセキュリティの強化

[IC とは++？を参照詳しくは、PayPal 開発者向けドキュメントを ](https://www.paypal.com/us/brc/article/what-is-interchange-plus-plus){target=_blank} 照してください。

## [!DNL Payment Services] におけるレベル 2 およびレベル 3 のカード支払トランザクション

レベル 2 またはレベル 3 の処理の対象となるためには、マーチャントは以前の情報を送信する必要がありますが、それは、トランザクションを処理する際に対象となるレベルを最終的に決定するのはカードネットワークです。

詳しくは、PayPal 開発者向けドキュメントの [ 支払い処理に関する FAQ](https://www.paypal.com/us/cshelp/article/ts2278?_ga=1.131773126.875104296.1712843492){target=_blank} を参照してください。

レベル 2 およびレベル 3 の処理は、ストアレベルの [!DNL Payment Services] マーチャントに対して、デフォルトで無効になっています。

既に IC++の価格設定を使用している場合は、レベル 2 およびレベル 3 の処理を利用できます。 この機能を有効にするには、[ コマンドラインインターフェイス（CLI](configure-cli.md) を使用します。

>[!IMPORTANT]
>
>ご不明な点は [!DNL Payment Services] 担当のアカウントマネージャーにお問い合わせください。
