## 1. サービスアドレス

APIは最寄り地域によるアクセスをサポートしています。この製品の最寄り地域によるアクセスのドメイン名はcvm.tencentcloudapi.comであり、また指定された地域のドメイン名によるアクセスもサポートしています。例えば、広州地域のドメイン名はcvm.ap-guangzhou.tencentcloudapi.comです。

最寄り地域によるアクセスのドメイン名を使用することをお勧めします。APIを呼び出すときのクライアントの場所に応じて、**最も近い**特定の地域サーバーが自動的に解析されます。例えば、広州でリクエストを送信すれば、広州のサーバーが自動的に解析されます。効果はcvm.ap-guangzhou.tencentcloudapi.comを指定することと同じです。

**注意：時間遅延に敏感な業務に対して、地域付きのドメイン名を指定することをお勧めします。**

現在サポートしているドメイン名のリストは：

| アクセス地域 | ドメイン名 |
|----------|------|
| 最寄り地域によるアクセス（推薦、非金融区のみサポート）| cvm.tencentcloudapi.com|
| 華南地区（広州） | cvm.ap-guangzhou.tencentcloudapi.com|
| 華東地区（上海） | cvm.ap-shanghai.tencentcloudapi.com|
| 華北地区（北京） | cvm.ap-beijing.tencentcloudapi.com|
| 西南地区（成都） | cvm.ap-chengdu.tencentcloudapi.com|
| 西南地区（重慶） | cvm.ap-chongqing.tencentcloudapi.com|
| 東南アジア地区（中国香港） | cvm.ap-hongkong.tencentcloudapi.com |
| 東南アジア地区（シンガポール） | cvm.ap-singapore.tencentcloudapi.com|
| アジア太平洋地区（バンコク） | cvm.ap-bangkok.tencentcloudapi.com |
| アジア太平洋地区（ムンバイ） | cvm.ap-mumbai.tencentcloudapi.com|
| アジア太平洋地区（ソウル） | cvm.ap-seoul.tencentcloudapi.com|
| アジア太平洋地区（東京） | cvm.ap-tokyo.tencentcloudapi.com |
| 米国東部（バージニア） | cvm.na-ashburn.tencentcloudapi.com|
| 米国西部（シリコンバレー） | cvm.na-siliconvalley.tencentcloudapi.com|
| 北米地区（トロント） | cvm.na-toronto.tencentcloudapi.com |
| ヨーロッパ地区（フランクフルト） | cvm.eu-frankfurt.tencentcloudapi.com |
| ヨーロッパ地区（モスクワ） | cvm.eu-moscow.tencentcloudapi.com |

**注意：[金融区](https://cloud.tencent.com/document/product/304/2766)と非金融区は分離されており、相互運用できないため、金融区サービスをアクセスする場合（共通パラメータRegionが金融区地域）、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。**

| 金融区アクセス地域 | 金融区ドメイン名 |
|----------|------|
|華東地区（上海金融）| cvm.ap-shanghai-fsi.tencentcloudapi.com|
|華南地区（深セン金融）| cvm.ap-shenzhen-fsi.tencentcloudapi.com|

## 2. 通信プロトコル

すべてのTencent Cloud APIはHTTPSを介して通信し、非常に安全な通信チャネルを提供します。

## 3. リクエスト方法

サポートしているHTTPリクエスト方法：

* POST（推薦）
* GET

POSTリクエストがサポートするContent-Typeタイプ：

* application/json（推薦）、TC3-HMAC-SHA256署名方法を使用する必要があります。
* application/x-www-form-urlencoded、HmacSHA1またはHmacSHA256署名方法を使用する必要があります。
* multipart/form-data（一部APIだけでサポート）、TC3-HMAC-SHA256署名方法を使用する必要があります。

GETリクエスト長さは32 KBを超えてはいけません。POSTリクエストの署名方法がHmacSHA1、HmacSHA256の場合、長さは1 MBを超えてはいけません。

## 4. 文字コーディング

常にUTF-8エンコードを使用します。

