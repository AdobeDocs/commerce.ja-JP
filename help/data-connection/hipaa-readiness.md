---
title: サービスに対する HIPAA [!DNL Commerce]  対応
description: 拡張機能を使用して  [!DNL Data Connection] Experience Platformとデータを共有し、HIPAA コンプライアンスを維持する方法に  [!DNL Commerce]  いて説明します。
role: Admin, Leader
feature: Security, Compliance
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# [!DNL Commerce] Services に対する HIPAA 対応

[!DNL Data Connection] 拡張機能を使用すると、バックオフィスイベントデータ [!DNL Commerce]Experience Platformと共有し、HIPAA への準拠を維持できます。

>[!IMPORTANT]
>
>ストアフロントイベントはクライアントサイドで生成されるため、マーチャントの責任は [ ストアフロントイベントデータをExperience Platformに送信しない ](connect-data.md#data-collection) ことです。

この記事では、次の内容について説明します。

- インストール内容
- Experience Platformに送信されるデータが HIPAA に対応していることを確認する方法
- [!DNL Commerce] でのデータ暗号化

## インストール

Adobe [!DNL Commerce] 用のヘルスケアアドオンを購入した場合は、[HIPAA 対応の拡張機能 ](https://experienceleague.adobe.com/ja/docs/commerce-admin/start/compliance/hipaa-ready-service/overview#installation) が既にインストールされている可能性があります。 [!DNL Commerce] バックオフィスイベントデータが HIPAA に対応していることを確認するには、追加の **データサービス HIPAA** 拡張機能を備えた [!DNL Data Connection] 拡張機能をインストールする必要もあります。 **データサービス HIPAA** 拡張機能により、Experience Platformに送信されるバックオフィスデータが HIPAA に対応できるようになります。 詳細情報 [ 拡張機能のインストール方法 ](install.md#install-the-data-services-hipaa-extension)。

>[!IMPORTANT]
>
>**データサービス HIPAA** 拡張機能をインストールすると、ライブ検索および製品レコメンデーションで使用されるストアフロントイベントデータが取得されなくなりました。 これは、ストアフロントのイベントデータがクライアントサイドで生成されるからです。 ストアフロントのイベントデータのキャプチャと送信を続行するには、これらのサービスのイベント収集を再度有効にします。 詳しくは、[ 一般設定 ](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general.html#data-services) を参照してください。

## Experience Platformに送信されるデータが HIPAA に対応していることを確認する方法

[!DNL Data Connection] 拡張機能からExperience Platformに送信されるすべてのバックオフィスイベントデータは、[!DNL Commerce] 内では機密と見なされます。 ただし、特定のデータを機密性が高いものとして明示的に識別するには、マーチャントの責任で、Experience Platformの [!DNL Commerce] スキーマにデータ使用ラベルを適用します。 データ使用ラベルをスキーマに直接適用すると、これらのラベルは、そのスキーマに基づくすべての既存のデータセットと今後のデータセットに伝播されます。

データ使用ラベルとそのデータガバナンスフレームワーク内での役割の概要については、Experience Platform ドキュメントの [ データ使用ラベルの概要 ](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/labels/overview) を参照してください。

### [!DNL Commerce] のフィールドへのデータ使用ラベルの適用

[!DNL Commerce] スキーマにラベルを適用する方法については、[ スキーマのデータ使用ラベルの管理 ](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/tutorials/labels) チュートリアルの手順に従ってください。

[!DNL Commerce] スキーマのフィールドに適用できる使用可能なラベルについて詳しくは、[ 機密ラベルの用語集 ](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/labels/reference#sensitive) を参照してください。 例えば、保護対象保健情報（PHI）や、Adobe`RHD` 契約上アップロードを許可している患者に関する情報を識別するラベルです。

[!DNL Commerce] データに「機密」というラベルを付けると、ポリシーを適用して、ポリシー違反を構成するデータ操作を防ぐことができます。 詳しくは、Experience Platformの [ ポリシーの適用 ](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/enforcement/overview) を参照してください。

## Commerceでのデータ暗号化

Adobe [!DNL Commerce] では、ブロックレベルの暗号化を使用します。 ストレージの場合、[!DNL Commerce] はAmazon Elastic Block Store （EBS）を使用します。 すべての EBS ボリュームは、AES-256 アルゴリズムを使用して暗号化されます。つまり、保存時にデータが暗号化されます。 転送中のデータ [!DNL Commerce]、HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246) を使用した、安全で暗号化された接続で転送されます。

>[!IMPORTANT]
>
>Commerceでは、データが休止状態ではない場合や、サーバー間で転送中でない場合は、列レベルまたは行レベルの暗号化または暗号化をサポートしていません。

### Experience Platformでのデータ暗号化

マーチャントがデータをExperience Platformに送信すると、そのデータは HTTPS TLS v1.2 を使用して送信されます。[Experience Platform](https://experienceleague.adobe.com/ja/docs/experience-platform/landing/governance-privacy-security/encryption) によるデータの暗号化方法の詳細を説明します。

## [!DNL Commerce] によるプライバシーリクエストの処理方法

[!DNL Commerce] でのプライバシーリクエストの処理方法を説明します [ プライバシーリクエストの処理 ](handle-privacy-request.md)。
