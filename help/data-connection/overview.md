---
title: ガイドの概要
description: 拡張機能を使用してAdobe Commerce データをAdobe Experience Platformと統合する方法  [!DNL Data Connection]  説明します。
recommendations: noCatalog
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1762'
ht-degree: 0%

---

# [!DNL Data Connection] の概要

>[!IMPORTANT]
>
>Experience Platform コネクタの名前は [!DNL Data Connection] に変更されました。

[!DNL Data Connection] 拡張機能は、Adobe Commerce web インスタンスをAdobe Experience PlatformとEdge Networkに接続します。 モバイルアプリ開発者は、CommerceでAdobe Experience Platform Mobile SDKを使用して、Commerce データを取得し、Experience Platformに送信します。 [ 詳細情報 ](./mobile-sdk-epc.md)。

Commerce ストアには、大量のデータが含まれています。 買い物客がサイト上の製品を参照、表示、最終的に購入する方法に関する情報を入手することで、よりパーソナライズされたショッピングエクスペリエンスを作成する機会が明らかになります。 そのデータは、買い物かごの価格ルールや動的ブロックなどのCommerceのネイティブ機能に情報を提供できますが、Commerce インスタンスではデータがサイロ化されたままになります。

Adobe Experience Platformは、Commerce ストアからのデータを取り込むと、そのデータをEdge Networkを通じて他のAdobe DX 製品に配信し、買い物客の購買行動に関するインサイトを得ることができる一連のテクノロジーを提供します。 これらの深いインサイトを使用すると、すべてのチャネルにわたって、よりパーソナライズされたショッピングエクスペリエンスを作成できます。

次の図は、[!DNL Data Connection] 拡張機能がインストールおよび設定されている場合の、ストアから他のAdobe DX 製品へのCommerce データのフローを示しています。

![Experience Platform エッジへのデータのフロー ](assets/commerce-edge.png)

上記の画像では、行動、バックオフィスおよび顧客プロファイルデータが、SDK、API およびソースコネクタを使用してExperience Platform Edge に送信されます。 拡張機能がデータ共有の複雑さを処理するので、これらの要素の仕組みを完全に理解する必要はありません。 イベントデータがエッジにある場合は、そのデータを他のExperience Platform アプリケーションに取り込むことができます。 例：

