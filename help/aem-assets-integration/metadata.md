---
title: AEM AssetsのCommerce メタデータ
description: AEM Assetsとの統合によってAEM Assets オーサリング環境に追加されるCommerceの名前空間、メタデータスキーマ、代替テキストについて説明します。
feature: CMS, Media, Integration
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: da3860b0-d637-47df-bef0-273751180266
source-git-commit: 0c2e50338cbf286704239b6d1f628180e85a3bef
workflow-type: tm+mt
source-wordcount: 749
ht-degree: 0%

---

# AEM AssetsのCommerce メタデータ

Commerce metadataは、AEM AssetsとCommerce間の契約です。 Commerceに対して、Commerceのアセット、そのアセットがどの製品に属しているか、その使用方法や表示方法について説明します。 このメタデータを使用すると、AEM Assets統合でアセットファイルを正しくマッピングおよび同期できます。

Commerce メタデータを使用すると、次の機能が有効になります。

* **`commerce:isCommerce` フィールドを使用して、アセットをCommerceの対象**&#x200B;としてマークします。
* **アセットを`commerce:skus` フィールドを使用して1つ以上の製品SKU**&#x200B;に関連付けます。
* **Commerce**&#x200B;でのアセットの表示方法を、`commerce:roles`および`commerce:positions` フィールドを使用して定義します。
* **ストアビュー**&#x200B;でキーを設定したCommerce固有のalt テキストを、`commerce:altTextStoreViews`および`commerce:altTextValues` フィールドを介して追加します。
* **これらのフィールドを&#x200B;**[!UICONTROL Commerce]**タブとスキーマフォームを使用してAEM Assets プロパティ UI**&#x200B;で公開します。

>[!IMPORTANT]
>
>**Commerce固有の代替テキスト**&#x200B;機能は、[ セルフサービスオンボーディング ](get-started/configure-aem.md#enable-aem-commerce-self-service)を通じてまだ利用できません。 現在、`assets-commerce` カスタムコードパッケージをデプロイする場合にのみ提供されます（[assets-commerce パッケージを手動でインストールする](get-started/configure-aem.md#install-the-assets-commerce-package-manually)を参照）。 ネイティブサポートは、今後のAEM リリースで予定されています。

AEM プロジェクトでこれらのリソースを設定するには、[AEM Assets プロジェクトの設定](get-started/configure-aem.md)を参照してください。 このトピックの残りの部分では、メタデータの提供方法について説明します。

## AEM Commerce assets-commerce パッケージの内容

Adobeには、Experience Manager Assets as a Cloud Service設定にCommerce名前空間とメタデータスキーマリソースを追加するための`assets-commerce` AEM Commerce コードパッケージが用意されています。

このパッケージコードは、次のリソースをAEM Assets オーサリング環境に追加します。

