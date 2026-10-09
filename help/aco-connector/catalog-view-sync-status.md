---
title: B2B共有カタログのカタログビュー同期の監視
last-update: 2026-09-03T00:00:00.000Z
description: カタログビューの同期ステータス ページを使用して、Adobe Commerce Optimizerに同期されたカタログビュー、ポリシー、価格表の参照、主要な設定データを監視および調整します。
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
subfeature_v2:
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
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 0%
---

# B2B共有カタログのカタログビュー同期の監視

Commerce Adminの[!UICONTROL Catalog View Sync Status] ダッシュボードを使用して、[!DNL Adobe Commerce]から[!DNL Adobe Commerce Optimizer]までのB2B カタログビューの同期を追跡します。

[!UICONTROL Catalog View Sync Status]は、各B2B共有カタログのカタログ ビュー、ポリシー、価格表参照、アクセス制限キー設定が[!DNL Adobe Commerce Optimizer]に存在し、[!DNL Adobe Commerce]設定と一致することを確認します。 代わりに、製品、価格、およびカテゴリーフィードの同期を追跡するには、[&#x200B; データの同期の管理](data-sync-status.md#verify-that-the-data-sync-is-working)を参照してください。

## 同期ステータスページへのアクセス {#access-the-sync-status-page}

Commerce管理者から、**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Catalog View Sync Status]**&#x200B;に移動します。

