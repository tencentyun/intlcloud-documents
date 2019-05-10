## 1. サービスアドレス

API は、最寄りリージョンへのアクセスに対応しています。本製品の最寄りリージョンのアクセスドメインは cvm.tencentcloudapi.com です。広州リージョンのドメインを cvm.ap-guangzhou.tencentcloudapi.com とするように、リージョンのドメインを指定してアクセスすることもできます。

最寄りのリージョンのアクセスドメインのご使用をお勧めします。インターフェースを呼び出す時のクライアントの位置に基づいて、自動的に**最寄りの**具体的なリージョンのサーバに解析されます。広州でリクエストを送信した場合、自動的に広州のサーバに解析され、cvm.ap-guangzhou.tencentcloudapi.com を指定するのと同じ効果があります。

**注意：遅延の影響を受けやすいサービスの場合、リージョンを含むドメインを指定することをお勧めします**

現在サポートするドメインのリストは次の通りです。

| アクセスリージョン | ドメイン |
|----------|------|
| 最寄りのリージョンにアクセス（推奨、金融エリア以外のみをサポート）| cvm.tencentcloudapi.com|
| 華南エリア(広州) | cvm.ap-guangzhou.tencentcloudapi.com|
| 華東エリア(上海) | cvm.ap-shanghai.tencentcloudapi.com|
| 華北エリア(北京) | cvm.ap-beijing.tencentcloudapi.com|
| 西南エリア(成都) | cvm.ap-chengdu.tencentcloudapi.com|
| 西南エリア(重慶) | cvm.ap-chongqing.tencentcloudapi.com|
| 東南アジアエリア(中国香港) | cvm.ap-hongkong.tencentcloudapi.com |
| 東南アジアエリア(シンガポール) | cvm.ap-singapore.tencentcloudapi.com|
| アジア太平洋エリア(バンコク) | cvm.ap-bangkok.tencentcloudapi.com |
| アジア太平洋エリア(ムンバイ) | cvm.ap-mumbai.tencentcloudapi.com|
| アジア太平洋エリア(ソウル) | cvm.ap-seoul.tencentcloudapi.com|
| アジア太平洋エリア(東京) | cvm.ap-tokyo.tencentcloudapi.com |
| 米国東部(ヴァージニア) | cvm.na-ashburn.tencentcloudapi.com|
| 米国西部(シリコンバレー) | cvm.na-siliconvalley.tencentcloudapi.com|
| 北米エリア(トロント) | cvm.na-toronto.tencentcloudapi.com |
| 欧州エリア(フランクフルト) | cvm.eu-frankfurt.tencentcloudapi.com |
| 欧州エリア(モスクワ) | cvm.eu-moscow.tencentcloudapi.com |

**注意：[金融エリア](https://cloud.tencent.com/document/product/304/2766)とそれ以外のエリアは隔てられており、相互運用できません。そのため、金融エリアのサービスにアクセスする場合（共通パラメータの Region は金融エリアのリージョンとする）、同時に金融エリアのリージョンを含むドメイン名を指定する必要があります。最も良いのは、Regionのエリアと一致することです。**

| 金融エリアアクセスリージョン | 金融エリア名 |
|----------|------|
|華東エリア(上海金融)| cvm.ap-shanghai-fsi.tencentcloudapi.com|
|華南エリア(深圳金融)| cvm.ap-shenzhen-fsi.tencentcloudapi.com|

## 2. 通信プロトコル

Tencent Cloud API のインターフェースは全て HTTPS で通信するため、安全性の高い通信チャネルを提供します。

## 3. リクエスト方法

サポートする HTTP リクエスト方法には次のようなものがあります。

* POST（推奨）
* GET

POST リクエストがサポートする Content-Type のタイプには次のようなものがあります。

* application/json（推奨）。必ず TC3-HMAC-SHA256 による署名方法を使用するものとします。
* application/x-www-form-urlencoded。必ず HmacSHA1 または HmacSHA256 による署名方法を使用するものとします。
* multipart/form-data（一部のインターフェースのみサポート）。必ず TC3-HMAC-SHA256 による署名方法を使用するものとします。

GET リクエストのパッケージのサイズは 32 KBを超えないようにします。POST リクエストの署名方法に HmacSHA1、HmacSHA256 を使用する場合、1 MB 超えないようにします。POST リクエストの署名方法に TC3-HMAC-SHA256 を使用する場合、10 MB をサポートします。

## 4. 文字列エンコード

全て UTF-8エンコーディングを使用します。