* Commerce関連のプロパティを識別するための[ カスタム名前空間](https://github.com/ankumalh/assets-commerce/blob/main/ui.config/jcr_root/apps/commerce/config/org.apache.sling.jcr.repoinit.RepositoryInitializer~commerce-namespaces.cfg.json)、`Commerce`。

   * Adobe Commerce プロジェクトに関連付けられたCommerce アセットにタグ付けするためのラベル `Eligible for Commerce`を持つカスタムメタデータタイプ `commerce:isCommerce`。

   * カスタムメタデータタイプ `commerce:skus`と、対応するUI コンポーネントを使用して&#x200B;**[!UICONTROL Product Data]** プロパティを追加します。 商品データには、Commerce アセットを商品SKUに関連付けるためのメタデータプロパティが含まれています。

     ![ カスタム製品データ UI コントロール ](assets/aem-commerce-sku-metadata-fields-from-template.png){width="600" zoomable="yes"}

   * Commerceでのアセットの視覚化方法を示すカスタムメタデータタイプ `commerce:roles`および`commerce:positions`属性。

   * 代替テキスト マルチフィールド （_[!UICONTROL Alt texts]_） メタデータを使用して、エディターがCommerce ストアビューコードごとに代替テキストを入力できるようにします。 マルチフィールドは、インデックスで整列された2つの`String[]` プロパティに保持されます。

      * `commerce:altTextStoreViews` – 各行のビューコードを格納します。
      * `commerce:altTextValues` — `commerce:altTextStoreViews`の各エントリと同じインデックスにあるalt テキストに一致します。

     [外部マッチャー](synchronize/custom-match.md){target=_blank}を使用するApp Builderの実装では、アセットペイロードの変換時にこれらのプロパティをインターセプトできます。 これは、カタログ内での製品画像の割り当てやスコープ設定は変更されません。 AEM Assets メタデータの[ ローカライズされたalt テキスト ](#localized-alt-text-in-aem-assets-metadata)を参照してください。

* Commerce アセットのタグ付け用の`Eligible for Commerce`および`Product Data` フィールドを含むCommerce タブを持つメタデータスキーマフォーム。 このフォームには、AEM Assets UIから`roles`および`position` フィールドを表示または非表示にするオプションも用意されています。

  ![AEM Assets メタデータスキーマフォームの「Commerce」タブ ](assets/assets-configure-metadata-schema-form-editor.png){width="600" zoomable="yes"}

* 最初のアセットの同期をサポートするために、[ サンプルにタグ付けして承認されたCommerce アセット ](https://github.com/ankumalh/assets-commerce/blob/main/ui.content/src/main/content/jcr_root/content/dam/wknd/en/activities/hiking/equipment_6.jpg/.content.xml) `equipment_6.jpg`が含まれています。 AEM AssetsからAdobe Commerceに同期できるのは、承認済みのCommerce アセットのみです。

>[!NOTE]
>
> **AEM Commerce パッケージコード**&#x200B;について詳しくは、GitHubの[readme](https://github.com/ankumalh/assets-commerce) ページを参照してください。

## AEM Assets メタデータのローカライズされたalt テキスト

_[!UICONTROL Alt texts]_マルチフィールドは、対象となる画像を編集するときに、**[!UICONTROL Commerce]**タブのAEM Assets アセットメタデータエディターで使用できます。

>[!IMPORTANT]
>
> ストアごとのビューの動作は、代替テキストにのみ適用されます。 AEM Assetsとの連携では、Adobe Commerceのストアビューごとに異なる商品画像が同期されません。 AEMの製品画像は、このリリース以前と同じギャラリー割り当て動作で引き続きCommerceに同期されます。

マルチフィールドには、Commerce ストアビューごとに1行が含まれます。 各行には2つの入力があります。

* **[!UICONTROL Store View Code]** — ストアビュー識別子（`default`または`en_US`など）。

* **[!UICONTROL Alt Text]** – そのストアビューの代替テキスト（255文字に制限）。

追加のストアビュー用に行を追加するには、**[!UICONTROL Add]**&#x200B;を選択します。 行を削除するには、その行の&#x200B;**[!UICONTROL Delete]** アイコンを選択して削除します。

![ ストアビューコードと代替テキスト入力を含む代替テキストマルチフィールド ](assets/commerce-metadata-alt-texts-multifield.png){width="600" zoomable="yes"}

保存すると、クライアント側の検証により、任意の行に空の&#x200B;_[!UICONTROL Store View Code]_がある場合、または2つの行で同じストアビューコードが使用されている場合は、送信がブロックされます（大文字と小文字は区別されません）。

代替テキストエントリは、次の2つのインデックス整列`String[]` プロパティとしてJCR アセットメタデータに保持されます。

* `commerce:altTextStoreViews`：各行のビューコードを格納します。
* `commerce:altTextValues`: `commerce:altTextStoreViews`の各エントリと同じインデックスにあるalt テキストに一致します。

これらのアセットがAdobe Commerceに同期すると、一致するストアビューコードのストアごとのビュー代替テキストが商品メディアギャラリーに書き込まれます。 基になる画像マッピングは変更されません。
