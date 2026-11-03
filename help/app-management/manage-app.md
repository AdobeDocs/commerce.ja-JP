---
title: アプリを管理
description: App Builder アプリケーションをCommerce インスタンスに関連付け、インストール、設定、アップグレード、関連付けを解除します。
feature: App Builder, Extensibility, Integration
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
    internal-label: Developer tools
subfeature_v2:
  - id: a743e5dc-8f37-4b5d-a848-03c32ca30598
    internal-label: App Builder
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: a00b9e1654a572e1773b5b7e321683332882d86f
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 0%
---

# アプリを管理

[!DNL App Management]を使用して、App Builder アプリケーションをCommerce インスタンスに関連付け、インストール、設定、アップグレード、関連付けを解除します。 設定フォームは各アプリのスキーマから生成されるため、カスタム管理UI開発なしで設定を管理できます。

![ アプリ管理](assets/app-management-view.png){width="500" zoomable="yes"}

## 管理画面でアプリケーションを検索

**[!UICONTROL Apps]** > **[!UICONTROL App Management]**&#x200B;の下では、各アプリケーションがカードとして表示されます。 リストには、選択したAdobe IMS組織のAdobe Commerce インスタンスに関連付けられたすべてのアプリを含めることができます。 カードの上にあるコントロールを使用して、結果を絞り込みます。

| 制御 | 説明 |
| --- | --- |
| **[!UICONTROL Filter by app...]** | アプリケーション名で検索します。 |
| **[!UICONTROL Status]** | ライフサイクルの状態ごとにカードを制限する： **[!UICONTROL All Statuses]**&#x200B;はすべてのアプリを表示します。その他の値には&#x200B;**[!UICONTROL Associated]**、**[!UICONTROL Installed]**、**[!UICONTROL Partially Installed]**、**[!UICONTROL Unassociated]**&#x200B;が含まれます。 各カードのステータスは、リストの色付きインジケーターと一致します。 |
| **[!UICONTROL Extensibility patterns]** | アプリが使用する機能によってカードを制限します。 **[!UICONTROL All Extensibility Patterns]**&#x200B;はすべてのアプリを表示します。他の値は各カードのバッジに一致します（**[!UICONTROL Business Configuration]**、**[!UICONTROL Admin UI SDK]**、**[!UICONTROL Webhooks]**、**[!UICONTROL Events]**&#x200B;など）。 |

検索フィールドと両方のフィルターが一緒に適用されます。 完全なリストをもう一度表示するには、検索フィールドをクリアし、**[!UICONTROL All Statuses]**&#x200B;と&#x200B;**[!UICONTROL All Extensibility Patterns]**&#x200B;を選択します。

### 申請の詳細を確認

アプリケーションのカードで、**[!UICONTROL Manage]** > **[!UICONTROL Details]**&#x200B;を選択して、名前、説明、バージョンを確認します。 このダイアログには、次の2つのタブがあります。

* **[!UICONTROL Details]**&#x200B;には、イベントやカスタム インストール手順など、アプリケーションのビジネスの使用例が一覧表示されます。 ラベルと説明を確認して、アプリケーションがCommerceに追加する内容を理解します。
* **[!UICONTROL App config]**&#x200B;は、検査のためにアプリケーションの設定をJSONとして表示します。

![ アプリケーションのビジネスユースケースを表示する「詳細」タブ ](assets/application-details.png){width="600" zoomable="yes"}

アプリケーションのJSON設定を表示する![ アプリ設定タブ ](assets/app-config.png){width="600" zoomable="yes"}

## アプリを入手

**[!UICONTROL Acquire App]**&#x200B;さんが新しいブラウザータブ （または別のブラウザビュー）を[Adobe Exchange](https://exchange.adobe.com/apps/browse/ec){target="_blank"}に開き、Commerce関連のマーケットプレイスのリストを見つけて、Adobe IMS組織にアプリケーションを追加できます。 アプリを取得、承認、デプロイすると、[association](#associate-an-app)および[ インストール ](#install-an-app)の[!DNL App Management]にアプリが表示されます。

## 前提条件

アプリを関連付ける前に、次の項目を確認してください。

| 要件 | 説明 |
| --- | --- |
| **管理者アクセス** | [!DNL App Management]権限を持つCommerce管理者 |
| **アプリをデプロイしました** | App Builder アプリケーションが組織にデプロイされ、接続する準備ができました |
| **組織アクセス** | アプリがデプロイされるAdobe組織へのアクセス |

## チュートリアル

このビデオでは、アプリをCommerce インスタンスに関連付けて設定する方法を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/3478944)

