---
title: Commerce Documentation Governance
description: Commerce Insightsの内部ガバナンスモデルについて説明します。 Experience Leagueには公開されません。意図的にTOC.mdから除外されます。
source-git-commit: 1da6d9753acbeadf3a0df5fae86a9386643c6d6d
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# Commerce Documentation governance

これはドキュメントチームの内部リファレンスです。 `TOC.md`にリストされていないため、ビルドもExperience Leagueに公開もされていません。 ここに保存して、管理するコンテンツに近づけます。

## 所有権

Commerce Insightsの記事は、記事の正確性と最新性を維持する責任のあるパブリッシング作成者またはパブリッシングチームによって所有されます。 これらの記事は現在、`commerce.en` リポジトリでホストされています。 Commerceのドキュメントチームが、コンテンツの品質を確保し、本番環境への公開をサポートします。

## Commerce Insightsの内容

- **ここに属しています**：実際のシナリオに基づく実装ガイダンスをカバーするCommerce ソリューションの戦略的ガイダンスとホワイトペーパー。 関連するCommerceのドキュメントページへのリンクを含めて、サポートを受けることができます。

- **製品リポジトリに属しています**：ステップバイステップの設定、チュートリアル、参考資料（API/CLI/設定リファレンス）、およびトラブルシューティング。 もし、ここに投稿したコンテンツがその種の詳細を集めたら、関連する商品ガイドに移動し、代わりにそのリンクを貼りましょう。

## 新しいコンテンツの追加

公開する記事のCOMDOX JIRA チケットを作成します。 `[templates/comdox-intake-template.md](templates/comdox-intake-template.md)`をチケットの説明にコピーして入力します。依頼者に対して、オーディエンスの特定、コンテンツが一時的なものかどうか（有効期限あり）のフラグ付け、およびCommerce製品ドキュメントではなくインサイトガイドに属していることを確認するように求めます。

チケットのスコープを設定したら、`templates/`のテンプレートから記事を開始します（`whitepaper-template.md`、`security-guidance-template.md`、`insight-perspective-template.md` – 未公開、関連する記事をターゲットファイルにコピーし、テンプレートの独自のフロントマタープレースホルダーコメントを削除）。 コンテンツを公開する準備ができたら、`TOC.md` エントリを追加します。

- **新しいトップレベルのセクション** （インサイト/カタログ管理など）では、ガイドのナビゲーション形状が変更されるため、追加する前にIA レビューが必要です。 Commerce AIを所有している人が誰で、ストーリーやタスクをレビューするかを調べます。

- **目次に追加** – 公開前に目次に新しいトピックを追加します。 必要に応じて、メタデータを非表示を使用して、リンクを持つユーザーのみがアクセスできる非表示の記事を公開します。 ExL作成者ガイドの「[&#x200B; コンテンツを非表示](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/hiding-files)」を参照してください。

## レビュー頻度

新しいCommerce ソリューションの名前が変更または更新された場合、またはインサイトが関連性がなくなった場合は、記事の内容を確認します。
