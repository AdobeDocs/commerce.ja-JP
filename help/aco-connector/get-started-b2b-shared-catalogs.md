---
title: B2B Commerce用コネクタの設定
description: B2B コネクタのインストール、Commerce スコープの選択、共有カタログデータの同期、カタログビューの検証、プロジェクションの正常性の監視の方法について説明します。
feature: Integration, Configuration
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
last-update: 2026-10-01
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
subfeature_v2:
  - id: e126554b-28f9-4290-b58c-10b888b88174
    internal-label: IMS integration
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
    internal-label: Data Transfer
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: c76e776250d9f996daf61d3cf62e2070803e998c
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%
---

# B2B Commerce用コネクタの設定

[!DNL Adobe Commerce]個のB2B共有カタログを使用しているマーチャントは、[!DNL Adobe Commerce Optimizer Connector for B2B]を使用して、カスタム共有カタログデータと設定を[!DNL Adobe Commerce Optimizer]に同期できます。

{{aco-integration-environment-alignment}}

## 統合の使用要件 {#requirements-to-use-the-integration}

* Adobe Commerce 2.4.8以降（[Commerce B2B バージョン 1.5.3+](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/install)がインストールされ、有効）

* プロビジョニングされたサンドボックスインスタンスを使用する[!DNL Commerce Optimizer] ライセンス。

* Composerを使用してコネクタメタパッケージをダウンロードするための[認証キー](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)。

* [[!DNL Commerce Optimizer]  サンドボックスインスタンス ](../optimizer/get-started.md)への管理者アクセス。

統合を構成する[!DNL Adobe Commerce] ユーザーには、次の要件が必要です。

* Commerce管理者への管理者アクセス。

* [ アプリケーションサーバー [!DNL Adobe Commerce] へのコマンドラインアクセス ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access)。

* [!DNL Commerce Optimizer] プロジェクトがプロビジョニングされている[IMS組織](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations?)への開発者アクセス。

### アプリケーション要件

* Commerce cronとインデクサーは正常に動作しています。
* 書き出し用に特定された必要なweb サイトとストアビュー。
* Adobe Commerceで設定または設定可能な共有カタログ、企業の割り当て、品揃え、B2B価格設定。

>[!BEGINSHADEBOX]

## 競合する拡張機能の削除 {#remove-conflicting-extensions}

{{$include /help/_includes/aco-connector/remove-conflicting-extensions.md}}

>[!ENDSHADEBOX]

## 設定手順 {#configuration-steps}

[!DNL Adobe Commerce Optimizer Connector for B2B]を有効にし、[!DNL Adobe Commerce]から[!DNL Commerce Optimizer] インスタンスへのカスタム共有カタログ設定の同期を開始するには、次の手順に従います。

