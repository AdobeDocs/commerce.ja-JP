---
title: トラブルシューティング  [!DNL App Management]
description: アプリの関連付けと設定に関する一般的な問題を解決します。
feature: App Builder, Extensibility, Integration
source-git-commit: ab635fecb7b82294bd4a4fd045ed71931e9d265d
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# [!DNL App Management] のトラブルシューティング

アプリの関連付けと設定に関する一般的な問題を解決するには、次の解決策を使用します。

## アプリが表示されない

デプロイ後にアプリがリストに表示されない場合は、次の手順を確認してください。

1. アプリがデプロイされ、組織で使用できるようになっていることを確認します。

1. Developer Consoleで正しいAdobe組織にログインしていることを確認します。

1. アプリが接続する準備ができていることを確認します（アプリ開発者またはパートナーが確認できます）。

それでもアプリが表示されない場合は、アプリ開発者に問い合わせるか、[Commerce拡張機能  [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"} のドキュメントで技術情報を確認してください。

## 範囲の同期に失敗しました

アプリを関連付ける際にスコープの同期に失敗した場合は、次の操作を試してください。

1. Commerce インスタンスがアクセス可能でオンラインであることを確認します。

1. API 資格情報が有効であり、正しい権限を持っていることを確認します。

1. アプリ設定で **[!UICONTROL Manage Scopes]** から手動で同期してみてください。

## 設定が保存されていません

設定の変更が保存されない場合は、次の操作を試してください。

1. すべての必須フィールドが入力され、有効であることを確認します。

1. アプリ設定を変更するための適切な権限があることを確認します。

1. ページを更新して、もう一度保存してみてください。

問題が解決しない場合は、ブラウザーコンソールでエラーを確認するか、アプリ開発者に問い合わせてください。

技術的なトラブルシューティングについては、[Commerce拡張機能  [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"} を参照してください。
