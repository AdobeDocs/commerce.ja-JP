---
title: セキュリティの概要
description: Adobe Commerce as a Cloud Serviceのセキュリティ機能について説明します。
role: Admin, Architect, Leader
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"
source-git-commit: 0343c4f3ecc182145a97e08eca2790bd1512aa27
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---


# セキュリティの概要

[!DNL Adobe Commerce as a Cloud Service]は、セキュリティを中心に設計されており、エンタープライズレベルの保護、運用上の回復力、あらゆる規模の企業に安心を提供する、最新のSaaS ネイティブなコマースプラットフォームを提供します。

従来のPaaS モデルとは異なり、SaaS モデルは、手作業によるパッチ適用、インフラのメンテナンス、アップグレードサイクルなどの負担を排除します。 Adobeで管理されているインフラストラクチャから、自動化されたデプロイメントパイプライン、ID管理、アクセス管理[!DNL Adobe IMS]に至るまで、プラットフォームのあらゆるレイヤーにセキュリティが組み込まれています。

[!DNL Adobe Commerce as a Cloud Service]は、Adobeのグローバルなセキュリティおよびコンプライアンスフレームワークを活用し、ISO 27001、SOC 2、GDPRなどの業界標準との整合性を確保します。 お客様は、プラットフォームのセキュリティを確保する上でのAdobeの役割と、データとアクセスの管理における顧客の役割を明確に示す[共有責任モデル ](./shared-responsibility.md)を利用できます。

Web Application Firewall （WAF）、DDoSの緩和策、セキュアなプロビジョニング、継続的な脆弱性スキャンなどの組み込みの保護機能により、[!DNL Adobe Commerce as a Cloud Service]はセキュリティを損なうことなく、より迅速にイノベーションを進めることができます。

このドキュメントでは、[!DNL Adobe Commerce as a Cloud Service]のセキュリティアーキテクチャ、運用上の保護措置、コンプライアンス体制の概要を説明します。これにより、顧客が情報にもとづいた意思決定を行い、自信を持ってデジタルコマース業務を拡大できるようになります。

## Content delivery network （CDN）とweb アプリケーションファイアウォール（WAF）

### Storefront CDN

Commerceを活用したストアフロントを保護するために、Adobeで管理されるCDNを導入するか、独自のCDN ソリューションを購入することができます。

>[!IMPORTANT]
>
>お客様がAdobeで管理されているCDNをデプロイする場合、CDN ルールを設定することはできません。 カスタムキャッシングルールまたはWAF ルールは、お客様が独自のCDNを持ち込んでストアフロントを保護する際に設定できます。

### [!DNL API Mesh for Adobe Developer App Builder] CDN

[!DNL API Mesh]のCDN レイヤーはTLSを終了し、GraphQL ゲートウェイをWorkerとして実行し、グローバル エッジ キャッシュと自動DDoS/WAFを提供し、パブリック メッシュ エンドポイントとして`edge‑graph.adobe.io`/`edge‑sandbox‑graph.adobe.io`を公開します。お客様は自分のCDNを前面に追加できますが、[!DNL API Mesh]のCDNはAdobeによって修正および管理され、お客様は自分のWAF ルールを設定できません。

[!DNL API Mesh]のセキュリティ機能について詳しくは、[API Mesh ドキュメント ](https://developer.adobe.com/graphql-mesh-gateway/mesh/security/){target="_blank"}を参照してください。

### バックエンド CDN

ビルトイン CDNは[!DNL Adobe Commerce as a Cloud Service]を保護します。

[!DNL Adobe Commerce as a Cloud Service] アーキテクチャにより、マーチャントが`na1`、`eu1`、`au1`などの複合セル内のインスタンスをプロビジョニングすると、次の3つの公開サーフェスが公開されます。

| サーフェス | URL パターンの例 |
| --- | --- |
| 管理者UI | `https://<region>.admin.commerce.adobe.com/<tenant-id>/admin/` |
| REST API | `https://<region>.api.commerce.adobe.com/<tenant-id>/<endpoint>` |
| GRAPHQL API | `https://na1.api.commerce.adobe.com/<tenant_id>/graphql/` |

[!DNL Adobe Commerce as a Cloud Service]は、WAFとCDNを組み合わせて使用します。

- **WAF** – すべての[!DNL Adobe Commerce as a Cloud Service]公開サーフェスに対するWeb Application Firewall保護。
- **CDN** – 静的アセットとキャッシュ可能なGraphQL応答のEdge キャッシュ。

WAFとCDNは[!DNL Adobe Commerce as a Cloud Service] プラットフォームによって管理され、お客様が設定することはできません。

### DDoS対策

組み込みのCDNおよびWAFは、ネットワーク層とHTTP層の両方のDDoS攻撃対策を提供します。 [!DNL Adobe Commerce as a Cloud Service]は、これらのWAFまたはDDoS ログをマーチャントに直接公開しません。

## データの保存と暗号化

データが[!DNL App Builder]に保存されている場合、マーチャントは[!DNL App Builder] [ ストレージオプション ](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/)を参照できます。 [!DNL App Builder]では、テナントの分離が適用され、これらのサービスに保存されているデータへのアクセスは、アクションが実行されるランタイム名前空間に制限されます。 ストレージ内のデータは暗号化されません。

[!DNL API Mesh]を使用する場合、シークレットはメッシュ設定の`secrets.yaml` ファイルに保存する必要があります。 [!DNL API Mesh]は、AES-256暗号化（[https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/secrets/](https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/secrets/)）を使用してこれらのシークレットを暗号化します。

[!DNL Adobe Commerce as a Cloud Service]に保存されているデータはすべて、AES 256 ビットの暗号化を使用して保存中に暗号化され、すべてのデータは、転送中にTLS 1.2以降を使用してHTTPS経由で暗号化されます。