1. **[Composerを使用して [!DNL Adobe Commerce Optimizer Connector for B2B]  パッケージ](#install-the-adobe-commerce-optimizer-connector-for-B2B-package)**&#x200B;をインストールし、[!DNL Adobe Commerce] インスタンスを[!DNL Commerce Optimizer]に接続します。

1. **[管理者からCommerce スコープの書き出し設定](#data-export-and-scope-mapping)**&#x200B;をカスタマイズします。

1. **[ [!DNL Commerce Optimizer] 統合](#enable-the-adobe-commerce-optimizer-integration)**&#x200B;を有効にします。

1. **[データ同期が機能していることを確認します](#verify-that-the-data-sync-is-working)**。

## [!DNL Adobe Commerce Optimizer Connector for B2B] パッケージのインストール {#install-the-adobe-commerce-optimizer-connector-for-B2B-package}

[!DNL Adobe Commerce Optimizer Connector for B2B]は、[!DNL Commerce Optimizer]のアクティブなライセンスを持つすべてのCommerce マーチャントが利用できるComposer メタパッケージとして配信されます。

### インストール手順

1. Composerを使用して`adobe-commerce/commerce-data-export-aco-adapter-b2b` モジュールを追加します。

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter-b2b
   ```

1. [!DNL Adobe Commerce] ステージング環境に変更をデプロイします。

   デプロイメントが完了すると、[!DNL Commerce Optimizer] オプションがCommerce管理メニューから使用できるようになります。 「**[!UICONTROL Commerce Optimizer]**」を選択して、Commerce管理者から直接[!DNL Commerce Optimizer] インスタンスを開きます。

{{install-extension-links}}

### データ書き出しとスコープのマッピング

同期するweb サイトとストアビューを選択してから、最初のフィードを検証します。 B2Bの場合、コネクターは、共有カタログデータを[!DNL Commerce Optimizer]にプロジェクトする際に、有効なスコープを使用します。

* **製品のローカライズされたコンテンツを含むカタログ ソース→ストア ビュー**
* **web サイトと顧客グループ**→ web サイトと顧客グループの価格表
* **共有カタログ**→保護されたプライベート カタログ ビューと適用されたポリシー

共有カタログは商品の品揃えを定義し、有効になっている各ストアビューにはローカライズされたカタログソースが提供されます。 Web サイトと顧客グループが該当する価格表を決定します。 コネクターは、有効化されたストアビューごとに各カスタム共有カタログをプロジェクトするので、B2B投影に対して個別のスコープ設定は必要ありません。

カスタム共有カタログでは、有効なストアビューごとに、複数の保護されたプライベートカタログビューを生成できます。 デフォルトの公開共有カタログは、B2B プライベートカタログビューとして表示されません。 詳しいオブジェクトマッピングとランタイム認証フローについては、[B2B共有カタログ投影](b2b-shared-catalog-projection.md)を参照してください。

>[!IMPORTANT]
>
>書き出し設定を変更すると、カタログのサイズに応じて大幅な時間がかかる場合がある、完全なインデックス再作成がトリガーされます。 統合を有効にして最初のデータ同期を開始する前に、Commerce スコープを設定します。

### 範囲の書き出し設定を変更するには

1. Commerce Adminで、**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL All Stores]**&#x200B;に移動します。

1. 設定するweb サイトまたはストアビューを選択します。

1. **[!DNL Commerce Optimizer]エクスポーター設定**&#x200B;で、チェックボックスを使用して、必要に応じてデータ同期を有効または無効にします。

   ![ データ同期設定の更新](./assets/aco-connector-b2b-storeview-list.png){width="500" zoomable="yes"}

1. 変更を保存します。

### ビヘイビアーを有効または無効にする

| アクション | 結果 |
| -------- | -------- |
| ストアビューを無効にする | **同期を無効にすると、B2B ストアフロントからカタログデータが削除されます。** カタログ ソースは[!DNL Adobe Commerce Optimizer]に残りますが、次回のcron実行時にすべての同期データが削除されます。 |
| ストアビューを無効にして再度有効にする | 同じカタログソースに、完全なデータ再同期が再入力されます。 |

### B2B共有カタログの変更を監視する

コネクターは、共有カタログと会社の割り当ての変更を監視します。 Commerce Adminで共有カタログを削除すると、コネクタは、設定可能な猶予期間の後に、そのプライベートカタログビューへのアクセスを削除します。

>[!NOTE]
>
>削除猶予期間は、デフォルトで7日間です。 カタログビューの同期設定の設定を更新して変更できます。 [ カタログ ビューの同期ステータス設定](catalog-view-sync-status.md#configure-aco-catalog-view-sync-settings)を参照してください。

## [!DNL Commerce Optimizer]統合を有効にする {#enable-the-adobe-commerce-optimizer-integration}

統合を有効にし、`aco:config:init` CLI コマンドを実行してデータ同期を開始します。 このコマンドは、次の手順を完了します。

1. コマンドライン引数として指定された資格情報を使用して、IMS アクセストークンを取得します。
1. `https://ccm.api.commerce.adobe.com/api/v1/tenants/{tenantId}/owner/{orgId}`のCommerce Cloud Manager （CCM） サービスを呼び出して、テナントを検証し、取り込みURLと[!DNL Commerce Optimizer] Studio URLを抽出します。
1. すべての設定（クライアントシークレットが暗号化）を`core_config_data`に保存します。
1. すべての[!DNL Commerce Optimizer] フィードのインデクサーを無効にすることで、最初の完全同期をスケジュールします。

{{aco-data-sync-processing-note}}

## 必要な接続の詳細を取得

{{$include /help/_includes/aco-connector/connection-details.md}}

### [!DNL Commerce Optimizer] インスタンスの詳細を取得

{{$include /help/_includes/aco-connector/configure-connection.md}}

## データ同期が機能していることを確認します {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## 次のステップ

1. **B2B カタログ ビューの投影を監視**

最初のフィード同期の後、[ カタログ ビュー同期ステータス ](catalog-view-sync-status.md)を使用して、予測されるプライベート カタログ ビュー、ポリシー、価格表の参照、およびアクセス キーの制限付き設定を確認します。 投影モデルとランタイム認証フローについては、[B2B共有カタログ投影](b2b-shared-catalog-projection.md)を参照してください。

1. **[!DNL Edge Delivery Services]**&#x200B;にCommerce ストアフロントを設定

   ストアフロントを[!DNL Commerce Optimizer] インスタンスに接続し、パーソナライズされたコマースエクスペリエンスの提供を開始するには、[ ストアフロント設定ドキュメント ](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/){target="_blank"}に従います。
