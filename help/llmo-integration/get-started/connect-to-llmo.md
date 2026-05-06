---
title: ' [!DNL Adobe Commerce] から [!DNL Adobe LLM Optimizer]への接続'
description: 必要なCommerce サービスを有効にし、LLM Optimizer接続を設定し、カタログアクセスを検証し、テナントの準備を確認してから、機会を確認するか、更新をデプロイします。
role: Admin, User
recommendations: noCatalog
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# [!DNL Adobe Commerce]を[!DNL Adobe LLM Optimizer]に接続

>[!IMPORTANT]
>
>この統合へのアクセスは制限されています。 詳しくは、テクニカルアカウントマネージャーにお問い合わせください。

この記事では、LLM Optimizerで利用可能な[!DNL Adobe Commerce] カタログを接続する方法について説明します。

>[!NOTE]
>
>この記事では、統合のCommerce側に焦点を当てます。 LLM Optimizerについて詳しくは、[LLM Optimizer製品ドキュメント ](https://experienceleague.adobe.com/en/docs/llm-optimizer/using/home)を参照してください。

## 必要なCommerce サービスを有効にする {#enable-commerce-services}

Commerceの管理者または実装パートナーと協力して、次のことを確認します。

- LLM Optimizerが読み取る必要があるカタログデータは、アーキテクチャに応じて&#x200B;**書き出されるか、同期されます（デプロイメント内の任意のSaaS データエクスポーターまたはコネクタを含む）。**
- API アクセス、資格情報、および環境URL （サンドボックスと実稼動環境の比較）が、LLM Optimizerで使用する&#x200B;**テナント**&#x200B;と一致します。

## LLM OptimizerでのCommerce接続の設定 {#configure-commerce-connection}

**Commerce接続を設定するには：**

1. [!DNL Adobe LLM Optimizer] UIで、**顧客設定**&#x200B;を開き、「**[!UICONTROL Commerce]**」タブを選択します。

   ![お客様の設定タブのCommerce設定](../assets/llmo-commerce-config.png)

1. **[!UICONTROL Add Store View]**&#x200B;をクリックして新しい行を作成するか、既存のストアビューエントリを展開して編集します。
1. **[!UICONTROL Store View URL]**&#x200B;を入力します（必須）。

   そのストアビューには、ロケールまたはパスのプレフィックス （例：`https://brand.example.com/`または`https://brand.example.com/fr/`）を含むストアフロント URLを使用します。

1. **[!UICONTROL Environment ID]** （必須） - LLM Optimizerが接続する必要があるAdobe Commerce環境の識別子を入力します。
1. **[!UICONTROL Website Code]**、**[!UICONTROL Store Code]**&#x200B;および&#x200B;**[!UICONTROL Store View Code]**&#x200B;を入力してください（必須）。

   これらの値は、接続するweb サイト、ストア、ストアビューのCommerce管理画面のコードと一致する必要があります。

1. オプション：URLと値が異なる場合は、**[!UICONTROL Host Name]**&#x200B;をCommerce インスタンスのホスト名（例：`www.example.com`）で入力します。
1. **[!UICONTROL Adobe Commerce Endpoint]** - API アクセスに使用するAdobe Commerce インスタンスのベース URLを入力します。
1. リクエストの認証に使用した&#x200B;**[!UICONTROL API Key]**&#x200B;をCommerce APIに入力するか、貼り付けます。

   安全に別の場所にキーをコピーする必要がある場合は、フィールドの横にある「**[!UICONTROL Copy]**」をクリックします。

1. **[!UICONTROL Save]**&#x200B;をクリックして設定を保存します。

保存したら、カタログまたは監査結果をストアビューに頼る前に、**初期同期**&#x200B;または検証ジョブが完了するのを待ちます。

ストアビュー設定を削除するには、そのエントリを開き、**[!UICONTROL Delete]**&#x200B;をクリックします。

### フィールドの説明 {#commerce-connection-fields}

| フィールド | 説明 |
| --- | --- |
| ストアビューURL | ストアビューのパブリック URL LLM Optimizerは、カタログおよび監査ワークフローのスコープとして扱う必要があります。 |
| 環境ID | Commerce環境ID （クラウドまたはデプロイメントドキュメント、または該当する場合は管理者）。 |
| web サイトコード | カタログを所有するweb サイトのCommerce **[!UICONTROL Website Code]**。 |
| ストアコード | そのweb サイトの下にある店舗のCommerce **[!UICONTROL Store Code]**。 |
| ストアビューコード | ストアビューのCommerce **[!UICONTROL Store View Code]** （例：`default`）。 |
| ホスト名 | フォームが他のURLに加えてCommerce ストアフロントまたはインスタンスを要求する際のホスト名。 |
| Adobe Commerce Endpoint | LLM OptimizerがCommerce APIに到達するために使用するインスタンス URL。 |
| API キー | API認証用の秘密鍵。本番用資格情報と同様に扱います。 |

## テナントと環境の準備状況を確認する {#confirm-tenant-readiness}

- 意図的でない限り、接続された&#x200B;**サンドボックス** プロジェクトが&#x200B;**本番** Commerce データと混在していないことを確認します。
- Experience CloudとCommerceで&#x200B;**ユーザーの役割**&#x200B;を調整して、デプロイアクションを承認するユーザーが双方で適切な権限を持つようにします。

## 次のステップ {#next-steps}

[LLM OptimizerとAdobe Commerce](use-llmo-with-commerce.md)を使用して、オポチュニティのレビュー、カタログ更新のデプロイ、上書きの動作の把握を行います。