## アプリの関連付け

関連付けプロセスでは、Commerceからweb サイト、ストア、ストアビューを読み込み、アプリとCommerce インスタンス間のリンクを作成します。

App Builder アプリケーションをCommerce インスタンスにリンクするには：

1. **[!UICONTROL Apps]** > **[!UICONTROL App Management]**&#x200B;に移動します。

1. **[!UICONTROL Associate App]**&#x200B;をクリックします。

   ![ アプリの関連付け](assets/associate-app.png){width="500" zoomable="yes"}

1. リストから&#x200B;**[!UICONTROL Project]**&#x200B;を選択します。

1. **[!UICONTROL Workspace]**&#x200B;を選択します。

1. **[!UICONTROL Associate]**&#x200B;をクリックします。

   ![ アプリの詳細](assets/app-details.png){width="500" zoomable="yes"}

>[!WARNING]
>
>スコープの同期が失敗しても、関連付けは完了します。 関連付けられたアプリの設定の&#x200B;**[!UICONTROL Manage Scopes]** ビューから、後でスコープを手動で同期できます。

## アプリのインストール

関連付けにより、アプリがCommerce インスタンスにリンクされます。 イベント、webhook、Admin UI拡張機能、カスタムインストール手順など、インストール可能なコンポーネントを含むアプリの場合、インストールは、これらのコンポーネントをインスタンスに適用します。

1. 関連付けられたアプリのインストール ダイアログを[!DNL App Management]で開きます。

1. アプリケーションのビジネスユースケースと、リストされたインストール手順を確認します。

1. **[!UICONTROL Pre Installation Instructions]**&#x200B;が表示されている場合は、続行する前に、これらの前提条件を完了してください。

   ![ インストール前の手順とビジネスの使用例を含むインストールのレビュー](assets/installation-review.png){width="600" zoomable="yes"}

1. **[!UICONTROL Install]**&#x200B;をクリックします。

1. インストールが完了するまで、個々のアイテムの進行状況インジケーターを監視します。

   ![個々のアイテムのインストールの進行状況](assets/installation-progress.png){width="600" zoomable="yes"}

   >[!WARNING]
   >
   >インストールが完了するまで、ページを開いたままにします。 ページを閉じたり更新したりすると、インストールが正しく完了しない場合があります。

1. **[!UICONTROL Successfully Installed]**&#x200B;が表示され、完了した項目にチェックマークが付いていることを確認します。

   ![完了した項目のチェックマークが付いたインストールが正常に完了しました](assets/installation-success.png){width="600" zoomable="yes"}

