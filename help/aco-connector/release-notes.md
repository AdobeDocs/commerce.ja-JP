---
title: '[!DNL Adobe Commerce Optimizer Connector] リリースノート'
description: Adobe Commerceの [!DNL Adobe Commerce Optimizer Connector] の最新リリース情報。
feature: Services, Catalog Service, Release Notes
source-git-commit: 205fca38b379f94027a965b58826ffd922577f61
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Adobe Commerce Optimizer Connector リリースノート

これらのリリースノートには、[!DNL Adobe Commerce Optimizer Connector]のすべてのリリースが記載されており、次の内容が含まれています。

![新機能](../assets/new.svg)
![修正された問題](../assets/fix.svg)修正と改善
![既知の問題](../assets/bug.svg)既知の問題

## 2026 リリース

### 1.0.12 リリース

_2026年4月2日_

![新規](../assets/new.svg) **`saas:resync` コマンドのカテゴリフィードのサポートを追加しました**- `saas:resync` CLI コマンドを使用して、最新のカテゴリデータを簡単に更新および表示できるようになりました。

```terminal
bin/magento saas:resync --feed=categories
```

_2026年3月10日_

![修正済みの問題](../assets/fix.svg) Adobe Commerce Optimizer ConnectorがCommerce インスタンスにインストールされている場合に、Commerce管理システムと設定メニューからCommerce Services Connector設定ページへのアクセスをブロックする互換性の問題を修正しました。  両方の拡張機能がインストールされている場合は、Commerce Services Connector設定ページにアクセスできます。<!--MDEE-1322-->


### v1.0.10 リリース

_2026年3月9日_

![修正](../assets/fix.svg) コネクタ設定を完了する前にデータフィード同期ステータス ページにアクセスすると、コネクタ設定ページに自動的にリダイレクトされるようになりました。 このガイド付きフローは、コネクタの設定が完了したことを確認し、失敗または不完全なステータス項目につながる可能性のある構成設定が欠落したことによるエラーを防ぐのに役立ちます。<!--MDEE-1296-->

### v1.0.9 リリース

_2026年3月1日_

Adobe Commerce Optimizer Connectorの一般公開リリース。

>[!NOTE]
>
>Adobe Commerce Optimizer ConnectorのBeta プログラムに参加し、以前のバージョンの拡張機能がインストールされている場合は、一般公開版にアップグレードして最新のアップデートを入手してください。

