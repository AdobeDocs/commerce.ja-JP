---
title: プロファイルレコード
description: プロファイルレコードが取得するデータを説明します。
role: Admin, Developer
feature: Personalization, Integration, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# [!DNL Data Connection] プロファイルレコード

以下は、[!DNL Data Connection] 拡張機能をインストールする際に利用できるCommerce プロファイルレコードデータを説明しています。 プロファイルレコードのデータはAdobe Experience Platformに送信されます。

## プロファイルレコード

プロファイルレコードの更新は、新しいプロファイルを作成、更新または削除すると、Experience Platformで利用できます。

### プロファイルレコードから収集されたデータ

次に、プロファイルレコードに対して取り込まれるデータを示します。

| フィールド | 説明 |
|---|---|
| `channel` | データのソースに関する情報が含まれます。 `_id` と `_type` の両方に [ 名前空間の値 ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/namespaces) が含まれています。 |
| `channel._id` | チャネルの一意の識別子（`"https://ns.adobe.com/xdm/channels/web"` など）。 |
| `channel._type` | `"https://ns.adobe.com/xdm/channel-types/web"` などのチャネルデータのソースを識別します。 |
| `person` | 顧客に関する情報が含まれます。 |
| `person.name` | 顧客の名前に関する情報が含まれます。 |
| `person.name.firstName` | 顧客の名が含まれます。 |
| `person.name.lastName` | 顧客の姓が含まれます。 |
| `person.birthDate` | 買い物客の生年月日。 |
| `personalEmail` | 個人の電子メールアドレス。 |
| `personalEmail.address` | 例えば、技術的アドレス `name@domain.com`、RFC2822 および後続の標準で一般的に定義されています。 |
| `billingAddress` | 請求先住所。 |
| `billingAddress.street1` | プライマリの番地レベルの情報、アパート番号、通り番号、通り名。 |
| `billingAddress.street2` | オプションの住所情報 2 行目。 |
| `billingAddress.city` | 市区町村の名前。 |
| `billingAddress.state` | 州の名前。 これは自由形式フィールドです。 |
| `billingAddress.country` | 政府が管理する領土の名前。 `xdm:countryCode` 以外の場合、これは自由形式のフィールドで、どの言語でも国名を持つことができます。 |
| `billingAddress.primary` | これが主要請求先住所かどうかを示します。 値は常に `False` です。 |
| `billingAddressPhone` | 請求先住所に関連付けられた電話番号。 |
| `billingAddressPhone.number` | 電話番号。 電話番号は文字列で、意味のある文字（角括弧 `()`、ハイフン `-` など）や、サブダイヤル識別子を示す文字（内線 `x` 例：`1-353(0)18391111`、`+613 9403600x1234` など）を含める場合があることに注意してください。 |
| `billingAddressPhone.primary` | これが請求先住所の主要電話番号かどうかを示します。 値は常に `False` です。 |
| `shippingAddress` | 配送先住所。 |
| `shippingAddress.street1` | プライマリの番地レベルの情報、アパート番号、通り番号、通り名。 |
| `shippingAddress.street2` | オプションの住所情報 2 行目。 |
| `shippingAddress.city` | 市区町村の名前。 |
| `shippingAddress.state` | 州の名前。 これは自由形式フィールドです。 |
| `shippingAddress.country` | 政府が管理する領土の名前。 `xdm:countryCode` 以外の場合、これは自由形式のフィールドで、どの言語でも国名を持つことができます。 |
| `shippingAddress.primary` | これがプライマリ配送先住所かどうかを示します。 値は常に `False` です。 |
| `shippingAddressPhone` | 配送先住所に関連付けられた電話番号。 |
| `shippingAddressPhone.number` | 電話番号。 電話番号は文字列で、意味のある文字（角括弧 `()`、ハイフン `-` など）や、サブダイヤル識別子を示す文字（内線 `x` 例：`1-353(0)18391111`、`+613 9403600x1234` など）を含める場合があることに注意してください。 |
| `shippingAddressPhone.primary` | これが配送先住所の基本電話番号かどうかを示します。 値は常に `False` です。 |
| `userAccount` | ロイヤルティの詳細、環境設定、ログインプロセス、その他のアカウント環境設定を示します。 |
| `userAccount.startDate` | プロファイルが最初に作成された日付。 |

>[!NOTE]
>
>各プロファイルレコードには、[`identityMap`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/identitymap) フィールドも含まれています。このフィールドには、プロファイルのプライマリ識別子としてシステム生成のCommerce顧客 ID と、セカンダリ識別子として使用されるメール ID が含まれます。

プロファイルレコードからデータを取り込むことができる [ プロファイルレコード固有のスキーマを作成 ](profile-data.md) する方法を説明します。