1. アプリから提供されたインストール後の手順をすべて完了し、必要に応じて[設定を行います](#configure-settings)。

## 設定の設定

[!DNL App Management] ビューでアプリを関連付けた後、次のフォームで設定を行います。

1. 関連するアプリのカードで、**[!UICONTROL Manage]** > **[!UICONTROL Configure]**&#x200B;を選択します。

フォームには、アプリの設定可能な設定が表示されます。

1. 必要に応じて値を変更します。

1. **[!UICONTROL Save]**&#x200B;をクリックします。

### スコープ固有の設定

さまざまなweb サイト、ストア、ストアビューに一意の設定が必要な場合は、スコープに特化した設定を利用できます。 例えば、特定の地域やストアビューに対してのみ機能を有効にしたり、ブランドごとに異なる設定を使用したりできます。 より低い範囲の設定は、より高い範囲の設定よりも優先されます。

特定の範囲レベルでグローバル値を上書きするには：

1. **[!UICONTROL Change Scope]**&#x200B;をクリックします。

1. リストから範囲を選択します。

1. このスコープの値を変更します。

1. **[!UICONTROL Save]**&#x200B;をクリックします。

## スコープの管理

アプリの詳細画面から&#x200B;**[!UICONTROL Manage Scopes]**&#x200B;にアクセスして、アプリのスコープ階層を管理します。

![ スコープの管理](assets/manage-scopes.png){width="500" zoomable="yes"}

| アクション | 説明 |
| --- | --- |
| **[!UICONTROL Add root scope]** | アプリにのみ適用される範囲を追加します。 |
| **[!UICONTROL Sync Commerce scopes]** | 追加または変更後に、Commerceからweb サイト、ストア、ストアビューのリストを更新します。 |
| **[!UICONTROL Import scopes]** | ファイルからスコープを一括インポートします。 |

## アプリのアップグレード

アプリ開発者がインストール済みアプリの新しいバージョンをデプロイすると、アップグレードが利用可能であることが[!DNL App Management]に通知されます。 App BuilderのデプロイメントとApp Managementのアップグレードは個別の操作です。アップグレードは、イベント、webhook、Admin UI拡張機能など、インストールされているコンポーネントに予定された変更を適用します。

アプリの開発者に、アプリがアップグレードをサポートしていることを確認してもらいます。 SDKの前提条件と移行要件については、開発者向けドキュメントの[ アプリのアップグレード ](https://developer.adobe.com/commerce/extensibility/app-management/upgrade-app/){target="_blank"}を参照してください。

### アップグレードの確認と開始

既定の手動モードでは、[!DNL App Management]でアップグレードを確認して開始します。

1. アプリ開発者の助けを借りて、インストール済みのアプリのバージョンと設定を記録し、アプリケーションデータと外部リソースをバックアップします。

1. **[!UICONTROL Apps]** > **[!UICONTROL App Management]**&#x200B;に移動し、アプリの利用可能なアップグレードを開きます。

1. 計画された変更と警告を確認します。 アップグレードでは、コンポーネントを追加、変更、または削除できます。 カスタムインストール手順を削除すると、そのアンインストールスクリプトは実行されず、作成したリソースは自動的にクリーンアップされません。 続行する前に、アプリ開発者に必要なクリーンアップを確認してください。

1. アップグレードを開始し、リストされた操作の進行状況を監視します。

1. アップグレード結果を確認し、失敗した操作を確認します。 アップグレードに失敗した場合は、**[!UICONTROL Retry Upgrade]**&#x200B;を使用する前に[ アップグレードに失敗](troubleshooting.md#upgrade-fails)します。

手動モードでは、インストール済みのCommerce コンポーネントに対して計画された変更は、アップグレードを開始するまで適用されません。 ただし、デプロイメントでは、アップグレードが実行される前に、インストール済みアプリが既に使用しているランタイムアクションコードを更新できます。

### 自動アップグレード

アプリ開発者がアップグレードモードを制御します。 アプリで手動アップグレードと自動アップグレードのどちらを使用しているか、開発者に確認してもらいます。

>[!WARNING]
>
>自動アップグレードは実験的なもので、外部リソースを変更できるカスタムインストールスクリプトなど、管理者のレビューなしでデプロイメント後に開始されます。 新しくデプロイされたバージョンが手動から自動にモードを変更する場合など、自動アップグレードが有効になる前に、開発者と調整してください。

### ビジネス設定の変更

アプリのビジネス設定スキーマへの変更は、デプロイメント後に自動的に表示されます。 これらはインストールやアップグレードとは別のもので、アプリのアップグレードはトリガーしません。

## アプリの関連付けを解除

Commerce インスタンスに接続する必要がなくなったアプリの関連付けを解除します。 例えば、統合を廃止する、別のワークスペースに切り替える、テスト設定をクリーンアップする必要があるとします。

>[!WARNING]
>
>関連付けを解除すると、このインスタンスのすべての設定値が削除されます。 この操作は元に戻せません。 アンインストールでは、カスタムアンインストールスクリプトを使用して、アプリコンポーネントとリソースを削除することもできます。

続行する前に、インストール済みのバージョンと設定を記録し、アプリケーションデータをバックアップし、アプリのアンインストールスクリプトが削除するリソースと手動クリーンアップが必要なリソースをアプリ開発者に尋ねます。 サービスの中断に備えて、アプリ、設定、データを復元する方法を計画します。 日常的な更新の場合は、アプリの関連付けを解除せずに[ アプリをアップグレードします](#upgrade-an-app)。

Commerce インスタンスからアプリを削除するには：

1. **[!UICONTROL Apps]** > **[!UICONTROL App Management]**&#x200B;に移動します。

1. アプリのカードで、**[!UICONTROL Manage]** > **[!UICONTROL Unassociate]**&#x200B;を選択します。

1. イベントやカスタムインストール手順など、アンインストールの影響を受けるビジネスユースケースとコンポーネントを確認します。

   ![影響を受けるビジネスのユースケースを一覧表示する確認の関連付けを解除](assets/unassociate-app.png){width="600" zoomable="yes"}

1. アクションを確認します。

## 関連ドキュメント

* [ トラブルシューティング  [!DNL App Management]](troubleshooting.md) – 関連付け、インストール、設定、アップグレードに関する一般的な問題を解決します。
* [ アプリのアップグレード ](https://developer.adobe.com/commerce/extensibility/app-management/upgrade-app/){target="_blank"} - アップグレードモード、移行スクリプト、および診断の開発者要件。
