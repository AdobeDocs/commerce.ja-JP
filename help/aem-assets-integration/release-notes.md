---
title: AEM Assets統合のリリースノート
description: すべてのAEM Assets統合リリースについて詳しくは、リリースノートを参照してください。
feature: CMS, Media, Release Notes
exl-id: 0d639565-812f-481a-afd6-6e6fa54ed70e
source-git-commit: cd7a332dd09840aabcc0efae081ba0a713506897
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 0%

---

# AEM Assets統合のリリースノート

このリリースノートでは、AEM Assets統合のすべてのリリースについて説明します。次の内容が含まれます。

![新機能](../assets/new.svg)
![修正された問題](../assets/fix.svg)修正と改善
![既知の問題](../assets/bug.svg)既知の問題

通常の機能リリースバージョン以外でリリースされた機能の変更と修正については、_ホスト型サービスの更新_&#x200B;の節を参照してください。

今後のリリース、製品サポート、およびAEM Assets Integration拡張機能をサポートするAdobe Commerce バージョンについて詳しくは、「Adobe Commerce [&#x200B; リリーススケジュール &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule)」および「[製品の可用性](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability)」のトピックを参照してください。

## ホスト型サービスの更新

このリリースノートでは、ホストされたサービスの通常の機能リリース以外で発生した機能変更と修正について説明します。

+++ホスト型サービスの更新

_2025年9月11日_

![新しい問題](../assets/new.svg)新しい[属性を持つ](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank} カスタム自動一致`asset_matches` エンドポイントを更新しました。

_2025年2月11日_

![新しい問題](../assets/new.svg)これで、マーチャントは商品とカテゴリの画像を同期できます。

+++

## v1.3.5

_2026年4月1日_

[!BADGE Adobe Commerce バージョン 2.4.5以降のリリースを]{type=Informative tooltip="サポート対象"} サポートしています。

![修正済みの問題](../assets/fix.svg)<!-- Issue ACAP-1223 -->構成可能な製品の管理者に、製品イメージの役割の重複セットが表示される問題を修正しました。

![修正済みの問題](../assets/fix.svg)<!-- Issue CCSAAS-4769 --> アップグレードまたはデータパッチ中に統合性制約の違反を引き起こした`UpdateAssetImageRolesDataPatch`の問題を修正しました。

## v1.3.4

_2026年3月11日_

[!BADGE Adobe Commerce バージョン 2.4.5以降のリリースを]{type=Informative tooltip="サポート対象"} サポートしています。

![新しい問題](../assets/new.svg)<!-- Issue PAY-1041 --> Adobe Commerce 2.4.9-beta1およびPHP 8.5のサポートを追加しました。

![新しい問題](../assets/new.svg)<!-- Issue ACCS-169 --> **[!UICONTROL Program ID]**、**[!UICONTROL Environment ID]**、[**[!UICONTROL Domain mapping]**](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/domain-mappings/add-domain-mapping){target=_blank} フィールドが、[&#x200B; ユーザーのIMS セッション &#x200B;](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/permissions#user-permissions-and-ims){target=_blank}に基づいて、ドロップダウンとして自動入力されるようになりました。

## v1.2.14

_2026年2月13日_

[!BADGE Adobe Commerce バージョン 2.4.5以降のリリースを]{type=Informative tooltip="サポート対象"} サポートしています。

![修正済みの問題](../assets/fix.svg)<!-- Issue ACCS-171 --> ランタイムアクションのドロップダウンに、ページのリロード後に保存されていないワークスペースデータが表示される[&#x200B; カスタムマッチャー](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match)の問題を修正しました。

## v1.2.13

_2026年2月10日_

[!BADGE Adobe Commerce バージョン 2.4.5以降のリリースを]{type=Informative tooltip="サポート対象"} サポートしています。

![新しい問題](../assets/new.svg)<!-- Issue ACCS-171 --> **[!UICONTROL Adobe I/O Workspace Configuration]**&#x200B;一致するカスタム [設定を簡素化する](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank} フィールドを追加しました。 マーチャントは、App Builder `workspace.json` ファイルをアップロードして、OAuth資格情報とランタイムアクションエンドポイントを自動的に入力できるようになりました。

## v1.2.12

_2026年1月29日_

[!BADGE Adobe Commerce バージョン 2.4.5以降のリリースを]{type=Informative tooltip="サポート対象"} サポートしています。

![修正済みの問題](../assets/fix.svg)<!-- Issue ACAP-1206 --> アセットの同期中に、アセットの役割のカスタム属性の古い`no_selection`値が削除されず、一部の画像がEdge Delivery Servicesで正しく表示されない問題を修正しました。

## v1.2.11

_2026年1月15日_

[!BADGE Adobe Commerce バージョン 2.4.5以降のリリースを]{type=Informative tooltip="サポート対象"} サポートしています。

![修正済みの問題](../assets/fix.svg)<!-- Issue ACAP-1180 --> AEM アセットはCDNによって動的に最適化されているため、ファイルサイズとディメンションを非表示にすることで、商品編集ページを改善しました。 AEM Assets統合が有効になっている場合に、ページが正しくプリレンダリングされるようになりました。

## v1.2.10

_2026年1月12日_

[!BADGE Adobe Commerce バージョン 2.4.5以降のリリースを]{type=Informative tooltip="サポート対象"} サポートしています。

![修正済みの問題](../assets/fix.svg)<!-- Issue ACAP-1178 -->製品に画像があり、AEM Assets統合が有効になっている場合に、REST APIを介して製品のカスタム属性を更新できない問題を修正しました。 現在、製品カスタム属性はREST APIを介して正しく更新されます。

![修正済みの問題](../assets/fix.svg)<!-- Issue ACAP-1172 -->製品編集ページの管理UIで、非表示の製品画像が非表示として表示されない問題を修正しました。 これで、画像の表示ステータスが正しく表示されるようになりました。

![修正済みの問題](../assets/fix.svg)<!-- Issue ACAP-1170 -->逆シリアル化エラーにより、AEM Assetsの製品画像がAdobe Commerceに同期されない問題を修正しました。 これで、すべての画像属性（`image`、`small_image`、および`swatch_image`）が正しく同期されるようになりました。

## v1.2.7

_2025年11月6日_

[!BADGE Adobe Commerce バージョン 2.4.5以降のリリースを]{type=Informative tooltip="サポート対象"} サポートしています。

![修正済みの問題](../assets/fix.svg)<!-- Issue ACAP-1169 --> **ミニカート**、**カート**、**チェックアウト** ページでAEM Assets統合を有効にした後、商品のサムネイル画像が一貫性なく表示される問題を修正しました。 これにより、ページを更新した後でも、あらゆるページをまたいで一貫性のある商品画像をレンダリングできます。

## v1.2.6

_2025年10月24日_

[!BADGE Adobe Commerce バージョン 2.4.5以降のリリースを]{type=Informative tooltip="サポート対象"} サポートしています。

![修正済みの問題](../assets/fix.svg)<!-- Issue ACAP-1163 -->製品の一括更新要求が連続してステータス追跡フラグを停止し、後続の更新が正しく処理されなくなる問題を解決しました。 エラーが発生した場合でも、ステータスがリセットされるようになりました。

## v1.2.5

_2025年10月22日_

[!BADGE Adobe Commerce バージョン 2.4.5以降のリリースを]{type=Informative tooltip="サポート対象"} サポートしています。

![修正済みの問題](../assets/fix.svg)<!-- Issue ACAP-1161 --> Adobe Commerce Adminで既存の画像マッピングの位置を更新すると、PHPのタイプエラーが発生する問題を修正しました。

## v1.2.4

_2025年10月17日_

[!BADGE Adobe Commerce バージョン 2.4.5以降のリリースを]{type=Informative tooltip="サポート対象"} サポートしています。

![修正された問題](../assets/fix.svg)<!-- Issue ACAP-1155 --> カスタム属性の全体的な安定性が向上しました。 非同期APIを使用する際に、カスタム属性が正しく更新されるようになりました。

![修正された問題](../assets/fix.svg)<!-- Issue ACAP-1074 -->これで、ベースリンク URLが定義されている場合、[製品アセットの同期](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/store-urls#configure-the-base-url){target=_blank}が失敗しません。

## v1.2.3

_2025年10月2日_

[!BADGE Adobe Commerce バージョン 2.4.5以降のリリースを]{type=Informative tooltip="サポート対象"} サポートしています。

![修正済みの問題](../assets/fix.svg)<!-- Issue ACAP-1135 -->製品属性の更新に関する問題を修正しました。 製品属性が期待どおりに更新され、更新が失敗した場合は、200応答ではなく適切なエラーが返されるようになりました。

## v1.2.2

_2025年9月18日_

[!BADGE Adobe Commerce バージョン 2.4.5以降のリリースを]{type=Informative tooltip="サポート対象"} サポートしています。

![修正済みの問題](../assets/fix.svg)<!-- Issue ACAP-1110 --> ミニカート、カート、チェックアウトページでの全体的な画像の安定性が向上しました。 これらのページの画像が正しく読み込まれるようになりました。

## v1.2.0

_2025年8月7日_

[!BADGE Adobe Commerce バージョン 2.4.5以降のリリースを]{type=Informative tooltip="サポート対象"} サポートしています。

![新しい問題](../assets/new.svg)<!-- Issue ACAP-1018 -->これで、管理者からAssets統合を設定する際に[&#x200B; ビジュアライゼーションオーナー](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization){target=_blank}を選択することで、画像アセットとメディアアセットのソースを選択できるようになりました。

![新しい問題](../assets/new.svg)<!-- Issue ACAP-1078 -->新しい[属性を持つ](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank} カスタム自動一致`asset_matches` エンドポイントを更新しました。 この変更により、特定の`productSku`に関連付けられたすべてのアセットを返すために、独自のマッチングロジックを実装できます。

## v1.1.2

_2025年6月11日_

[!BADGE Adobe Commerce バージョン 2.4.5以降のリリースを]{type=Informative tooltip="サポート対象"} サポートしています。

![新しい問題](../assets/new.svg)<!-- Issue ACAP-1041 --> Adobe Commerce 2.4.8およびPHP 8.4のサポートを追加しました。

## v1.1.0

_2025年4月23日_

[!BADGE Adobe Commerce バージョン 2.4.5以降のリリースを]{type=Informative tooltip="サポート対象"} サポートしています。

![新しい問題](../assets/new.svg)<!-- Issue ACAP-955 -->これで、[&#x200B; カスタムドメイン URL](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization#optional-configure-the-custom-domain-url)をAEM配信URLの代わりに使用できます。 販売者がAEM ダッシュボードで&#x200B;**カスタムドメイン名**&#x200B;を設定した場合は、この&#x200B;**カスタムドメイン URL**&#x200B;をCommerceに追加する必要があります。

![修正済みの問題](../assets/fix.svg)<!-- Issue ACAP-987 --> AEM Assets同期プロセスの全体的なログを改善しました。

## v1.0.22

_2025年3月12日_

[!BADGE Adobe Commerce バージョン 2.4.5以降のリリースを]{type=Informative tooltip="サポート対象"} サポートしています。

![新しい問題](../assets/new.svg)<!-- Issue ACAP-xx -->現在、[Assets セレクタ IMS クライアント ID](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization)は、Assets セレクタで必要です。この機能を使用して、AEM Assets イメージと製品カテゴリおよびページビルダー生成コンテンツのマッピングを有効にします。

## v1.0.20

_2025年2月11日_

[!BADGE Adobe Commerce バージョン 2.4.5以降のリリースを]{type=Informative tooltip="サポート対象"} サポートしています。

![新規](../assets/new.svg)<!-- Issue ACAP-xx -->一般公開リリース。
