---
title: '[!DNL App Management]のトラブルシューティング'
description: アプリの関連付けと設定に関する一般的な問題を解決します。
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
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%
---
# [!DNL App Management]のトラブルシューティング

アプリの関連付けと設定に関する一般的な問題を解決するには、次の解決策を使用します。

## アプリは表示されません

アプリがデプロイメント後にリストに表示されない場合は、次の手順を確認します。

1. アプリがデプロイされ、組織で使用可能であることを確認します。

1. Developer Consoleで正しいAdobe組織にログインしていることを確認します。

1. アプリに接続する準備ができていることを確認します（アプリの開発者またはパートナーが確認できます）。

それでもアプリが表示されない場合は、アプリ開発者にお問い合わせいただくか、[Commerce Extensibility [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}のドキュメントで技術情報をご確認ください。

## スコープの同期が失敗する

アプリの関連付け時にスコープの同期が失敗した場合は、次の手順を試してください。

1. Commerce インスタンスにアクセス可能でオンラインであることを確認します。

1. API資格情報が有効で、正しい権限を持っていることを確認します。

1. アプリ設定で&#x200B;**[!UICONTROL Manage Scopes]**&#x200B;から手動で同期してみてください。

## 設定が保存されていません

設定の変更が保存されない場合は、次の手順を実行します。

1. すべての必須フィールドが入力され、有効であることを確認してください。

1. アプリ設定を変更するための適切な権限があることを確認します。

1. ページを更新して、もう一度保存してみてください。

問題が解決しない場合は、ブラウザーコンソールでエラーを確認するか、アプリ開発者にお問い合わせください。

技術的なトラブルシューティングについて詳しくは、[Commerceの拡張機能 [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}を参照してください。
