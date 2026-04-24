---
title: Commerce製品ソリューション
description: バッジを使用して、さまざまなAdobe Commerce ソリューション（SaaS、PaaS、オンプレミス）に適用されるドキュメントを特定する方法について説明します。
feature: Paas, Saas
recommendations: noDisplay, noCatalog
hide: true
hidefromtoc: true
exl-id: 5ba1fa65-391f-4af7-8c40-d8314ec9d3e5
source-git-commit: ba445bf33ec9334c853245fce125af12cd244367
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# Adobe Commerce製品ソリューション

Adobeは、コマースビジネスの要件を満たすソリューションをいくつかご提供しています。 [Experience League](https://experienceleague.adobe.com/en/docs/commerce)および[Adobe Developer](https://developer.adobe.com/commerce/docs/) サイトのAdobe Commerce ドキュメントでは、すべてのソリューションをサポートするセルフサービス リソースをお客様に提供しています。 しかし、こうした膨大なコンテンツを適切に管理することは、容易なことではありません。

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service] （SaaS）の利用可能な機能と、これらの機能が[!DNL Adobe Commerce on Cloud]や[!DNL Adobe Commerce on Premises] （PaaS）などの他のバージョンのAdobe Commerceとどのように連携しているかについて詳しくは、[機能の比較](../cloud-service/feature-comparison.md)を参照してください。

## バッジ

バッジは、従来のサイトナビゲーションやインターネット検索を通じて見つかったCommerce ドキュメントが、使用するCommerce製品ソリューションに関連しているかどうかを素早く特定するのに役立ちます。 これは、コンテンツがひとつのソリューションにのみ適用される場合に、特に重要になります。

バッジが表示されている場合、コンテンツは指定されたソリューションにのみ適用されます。 バッジが表示されない場合は、その内容がすべてのAdobe Commerce ソリューションに適用されます。

例えば、Adobe Commerce as a Cloud Serviceを使用している場合、Product Recommendations拡張機能を[&#x200B; インストール &#x200B;](../product-recommendations/install-configure.md#install-product-recommendations)し、Commerce Services Connectorを[設定](../product-recommendations/install-configure.md#configure-product-recommendations)するといった内容は無視する必要があります。 Adobeは、インスタンスを作成すると、これらの手順を自動的に実行します。

### 定義

次の表に、Adobe Commerce ドキュメント全体に表示されるバッジを示します。

>[!BEGINSHADEBOX]

![info](../cloud-service/assets/Smock_InfoOutline_18_N.svg)ここで説明するバッジは、Adobe Commerce ドキュメントに特に適用されます。 他のAdobe Experience Cloud製品のドキュメントでバッジがどのように使用されるかは示されません。

>[!ENDSHADEBOX]

#### [!BADGE SaaSのみ]{type=Positive tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"}

このバッジは、[Adobe Commerce as a Cloud Service](../cloud-service/overview.md)および[Adobe Commerce Optimizer](../optimizer/overview.md) プロジェクトのドキュメントのみを識別します。 これらのプロジェクトは、クラウドネイティブのフルマネージド型のSaaS （Software-as-a-Service）ソリューションでホストされます。Adobeは、継続的なアップデート、セキュリティモニタリング、スケーラビリティなど、ほとんどの運用面を担当するため、インフラストラクチャではなくコマースに集中できます。

#### [!BADGE PaaSのみ]{type=Informative tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"}

このバッジは、[Adobe Commerce on Cloud](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/overview)およびオンプレミス プロジェクトに関連するドキュメントのみを識別します。 Adobe Commerce on Cloud プロジェクトは、Adobe Commerceのすべてのコア機能を備えた、クラウドネイティブでフルマネージドのPaaS （Platform-as-a-Service）ソリューション上で事前プロビジョニングされた環境でホストされます。 オンプレミスのプロジェクトは、顧客が管理するインフラストラクチャ上でホストされます。

>[!NOTE]
>
>特に記載がない限り、これには、Magento Open Source コードベースに基づくセルフホストプロジェクトも含まれます。

### ルール

次のルールを使用して、Adobe Commerceの各ソリューションに適用されるコンテンツを把握します。

- **ページレベルのバッジ**: ページの上部（ページタイトルの上）に表示されます。 ページ上の&#x200B;_all_ コンテンツが、指定されたソリューションにのみ適用されることを示します。

- **セクションレベルのバッジ**: ページ上の他のすべての見出しの直後に表示されます（ページタイトルを除く）。 このセクションの内容が、指定されたソリューションにのみ適用されることを示します。

- **インラインバッジ**：表、段落、リストなど、見出し以外のすべてのページエレメント内に表示されます。 そのエレメント内のコンテンツが、指定されたソリューションにのみ適用されることを示します。

>[!NOTE]
>
>バッジは、相互に排他的であることを目的としています。 つまり、同じページやセクションに複数のページレベルやセクションレベルのバッジは表示されません。 ただし、同じページまたは同じセクションの複数のインラインバッジを使用できます。