| 用途 | 目的 | ユースケース |
|---|---|---|
| [Adobe [!DNL Real-Time CDP]](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=ja) | プロファイル管理およびセグメント化サービス | **購入履歴のセグメント化**：マーチャントは、特定の期間（毎月、四半期、毎年など）に基づいて商品を購入した顧客を識別できます。 マーチャントは、これらの顧客のセグメントを作成し、それらをプロモーションやキャンペーンのターゲットに設定したり、購読サービスのリードの _ファネルの一番上_ データとして <br> ターゲットに設定したりできます。 **カテゴリベースのセグメント化**：マーチャントは、購入された製品のカテゴリを確認できます。<br> **オファリングベースのセグメント化**：マーチャントは、製品を一貫して返す顧客を識別できます。 彼らに与えられるオファーと割引は、よりインテリジェントになりました。 例えば、常に商品を返品する顧客の場合は、送料無料を削除できます。<br> **類似ターゲティング**:_類似オーディエンス_ は、マーチャントがプロモーションのために採用する手法で、既存の顧客と類似の特性を共有するので、ビジネスに興味を持つ可能性が高い新しい人物にリーチします。 行動データとトランザクションデータに基づいて、類似セグメントを作成できます。<br> **顧客の傾向**：顧客の行動の変化は、トランザクションデータから作成できる、より深い顧客プロファイルの結果として識別できます。 製品の返品数や製品設定などの計算に流入するデータが多くなるため、傾向スコアの信頼性が高くなります。<br> **クロスセル**：マーチャントは、Commerceで取得したきめ細かい情報から、強力なクロスセルおよびアップセルの機会を特定できます。 |
| [ 顧客  [!DNL Journey Analytics]](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html) | Commerce ジャーニー全体の詳細な分析 | **季節的なトレンド**：特定の商品の需要の周期的な変化に備えるのに役立つ、季節的なトレンドを特定できます。 また、マーチャントは、何年にもわたってあらゆる製品の全体的な人気の変化を特定できます。<br> **コンバージョン分析**：製品の購入時期を把握し、ストアフロントのインプレッションイベントにアクセスできるので、マーチャントは顧客の豊富なプロファイルを生成してコンバージョン分析を実行できます。 |
| [Adobe [!DNL Analytics]](https://experienceleague.adobe.com/docs/analytics/analyze/admin-overview/analytics-overview.html) | 顧客の行動とキャンペーンのパフォーマンスの詳細な分析 | **注文返品**：マーチャントは、製品を返品するパターンを持つ顧客や大規模な顧客セグメントを識別できます。 これにより、マーチャントは顧客ベースの行動がどのようなものかを理解できるので、コマース戦略を改善できます <br>。 **注文住所**：配送先住所に基づいて、マーチャントは、注文が顧客自身によって行われているかどうか、または別の個人またはエンティティに対するものかどうかを理解できます。<br> **季節性トレンド**：ある業者は季節性のトレンドを特定し、特定の製品の需要の周期的な変化に備えるのに役立ちます。 また、マーチャントは、何年にもわたってあらゆる製品の全体的な人気の変化を特定できます。<br> **コンバージョン分析**：製品の購入時期を把握し、ストアフロントのインプレッションイベントにアクセスできるので、マーチャントは顧客の豊富なプロファイルを生成してコンバージョン分析を実行できます。 **メモ** Adobe Analyticsでは、行動（ストアフロント）イベントデータのみをサポートしています。 Adobe Analyticsはトランザクション（backoffice）イベントデータをサポートしていません。 |
| [Adobe [!DNL Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html) | チャネルをまたいだキャンペーンオーケストレーション | **行動ベースのジャーニー**：マーチャントは、2 年前に携帯電話を購入した顧客を、新しいモデルの購入を提案することでターゲットにすることができます。 マーチャントは、これらの顧客に対してパーソナライズされたキャンペーンやプロモーションを作成し、メールや SMS 機能を使用して連絡を取ることができます。 また、マーチャントは、履歴の順序と行動データを使用してトレンドを特定できます。 例えば、過去に特定の設定を持つ品目を購入し、現在は同じ製品を再度購入しようとしている顧客は、同じ製品設定を表示してアクセスできるようにすることで、購入ジャーニーを強化できます。<br> **Personalization**：顧客プロファイル情報にアクセスでき [!DNL Journey Optimizer] と、高度にパーソナライズされたジャーニーのロックを解除でき、マーチャントは複数の異なるチャネルで顧客に連絡できます。<br> **新しいプロファイルが作成されました**：ようこそメールとプロモーションアクティビティは、買い物のジャーニーで新規顧客を奨励し、影響を与えることができます。<br> **プロファイル削除**：マーチャントは、アカウントを閉鎖したクライアントへのプロモーションメールの送信を停止することを選択できます。 また、マーチャントは、失われた顧客を取り戻すためにキャンペーンを構築することもできます。 |

## Experience Platform データのCommerceへの取り込み

[!DNL Data Connection] 拡張機能を使用してCommerce データをExperience Platformに送信することは、Commerceのデータ共有機能の 1 つの側面です。 もう一方のサイド（オプションの拡張機能）は、[Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html) と呼ばれます。 この拡張機能を使用すると、Real-Time CDPでオーディエンスを作成し、それらのオーディエンスをCommerce ストアにデプロイして、買い物かごの価格ルール、関連する商品ルール、動的ブロックを知らせることができます。

大まかに言えば、Commerce ストアからExperience Platformに送られ、Audience Activation拡張機能を介して戻されるデータのフローは、次のようになります。

![[!DNL Data Connection] フロー ](assets/data-connection.png)

CommerceとCommerceの間およびExperience PlatformとExperience Platformの間の接続を設定すると、データは引き続きフローされます。 アップグレードで再接続が必要になる場合を除き、再接続の必要はありません。

## 概念

これらの 2 つのシステム間でデータを共有するには、いくつかの概念を理解している必要があります。

- **データ** - Experience Platformと共有されるデータは、ストアフロントのブラウザーイベント、サーバーのバックオフィスイベント、プロファイルレコードデータから収集されたデータです。 ストアフロントイベントは、サイトでの買い物客のインタラクションからキャプチャされ、[`addToCart`](events.md#addtocart)、[`pageView`](events.md#pageview)、[`createAccount`](events.md#createaccount)、[`editAccount`](events.md#editaccount)、[`startCheckout`](events.md#startcheckout)、[`completeCheckout`](events.md#completecheckout)、[`signIn`](events.md#signin)、[`signOut`](events.md#signout) などのイベントが含まれます。 ストアフロントイベントの完全なリストについては、[ ストアフロントイベント ](events.md#storefront-events) を参照してください。 サーバーサイドまたはバックオフィスイベントには、[`orderPlaced`](events-backoffice.md#orderplaced)、[`orderReturned`](events-backoffice.md#orderitemreturncompleted)、[`orderShipped`](events-backoffice.md#ordershipmentcompleted)、[`orderCancelled`](events-backoffice.md#ordercancelled) などの [ 注文ステータス ](events-backoffice.md#order-status) 情報が含まれます。 バックオフィスイベントの完全なリストについては、[ バックオフィスイベント ](events-backoffice.md) を参照してください。 プロファイルレコードデータには、新しいプロファイルが作成、更新または削除された際の情報が含まれています。 詳しくは、[ プロファイルレコードデータ ](events-profilerecord.md) を参照してください。

- **Experience PlatformとEdge Network** – ほとんどのAdobe DX 製品のデータウェアハウスです。 Experience Platformに送信されたデータは、Experience Platform Edge Networkを通じてAdobe DX 製品に伝播されます。 例えば、Journey Optimizerを起動し、特定のCommerce イベントデータをエッジから取得し、放棄された買い物かごメールをJourney Optimizerに作成できます。 Journey Optimizerは、Commerce ストアに放棄された買い物かごがある場合に、そのメールを送信できます。 [Experience PlatformとEdge Network](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/overview.html) の詳細をご覧ください。

- **スキーマ** - スキーマは、送信されるデータの構造を記述します。 Experience PlatformがCommerce データを取り込む前に、データ構造を記述するスキーマを作成し、各フィールドに含めることができるデータのタイプに制約を指定する必要があります。 スキーマは、基本クラスと 0 個以上のスキーマフィールドグループで構成されます。 このスキーマは、すべてのAdobe DX 製品が読み取り可能な XDM 構造を使用します。 これにより、Experience Platformに送信されたデータは、すべての DX 製品で確実に理解されます。 詳しくは、[ スキーマ ](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html) を参照してください。

- **データセット** - データのコレクションのためのストレージと管理の構成体。通常、スキーマ（列）とフィールド（行）を含むテーブル。 データセットには、保存するデータの様々な側面を記述したメタデータも含まれます。 Adobe Experience Platformに正常に取り込まれたすべてのデータは、データセットに含まれています。 [ データセット ](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html) の詳細情報。

- **データストリーム** - Adobe Experience Platformから他のAdobe DX 製品にデータを送信できるようにする ID。 この ID は、特定のAdobe Commerce インスタンス内の特定の web サイトに関連付ける必要があります。 このデータストリームを作成する場合は、上記で作成した XDM スキーマを指定します。 詳細情報：[ データストリーム ](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html)。

## サポートされるアーキテクチャ

[!DNL Data Connection] 拡張機能は、次のアーキテクチャで使用できます。

- PHP/Luma
- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/integrations/adobe-commerce/aep/)
- [AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/aep.html)

>[!BEGINSHADEBOX]

## 前提条件

[!DNL Data Connection] 拡張機能を使用するには、次の要件を満たす必要があります。

- Adobe Commerce 2.4.4 以降
- Adobe IDと組織 ID
- [Adobe Client Data Layer （ACDL） ](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/client-data-layer/overview.html) （ストアフロントのイベントデータを収集するために必要）
- その他のAdobe DX 製品に対する使用権限。

>[!ENDSHADEBOX]

## オンボーディング手順

大まかに言えば、[!DNL Data Connection] 拡張機能を有効にするには、次の手順を実行します。

1. [!DNL Data Connection] 拡張機能 ](install.md)[ インストールします。
1. Adobe アカウントに [ ログイン ](https://helpx.adobe.com/manage-account/using/access-adobe-id-account.html) し、組織 ID を [ 確認するために表示 ](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255) します。 組織 ID は、プロビジョニングされているExperience Cloud会社に関連付けられた ID です。 この ID は 24 文字の英数字から成る文字列の後に `@AdobeOrg` （必須）を付けたものです。
1. [Experience Platformのデータ収集に対する権限 ](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html) があることを確認します。
1. 収集して送信できる [ データのタイプ ](data-ingestion.md) を確認します。
1. Commerce固有のフィールドグループを使用して、[ 時系列イベントスキーマ ](update-xdm.md) または [ プロファイルレコードデータスキーマ ](profile-data.md) を作成または更新します。
1. 作成または更新したスキーマに基づいて [ データセットを作成 ](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset) します。 このデータセットには、Experience Platform Edgeに送信されるCommerce データが含まれています。
1. [ データストリームを作成 ](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html) し、Commerce固有のフィールドグループを含む XDM スキーマを選択します。
1. [Commerce サービスに接続します ](../landing/saas.md)。
1. [Adobe Experience Platformに接続します ](connect-data.md)。

このガイドの残りの部分では、これらの手順をすべて詳しく説明するので、Commerce店でAdobe DX 製品の機能を最大限に活用し、活用を開始できます。

>[!NOTE]
>
>モバイル開発者向けに、Adobe Experience Platform Mobile SDKをCommerceと [ 統合 ](./mobile-sdk-epc.md) する方法を説明します。

## HIPAA 対応

[!DNL Data Connection] 拡張機能を使用すると、バックオフィスデータ [!DNL Commerce]Experience Platformと共有し、HIPAA 準拠を維持できます。 [ 詳細情報 ](hipaa-readiness.md)。

## オーディエンス

このガイドは、Adobe Commerce ストアを充実させ、パーソナライズして、お客様のショッピングエクスペリエンスを向上させたいCommerce マーチャント向けに設計されています。

## サポート

情報が必要な場合や、このガイドで扱われていない質問がある場合は、次のリソースを使用してください。

- [ ヘルプセンター ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/overview.html){target="_blank"}
- [ サポートチケット ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket){target="_blank"} - チケットを送信すると、追加のヘルプを受けることができます。
