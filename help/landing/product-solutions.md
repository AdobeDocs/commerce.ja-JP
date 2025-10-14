---
title: Commerce製品ソリューション
description: バッジを使用して、様々なAdobe Commerce ソリューション（SaaS、PaaS、オンプレミス）に適用されるドキュメントを特定する方法を説明します。
feature: Paas, Saas
recommendations: noDisplay, noCatalog
hide: true
hidefromtoc: true
exl-id: 5ba1fa65-391f-4af7-8c40-d8314ec9d3e5
source-git-commit: 7b59d3a3c7d3cdc875e3329c7949eccc3a6c9fdc
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---

# Adobe Commerce製品ソリューション

Adobeでは、e コマースビジネスの要件を満たすソリューションをいくつか提供しています。 [Experience League](https://experienceleague.adobe.com/ja/docs/commerce) のAdobe Commerce ドキュメントと [Adobe Developer](https://developer.adobe.com/commerce/docs/) サイトには、すべてのソリューションをサポートするセルフサービスリソースが用意されています。 ただし、このような大量のコンテンツのナビゲーションは、ガイダンスがないと困難な場合があります。

## バッジ

バッジは、従来のサイトナビゲーションやインターネット検索で見つけたCommerce ドキュメントが、お使いのCommerce製品ソリューションに関連しているかどうかを素早く特定するのに役立ちます。 これは、コンテンツが 1 つのソリューションのみに適用される場合に特に重要です。

バッジが表示された場合は、コンテンツが指定したソリューションにのみ適用されることを意味します。 バッジが表示されない場合は、コンテンツがすべてのAdobe Commerce ソリューションに適用されます。

例えば、Adobe Commerce as a Cloud Serviceを使用している場合、Product Recommendations 拡張機能の [&#x200B; インストール &#x200B;](../product-recommendations/install-configure.md#install-product-recommendations) およびCommerce サービスコネクターの [&#x200B; 設定 &#x200B;](../product-recommendations/install-configure.md#configure-product-recommendations) に関する内容は無視してください。 Adobeでは、インスタンスを作成すると、これらの手順が自動的に完了します。

### 定義

以下の表に、Adobe Commerce ドキュメント全体で表示されるバッジの定義を示します。

>[!BEGINSHADEBOX]

![&#x200B; 情報 &#x200B;](../cloud-service/assets/Smock_InfoOutline_18_N.svg) ここで説明するバッジは、特にAdobe Commerce ドキュメントに当てはまります。 他のAdobe Experience Cloud製品のドキュメントでのバッジの使用方法を表すものではありません。

>[!ENDSHADEBOX]

#### [!BADGE SaaS のみ &#x200B;]{type=Positive tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"}

このバッジは、[Adobe Commerce as a Cloud Service](../cloud-service/overview.md) および [Adobe Commerce Optimizer](../optimizer/overview.md) プロジェクト専用のドキュメントを特定します。 これらのプロジェクトは、完全に管理されたクラウドネイティブのサービスとしてのソフトウェア（SaaS）ソリューションでホストされ、Adobeが継続的な更新、セキュリティの監視、スケーラビリティなどのほとんどの運用側面を担当するので、お客様はインフラストラクチャではなくコマースに集中できます。

#### [!BADGE PaaS のみ &#x200B;]{type=Informative tooltip="Adobe Commerce on Cloud プロジェクト（Adobeが管理する PaaS インフラストラクチャ）およびオンプレミスプロジェクトにのみ適用されます。"}

このバッジは、[Adobe Commerce on Cloud](https://experienceleague.adobe.com/ja/docs/commerce-on-cloud/user-guide/overview) およびオンプレミスプロジェクトに関連するドキュメントのみを特定します。 クラウドプロジェクト上のAdobe Commerceは、クラウドネイティブで完全に管理されたサービスとしてのプラットフォーム（PaaS）ソリューションにホストされ、Adobe Commerceのすべてのコア機能が事前にプロビジョニングされます。 オンプレミスのプロジェクトは、顧客が管理するインフラストラクチャでホストされます。

>[!NOTE]
>
>特に断りのない限り、これにはMagento Open Source コードベースに基づくセルフホストプロジェクトも含まれます。

### ルール

これらのルールを使用すると、各Adobe Commerce ソリューションにどのようなコンテンツが適用されるかを理解できます。

- **ページレベルのバッジ**：ページの上部（ページタイトルの上）に表示されます。 ページ上の _すべて_ のコンテンツが、指定したソリューションにのみ適用されることを示します。

- **セクションレベルのバッジ**：ページのその他すべての見出しの直下に表示されます（ページタイトルを除く）。 そのセクションのコンテンツが指定されたソリューションにのみ適用されることを示します。

- **インラインバッジ**：テーブル、段落、リストなど、見出しではないすべてのページ要素内に表示されます。 その要素のコンテンツが指定されたソリューションにのみ適用されることを示します。

>[!NOTE]
>
>バッジは、相互に排他的な状態を意図しています。 つまり、同じページやセクションに複数のページレベルまたはセクションレベルのバッジが表示されることはありません。 ただし、同じページまたは同じセクションに複数のインラインバッジを配置することができます。
