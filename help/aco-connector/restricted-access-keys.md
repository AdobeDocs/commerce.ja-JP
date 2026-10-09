---
title: B2B共有カタログの制限付きアクセスキーの管理
description: Adobe Commerce Optimizer ConnectorがB2B共有カタログのプロジェクトを保護するために使用する制限付きアクセスキーを管理する方法について説明します。
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
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
source-wordcount: '1105'
ht-degree: 0%
---

# B2B共有カタログの制限付きアクセスキーの管理

[!BADGE Private Beta]{type=Caution tooltip="現在プライベートベータ版のAdobe Commerce Optimizer Connector B2B拡張機能が必要です。"}

[!DNL Adobe Commerce]個のB2B共有カタログを[!DNL Adobe Commerce Optimizer Connector B2B extension]と共に使用する場合、カタログ ビューの作成時に、拡張機能が自動的に最初の制限付きアクセス キーを生成して割り当てます。 Commerce管理者の[!UICONTROL Restricted Access Keys] ページを使用して、そのキーを表示し、追加のキーを作成、割り当て、または削除します。

![B2B共有カタログ ビューの制限付きアクセス キー](assets/restricted-access-keys.png){width="800" zoomable="yes"}

>[!NOTE]
>
>パートナーポータルなどのB2B以外のユースケース用に手動で作成したキーを管理するには、[制限付きアクセスキー](/help/optimizer/setup/restricted-access-keys.md#create-a-restricted-access-key)を参照してください。

## ページへのアクセス {#access-the-page}

Commerce管理者から、**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Restricted Access Keys]**&#x200B;に移動します。

