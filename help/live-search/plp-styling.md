---
title: 製品リストページウィジェット
description: ' [!DNL Live Search Product Listing Page Widget]の有効化とスタイル設定'
exl-id: 50ba8046-869a-4071-b3a3-a6392544c07b
TQID: https://experienceleague.adobe.com/rEQBfgR9CqVBTFtBtq21QFZ6L5ZvoWJ02VI2xiWqAcw
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 539
ht-degree: 0%

---

# 製品リストページウィジェット

[!DNL Live Search Product Listing Page Widget] （PLP）は、Commerce サービス プラットフォームを使用して、パフォーマンスが高く、検索可能で、ファセット可能な製品リスト ページを提供します。 このトピックでは、PLP ウィジェットを有効にしてスタイル設定する方法について説明します。

## PLP ウィジェットの有効化

[!DNL Live Search] サービスがインストールされると、デフォルトの検索機能が自動的に[!DNL Live Search]に変換されます。

[!DNL Live Search] PLP ウィジェットは、新規インストールに対してデフォルトで有効になっています。

[!DNL Live Search]をアップグレードする場合、PLP ウィジェットが既にオフになっている場合は、そのまま残ります。

>[!NOTE]
>
>非推奨の検索アダプタから移行する場合は、[移行ガイド ](migrate-to-plp.md)で、シナリオ、前提条件、および手順ごとの手順に関する詳細なガイダンスを参照してください。

PLP ウィジェットをオンにするには：

1. Adobe Commerce管理者で、「Stores → Settings → Configuration」に移動します。
1. 左側のナビゲーションで、**[!UICONTROL Live Search]** > **[!UICONTROL Storefront Features]**&#x200B;をクリックします。
1. 「[!UICONTROL Storefront Features]」セクションをクリックします。
1. Set [!UICONTROL Enable Product Listing Widget] = Yes
1. 設定を保存
1. プロンプトが表示されたら、キャッシュをフラッシュします（システム/ツール/キャッシュ管理/[!UICONTROL Flush Magento Cache]に移動）。

>[!IMPORTANT]
>
>[!DNL Live Search Product Listing Page Widget]が有効になっている場合、製品リストページの並べ替え順序を変更できません。

## ウィジェットの機能

PLP ウィジェットには、次のすぐに使える機能が用意されています。

- 「カートに追加」ボタン – シンプルな商品でのみ利用可能。
- 製品ごとに複数の画像 – 設定可能な製品に異なる色を選択すると、画像が変更される場合があります。
- カラースウォッチのサポート – コードを正しく検証するには、カラー属性に「`color`」のスペルを付ける必要があります。

### ウィジェットのカスタマイズ

PLP ウィジェットのすぐに使える機能に加えて、ウィジェットをさらにカスタマイズして次の機能を含めることができます。

- 属性によるフィルタリング
- 多言語サポート
- 価格スライダー

