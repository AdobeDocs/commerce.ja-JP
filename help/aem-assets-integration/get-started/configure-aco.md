---
title: Commerce Optimizer用AEM Assetsの設定
description: ' [!DNL Adobe Commerce Optimizer]のAEM Assets統合を設定する方法について説明します。'
feature: CMS, Media, Configuration, Integration
source-git-commit: 2cc7b70a6923687c74fe3f4b88448eaada6d16af
workflow-type: tm+mt
source-wordcount: '1453'
ht-degree: 0%

---


# [!DNL Adobe Commerce Optimizer]のAEM Assetsを設定

[!BADGE SaaSのみ]{type=Positive tooltip="Adobe Commerce Optimizer プロジェクトにのみ適用されます。"}

[!DNL Adobe Commerce Optimizer]のAEM Assets統合により、販売者はAEM Assetsを商品画像用の一元的なデジタルアセット管理ソリューションとして使用できるようになります。 このガイドでは、[!DNL Commerce Optimizer]に固有の設定について説明します。

Adobe Commerce （PaaS）または[!DNL Adobe Commerce as a Cloud Service]とは異なり、[!DNL Commerce Optimizer]には管理者設定UIがありません。 統合を有効にするには、[!DNL Adobe Commerce Optimizer]とAEM Assetsの詳細を記載したサポートチケットを作成します。 Adobe サポートは、統合を設定し、Assets Integration Serviceにテナントを登録します。

**チケットを送信する前にAEM Assetsを準備します。** テナント登録では、AEM側がCommerceで使用できることを前提としています。 例えば、メタデータとイベントが説明どおりに機能するように、AEM Commerce `assets-commerce` パッケージをデプロイした後です。 **AEMが設定される前にチケットを開くと、オンボーディングが遅れる可能性があります。**

次の図は、[!DNL Adobe Commerce Optimizer]とAEM Assets統合の間の製品同期の概要です。

![AEM Assetsから[!DNL Commerce Optimizer] フロー](../assets/aco-asset-sync-architecture.png){width="700"}

この統合には、主に2つのフローがあります。

* **AEM Assets**&#x200B;から：アセットが承認、拒否、または削除されると、イベントはAdobe パイプラインを通じてAssets Integration Serviceに流れます。 このサービスは、`match-by-SKU` （メタデータ駆動型）または[&#x200B; カスタムマッチャー（App Builder） &#x200B;](../synchronize/custom-match.md){target=_blank}を使用してアセットを商品と照合し、次に`product-asset` マッピングをCommerce Optimizerに送信し、そこで商品レイヤーとして保存します。

* **[!DNL Adobe Commerce Optimizer]**&#x200B;から：[!DNL Commerce Optimizer]で商品が更新されると、イベントはAdobe パイプラインを経由してAssets Integration Serviceに流れます。 サービスは、一致するアセットマッピングをすべて[!DNL Adobe Commerce Optimizer]に同期します。

## 前提条件

統合を設定する前に、次のことを確認してください。