共有カタロググリッドまたは会社グリッドからカタログビューにキーを割り当てることができます。 「[B2B共有カタログビューにキーを割り当てる](#assign-keys-to-a-shared-catalog-view)」を参照してください。

>[!NOTE]
>
>このページのフィールドの参照については、*Commerce管理者ガイド*&#x200B;の[制限付きアクセスキー管理](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys){target="_blank"}を参照してください。—>

## 自動キー以上のものが必要な場合 {#when-you-need-more-than-the-automatic-key}

[!DNL Adobe Commerce Optimizer Connector B2B extension]によって生成された自動キーは、ユーザーの操作を必要とせずに、ほとんどのB2B共有カタログをカバーします。 以下の場合は、自分でキーを管理します。

- **キーの回転** – 新しいキーを作成し、既存のキーと並行してカタログビューに割り当て、機能していることを確認してから、古いキーを削除します。 自動回転はまだ利用できません。
- **キーがリンクに失敗しました**- [&#x200B; カタログ ビュー同期ステータス &#x200B;](catalog-view-sync-status.md)にキー関連のドリフトが表示される場合は、カタログ ビューの割り当てを再度保存して、失敗したリンクを再試行してください。 それでもキーが失敗する場合は、[!UICONTROL Reconcile & Repair]を実行してキーまたはステータスを回復してから、置換を作成します。 キーの有効期限が切れているか、障害が永続的に回復不能な場合にのみ、置換キーを作成します。
- **公開鍵を検索** – 制限付きアクセスキーのページで、**[!UICONTROL View Public Key]**&#x200B;を選択して、キーの公開鍵を表示およびコピーします。

カタログビューには、一度に最大3つのキーを割り当てることができます。 キーのローテーション中、[!DNL Adobe Commerce Optimizer]は、割り当てられた、期限切れでないキーによって署名されたトークンを受け入れます。「アクティブ」キーを設定する手作業はありません。

## キーを作成

[!UICONTROL Restricted Access Keys] ページで、**[!UICONTROL Create Key]**&#x200B;を選択してキーを作成します。

Commerceは新しいキーペアを生成し、秘密鍵を保持します。 制限付きアクセスキーのテーブルは、一意のキーIDを示す新しいキーのエントリで更新されます。 この[!UICONTROL Key ID]は、カタログ ビューにキーを割り当てる場合に使用します。

カタログ ビューにキーを割り当てるまで、公開鍵は[!DNL Adobe Commerce Optimizer]に登録されません。 登録後、アクセス制限キーのテーブルエントリが更新され、カタログの割り当てと有効期限が表示されます。

## B2B共有カタログから投影されたカタログビューにキーを割り当てる {#assign-keys-to-a-shared-catalog-view}

メインの[!UICONTROL Restricted Access Keys] グリッドからではなく、会社アカウントまたは共有カタログページからカタログビューにキーを割り当てるか、割り当て解除します。

カタログビューには、少なくとも1つのキーを持ち、最大3つのキーを持つことができます。

- 4つ目のキーを割り当てようとすると、値`A Catalog View can have at most 3 access keys.`を保存しようとするとエラーメッセージが表示されます
- カタログビューにキーが1つしかない場合、そのキーを削除したり、割り当てを解除したりすることはできません。

カタログビューキー設定を更新するには、会社アカウントページまたは共有カタログページからアクセスできます。

>[!BEGINTABS]

>[!TAB 会社アカウントからキーを管理]

1. Commerce管理者から、会社ページ （**[!UICONTROL Customers]** > **[!UICONTROL Companies]**）を開きます。

1. 会社の[!UICONTROL Action]列で、[!UICONTROL Edit]を選択します。

1. 会社に割り当てられた共有カタログから予測されるカタログビューのリストを表示するには、_[!UICONTROL Catalog Views]_&#x200B;セクションを展開します。

このタブには、割り当てられたキーを含め、共有カタログから投影されたカタログビューが一覧表示されます。

1. 更新するカタログ ビューの[!UICONTROL Actions]列で、**[!UICONTROL Edit Restricted Access Keys]**&#x200B;を選択します。

   ![制限付きアクセスキーを編集ドロップダウンに、カタログビューに割り当てられたキーが表示されている](assets/restricted-access-key-selector.png){width="500" zoomable="yes"}

1. キーを割り当てるには、**[!UICONTROL Access Keys]** ドロップダウンリストを選択します。 次に、[!UICONTROL key ID]によって割り当てられていないキー（例：`#42`）を選択します。 次に、[!UICONTROL Done]をクリックして、カタログ ビューに割り当てます。

   別のカタログビューに既に割り当てられているキーには、それに応じてラベルが付けられます。

1. アクセストークンを削除するには、キーラベルの`x` コントロールを選択して、[!UICONTROL Access Tokens] フィールドからアクセストークンを削除します。

1. 構成更新を保存して適用するには、**[!UICONTROL Save]**&#x200B;を選択します。

>[!TAB 共有カタログからキーを管理]

1. Commerce管理者から、共有カタログページ（**[!UICONTROL Catalog]** > **[!UICONTROL Shared catalogs]**）を開きます。

1. 共有の[!UICONTROL Action]列で、[!UICONTROL Select] メニューから&#x200B;**[!UICONTROL General Settings]**&#x200B;を選択します。

1. 共有カタログから投影されたカタログビューのリストを表示するには、[!UICONTROL Shared Catalog Information] メニューから&#x200B;**[!UICONTROL Catalog Views]**&#x200B;を選択します。

[!UICONTROL Catalog Views] ページには、各カタログビューのカタログビューID、関連付けられたストアビュー、およびアクセスキーが一覧表示されます。

1. 更新するカタログ ビューの[!UICONTROL Actions]列で、**[!UICONTROL Edit Restricted Access Keys]**&#x200B;を選択します。

   ![制限付きアクセスキーを編集ドロップダウンに、カタログビューに割り当てられたキーが表示されている](assets/restricted-access-key-selector.png){width="500" zoomable="yes"}

1. キーを割り当てるには、**[!UICONTROL Access Keys]** ドロップダウンリストを選択します。 次に、デフォルトのキータイトル（例：`#42`）で未割り当てのキーを選択します。 次に、[!UICONTROL Done]をクリックして、カタログ ビューに割り当てます。

   別のカタログビューに既に割り当てられているキーには、それに応じてラベルが付けられます。

1. アクセストークンを削除するには、キーラベルの`x` コントロールを選択して、[!UICONTROL Access Tokens] フィールドからアクセストークンを削除します。

1. 構成更新を保存して適用するには、**[!UICONTROL Save]**&#x200B;を選択します。

>[!ENDTABS]

## キーの有効期限と更新を管理

制限付きアクセスキーのデフォルトのキーの有効期間を設定できます。 値は、[!DNL Adobe Commerce Optimizer Connector B2B]拡張機能が初期キーを生成する場合、または新しいキーを手動で作成する場合に、有効期限セットを決定します。

有効期限は、[!UICONTROL Restricted Access Keys] ページの[!UICONTROL Expires At]列に表示されます。

期間を変更するには、**[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL Configuration]** > **[!UICONTROL Services]** > **[!UICONTROL ACO Restricted Access Keys]**&#x200B;に移動します。 [!UICONTROL Provisioning] ページで、**[!UICONTROL Default Key Expiry (days)]** フィールドを更新します。 デフォルトのシステムキーの有効期間は、最初は長期（約100年）に設定されます。 セキュリティポリシーに一致する値に更新してください。

### キーの更新

キーの有効期限が10日以内の場合、[!UICONTROL Restricted Access Keys] ページには、そのエントリの横に警告アイコンが表示されます。 有効期限が切れる前にキーを更新しないと、新しいキーを割り当てるまでカタログビューにアクセスできなくなります。

新しいキーはいつでも作成して割り当てることができ、新しいキーが機能していることを確認した後に古いキーを削除できます。

## 既知の制限事項

自動キーローテーションはまだ利用できません。

>[!MORELIKETHIS]
>
> - [制限付きアクセスキーを管理](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys){target="_blank"} – このページの完全なフィールド参照（*Commerce管理ガイド*） – >
> - [&#x200B; カタログ ビュー同期の監視](catalog-view-sync-status.md) – これらのキーで保護されるカタログ ビューの監視
> - [&#x200B; プライベートカタログビュー](/help/optimizer/setup/private-catalog-view.md) — コネクター管理のプライベートカタログビューについて説明します
> - [制限付きアクセスキー](/help/optimizer/setup/restricted-access-keys.md) — ACO Studio ベースの手動キーフローがB2B以外のユースケースでどのように機能するかを説明します
