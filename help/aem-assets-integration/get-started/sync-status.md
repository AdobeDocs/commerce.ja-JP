---
title: AEM Assetsの同期ステータスの表示
description: Commerce管理画面のアセットを中心としたリストで、同期されたアセットを確認できます。
feature: CMS, Media, Integration
source-git-commit: 446739ffad0da97e2e923e6e02be3f8f6b3eb2b3
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---


# AEM Assetsの同期ステータスの表示

**[!UICONTROL Sync Status]** ビューには、AEM Assets統合を通じて同期されたアセットを中心としたアセットのリストが表示されます。 カタログ内で製品ごとに移動するのではなく、独自の属性を使用してアセットを検索、レビュー、トラブルシューティングできます。

![AEM Assets Sync ステータス ビュー](../assets/aem-assets-sync-status-view.png){width="700" zoomable="yes"}

>[!NOTE]
>
> [!UICONTROL Sync Status]は[!DNL Adobe Commerce Optimizer]には使用できません。

## 同期ステータスを開く

_管理者_ サイドバーで、**[!UICONTROL System]** > **[!UICONTROL AEM Assets]** > **[!UICONTROL Sync Status]**&#x200B;に移動します。

![&#x200B; システムメニューのAEM Assets Sync ステータス &#x200B;](../assets/aem-assets-configuration-admin-menu.png){width="600" zoomable="yes"}

## 統合同期の正常性

ページ上部の&#x200B;**AEM Sync Status** バナーには、パイプラインの正常性と、処理待ちのイベント数が表示されます。 同期ヘルスバナーを更新するには、**[!UICONTROL Refresh]**&#x200B;を選択します。

## アセットリスト

グリッドには、AEM Assets同期パイプラインで処理されたアセットと現在の同期状態が一覧表示されます。 各行は、Commerceの1つのアセットとその同期状態を表します。 製品レコードを表すものではありません。

| 列 | 説明 |
|--------|-------------|
| **アセット ID** | AEM アセット ID （例：`urn:aaid:aem:…`）。 |
| **ステータス** | アセットの最新の同期試行の結果。 使用可能な値は、**Success**、**Failed**、または&#x200B;**Waiting**&#x200B;です。 |
| **処理中** | アセットの処理が開始された日時。 |
| **ディスパッチ済み** | 同期イベントがディスパッチされた日時。 |
| **エラー** | **ステータス**&#x200B;が失敗を示す場合はエラーメッセージが表示され、同期に成功した場合は空になります。 |

### アセットのフィルタリング

1. **[!UICONTROL Filters]**&#x200B;を選択してフィルターパネルを展開します。

1. **アセット ID**&#x200B;を入力するか、**ステータス**&#x200B;の値を選択してください。

1. グリッドを更新するには&#x200B;**[!UICONTROL Apply Filters]**&#x200B;を選択し、変更を適用せずにパネルを閉じるには&#x200B;**[!UICONTROL Cancel]**&#x200B;を選択します。

フィルターはアセットレベルのデータに適用されるため、失敗した同期を分離したり、個々の製品を開くことなく特定のアセットをトレースしたりできます。

## 同期失敗

**ステータス**&#x200B;でエラーが表示された場合は、同期パイプラインから返されたメッセージについて、グリッドの&#x200B;**エラー**&#x200B;列を確認します。

完全なエラーメッセージと最後の同期試行の詳細を確認して、エラーを診断します。

[!BADGE PaaSのみ]{type=Informative tooltip="Cloud プロジェクト上のAdobe Commerce（Adobeで管理されるPaaS インフラストラクチャ）にのみ適用されます。"}その他のトラブルシューティングについては、[既定の自動一致](../synchronize/default-match.md)を参照してください。 統合ログファイルは、Commerce インスタンスの`/var/log/aem-assets-integration.log`および`/var/log/aem-assets-integration-errors.log`で利用できます。