* 製品ビジュアルの使用権限を持つアクティブな[!DNL Adobe Commerce Optimizer] インスタンス、またはDynamic Mediaを持つ任意のAEM Assets ライセンス。
* AEM Assets as a Cloud Serviceへのアクセス。
* [!DNL Commerce Optimizer]とAEM Assetsの両方が同じAdobe IMS組織内にあります。
* AEM Assets環境でOpenAPIが有効になっているDynamic Media （イネーブルメント手順については、[AEM Assets プロジェクトの設定](configure-aem.md#prerequisites)を参照）。

## 最初にAEM Assetsを設定する

テナント登録用のサポートチケット [&#128279;](#onboarding)を発行する&#x200B;**前**&#x200B;のAEM Assets手順を完了します。 インストールパターンはAdobe Commerce as a Cloud Serviceと一致します。[Commerce メタデータをサポートするようにAEM Assets プロジェクトを設定する](configure-aem.md)を参照してください。

### 手順1:AEM Commerce パッケージのデプロイ

AEM プロジェクトに`assets-commerce` パッケージをインストールしてデプロイし、Commerce メタデータスキーマ、イベント、UIを利用できるようにします。

[&#x200B; パッケージ `assets-commerce`をインストール &#x200B;](configure-aem.md#step-1-install-the-assets-commerce-package)で完全な手順を実行します。 サポートチケットを発行する前に、次の手順に従います。

1. Cloud Manager Git リポジトリを複製し、[AEM Assets Commerce リポジトリ &#x200B;](https://github.com/ankumalh/assets-commerce) コードをプロジェクトにコピーします。

1. プロジェクトのすべての`filter.xml`および`pom.xml` ファイルで、&lt;my-app>のすべての出現箇所をアプリ名に置き換えます。

1. デプロイメントパイプラインをコミット、プッシュ、実行し、アセットプロパティに「**[!UICONTROL Commerce]**」タブが表示されていることを検証します。

**[!UICONTROL Commerce]** タブが見つからない場合は、[Cloud Managerのスクリーンショット、パイプラインの手順、およびトラブルシューティングについては、`assets-commerce` パッケージ &#x200B;](configure-aem.md#step-1-install-the-assets-commerce-package)のインストールを参照してください。

### 手順2:OpenAPIでDynamic Mediaを有効にする

OpenAPI機能を備えたDynamic Mediaは、AEM Assets環境で有効にする必要があります。 セルフサービスパス（製品ビジュアル用のCloud Managerなど）とAdobe サポートルートについては、[AEM Assets プロジェクトの設定](configure-aem.md#prerequisites)で説明しています。

### 手順3:Commerce メタデータの適用とアセットの承認

AEM Assetsの商品画像にCommerce メタデータを追加します。フィールド定義については、[AEM Commerce パッケージの内容](configure-aem.md#aem-commerce-assets-commerce-package-contents)を参照してください。

トリガーにデータを同期するには、アセットが&#x200B;**承認済み** ステータスである必要があります。 メタデータのみを保存しても、イベントはトリガーされません。

### ステップ 4: オプション — Commerce メタデータプロファイルの設定

AEM メタデータプロファイルを使用してオーサリングを効率化する場合は、**パッケージがデプロイされた**&#x200B;後に設定し、必須のCommerce フィールドを理解します。これは、**AEM Assets プロジェクトの設定**&#x200B;と同じオプションパターンです。

[&#x200B; メタデータプロファイルの設定](configure-aem.md#step-2-optional-configure-a-metadata-profile)を参照してください。

## 制限

[!DNL Commerce Optimizer]統合には次の制限があります。

### レイヤー関連の制約

このセクションを読む&#x200B;**before** サポートチケットでカタログレイヤー名を選択します。 このコンテキストを使用せずにレイヤーを選択または共有することは、予防可能なサポートケースの頻繁な原因です。

**AEM Assets コンテンツに専用レイヤーを使用します。** AEM Assetsから送信されたペイロードは、Commerce Optimizer カタログ **レイヤー**&#x200B;に入力されます。 フィールドが指定されているベースカタログ属性を&#x200B;**上書き**&#x200B;のレイヤーの値。 統合でペイロードのフィールドが省略されると、そのレイヤーの対応する値が空の値で上書きされる場合があります。 関連のないCommerce ワークフローでレイヤーを共有したり、AEM以外のAssets製品データを既に保存しているレイヤーを再利用したりすると、**意図しないデータ損失**&#x200B;や混乱を招く上書きが発生する可能性があります。 サポートチケットを開く&#x200B;**前**&#x200B;にレイヤーの選択を計画し、そのレイヤー名（デフォルトの&#x200B;**`AEM-Assets`**&#x200B;など）は主にAEM主導の商品イメージの同期のために予約します。

>[!IMPORTANT]
>
>統合では、テナントごとに&#x200B;**1つのカタログソース**&#x200B;をサポートしています。1つのロケールと&#x200B;**1つの名前付きレイヤー**。 現在、同じテナントに対して複数のAEM-Assets レイヤーまたは複数のロケールを設定することはサポートされていません。

### その他の制約

* **画像のみ**：この段階では、統合はビデオまたはその他のメディアタイプをサポートしていません。
* **カテゴリ画像がありません**: カテゴリ画像の同期を利用できません。 Assets セレクター（UI挿入）用のAEM Assetsのカテゴリ画像はサポートされていません。
* **マルチサイトの区別がありません**：統合でマルチサイトは処理されません。製品に関連付けられている画像は、すべてのチャネルとポリシーで同じように表示されます。
* **画像の位置/順序**：画像の位置と順序はサポートされていません。
* **製品が存在する必要があります**：製品が[!DNL Commerce Optimizer]に存在しない場合、その製品アセットマッピング用にレイヤーは作成されません。

## オンボーディング

AEM Assets統合を[!DNL Commerce Optimizer]でオンボーディングするには、[&#x200B; サポートチケットを作成](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket)する必要があります。

Adobe サポートは、チケット内の情報を使用して、Assets Integration Serviceにテナントを登録し、統合を設定します。

チケットを送信する前に、[AEM Assetsを最初に設定](#configure-aem-assets-first)を完了していることを確認してください。

サポートチケットに次の情報を含めます。

* **[!DNL Adobe Commerce Optimizer]テナント ID** （インスタンス ID）が[!DNL Commerce Optimizer] URLまたはCommerce Cloud Manager UIに見つかりました。
* **AEM プログラム ID**。
* **AEM Environment ID**。
* **一致するルール**: SKUまたは[外部マッチャー（App Builder） &#x200B;](../synchronize/custom-match.md){target=_blank}によって一致します。
* **レイヤー**: テナントを登録するカタログレイヤー名（**レイヤー関連の制約**&#x200B;を参照）。 意図的な場合にのみカスタム名を指定します。それ以外の場合は、デフォルトの&#x200B;**`AEM-Assets`**&#x200B;が使用されます。
* **ロケール**: テナントを登録するカタログ ソース ロケール （例：`en-US`）。 これは、カタログビューと製品カタログデータで使用するロケールと一致する必要があります。

Adobe サポートがチケットを処理すると、統合が設定され、テナントがAssets Integration Serviceに登録されます。

オンボーディングが完了したら：

1. **Assets Integration Serviceへの登録**：お客様の[!DNL Commerce Optimizer] テナントは、[!DNL Adobe Commerce Optimizer] テナント ID、AEM プログラム ID、AEM Environment ID、一致するルール、ロケール、およびチケットで指定されたレイヤー名を使用してAssets Integration Serviceに登録されます。

1. **イベントサブスクリプション**:Assets Integration Serviceのサブスクリプション：

   * AEM Assets イベント（アセット承認済み、更新、削除）
   * [!DNL Commerce Optimizer]個のカタログイベント（製品が作成、更新されました）

ストアフロントとAPIがAEM駆動型の画像データを表示するように、[&#x200B; カタログビュー](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-view)を設定します。

* **カタログ ソース （ロケール）** — サポート チケットで指定したロケールと同じロケール （例：**`en-US`**）を選択します。 統合では、テナントごとに1つのロケールを登録します。一致しない場合、同期された画像が目的のカタログビューに表示されません。
* **カタログレイヤー** - **`AEM-Assets`** レイヤー（またはチケットのカスタムレイヤー名）をそのカタログビューに割り当てます。

ロケールまたはレイヤーが正しく割り当てられていない場合は、同期がアップストリームで成功したにもかかわらず、画像データが&#x200B;**表示されなかったり**&#x200B;予期せず動作したりする可能性があります。

## 同期

設定が完了すると、統合によって`product-asset` マッピングが自動的に同期されます。

詳しくは、[&#x200B; カスタム自動一致](../synchronize/custom-match.md)を参照してください。

### SKU ワークフローによる一致の例

既存のアセットを新製品に追加する際の一般的な流れ：

1. [!DNL Commerce Optimizer]で製品を作成します（APIまたはデータ取り込み経由）。 製品は、最初は画像なしで存在できます。

1. AEM Assetsで、商品にマッピングするアセットを開きます。

1. 商品SKUを&#x200B;**commerce:skus** メタデータに追加し、画像の役割を割り当てます（例：`thumbnail`、`image`）。

1. アセットの配信を承認します。 これにより、Assets Integration Serviceが処理するイベントがトリガーされます。

1. Assets Integration Serviceは、product-image マッピングを[!DNL Commerce Optimizer]に送信します。 [!DNL Commerce Optimizer]の製品が、アセットの画像で更新されます。

1. 画像が表示されていることを確認します。 同期が完了するまでの時間（通常は数分以内）を許可してから、[!DNL Commerce Optimizer] UI （データ同期やカタログビューなど）で商品を確認するか、ストアフロント API （カタログサービス、ライブサーチ、ストアフロントGraphQL API）をクエリして、画像が返されることを確認します。

## 画像の役割の処理

製品に同じ画像の役割を使用する複数のアセットがある場合（例えば、`thumbnail`の役割を持つ2つのアセット）、統合により、その役割を1つのアセットのみが保持され、[!DNL Commerce Optimizer] レイヤーでの役割の重複とストアフロントの予期しない動作が回避されます。

**ビヘイビアー：** AEM Assetsから更新が送信されると、最も新しく更新されたアセットに画像の役割（`thumbnail`など）が割り当てられ、その役割は前のアセットから削除されます。 これにより、重複した画像の役割がストアフロントに表示されるのを防ぐことができます。

## その他

* [製品ビジュアル](../../optimizer/setup/product-visuals.md)
* [AEM Assets プロジェクトの設定](configure-aem.md)
* [カスタム自動一致](../synchronize/custom-match.md)
* [AEM Assetsとの連携の概要](../overview.md)
