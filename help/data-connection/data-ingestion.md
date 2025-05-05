---
title: Commerce データのタイプ
description: 収集してExperience Platformに送信できるデータのタイプについて説明します。
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Commerce データのタイプ

[Data Connection extension](overview.md) は、Commerce データをExperience Platformに接続します。 Experience Platformで使用するデータは、**エクスペリエンスイベント** クラスに属する時系列データと、**個人プロファイル** クラスに属するレコードデータの 2 つの動作タイプに分類されます。

Experience Platformの [ データ動作 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=ja#data-behaviors) および [ クラス ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=ja#class) について詳しく説明します。

## 時系列データ

時系列データは、レコードの主体によって直接または間接的にアクションが実行された時点のシステムのスナップショットを提供します。 例えば、買い物客がサイトで製品を閲覧すると、買い物かごに製品を追加したり、注文を行ったりします。 時系列データは、クラスが **Experience Event** に設定されたスキーマを使用してExperience Platformに取り込まれます。

### キャプチャされた時系列データ

時系列イベントが生成されたときに取得されるデータについて詳しくは、[ 行動イベント ](events.md) および [ バックオフィスイベント ](events-backoffice.md) を参照してください。

### 時系列イベントデータの取り込みに必要なスキーマ

行動およびバックオフィスの時系列イベントデータを取り込める [ スキーマを作成 ](update-xdm.md) 方法を説明します。

## レコードデータ

レコードデータは、主体の属性に関する情報を提供します。 主体は、組織または個人にすることができます。 例えば、サイトの買い物客がアカウントを作成し、それがレコードデータを生成します。 このデータは、クラスが **個人プロファイル** に設定されたスキーマを使用してExperience Platformに取り込まれます。 そのレコードデータをAdobeのプロファイル管理およびセグメント化サービスに送信できます：[Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=ja)。

### キャプチャされたプロファイルレコードデータ

プロファイルレコードの生成時に取得するデータについて詳しくは、[ 顧客プロファイルレコードデータ ](events-profilerecord.md) を参照してください。

### プロファイルレコードデータを取り込むために必要なスキーマ

プロファイルレコードデータを取り込むことができる [ スキーマを作成 ](profile-data.md) する方法を説明します。
