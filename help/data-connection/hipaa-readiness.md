---
title: ' [!DNL Commerce]  サービスのHIPAA対応'
description: ' [!DNL Data Connection] 拡張機能を使用して [!DNL Commerce]  データをExperience Platformと共有し、HIPAA コンプライアンスを維持する方法について説明します。'
role: Admin, Leader
feature: Security, Compliance
exl-id: 8851e6d2-c466-4d8e-bfa4-20d0ad6522b5
TQID: https://experienceleague.adobe.com/PxrtL1nHtJsRJuAehDVKRk0ZuJz0ta7i84j1K6An1QU
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: ba9e5be9-7de1-4f71-a5d2-baead0e425eeid: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2: id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adebid: d095671a-1355-40aa-8b5f-06c33c68080bid: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 601
ht-degree: 1%

---

# [!DNL Commerce] サービスのHIPAA対応

[!DNL Data Connection]拡張機能を使用すると、[!DNL Commerce] バックオフィスのイベントデータをExperience Platformと共有し、HIPAAへの準拠を維持できます。

>[!IMPORTANT]
>
>ストアフロントイベントはクライアント側で生成されるため、Experience Platformにストアフロントイベントデータ ](connect-data.md#data-collection)を送信しないのは販売者の責任[です。

主な内容：

- インストールするもの
- Experience Platformに送信されたデータがHIPAAに対応していることを確認する方法
- [!DNL Commerce]でのデータの暗号化

## インストール

Adobe [!DNL Commerce]のヘルスケアアドオンを購入した場合は、[HIPAA対応拡張機能](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/hipaa-ready-service/overview#installation)が既にインストールされている可能性があります。 [!DNL Commerce] バックオフィスのイベントデータがHIPAA対応であることを確認するには、追加の&#x200B;**Data Services HIPAA**&#x200B;拡張機能を含む[!DNL Data Connection]拡張機能もインストールする必要があります。 **Data Services HIPAA**&#x200B;拡張機能を使用すると、Experience Platformに送信するすべてのバックオフィスデータがHIPAA対応になります。 拡張機能のインストール方法[について説明します](install.md#install-the-data-services-hipaa-extension)。

>[!IMPORTANT]
>
>**Data Services HIPAA**&#x200B;拡張機能をインストールすると、ライブサーチと製品レコメンデーションで使用されるストアフロントイベントデータがキャプチャされなくなります。 これは、ストアフロントのイベントデータがクライアントサイドで生成されるためです。 ストアフロントイベントデータの取得と送信を続行するには、これらのサービスのイベント収集を再度有効にします。 詳しくは、[一般設定](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general#data-services)を参照してください。

## Experience Platformに送信されたデータがHIPAAに対応していることを確認する方法

[!DNL Data Connection]拡張機能がExperience Platformに送信するすべてのバックオフィスイベントデータは、[!DNL Commerce]内では機密性が高いと見なされます。 ただし、特定のデータを機密性の高いものとして明示的に識別するには、Experience Platformの[!DNL Commerce] スキーマにデータ使用ラベルを適用する必要があります。 データ使用ラベルをスキーマに直接適用すると、そのラベルは、そのスキーマに基づくすべての既存および将来のデータセットに反映されます。

Data Governance フレームワーク内でのデータ使用ラベルとその役割の概要については、Experience Platform ドキュメントの[ データ使用ラベルの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/labels/overview)を参照してください。

### データ使用ラベルを[!DNL Commerce] フィールドに適用する

[!DNL Commerce] スキーマにラベルを適用する方法については、[ スキーマのデータ使用ラベルの管理](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/labels) チュートリアルの手順に従ってください。

[!DNL Commerce] スキーマのフィールドに適用できる使用可能なラベルについて詳しくは、[機密ラベルの用語集](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/labels/reference#sensitive)を参照してください。 例えば、ラベル `RHD`は、保護された医療情報（PHI）またはAdobeによってアップロードが契約上許可されている患者に関する情報を識別します。

[!DNL Commerce] データが機密としてラベル付けされている場合、ポリシーを適用して、ポリシー違反を構成するデータ操作を防止できます。 Experience Platformの[ ポリシーの適用](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/enforcement/overview)の詳細をご覧ください。

## Commerceでのデータの暗号化

Adobe [!DNL Commerce]では、ブロックレベルの暗号化が使用されています。 ストレージには、[!DNL Commerce]がAmazon Elastic Block Store （EBS）を使用します。 EBS ボリュームはすべてAES-256 アルゴリズムを使用して暗号化されているため、保存中のデータは暗号化されています。 転送中の[!DNL Commerce]個のデータは、HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246)を使用して、暗号化された安全な接続を通じて実行されます。

>[!IMPORTANT]
>
>Commerceでは、列レベルまたは行レベルでの暗号化はサポートしていません。また、データが保存中ではなく、なおかつサーバー間で送信中でもない場合の暗号化もサポートしていません。

### Experience Platformでのデータの暗号化

販売者がExperience Platformにデータを送信する場合、そのデータはHTTPS TLS v1.2を使用して送信されます。 [Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/landing/governance-privacy-security/encryption)がデータを暗号化する方法について詳しくは、こちらを参照してください。

## [!DNL Commerce]がプライバシー要求を処理する方法

[!DNL Commerce] [がプライバシーリクエストをどのように処理するかを説明します](handle-privacy-request.md)。
