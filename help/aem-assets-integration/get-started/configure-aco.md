---
title: Commerce Optimizer用AEM Assetsの設定
description: ' [!DNL Adobe Commerce Optimizer]のAEM Assets統合を設定する方法について説明します。'
feature: CMS, Media, Configuration, Integration
source-git-commit: 0c2e50338cbf286704239b6d1f628180e85a3bef
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 0%

---


# [!DNL Adobe Commerce Optimizer]のAEM Assetsを設定

[!BADGE SaaSのみ]{type=Positive tooltip="Adobe Commerce Optimizer プロジェクトにのみ適用されます。"}

[!DNL Adobe Commerce Optimizer]のAEM Assets統合により、販売者はAEM Assetsを商品画像用の一元的なデジタルアセット管理ソリューションとして使用できるようになります。 このガイドでは、[!DNL Commerce Optimizer]に固有の設定について説明します。

次の図は、[!DNL Adobe Commerce Optimizer]とAEM Assets統合の間の製品同期の概要です。

![AEM Assetsから[!DNL Commerce Optimizer] フロー](../assets/aco-asset-sync-architecture.png){width="700"}

この統合には、2つの独立したイベントフローがあります。 どちらも[Adobe I/O Events](https://developer.adobe.com/events/docs/)を使用してAssets Integration Serviceにイベントを転送しますが、各方向で独自のイベントプロバイダーが使用されます。

* **AEM AssetsからAssets Integration Serviceへ**: アセットが承認、拒否、または削除されると、そのイベントはAssets Integration Serviceに配信されます。 このサービスは、`match-by-SKU` （メタデータ駆動型）または[ カスタムマッチャー（App Builder） ](../synchronize/custom-match.md){target=_blank}を使用してアセットを製品と照合し、次に`product-asset` マッピングを[!DNL Commerce Optimizer]に送信し、そこで商品レイヤーとして保存します。

  >[!NOTE]
  >
  >統合で使用される`AEM-Assets` カタログレイヤーは、オンボーディング中に自動的に作成されます。 事前に作成する必要はありません。 カタログレイヤーの仕組みとAEM-Assets レイヤーの動作の背景については、[AEM-Assets レイヤー](../../optimizer/setup/catalog-layer.md#aem-assets-layer)を参照してください。

* **[!DNL Adobe Commerce Optimizer]からAssets Integration Service**&#x200B;へ：[!DNL Commerce Optimizer]で製品が更新されると、そのイベントはAssets Integration Serviceに配信されます。 サービスは、一致するアセットマッピングをすべて[!DNL Commerce Optimizer]に同期します。

## 制限

[!DNL Commerce Optimizer]統合には次の制限があります。

### レイヤー関連の制約

* AEM Assetsコンテンツには専用のレイヤーを使用します。

  AEM Assetsから送信されたペイロードは、Commerce Optimizer カタログレイヤーに入力されます。 そのレイヤーの値は、フィールドが指定されているベースカタログ属性を上書きします。 統合でペイロードのフィールドが省略されると、そのレイヤーの対応する値を空の値で上書きできます。 関連のないCommerce ワークフローでレイヤーを共有したり、AEM以外のAssets製品データを既に保存しているレイヤーを再利用したりすると、**意図しないデータ損失**&#x200B;や混乱を招く上書きが発生する可能性があります。 主にAEM駆動型の商品画像シンク用に、レイヤー名（デフォルトの&#x200B;**`AEM-Assets`**&#x200B;など）を予約します。

* この統合では、テナントごとに1つのカタログソース（1つのロケールと1つの名前付きレイヤー）をサポートしています。 現在、同じテナントに対して複数のAEM-Assets レイヤーまたは複数のロケールを設定することはサポートされていません。

* 既存のレイヤーを再利用したり、無関係なワークフローとレイヤーを共有したりすることは、回避可能なサポートケースの原因となることがよくあります。

### その他の制約

* **画像のみ**：この段階では、統合はビデオまたはその他のメディアタイプをサポートしていません。
* **カテゴリ画像がありません**: カテゴリ画像の同期を利用できません。 Assets セレクター（UI挿入）用のAEM Assetsのカテゴリ画像はサポートされていません。
* **マルチサイトの区別がありません**：統合でマルチサイトは処理されません。製品に関連付けられている画像は、すべてのチャネルとポリシーで同じように表示されます。
* **画像の位置/順序**：画像の位置と順序はサポートされていません。
* **製品が存在する必要があります**：製品が[!DNL Commerce Optimizer]に存在しない場合、その製品アセットマッピング用にレイヤーは作成されません。

## 前提条件

統合を設定する前に、次のことを確認してください。

* **Product Visuals**&#x200B;の使用権限を持つアクティブな[!DNL Adobe Commerce Optimizer] インスタンス （OpenAPI機能を備えたDynamic Media + [AEM Assets Prime](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-prime)）または、Dynamic Mediaを有効にした顧客提供のAEM Assets ライセンス （例：**AEM Assets Ultimate**）をバンドルします。
* AEM Assets as a Cloud Serviceへのアクセス。
* [!DNL Commerce Optimizer]とAEM Assetsの両方が同じAdobe IMS組織内にあります。
* AEM Assets環境でOpenAPIが有効になっているDynamic Media （イネーブルメント手順については、[AEM Assets プロジェクトの設定](configure-aem.md#prerequisites)を参照）。

### 最初にAEM Assetsを設定する

統合をサポートするには、AEM Assets統合を[!DNL Commerce Optimizer]にオンボーディングするプロセスを開始する前に、AEM Assets プロジェクトと環境を設定します。 これには、OpenAPI機能を備えたDynamic Mediaを有効にすることや、Commerce メタデータスキーマ、イベント、UIをAEM プロジェクトで利用できるようにすることなどが含まれます。

* [!BADGE おすすめ]{type=Positive} AEM リリース `2026.5.26309`以降では、コードをデプロイせずにCloud Managerからの統合を有効にします。 [Commerceとの連携を有効にする（セルフサービス） ](configure-aem.md#enable-aem-commerce-self-service)に従います。

* 以前のAEM リリースでは、`assets-commerce` パッケージを手動でデプロイします。
[Assets-commerce パッケージを手動でインストールします](configure-aem.md#install-the-assets-commerce-package-manually)。

>[!TIP]
>
> 現在のAEM バージョンは、右上のメニュー（**[!UICONTROL Help]** > **[!UICONTROL About AEM]**）から確認できます。

## オンボーディング

>[!IMPORTANT]
>
>[!DNL Commerce Optimizer]との統合を有効にするためのサポートチケットを送信する前に、[AEM Assets](#configure-aem-assets-first)の設定にプロセスを完了してください。 サポートするには、メタデータとイベントの`assets-commerce` パッケージ（またはセルフサービス対応）のデプロイメントなど、AEM Commerce統合をサポートするようにAEM Assets環境とプロジェクトを設定する必要があります。 AEMが設定される前にチケットを開くと、オンボーディングが遅れる可能性があります。

AEM Assets Integrationを[!DNL Commerce Optimizer]にオンボーディングするには、Adobe サポートがAdobe Commerce Optimizer インスタンスをAssets Integration Serviceに登録し、次の目的でサブスクライブする必要があります。

* AEM Assets イベント（アセット承認済み、更新、削除）
* [!DNL Commerce Optimizer]個のカタログイベント（製品が作成、更新されました）

このプロセスを開始するには、次の情報を含むサポートチケット ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket)を[作成します。

* **[!DNL Adobe Commerce Optimizer]テナント ID** （インスタンス ID）が[!DNL Commerce Optimizer] URLまたはCommerce Cloud Manager UIに見つかりました。
* **AEM プログラム IDとEnvironment ID**&#x200B;は、[統合にAEM Assets](#configure-aem-assets-first)を設定したときに設定します。
* **一致するルール**: SKUまたは[外部マッチャー（App Builder） ](../synchronize/custom-match.md){target=_blank}によって一致します。
* **レイヤー**: テナントを登録するカタログレイヤー名（**レイヤー関連の制約**&#x200B;を参照）。 意図的な場合にのみカスタム名を指定します。それ以外の場合は、デフォルトの&#x200B;**`AEM-Assets`**&#x200B;が使用されます。
* **ロケール**: テナントを登録するカタログ ソース ロケール （例：`en-US`）。 このロケールは、カタログビューと製品カタログデータで使用するロケールと一致している必要があります。

### カタログビューの設定

[!DNL Commerce Optimizer] テナントを登録したら、ストアフロントとAPIがAEM駆動型の画像データを表示するようにカタログビューを設定します。

* **カタログソース（ロケール）を選択** — サポートチケットで指定したロケールと同じロケール（例：**`en-US`**）を選択します。 統合では、テナントごとに1つのロケールを登録します。一致しない場合、同期された画像が目的のカタログビューに表示されません。
* **カタログレイヤーを割り当てる** — **`AEM-Assets`** レイヤー（またはチケットのカスタムレイヤー名）をそのカタログビューに割り当てます。

ロケールまたはレイヤーが正しく割り当てられていない場合、同期がアップストリームで成功したにもかかわらず、画像データが&#x200B;**表示されない**&#x200B;か、予期せず動作します。

## 同期

設定が完了すると、統合によって`product-asset` マッピングが自動的に同期されます。

詳しくは、[ カスタム自動一致](../synchronize/custom-match.md)を参照してください。

### SKU ワークフローによる一致の例

既存のアセットを新製品に追加する際の一般的な流れ：

1. [!DNL Commerce Optimizer]で製品を作成します（APIまたはデータ取り込み経由）。 製品は、最初は画像なしで存在できます。

1. AEM Assetsで、商品にマッピングするアセットを開きます。

1. 商品SKUを&#x200B;**commerce:skus** メタデータに追加し、画像の役割を割り当てます（例：`thumbnail`、`image`）。

1. アセットの配信を承認します。 これにより、Assets統合サービスが処理するイベントがトリガーされます。

1. Assets Integration Serviceは、product-image マッピングを[!DNL Commerce Optimizer]に送信します。 [!DNL Commerce Optimizer]の製品が、アセットの画像で更新されます。

1. 画像が表示されていることを確認します。 同期が完了するまで数分待ってから、[!DNL Commerce Optimizer] UIで製品を確認するか、ストアフロント APIをクエリして画像が返されることを確認します。

## 画像の役割の処理

製品に同じ画像の役割を使用する複数のアセットがある場合（例えば、`thumbnail`の役割を持つ2つのアセット）、統合により、その役割を1つのアセットのみが保持され、[!DNL Commerce Optimizer] レイヤーでの役割の重複とストアフロントの予期しない動作が回避されます。

**ビヘイビアー：** AEM Assetsから更新が送信されると、最も新しく更新されたアセットに画像の役割（`thumbnail`など）が割り当てられ、その役割は前のアセットから削除されます。 これにより、重複した画像の役割がストアフロントに表示されるのを防ぐことができます。

## その他

* [製品ビジュアル](../../optimizer/setup/product-visuals.md)
* [AEM Assets プロジェクトの設定](configure-aem.md)
* [カスタム自動一致](../synchronize/custom-match.md)
* [AEM Assetsとの連携の概要](../overview.md)
