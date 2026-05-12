---
title: Commerceデータの種類
description: Experience Platformに送信できるデータの種類について説明します。
role: Admin, Developer
feature: Personalization, Integration
exl-id: 6354963c-f27f-4e69-9ecb-acb4befb7c2a
TQID: https://experienceleague.adobe.com/LXMqOhHAZpUHaCeeU5ioKKXVrkLftospQEPDd9H-MD8
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 339
ht-degree: 2%

---

# Commerceデータの種類

[Data Connection拡張機能](overview.md)は、Commerce データをExperience Platformに接続します。 Experience Platformで使用するデータは、**Experience Event** クラスに属する時系列データと、**Individual Profile** クラスに属するレコードデータの2つのビヘイビアータイプにグループ化されます。

Experience Platformの[data behavior](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html#data-behaviors)および[classes](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html#class)の詳細をご覧ください。

## 時系列データ

時系列データは、アクションがレコード主体によって直接または間接的に実行された時点でのシステムのスナップショットを提供します。 例えば、買い物客がサイトで商品を閲覧し、カートに商品を追加し、注文したとします。 時系列データは、クラスが&#x200B;**Experience Event**&#x200B;に設定されたスキーマを使用してExperience Platformに取り込まれます。

### 取得した時系列データ

時系列イベントが生成されたときに取り込まれるデータについては、[行動イベント &#x200B;](events.md)および[&#x200B; バックオフィスイベント &#x200B;](events-backoffice.md)を参照してください。

### 時系列イベントデータの取り込みに必要なスキーマ

行動およびバックオフィスの時系列イベントデータを取り込むことができるスキーマ [&#128279;](update-xdm.md)を作成する方法について説明します。

## レコードデータ

レコードデータは、被写体の属性に関する情報を提供します。 テーマには、組織や個人が含まれます。 例えば、サイトの買い物客がアカウントを作成し、そのアカウントがレコードデータを生成するとします。 このデータは、クラスが&#x200B;**個人プロファイル**&#x200B;に設定されたスキーマを使用してExperience Platformに取り込まれます。 そのレコードデータをAdobeのプロファイル管理およびセグメント化サービス [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=ja)に送信できます。

### 取得したプロファイルレコードデータ

プロファイルレコードの生成時にどのようなデータが取り込まれるかは、[顧客プロファイルレコードデータ &#x200B;](events-profilerecord.md)を参照してください。

### プロファイルレコードデータの取り込みに必要なスキーマ

プロファイルレコードデータを取り込むことができるスキーマ [&#128279;](profile-data.md)を作成する方法について説明します。
