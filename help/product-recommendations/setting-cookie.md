---
title: Cookie 制限の処理
description: 製品レコメンデーションでの cookie 制限の処理方法を説明します。
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# Cookie 制限の処理

データがブラウザーの Cookie に保存される前に、Adobe CommerceとMagento Open Sourceの両方が同意を求めます。 詳しくは、「[Cookie 制限モード ](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html?lang=ja)」を参照してください。

`magento/product-recommendations` モジュールを実稼動環境にデプロイすると、ストアフロントで買い物客インタラクションイベントの収集を開始します。 これらのイベントのデータはブラウザーの Cookie またはローカルストレージに保存できるので、この機能は、買い物客が Cookie に同意するまでイベントを収集しないことで、Cookie 制限モードをサポートします。

これは、サードパーティ cookie 同意ソリューションでは機能しない場合があります。 法律で多くの場合に必要とされるように、Cookie の同意が得られる前にデータ収集が行われないことを確認するのは、各マーチャントの責任です。 カスタムコードで cookie の同意を管理している場合は、`mg_dnt` と呼ばれる追跡対象外の cookie を使用してデータ収集を制限できます。

- Cookie の名前：

  ```text
  `const DNT_COOKIE = "mg_dnt";`
  ```

- データ収集を無効にするために追跡禁止 Cookie を設定します。

  ```text
  `$.mage.cookies.set(DNT_COOKIE, true);`
  ```

- ユーザーが Cookie を受け入れた際に Cookie を消去するには：

  ```text
  `$.mage.cookies.clear(DNT_COOKIE);`
  ```
