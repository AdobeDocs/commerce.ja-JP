---
title: プロファイルレコード
description: プロファイルレコードがどのようなデータを取得するかをご確認ください。
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: aaa30886-d9c0-4909-81ee-fad3407cac43
TQID: https://experienceleague.adobe.com/bHKuzUSApLQNW-M8NY1xb6-WZtjACmRRZ0TtsPM55rU
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 499
ht-degree: 0%

---

# [!DNL Data Connection] プロファイルレコード

次に、[!DNL Data Connection]拡張機能のインストール時に使用可能なCommerce プロファイル レコード データについて説明します。 プロファイルレコードのデータがAdobe Experience Platformに送信されます。

## プロファイルレコード

プロファイルレコードの更新は、新しいプロファイルが作成、更新、または削除されたときに、Experience Platformで利用できます。

### プロファイルレコードから収集されたデータ

次に、プロファイルレコード用にキャプチャされるデータについて説明します。

| フィールド | 説明 |
|---|---|
| `channel` | データのソースに関する情報が含まれます。 `_id`と`_type`の両方に[名前空間値](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/namespaces)が含まれています。 |
| `channel._id` | チャネルの一意の識別子（`"https://ns.adobe.com/xdm/channels/web"`など）。 |
| `channel._type` | `"https://ns.adobe.com/xdm/channel-types/web"`などのチャネルデータのソースを識別します。 |
| `person` | 顧客に関する情報が含まれます。 |
| `person.name` | 顧客の名前に関する情報が含まれます。 |
| `person.name.firstName` | 顧客の名前が含まれます。 |
| `person.name.lastName` | 顧客の姓が含まれます。 |
| `person.birthDate` | 買い物客の誕生日。 |
| `personalEmail` | 個人のメールアドレス。 |
| `personalEmail.address` | テクニカルアドレス （例：`name@domain.com`）は、RFC2822およびそれ以降の規格で一般的に定義されています。 |
| `billingAddress` | 請求先住所。 |
| `billingAddress.street1` | プライマリの住所、アパート番号、住所、住所の名前。 |
| `billingAddress.street2` | オプションのストリート情報2行目。 |
| `billingAddress.city` | 市の名前。 |
| `billingAddress.state` | 州の名前。 これは自由形式のフィールドです。 |
| `billingAddress.country` | 政府が管理する地域の名前。 `xdm:countryCode`以外の自由形式フィールドで、国名を任意の言語で使用できます。 |
| `billingAddress.primary` | これがプライマリ請求先住所かどうかを示します。 値は常に`False`です。 |
| `billingAddressPhone` | 請求先住所に関連付けられている電話番号。 |
| `billingAddressPhone.number` | 電話番号。 電話番号は文字列であり、括弧`()`、ハイフン `-`、または拡張機能`x`などのサブダイヤル識別子（例：`1-353(0)18391111`、または`+613 9403600x1234`など）を示す文字など、意味のある文字を含める場合があります。 |
| `billingAddressPhone.primary` | 請求先住所のプライマリ電話番号かどうかを示します。 値は常に`False`です。 |
| `shippingAddress` | 配送先住所。 |
| `shippingAddress.street1` | プライマリの住所、アパート番号、住所、住所の名前。 |
| `shippingAddress.street2` | オプションのストリート情報2行目。 |
| `shippingAddress.city` | 市の名前。 |
| `shippingAddress.state` | 州の名前。 これは自由形式のフィールドです。 |
| `shippingAddress.country` | 政府が管理する地域の名前。 `xdm:countryCode`以外の自由形式フィールドで、国名を任意の言語で使用できます。 |
| `shippingAddress.primary` | これがメインの配送先住所かどうかを示します。 値は常に`False`です。 |
| `shippingAddressPhone` | 輸送先住所に関連付けられている電話番号。 |
| `shippingAddressPhone.number` | 電話番号。 電話番号は文字列であり、括弧`()`、ハイフン `-`、または拡張機能`x`などのサブダイヤル識別子（例：`1-353(0)18391111`、または`+613 9403600x1234`など）を示す文字など、意味のある文字を含める場合があります。 |
| `shippingAddressPhone.primary` | これが配送先住所のプライマリ電話番号かどうかを示します。 値は常に`False`です。 |
| `userAccount` | ロイヤルティの詳細、嗜好、ログインプロセス、その他のアカウント設定を示します。 |
| `userAccount.startDate` | プロファイルが最初に作成された日付。 |

>[!NOTE]
>
>各プロファイルレコードには、[`identityMap`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/identitymap) フィールドも含まれます。このフィールドには、プロファイルのプライマリ IDとして生成されたCommerce Customer IDと、セカンダリ IDとして使用される電子メール IDが含まれます。

プロファイルレコードからデータを取り込むことができる、プロファイルレコード固有のスキーマ [&#128279;](profile-data.md)を作成する方法について説明します。