上記の機能を処理するようにPLP ウィジェットをカスタマイズする方法について詳しくは、次の[ リポジトリ ](https://github.com/adobe/storefront-product-listing-page/)の`storefront-product-listing-page`のreadmeを参照してください。 このリポジトリのreadmeでは、PLP ウィジェットをカスタマイズしてサイトにデプロイする方法の例を示します。

>[!WARNING]
>
>リポジトリで使用可能なコードを使用してPLP ウィジェットをカスタマイズする場合は、メンテナンスと必要な更新の責任を負います。 Adobeがリリースする新しいPLP ウィジェット機能は、カスタマイズした実装と互換性がない可能性があります。

## スタイル設定の例

[CSS](https://developer.adobe.com/commerce/frontend-core/guide/css/)を使用して、PLP ウィジェットの外観をサイトに合わせてカスタマイズできます。

>[!NOTE]
>
>Adobe Commerce テーマ内のカスタムクラスを持つエレメントは継承されません。 これらの要素は、カスタムクラスに一致するように、特定のクラスでターゲットにする必要があります。プライマリアクションクラスは、ウィジェットボタンでは動作しません。 CSS内の汎用ターゲット要素は継承されます。`button`はウィジェットボタンに適用されます。

ハイライト表示されたdivには、ターゲットクラス `ds-sdk-product-item__product-name`が含まれています。

![Pagination](assets/plp-css-example.png)

大文字にするルールを追加して、製品名をカスタマイズします。

```css
.ds-sdk-product-item__product-name {
 text-transform: uppercase;
}
```

![Pagination](assets/plp-css-example-after.png)

## CSS クラス

### 製品リスト

- `.ds-sdk-product-list`：外部div
- `.ds-sdk-product-list__grid`：内部div

![Pagination](assets/plp-css-product-list.png)

#### 製品リストのページネーション

- `.ds-plp-pagination`

![Pagination](assets/plp-css-pagination.png)

- `.ds-plp-pagination_item`

![ ページネーション項目](assets/plp-css-pagination-item.png)

- `.ds-plp-pagination_item--current`

![現在のアイテムをページ化](assets/plp-css-pagination-item-current.png)

### ウィジェット

- `.ds-widgets`：外部div
- `.ds-widgets__actions`：左側の内側div
- `.ds-widgets__results`：右側の内側div

![ ウィジェット結果](assets/plp-css-widgets.png)

### 並べ替えドロップダウン

- `.ds-sdk-sort-dropdown`

![並べ替えドロップダウン ](assets/plp-css-dropdown.png)

- `.ds-sdk-sort-dropdown__button`

![ ドロップダウンボタン ](assets/plp-css-dropdown-button.png)

- `.ds-sdk-sort-dropdown__items`

![ ドロップダウンアイテム ](assets/plp-css-dropdown-items.png)

- `.ds-sdk-sort-dropdown__items--item`

![ ドロップダウンアイテム ](assets/plp-css-dropdown-item.png)

- `.ds-sdk-sort-dropdown__items--item-selected`

![選択した項目をドロップダウン ](assets/plp-css-dropdown-selected.png)

- `.ds-sdk-sort-dropdown__items--item-active`

![ アクティブな選択範囲をドロップダウン ](assets/plp-css-dropdown-active.png)

### ファセット

- `.ds-plp-facets`
- `.ds-plp-facets__header`
- `.ds-plp-facets__header_title`
- `.ds-plp-facets__header__clear-all`

![ ファセット ヘッダーのタイトル ](assets/plp-css-facets-title-clear.png){width="350"}

- `.ds-plp-facets__pills`
- `.ds-sdk-pill`

![ ファセット ピル ](assets/plp-css-facets-pill.png){width="350"}

- `.ds-sdk-pill__label`
- `.ds-sdk-pill__cta`

![ ファセットラベル ](assets/plp-css-pill-label-cta.png){width="350"}

- `.ds-plp-facets__list`

![ ファセットリスト ](assets/plp-css-facets-list.png){width="350"}

- `.ds-sdk-input`
- `.ds-sdk-input__label`
- `.ds-sdk-product-item__product-swatch-group`
- `ds-sdk-product-item__product-swatch-item`
- `.ds-sdk-input_fieldset_show-more`

![入力](assets/plp-css-sdk-input.png)

- `.ds-sdk-labelled-input`

![ ラベル付き入力](assets/plp-css-labelled-input.png)

- `.ds-sdk-labelled-input__input`
- `.ds-sdk-labelled-input__label`

![入力ラベル ](assets/plp-css-labelled-input-label.png)

### 製品項目

- `.ds-sdk-product-item`
- `.ds-sdk-product-item__image`
- `.ds-sdk-product-item__product-name`
- `.ds-sdk-product-item__product-options`
- `.ds-sdk-product-price`
   - `.ds-sdk-product-price--no-discount`
   - `.ds-sdk-product-price--grouped`
   - `.ds-sdk-product-price--bundle`
   - `.ds-sdk-product-price--discount`

![製品](assets/plp-css-product.png)

### 読み込み

- `.ds-sdk-loading`
- `.ds-sdk-loading__spinner`
- `.ds-sdk-loading__spinner-label`

![ インジケーターを読み込んでいます](assets/plp-css-loading.png)

## PLP ウィジェットの無効化

PLP ウィジェットを無効にするには：

1. **Stores** / 設定/**設定** / **[!DNL Live Search]** / **Storefront機能**&#x200B;に移動し、**製品リストウィジェットを有効にする**&#x200B;を「いいえ」に設定します。
1. 設定を保存するには、**設定を保存**&#x200B;を選択します。
