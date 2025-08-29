---
source-git-commit: 39977196f322cac571ecdb0219f006970aff3575
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 5%

---
# Adobe Commerce技術ドキュメント

ドキュメントチーム以外のAdobe社員やコミュニティからのコントリビューションを歓迎します。

## Adobe オープン Source行動規範

このプロジェクトでは、[アドビオープンソース行動規範](code-of-conduct.md) または [.NET Foundation 行動規範](https://dotnetfoundation.org/code-of-conduct)を採用しています。詳しくは、[投稿](contributing.md)の記事を参照してください。

## Adobe コンテンツへの投稿について

[Adobe ドキュメント投稿者ガイドを参照してください ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html)。

投稿方法は、投稿者と、投稿したい変更の種類に応じて異なります。

### 軽微な変更

軽微な変更をコントリビューションする場合は、記事にアクセスして記事の下部に表示されるフィードバックエリアをクリックし、**詳細なフィードバックオプション** をクリックします。次に、**編集の提案** をクリックして、GitHub の Markdown ソースファイルに移動します。 GitHub UI を使用して更新を行います。 一般的な [Adobe ドキュメント投稿者ガイド ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html) を参照してください。

このリポジトリのドキュメントおよびコード例について投稿者が送信した軽微な修正や説明は、Adobeの利用規約の対象となります。

### コミュニティメンバーによる大幅な変更または新しい記事

Adobe コミュニティのメンバーが新しい記事を作成したり、大きな変更をコントリビューションしたりする場合は、Git リポジトリーの「イシュー」タブを使用してイシューを送信し、ドキュメントチームとのやり取りを開始してください。 計画に同意したら、公開リポジトリと非公開リポジトリでの作業を組み合わせて新しいコンテンツを取り込むために、従業員と協力する必要があります。

### Adobe社員からの大きな変化

Adobe Experience Cloud ソリューションの製品チームのテクニカルライター、プログラムマネージャー、または開発者で技術記事の投稿または作成を担当している場合は、`https://git.corp.adobe.com/AdobeDocs` のプライベートリポジトリを使用する必要があります。

## ツールと設定

コミュニティのコントリビューターは、基本的な編集を行う場合は GitHub UI を使用し、大きな変更を加える場合はリポジトリをフォークします。

詳しくは、[Adobe ドキュメント投稿者ガイド ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html) を参照してください。

## Markdown を使用してトピックを書式設定する方法

このリポジトリ内の記事はすべて、GitHub 固有の Markdown を使用しています。 Markdown について詳しくは、以下を参照してください。

- [Markdown の基本 ](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)
- [ 印刷用 Markdown チートシート ](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf)

## 画像の最適化のプリコミットフック

このリポジトリには、コミット前に画像を最適化する、自動プリコミットフックが含まれています。 **すべてのコントリビューターは、これらのフックを有効にして** 一貫性のある画像の最適化とリポジトリサイズの縮小を実現する必要があります。

### クイックセットアップ

リポジトリのクローンを作成したら、次のコマンドを実行します。

```bash
.githooks/setup-hooks.sh
```

### フックの機能

- ステージングされた画像ファイル（PNG、JPG、JPEG、GIF、SVG）を自動検出
- `image_optim` を実行して画像を圧縮および最適化する
- 最適化された画像を自動的に再ステージ
- コミットされたイメージがすべて適切に最適化されていることを確認します。

### 利点

- リポジトリサイズの縮小
- ドキュメントのページ読み込みの高速化
- すべてのコントリビューターで一貫した画質
- 手動での最適化は不要です

設定手順、トラブルシューティング、設定について詳しくは、[`.githooks/README.md`](.githooks/README.md) を参照してください。
