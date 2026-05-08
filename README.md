---
source-git-commit: e761e54e7bd7997f3f40b1dfc1293012931111b0
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---
# Adobe Commerceのユーザーガイド

私たちは、コミュニティやAdobeの職員によるドキュメント部門以外からの貢献を歓迎します。

## AdobeオープンSource行動規範

このプロジェクトでは、[Adobe Open Source Code of Conduct](code-of-conduct.md)または[.NET Foundation Code of Conduct](https://dotnetfoundation.org/code-of-conduct)を採用しています。 詳しくは、[寄付](contributing.md)の記事を参照してください。

## Adobe コンテンツへのコントリビューションについて

[Adobe Docs Contributor Guide](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html)を参照してください。

貢献の方法は、自身が誰であるか、また貢献したい変更の種類によって異なります。

### 軽微な変更

マイナーアップデートを投稿する場合は、記事にアクセスし、記事の下部に表示されるフィードバック領域をクリックし、**詳細なフィードバックオプション**&#x200B;をクリックしてから、**編集を提案**&#x200B;をクリックして、GitHubのマークダウンソースファイルに移動します。 GitHub UIを使用して更新します。 詳しくは、[Adobe Docs コントリビューターガイド ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html)を参照してください。

このリポジトリのドキュメントやコード例に対して提出する軽微な修正や明確化は、Adobe利用条件の対象となります。

### コミュニティメンバーからの主な変更点や新しい記事

Adobe コミュニティに参加していて、新しい記事を作成したり、大きな変更を送信したりしたい場合は、Git リポジトリの「イシュー」タブを使用してイシューを送信し、ドキュメントチームとの会話を開始してください。 計画に同意したら、従業員と協力して、公開リポジトリと非公開リポジトリの作業を組み合わせて、新しいコンテンツを導入する必要があります。

### Adobe社員の主な変化

テクニカルライター、プログラムマネージャー、またはAdobe Experience Cloud ソリューションのプロダクトチームの開発者で、技術記事の投稿や作成を担当する場合は、`https://git.corp.adobe.com/AdobeDocs`にあるプライベートリポジトリを使用してください。

## ツールと設定

コミュニティのコントリビューターは、GitHub UIを使用して基本的な編集をおこなったり、リポジトリをフォークして主要なコントリビューションを作成したりできます。

詳しくは、[Adobe Docs Contributor Guide](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html)を参照してください。

## Markdownを使用してトピックを書式設定する方法

このリポジトリのすべての記事では、GitHubでカスタマイズされたMarkdownを使用しています。 Markdownに詳しくない方は、以下を参照してください。

- [Markdownの基本](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)
- [印刷可能なマークダウンのチートシート](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf)

## 画像の最適化のためのプリコミットフック

このリポジトリには、コミット前に画像を最適化する自動のプリコミットフックが含まれています。 **すべてのコントリビューターは、一貫した画像の最適化とリポジトリサイズの削減を確実にするために、これらのフック**&#x200B;を有効にする必要があります。

### クイック設定

リポジトリのクローンを作成したら、次を実行します。

```bash
.githooks/setup-hooks.sh
```

### フックの機能

- ステージングされた画像ファイルを自動検出（PNG、JPG、JPEG、GIF、SVG）
- `image_optim`を実行して画像を圧縮および最適化
- 最適化された画像を自動的にリステージ
- コミットされたすべての画像が適切に最適化されていることを確認します

### Adobe Workfrontの利点

- リポジトリサイズの削減
- ドキュメントのページ読み込みを高速化
- あらゆる貢献者で一貫した画質
- 手作業による最適化は不要です

セットアップ手順、トラブルシューティング、設定の詳細については、[`.githooks/README.md`](.githooks/README.md)を参照してください。

## 使用可能なレイク タスク

このリポジトリは、`adobe-comdox-exl-rake-tasks` gemが提供するrake タスクを使用します。 使用可能なすべてのタスクを表示するには、次を実行します。

```bash
cd _jekyll
bundle exec rake --tasks
```
