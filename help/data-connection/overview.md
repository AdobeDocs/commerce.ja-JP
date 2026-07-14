---
title: '[!DNL Data Connection]の概要'
description: ' [!DNL Data Connection] 拡張機能を使用してAdobe Commerce データをAdobe Experience Platformと統合する方法について説明します。'
recommendations: noCatalog
exl-id: 660f9337-cad8-47fb-a959-0770f0fd813c
TQID: https://experienceleague.adobe.com/-wfkGM2isTVmAaJokndxVy0-UtZ4pM9msYXmh2IE-Hc
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 5ba5dfa23580b5eefa8271277e78c6ea67879b90
workflow-type: tm+mt
source-wordcount: 1373
ht-degree: 1%

---

# [!DNL Data Connection]の概要

>[!IMPORTANT]
>
>Experience Platform コネクタの名前が[!DNL Data Connection]に変更されました。

[!DNL Data Connection]拡張機能は、Adobe Commerce web インスタンスをAdobe Experience PlatformおよびEdge Networkに接続します。 モバイルアプリ開発者向けには、Adobe Experience Platform Mobile SDKとCommerceを使用して、Commerce データを取得し、Experience Platformに送信します。 [学習を増やす](./mobile-sdk-epc.md)。

複数のweb サイトを利用するマーチャントは、Experience Platform サンドボックスの選択など、web サイトごとに該当する[!DNL Data Connection]設定を設定できます。 グローバルフィールドとweb サイト範囲フィールドの比較については、[Commerce データをAdobe Experience Platform](connect-data.md#configuration-scope)に接続するを参照してください。

Commerceストアには豊富なデータが含まれています。 顧客がサイト上の商品をどのように閲覧、閲覧、最終的に購入したかに関する情報は、よりパーソナライズされたショッピング体験を構築する機会を明らかにすることができます。 このデータは、カートの価格ルールやダイナミックブロックなど、Commerceのネイティブ機能に反映される可能性がありますが、Commerceインスタンスではデータが分断されたままになります。

Adobe Experience Platformは、Adobeストアからのデータを組み合わせることで、そのデータをEdge Networkを通じて他のCommerce DX製品に配信し、買い物客の購買行動に関するインサイトを引き出すための一連のテクノロジーを提供します。 また、詳細なインサイトを獲得することで、あらゆるチャネルをまたいでパーソナライズされたショッピング体験を実現できます。

次の図は、[!DNL Data Connection]拡張機能がインストールされ、設定されている場合に、ストアから他のAdobe DX製品にCommerce データがどのように流れるのかを示しています。

![Experience Platform エッジへのデータの流れ](assets/commerce-edge.png)

上の画像では、SDK、API、ソースコネクタを使用して、行動プロファイルデータ、バックオフィスおよび顧客プロファイルデータがExperience Platform Edgeに送信されます。 拡張機能がデータ共有の複雑さを処理するため、これらの部分がどのように機能するかを完全に理解する必要はありません。 イベントデータがエッジにある場合は、[Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=ja)、[Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html)、[Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/admin-overview/analytics-overview.html)、[Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html)などのダウンストリームのAdobe DX製品で使用できます。 ガイド付きの例については、[Adobe Journey Optimizerを使用して放棄されたカートに関する電子メールを送信する](using-ajo.md)および[Commerce イベントデータを使用してReal-Time CDPでオーディエンスを作成する](create-audience.md)を参照してください。

## Experience PlatformデータをCommerceに取り込み

[!DNL Data Connection]拡張機能を使用してCommerce データをExperience Platformに送信することは、Commerceのデータ共有機能の1つの側面です。 オプションの拡張機能である反対側は[Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html)と呼ばれます。 この拡張機能を使用すると、Real-Time CDPでオーディエンスを作成し、そのオーディエンスをCommerce ストアにデプロイして、カートの価格ルール、関連する商品ルール、動的ブロックに情報を提供できます。

大まかに言えば、Commerce ストアからExperience Platformへ、そしてAudience Activation拡張機能を通じて戻るデータのフローは次のようになります。

![[!DNL Data Connection] フロー](assets/data-connection.png)

CommerceとExperience Platform間およびExperience PlatformとCommerce間の接続を設定すると、データは引き続き流れます。 アップグレードによって再接続する必要がない限り、再接続する必要はありません。

## 概念

このふたつのシステム間でデータを共有するには、いくつかの概念を理解する必要があります。

- **データタイプ** — [!DNL Data Connection]は、ブラウザーから&#x200B;**行動（ストアフロント）** データ、Commerce サーバーから&#x200B;**バックオフィス** データ、および&#x200B;**プロファイル** データを収集します。 管理者は、ストアフロントコレクション **ストアフロントイベント**&#x200B;にラベルを付けます。 完全な分類については、[Commerce データの種類](data-ingestion.md)を参照してください。

- **行動（ストアフロント）データ** — `addToCart`、`pageView`、`startCheckout`、`completeCheckout`など、サイトでの買い物客とのやり取りから取得しました。 [&#x200B; ストアフロントイベント &#x200B;](events.md#storefront-events)を参照してください。

- **バックオフィスデータ** — [注文状況](events-backoffice.md#order-status) イベント（[`orderPlaced`](events-backoffice.md#orderplaced)や[`orderShipped`](events-backoffice.md#ordershipmentcompleted)など）を含むCommerce サーバーでキャプチャされました。 [&#x200B; バックオフィスイベント &#x200B;](events-backoffice.md)を参照してください。

- **プロファイルレコード** – 買い物客プロファイルがCommerceで作成されたときに送信されるスナップショットデータ。 [&#x200B; プロファイルレコード &#x200B;](events-profilerecord.md)および[&#x200B; プロファイルレコードスキーマの更新](profile-data.md)を参照してください。

- **プロファイルイベント** — サーバー上のプロファイルライフサイクルの変更に関する時系列イベント。 [顧客プロファイルイベント &#x200B;](events-backoffice.md#customer-profile-events)を参照してください。

- **Experience PlatformとEdge Network** – ほとんどのAdobe DX製品のデータウェアハウス。 Experience Platformに送信されたデータは、Experience Platform Edge Networkを通じてAdobe DX製品に反映されます。 たとえば、Journey Optimizerを起動し、エッジから特定のCommerceイベントデータを取得し、Journey Optimizerでカート放棄メールを作成することができます。 また、Commerceストアにカート放棄がある場合は、Journey Optimizerからその電子メールを送信できます。 [Experience PlatformとEdge Network](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/overview.html)について詳しく説明します。

- **スキーマ** - スキーマは、送信されるデータの構造を記述します。 Experience PlatformでCommerce データを取り込む前に、データの構造を説明するスキーマを作成し、各フィールドに含めることができるデータタイプの制約を指定する必要があります。 スキーマは、基本クラスと0個以上のスキーマフィールドグループで構成されます。 このスキーマでは、すべてのAdobe DX製品が読み取り可能なXDM構造を使用します。 このスキーマにより、Experience Platformに送信されたデータがあらゆるDX製品で理解されることが保証されます。 [&#x200B; スキーマ &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html)の詳細をご覧ください。

- **データセット** - データのコレクション用のストレージおよび管理コンストラクト。通常、スキーマ（列）とフィールド（行）を含むテーブルです。 データセットには、保存するデータのさまざまな側面を説明するメタデータも含まれます。 Adobe Experience Platformに正常に取り込まれたすべてのデータは、データセット内に含まれます。 [&#x200B; データセット &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html)の詳細をご覧ください。

- **Datastream** - Adobe Experience Platformから他のAdobe DX製品へのデータの流れを許可するID。 このIDは、特定のAdobe Commerce インスタンス内の特定のweb サイトに関連付ける必要があります。 このデータストリームを作成する場合は、上記で作成したXDM スキーマを指定します。 [&#x200B; データストリーム &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html)の詳細をご覧ください。

## サポートされているアーキテクチャ

[!DNL Data Connection]拡張機能は、次のアーキテクチャで使用できます。

- PHP/Luma
- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/integrations/adobe-commerce/aep/)
- [AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/aep.html)

>[!BEGINSHADEBOX]

## 前提条件

[!DNL Data Connection]拡張機能を使用するには、次のものが必要です。

- Adobe Commerce 2.4.4以降
- Adobe IDと組織ID
- [&#x200B; ストアフロント イベント データの収集に必要なAdobe Client Data Layer （ACDL） &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/client-data-layer/overview.html)
- 他のAdobe DX製品の使用権限。

>[!ENDSHADEBOX]

## 拡張機能を有効にする {#enable-extension}

大まかに言えば、[!DNL Data Connection]拡張機能を有効にするには、次の手順を実行します。

1. [!DNL Data Connection]拡張機能を[&#x200B; インストール &#x200B;](install.md)します。
1. [Adobe アカウントに](https://helpx.adobe.com/manage-account/using/access-adobe-id-account.html) ログインし、[表示して](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255)組織IDを確認します。 組織IDは、プロビジョニングされたExperience Cloud会社に関連付けられたIDです。 このIDは24文字の英数字の文字列で、その後に`@AdobeOrg`が続きます（含める必要があります）。
1. Experience Platform[&#128279;](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html)でのデータ収集に対して権限があることを確認してください。
1. 収集して送信できる[種類のデータ &#x200B;](data-ingestion.md)を確認してください。
1. Commerce固有のフィールドグループを使用して、[時系列イベントスキーマ &#x200B;](update-xdm.md)または[&#x200B; プロファイルレコードデータスキーマ &#x200B;](profile-data.md)を作成または更新します。
1. [作成または更新したスキーマに基づいてデータセット &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset)を作成します。 このデータセットには、Experience Platform Edgeに送信されたCommerce データが含まれます。
1. [&#x200B; データストリーム &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html)を作成し、Commerce固有のフィールドグループを含むXDM スキーマを選択します。
1. [Commerce サービスに接続](../landing/saas.md)。
1. [Adobe Experience Platformに接続](connect-data.md)。

このガイドでは、CommerceストアでAdobe DXの機能を利用できるように、これらのステップをより詳しく説明します。

>[!NOTE]
>
>モバイル開発者向けに、Adobe Experience Platform Mobile SDKとCommerceを[統合](./mobile-sdk-epc.md)する方法について説明します。

## HIPAAへの対応

[!DNL Data Connection]拡張機能を使用すると、[!DNL Commerce]のバックオフィスデータをExperience Platformと共有し、HIPAAへの準拠を維持できます。 [学習を増やす](hipaa-readiness.md)。

## オーディエンス

このガイドは、Adobe Commerce ストアを充実させ、パーソナライズして、お客様のショッピング体験を向上させたいCommerce マーチャント向けに設計されています。

## サポート

このガイドで説明されていない情報や質問が必要な場合は、次のリソースを使用してください。

- [ヘルプセンター](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/overview.html){target="_blank"}
- [&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket){target="_blank"} — チケットを送信して追加のヘルプを受け取ります。
