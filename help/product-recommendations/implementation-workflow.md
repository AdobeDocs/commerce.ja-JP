---
title: 導入ワークフロー
description: ストアフロントに [!DNL Product Recommendations] を正常に実装する手順について説明します。
exl-id: 4a784d04-8be6-473f-afb3-264af06c850a
TQID: https://experienceleague.adobe.com/-nvORlxBNwoCcZb6s-OvaX8TtIh28Q-fjeUxsDXpe9E
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 563
ht-degree: 0%

---

# 導入ワークフロー

[!DNL Product Recommendations]は、行動データとカタログデータの両方を使用します。

- 行動 – 商品ビュー、カートに追加された商品、購入など、サイトでの買い物客のエンゲージメントに関するデータ。 Adobe CommerceおよびAdobe AIは、個人を特定できる情報を収集しません。

- カタログ – 名前、価格、在庫状況などの商品メタデータ。

`magento/product-recommendations module`をインストールすると、Adobe AIは行動データとカタログデータを集計し、レコメンデーションタイプごとに[!DNL Product Recommendations]を作成します。 次に、[!DNL Product Recommendations] サービスは、これらのレコメンデーションをストアフロントにデプロイします。 ストアフロントに商品レコメンデーションを導入するには、次のワークフローを使用します。

>[!NOTE]
>
> ストアフロントがPWA Studioを使用して実装されている場合は、[PWA ドキュメント &#x200B;](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)を参照してください。 ReactやVue JSなどのカスタムフロントエンドテクノロジーを使用する場合は、[&#x200B; ヘッドレスストアフロントに](headless.md) [!DNL Product Recommendations]を統合する方法を説明します。

## ワークフロー

1. **実稼動環境へのデータ収集のデプロイ**

   [!DNL Product Recommendations]をデプロイするには、カタログと行動の2つの主要な[&#x200B; データソース &#x200B;](type.md)が必要です。 プロダクションは、顧客の行動を把握および分析する唯一の環境です。そのため、できるだけ早い段階でプロダクションに関するデータ収集を開始しましょう。 [Adobe AIがマシンラーニングモデルのトレーニングを行い、より質の高いレコメンデーションを提供する方法を](events.md)学びます。 さらに、実稼動環境で行動データの収集を開始すると、実稼動以外の環境での運用中に、この実稼動データに基づいて[推奨事項](staging-environment.md#fetch-recommendations-from-production-environment-recommended)を取得できます。 その後、本番環境で収集された実際の買い物客データにもとづいて計算されたさまざまなレコメンデーションをテストして、実験することができます。

   データ収集を実稼動環境にデプロイするには、[API キー](https://experienceleague.adobe.com/docs/commerce/user-guides/integration-services/saas.html?lang=ja)を指定して[!DNL Product Recommendations] モジュールを[&#x200B; インストールして設定](install-configure.md)する必要があります。

   >[!TIP]
   >
   > データ収集を導入しても、ストアフロントの外観や買い物客の体験は変わりません。 レコメンデーションユニットを作成および展開するだけで、ストアフロントの顧客体験が変化します。 実稼動環境にデプロイする前に、実稼動以外の環境でテストを行ってください。 また、テンプレートをカスタマイズするまで、レコメンデーションユニットを作成しないでください。 次のステップ。

1. **自分のスタイルに合わせてテンプレートをカスタマイズ**

   ストアフロントはブランドの象徴であるため、サイトテーマに合わせて商品レコメンデーションテンプレートを変更しましょう。

   >[!TIP]
   >
   > テンプレートをカスタマイズすることで、スタイルシートを指定したり、レコメンデーションユニットがページ上に表示される場所を上書きしたりできます。

   この手順を完了する方法については、開発者ドキュメントの「[&#x200B; カスタマイズ &#x200B;](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/customize.html?lang=ja)」を参照してください。

1. **実稼動以外の環境でレコメンデーションをテストする**

   実稼動環境にデプロイする前に、非実稼動環境で新しいテクノロジーをテストすることをお勧めします。 実稼動以外の環境でレコメンデーションをテストすると、様々なレコメンデーションユニットタイプ、ポジショニング、ページを使用して再生できます。 実稼働環境でのテスト中に、実稼働環境ですでに収集された行動データに基づいてレコメンデーションを取得できるため、実際の顧客のショッピング行動に基づいてレコメンデーション結果を得ることができます。

   >[!TIP]
   >
   > 実稼動以外の環境カタログと、実稼動環境のカタログとほぼ同じであることを確認します。 類似のカタログを使用することで、レコメンデーションユニットに返される製品が、生産時の製品を密接に模倣することができます。

   この手順を完了する方法については、実稼動環境から[Fetch](staging-environment.md)行動データを取得するを参照してください。

1. **レコメンデーションを作成して実稼動ストアフロントにデプロイ**

   実稼動環境に行動データ収集をデプロイし、商品レコメンデーションテンプレートを変更し、実際の買い物客の行動を使用してレコメンデーションをテストしたら、すべてのコードを実稼動環境にプロモートし、[create](create.md)実稼動商品レコメンデーションを作成する準備が整いました。
