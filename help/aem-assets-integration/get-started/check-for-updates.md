---
title: 拡張機能の更新を確認する
description: Adobe Commerceが手動CLI チェックを含む新しいAEM Assets Integration拡張機能のバージョンをチェックし、管理者に通知する方法について説明します。
feature: CMS, Media
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: ddbd0f6e-b569-5a04-8a70-55058777c373
    internal-label: CMS
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 4%
---
# 拡張機能の更新を確認する

AEM Assets Integration拡張機能バージョン 1.4.6以降では、Adobe Commerceは新しいバージョンの拡張機能が使用可能かどうかを自動的に確認し、管理者に通知します。 このチェックは、スケジュールされた処理の一部として非同期で実行され、管理者ページのレンダリングはブロックされません。

## 更新チェックの仕組み

* 更新チェックでは、インストール済みの`aem-assets-integration` パッケージのバージョンと、[repo.magento.com](https://repo.magento.com/admin/dashboard)で利用可能な最高の互換性のあるバージョンを比較します。
* 結果はキャッシュされます。 管理者ページを読み込むと、ライブネットワークリクエストがトリガーされるのではなく、最新のキャッシュされた結果が読み込まれます。
* `repo.magento.com`が利用できない場合、または返されたメタデータが無効な場合、Commerceは最後に成功したキャッシュ結果を保持し、管理者をブロックしません。

>[!NOTE]
>
>更新チェックは、Adobe Commerce on Cloudおよびオンプレミスのデプロイメントを対象としています。

## 更新通知の表示

管理者は、次のいずれかの場所で使用可能な更新通知を確認できます。

* **[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL Configuration]** > **[!UICONTROL Adobe Services]** > **[!UICONTROL AEM Assets Integration]**
* 管理者通知ドロップダウン

各通知は次のように表示されます。

* インストールされているバージョン
* 使用可能なバージョン
* リリースの分類
* リリースノートへのリンク

このCommerce インスタンスの通知を一時停止するか、更新通知を完全にオプトアウトするには、**[!UICONTROL Remind me later]**&#x200B;を選択します。

## 手動の更新チェックの実行

利用可能なアップデートをすぐに確認するには、Commerce ルートディレクトリから次のコマンドを実行します。

```bash
bin/magento aem:assets:check-update
```

このコマンドは、使用可能な更新プログラムのみをチェックしてレポートします。 Composer ファイルを変更したり、アップデートをデプロイしたりすることはありません。 アップデートをインストールするには、[Adobe Commerce パッケージのインストール ](configure-commerce.md)のComposerの手順に従います。

## 拡張機能パッケージのリリースメタデータ

更新チェックは、インストールされたパッケージの`composer.json` ファイルの`extra` セクションからリリースメタデータを読み取ります。

```json
{
  "extra": {
    "release_notes_url": "https://experienceleague.adobe.com/...",
    "release_type": "feature",
    "compatible_commerce_versions": ">=2.4.7 <2.5.0"
  }
}
```

## 次のステップ

* [Adobe Commerce パッケージのインストール](configure-commerce.md)