![&#x200B; カタログ ビューの同期ステータス ページ。Adobe Commerce Optimizerのカタログ ビュー、ポリシー、価格表、およびアクセス キー設定の同期ステータスを監視します](assets/catalog-view-sync-status.png){width="600" zoomable="yes"}

このページには、[!UICONTROL Catalog Views]、[!UICONTROL Orphaned in ACO]、[!UICONTROL Deleted]の3つのタブがあります。

## 共有カタログの同期ステータスを解釈 {#interpret-sync-status}

[!UICONTROL Catalog View] タブでは、各行は、共有カタログとストアビューの組み合わせから投影された1つのカスタム共有カタログビューを表します。 予測は、カタログ ビュー、ポリシー、価格表参照、およびアクセス制限キー設定データで、[!DNL Commerce Optimizer Connector]が共有カタログの[!DNL Adobe Commerce Optimizer]に書き出します。 ステータス情報を使用して、ストアフロント体験に配信されたデータが完全かつ正しいかどうかを判断します。 次の表は、最も一般的なステータス値と、共有カタログに対するステータス値の意味をまとめたものです。

| ステータス | 共有カタログの意味 |
| --- | --- |
| **デグレード済み** | ポリシーまたはリンクされた価格表など、[!DNL Adobe Commerce Optimizer]で直接変更されました。 問題が解決するまで、間違った品揃えや価格が会社に表示されることがあります。 これは、Commerce Optimizerでアクセスキー、ビュー名、またはソースが変更された場合にも発生する可能性があります。 |
| **失敗** | カタログ ビューが[!DNL Adobe Commerce Optimizer]に存在しないか、最初の投影が行われる前に猶予期間が経過した場合。 （[ACO カタログビューの同期設定の設定](#configure-aco-catalog-view-sync-settings)を参照）。 カタログの同期ステータスが`Failed`の場合、会社はこの共有カタログのストアフロントエクスペリエンスにアクセスできません。 |
| **期限切れ** | 共有カタログを[!DNL Adobe Commerce]で削除しました。 カタログビューには、削除猶予期間が終了するまで引き続きアクセスできます。 デフォルトの猶予期間は7日間です。 [&#x200B; カタログ ビューの同期設定](#configure-aco-catalog-view-sync-settings)を更新することで、デフォルトを変更できます。 |
| **孤立** | カタログ ビューまたはキーは、コネクタではなく、[!DNL Adobe Commerce Optimizer] Studioで直接作成されました。 [孤立したエントリと削除されたエントリの確認](#review-orphaned-and-deleted-entries)を参照してください。 |

[!UICONTROL Healthy]、[!UICONTROL Pending]および[!UICONTROL Deleted]は、アクションを必要としない情報状態です。 完全なリストについては、*Commerce管理ガイド*&#x200B;の[Sync ステータス値](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/catalog-view-sync-status#sync-status-values){target="_blank"}を参照してください。

### ACO カタログビューの同期設定 {#configure-aco-catalog-view-sync-settings}

[!DNL Adobe Commerce]管理者（[!DNL Adobe Commerce Optimizer] Studioではなく）から、**[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Services]** > **[!UICONTROL ACO Catalog View Sync]**&#x200B;に移動して、コネクタが削除と作成をどのように実行するか、および修復が自動的にドリフトするかどうかを制御します。

![ACO カタログビュー同期設定ページに表示される削除、作成、およびドリフト再調整セクション &#x200B;](assets/aco-catalog-view-sync-configuration.png){width="600" zoomable="yes"}

- **[!UICONTROL Deletion Grace Period (days)]** – 削除された共有カタログのカタログビュー、ポリシー、メタデータが、削除される前に[!DNL Adobe Commerce Optimizer]に保持される日数。 デフォルトは7日間です。 `0`に設定すると、猶予期間なしで、プロジェクションをすぐに削除できます。

- **[!UICONTROL Creation Grace Period (days)]** – 新しく登録されたカタログビューが[!UICONTROL Pending]として報告されている間、[!DNL Adobe Commerce Optimizer]への最初の投影を待機できる日数。 投影無しで猶予期間が終了すると、ステータスは[!UICONTROL Failed]になります。 デフォルトは1です。

- **[!UICONTROL Enabled]** （Drift Reconciler） - [!DNL Adobe Commerce Optimizer]と[!DNL Adobe Commerce]の投影状態を比較し、相違を修正またはレポートするスケジュールされたドリフト調整プログラムを実行します。

- **[!UICONTROL Automatically Repair Drift]** - **[!UICONTROL Yes]**&#x200B;に設定すると、スケジュールされた実行は、修復可能なドリフトのために[!DNL Adobe Commerce Optimizer]を[!DNL Adobe Commerce]に戻します。 **[!UICONTROL No]**&#x200B;に設定すると、スケジュールされた実行ではドリフトのみが検出され、ログが記録されます。孤立したエントリは常に報告され、自動的に削除されることはありません。 この設定は、スケジュールされた紐付け機能にのみ影響します。 このページの&#x200B;**[!UICONTROL Reconcile & Repair]** アクションは、常にドリフトを修復します。 [監視または修復の選択](#choose-monitoring-or-repair)を参照してください。

各設定について詳しくは、*[!DNL Commerce Admin]ガイド*&#x200B;の[ACO カタログビュー同期設定](https://experienceleague.adobe.com/en/docs/commerce-admin/configuration-reference/services/aco-catalog-view-sync.md)を参照してください。

## 監視または修復を選択 {#choose-monitoring-or-repair}

[!DNL Adobe Commerce]は、B2B共有カタログのカタログ ビュー、ポリシー、価格表、および主要な構成の信頼できる唯一の情報源です。 ユーザーまたは別の管理者が[!DNL Adobe Commerce Optimizer] Studioで直接ポリシー、価格表、またはキー設定設定を変更した場合、調整では、設定の違いがドリフトとして報告されます。

- 何も変更せずにドリフトを確認するには、**[!UICONTROL Reconcile]**&#x200B;を選択します。これにより、アクションを実行する前に違いを確認できます。
- 修復可能なドリフトの想定される設定を復元するには、**[!UICONTROL Reconcile & Repair]**&#x200B;を選択します。

変更された内容とその理由を確認するには、カタログビューの詳細ページを開き、ドリフト履歴を確認します。

## 孤立したエントリと削除されたエントリのレビュー {#review-orphaned-and-deleted-entries}

**[!UICONTROL Orphaned in ACO]**&#x200B;と&#x200B;**[!UICONTROL Deleted]**&#x200B;のタブには、調整する共有カタログが[!DNL Adobe Commerce]がないため、コネクタが自動的に修復できない2つのケースがあります。

- **[!UICONTROL Orphaned in ACO]** - コネクタは、同期ステータスとドリフト調整中に孤立したエンティティをレポートします。 修復が有効になっている状態で紐付けが実行された場合でも、自動的に適用または削除されません。

  エンティティが[!DNL Adobe Commerce Optimizer]に存在する場合、そのエンティティは孤立していますが、コネクタはそれを追跡しないか、追跡されたカタログ ビューに関連付けません。 これは、エンティティが手動で作成された場合、別の統合によって作成された場合、または中断されたコネクタ操作の後に残された場合に発生する可能性があります。

  - **カタログ ビュー** - コネクタがビューを追跡しません。 カタログ ビューのリンクを選択して、[!DNL Adobe Commerce Optimizer] Studioでカタログ ビューの詳細ページを開きます。 カタログビューが不要になった場合は、削除します。

  - **制限付きアクセスキー** - ライブカタログビューがキーを参照しません。 カタログ ビューのリンクを選択して、[!DNL Adobe Commerce Optimizer] Studioでカタログ ビューの詳細ページを開きます。 設定されたアクセスキーを確認し、不要になった場合は削除します。

  - **ポリシー** - コネクタはポリシーを追跡せず、ライブカタログビューはそれを参照しません。 ポリシーリンクを選択して、[!DNL Adobe Commerce Optimizer] Studioで開きます。  見直して、不要になった場合は削除します。

- **[!UICONTROL Deleted]** - [!DNL Adobe Commerce]の共有カタログを削除し、そのカタログ ビューの投影が後で削除されました。 これらの行は、削除された内容の記録として90日間保持されます。

>[!MORELIKETHIS]
>
> - [&#x200B; カタログ ビュー同期ステータスの監視](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/catalog-view-sync-status.md){target="_blank"} — *Commerce管理ガイド*&#x200B;のカタログ ビュー同期ステータス ページの完全なドキュメント リファレンス —>
> - [&#x200B; データ同期の管理](data-sync-status.md) – 製品、価格、カテゴリ フィードの同期を確認します
> - [&#x200B; プライベートカタログビュー](/help/optimizer/setup/private-catalog-view.md) — コネクター管理のプライベートカタログビューについて説明します
> - [制限付きアクセスキー](/help/optimizer/setup/restricted-access-keys.md) — コネクタで管理されるキーの仕組みを説明します
> - [B2B共有カタログの変更を監視](get-started-b2b-shared-catalogs.md#monitor-b2b-shared-catalog-changes) — B2B共有カタログのコネクタによる自動処理について説明します
