> !
> 1. このドキュメントはCOS XMLバージョンでのみ利用可能で、ログイン後にCOSコンソールのホームページで確認することができます。
> 2. このドキュメントはPOST objectのHTTPリクエストには適用されません。

COSを使用する場合、RESTful APIを介してHTTP匿名リクエストまたはHTTP署名リクエストをCOSに開始することができ、署名リクエストの場合、COSサーバーはリクエストの発信元を認証します。

- 匿名リクエスト：HTTPリクエストにはID識別と認証情報が含まれていません。HTTPリクエスト操作はRESTful APIを介して実行されます。
- 署名リクエスト：HTTPリクエストときに署名を追加し、COSサーバーがメッセージを受信した後に身元認証を行います。検証に成功した場合はリクエストを受け入れて実行し、そうでない場合、エラーメッセージを返してこのリクエストを破棄します。

Tencent Cloud COSは、HMAC（Hash Message Authentication Code）暗号鍵のカスタムHTTPプランに基づいて身元認証します。
Tencent Cloud COSは現在、ユーザーが署名を生成するための[COS署名ツール](https://cos5.cloud.tencent.com/static/cos-sign/)を提供しています。これは必要に応じて使用できます。

## 署名適用シナリオ

COSが使用されるシナリオでは、外部へリリースする必要があるデータについて、オブジェクトを通常パブリック読み取り、プライベート書き込みに設定できます。つまり、誰でも見ることができ、ACLポリシーで指定されたアカウントまたはIPを通して書き込むことができます。この時点で、ACLポリシーをAPIリクエスト署名と組み合わせて、アクセスに対して身元を認証し、操作の権限と有効期間を制御することができます。

>!SDKを使用して開発している場合は、この文書に記載されているAPIリクエスト署名が含まれています。**元のAPIを介して再開発したい場合にのみ、この文章に記載されている手順に従う必要があります**。

上記のシナリオでは、APIリクエストに対する多くの側面でセキュリティ保護を行います：

1. **リクエスト者身元検証**。リクエスト者の身元は、アクセス者の一意のIDと暗号鍵によって決まります。
2. **送信データの改ざんを防ぐ**。データーを暗号化して検証し、送信された内容の完全性を保証します。
3. **署名の盗難を防ぐ**。署名の盗難や重複利用を防ぐために署名の有効期間を設定し、データーを暗号化します。

## 署名プロセス

クライアントはHTTPリクエストを通して署名し、署名されたリクエストをTencent Cloudに送信して署名検証を行います。具体的なプロセスは下図の通りです。
![フローチャート](//mc.qcloudimg.com/static/img/4a1eb29033caa977c648cb84d9398fdd/image.png)

## 準備作業

1. APPID、SecretIdとSecretKey。 
   CAMコンソールの[API暗号鍵管理](https://console.cloud.tencent.com/cam/capi)ページで取得します。
2.開発言語を決めます。
   サポートされている言語には、Java、PHP、C Sharp、C++、Node.js、Pythonが含まれますが、これらに限定されません。開発言語に応じてHMAC-SHA1、SHA1関数を指定する必要があります。

## 署名コンテンツ

次の例に示すように、RESTful APIを介してCOSに開始されたHTTP署名リクエストについては、標準のHTTP Authorizationヘッダーを使用して渡されます。

```shell
PUT ?versioning HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q&q-sign-time=1480932292;1481012298&q-key-time=1480932292;1481012298&q-header-list=host&q-url-param-list=versioning&q-signature=438023e4a4207299d87bb75d1c739c06cc9406bb
```

その中で、署名内容は複数のkey = valueペアで構成され、それらは「＆」で接続されています。フォーマットは次のとおりです：

```shell
q-sign-algorithm=sha1&q-ak=[SecretID]&q-sign-time=[SignTime]&
q-key-time=[KeyTime]&q-header-list=[SignedHeaderList]&
q-url-param-list=[SignedParameterList]&q-signature=[Signature]
```

<span id="signaturesplit"></span>

### 鍵値説明

その中で、署名内容を構成する鍵値（key = value）は、次のように説明されています：

<style>
table th:first-of-type {
    width: 150px;
}
</style><style  rel="stylesheet"> table th:nth-of-type(1) { width: 140px; }</style>

| 鍵（key）        | 値（value）                   | 説明                                                         | 必須であるかどうか |
| ---------------- | --------------------------- | ------------------------------------------------------------ | -------- |
| q-sign-algorithm | sha1                        | 署名アルゴリズムは現時点でsha1、つまりsha1のみサポートします。                      | はい       |
| q-ak             | パラメータ[*SecretID*]            | アカウントID、つまりSecretIdです。CAMコンソールの[API暗号鍵管理](https://console.cloud.tencent.com/cam/capi)ページで取得します。<br>**例えば：**AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q 。 | はい       |
| q-sign-time      | パラメータ[*SignTime*]            | この署名の有効な開始時刻と終了時刻。[Unixタイムスタンプ]（#add）による開始時刻と終了時刻（秒単位）を説明します。フォーマットは[*start-seconds*];[*end-seconds*]。<br>**例えば：** 1480932292;1481012298 。 | はい       |
| q-key-time       | パラメータ[*KeyTime*]             | q-sign-time値と同じです。                                      | はい       |
| q-header-list    | パラメータ[*SignedHeaderList*]    | HTTPリクエストヘッダー。key:valueから一部またはすべてのkeyを抽出し、keyを小文字に変換し、複数のkeyを辞書順に並べ替える必要があります。keyのセットが複数ある場合は、「;」を使用して接続できます。<br>**例えば：** HTTPリクエスト   「Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com Content-Type: image/jpeg」、そのSignedHeaderListはcontent-type;hostです。 | はい       |
| q-url-param-list | パラメータ[*SignedParameterList*] | HTTPリクエストパラメータ。key=valueから一部またはすべてのkeyを抽出し、keyを小文字に変換し、複数のkeyを辞書順に並べ替える必要があります。keyのセットが複数ある場合は、「;」を使用して接続できます。<br>**例えば：** HTTPリクエスト   「GET /?prefix=abc&max-keys=20」、そのSignedParameterListはmax-keys;prefixまたはprefixです。 | はい       |
| q-signature      | パラメータ[Signature]             | HTTP内容署名、[Signature計算](#signature)を確認してください。         | はい       |

<a id="add">&nbsp;</a><!-- アンカーポイントを定義します --> 
>?q-sign-timeとq-key-timeについて：
>1. UNIXタイムスタンプは、GMT 1970年01月01日00時00分00秒（北京時間1970年01月01日08時00分00秒）から今までの合計秒数です。
>2. 終了タイムスタンプは開始タイムスタンプよりも大きくする必要があります。そうしないと、署名はすぐに期限切れになります。
>**3. 署名を計算してリクエストを送信するときには、このマシンの時間が国際標準時間で調整されていることを確認してください。その差が大きすぎると、サーバーは関連するリクエストを拒否します。**

<span id="signature"></span>
### Signature計算

Signatureの計算は4つのステップがあります：

1. 署名の有効な開始時刻と終了時刻に対して、値SignKeyを暗号化して計算します。
2. 固定フォーマットの組み合わせに基づいてHttpStringを生成します。
3. HttpStringを暗号化し、固定フォーマットの組み合わせに基づいてStringToSignを生成します。
4. StringToSignを暗号化し、Signatureを生成します。

#### コード説明

その疑似コードは：

```shell
SignKey = HMAC-SHA1(SecretKey,"[q-key-time]")
HttpString = [HttpMethod]\n[HttpURI]\n[HttpParameters]\n[HttpHeaders]\n
StringToSign = [q-sign-algorithm]\n[q-sign-time]\nSHA1-HASH(HttpString)\n
Signature = HMAC-SHA1(SignKey,StringToSign)
```

その中で、異なる開発言語環境では、以下を含む異なる言語規則でコードをアップデートしてください：

1. 変数の定義と割り当て値、使用する開発言語の規則に従ってアップデートしてください。
2. 擬似関数SHA1-HASH、出力は16進数小文字です。

#### 暗号化アルゴリズムの例

HMAC-SHA1とSHA1-HASHを異なる言語で呼び出す方法は、次の例を参照できます：

#### PHP

```c
$sha1HttpString = sha1('ExampleHttpString');

$signKey = hash_hmac('sha1', 'ExampleKeyTime', 'YourSecretKey');
```

#### Java

```shell
import org.apache.commons.codec.digest.DigestUtils;
import org.apache.commons.codec.digest.HmacUtils;

String sha1HttpString = DigestUtils.sha1Hex("ExampleHttpString");

String signKey = HmacUtils.hmacSha1Hex("YourSecretKey", "ExampleKeyTime");
```

#### Python

```shell
import hmac
import hashlib

sha1 = hashlib.sha1()
sha1_http_string = sha1.update('ExampleHttpString'.encode('utf-8')).hexdigest()

sign_key = hmac.new('YourSecretKey'.encode('utf-8'), 'ExampleKeyTime'.encode('utf-8'), hashlib.sha1).hexdigest()
```

#### Node.js

```shell
var crypto = require('crypto');

var sha1HttpString = crypto.createHash('sha1').update('ExampleHttpString').digest('hex');
var signKey = crypto.createHmac('sha1', 'YourSecretKey').update('ExampleKeyTime').digest('hex');
```

#### Go

```shell
import (
	"crypto/hmac"
	"crypto/sha1"
)

h := sha1.New()
h.Write([]byte("ExampleHttpString"))
sha1HttpString := h.Sum(nil)

var hashFunc = sha1.New
h = hmac.New(hashFunc, []byte("YourSecretKey"))
h.Write([]byte("ExampleKeyTime"))
signKey := h.Sum(nil)
```

#### パラメータ説明

| パラメータ               | 説明                                                         |
| ------------------ | ------------------------------------------------------------ |
| [q-key-time]       | [鍵値の説明](#signaturesplit)に入力されたq-key-timeと一致している必要があります |
| [HttpMethod]       | HTTPリクエスト方法。小文字、すなわちget、post、put、delete、head、optionsだけがサポートされています。<br>**例えば：** HTTPリクエスト   「GET /testfile」、そのHttpMethodはgetです。 |
| [HttpURI]          | HTTPリクエストURI部分。つまり、「/」から始まる仮想パス部分です。<br>**例えば：** HTTPリクエスト「GET /testfile」、そのHttpURIは/testfileです。<br>**注意：**URIに中国語または特殊文字が含まれている場合は、URLEncodeは不要です。 |
| [HttpParameters]   | HTTPリクエストパラメータ。つまり、URIの「？」の後に「＆」で接続されているの部分です。key = valueの全部または一部を選択し、keyを小文字に変換し、valueをURLEncodeで変換し、複数のkey = valueペアを「＆」で接続して辞書順にソートする必要があります。<br>**例えば：**  HTTPリクエスト   「GET /?prefix=abc&max-keys=20」、そのHttpParametersはmax-keys=20&prefix=abcまたはprefix=abcです。<br>**注意：**含まれるkey = valueペアのkeyは、[鍵値説明](#signaturesplit)に入力されたq-url-param-listのkeyと同じである必要があります。 |
| [HttpHeaders]      | HTTPリクエストヘッダー。key:valueの全部または一部を選択し、それをkey=valueフォーマットに変換し、valueをURLEncodeで変換し、複数のkey = valueペアを「＆」で接続して辞書順にソートする必要があります。<br>**例えば：**  HTTPリクエスト  「Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com Content-Type: image/jpeg」、そのHttpHeadersはcontent-type=image%2Fjpeg&host=examplebucket-1250000000.cos.ap-beijing.myqcloud.comです。<br>**注意：**含まれるkey = valueペアのkeyは、[鍵値説明](#signaturesplit)に入力されたq-header-listのkeyと同じである必要があります。 |
| [q-sign-algorithm] | sha1。現時点ではsha1暗号化アルゴリズムのみサポートします。                             |
| [q-sign-time]      | [鍵値の説明](#signaturesplit)に入力されたq-sign-timeと一致している必要があります |

#### パラメータインスタンス

| パラメータ               | 値                                                        |
| ------------------ | --------------------------------------------------------- |
| [q-key-time]       | 1417773892;1417853898                                     |
| [HttpMethod]       | get                                                       |
| [HttpURI]          | /testfile                                                 |
| [HttpParameters]   | max-keys=20&prefix=abc                                    |
| [HttpHeaders]      | host=examplebucket-1250000000.cos.ap-beijing.myqcloud.com |
| [q-sign-algorithm] | sha1                                                      |
| [q-sign-time]      | 1417773892;1417853898                                     |

## 例

例えば、あるユーザーがAPI呼び出し方法を使用してオブジェクトをダウンロードおよびアップロードし、呼び出しに署名しようとする場合。

### 準備作業

CAMコンソールの[API暗号鍵管理](https://console.cloud.tencent.com/cam/capi)ページにログインして、そのAPPID、SecretIdとSecretKeyを取得し、次のように開発言語を決定します：

| APPID      | SecretId                             | SecretKey                        | 開発言語 |
| ---------- | ------------------------------------ | -------------------------------- | -------- |
| 1250000000 | AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q | BQYIM75p8x0iWVFSIgqEKwFprpRSVHlz | PHP      |

### アップデートオブジェクト

要件：オブジェクトをバケットexamplebucketにアップロードします

元のHTTPリクエストは：

```shell
PUT /example-file HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
x-cos-storage-class: standard

Hello world
```

署名後のHTTPリクエストは：

```shell
PUT /example-file HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
x-cos-storage-class: standard
x-cos-content-sha1: 7b502c3a1f48c8609ae212cdfb639dee39673f5e
Authorization: q-sign-algorithm=sha1&q-ak=AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q&q-sign-time=1417773892;1417853898&q-key-time=1417773892;1417853898&q-header-list=host;x-cos-content-sha1;x-cos-storage-class&q-url-param-list=&q-signature=14e6ebd7955b0c6da532151bf97045e2c5a64e10

Hello world
```

各パラメータに対応する値と説明は以下のとおりです：

| 鍵（key）          | 値（value）                                   | 備考                                     |
| ---------------- | ------------------------------------------- | ---------------------------------------- |
| q-sign-algorithm | sha1                                        | 現時点ではsha1署名アルゴリズムのみサポートします。               |
| q-ak             | AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q        | SecretIdフィールド                            |
| q-sign-time      | 1417773892;1417853898                       | 2014/12/5 18:04:52 から 2014/12/6 16:18:18 |まで
| q-sign-time      | 1417773892;1417853898                       | 2014/12/5 18:04:52 から 2014/12/6 16:18:18 |まで
| q-header-list    | host;x-cos-content-sha1;x-cos-storage-class | HTTPヘッダーkeyの辞書順ソートリスト        |
| q-url-param-list |                                             | HTTPパラメータリストはブランクです                        |
| q-signature      | 14e6ebd7955b0c6da532151bf97045e2c5a64e10    | コード計算によって取得します                         |

その中で、q-signatureの計算コードは：

```c
$signTime = '1417773892;1417853898';
$keyTime = $signTime;
$signKey = hash_hmac('sha1', $keyTime, 'BQYIM75p8x0iWVFSIgqEKwFprpRSVHlz');
$httpString = "put\n/example-file\n\nhost=examplebucket-1250000000.cos.ap-beijing.myqcloud.com&x-cos-content-sha1=7b502c3a1f48c8609ae212cdfb639dee39673f5e&x-cos-storage-class=standard\n";
$sha1edHttpString = sha1($httpString);
$stringToSign = "sha1\n$signTime\n$sha1edHttpString\n";
$signature = hash_hmac('sha1', $stringToSign, $signKey);
```

### ダウンロード対象

要件：バケットexamplebucket内のオブジェクトの最初の4バイトをダウンロードします。

元のHTTPリクエストは：

```shell
GET /example-file HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Range: bytes=0-3
```

署名後のHTTPリクエストは：

```shell
GET /example-file HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Range: bytes=0-3
Authorization: q-sign-algorithm=sha1&q-ak=AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q&q-sign-time=1417773892;1417853898&q-key-time=1417773892;1417853898&q-header-list=host;range&q-url-param-list=&q-signature=4b6cbab14ce01381c29032423481ebffd514e8be
```

各パラメータに対応する値と説明は以下のとおりです：

| 鍵（key）        | 値（value）                              | 備考                                     |
| ---------------- | ---------------------------------------- | ---------------------------------------- |
| q-sign-algorithm | sha1                                     | 現時点ではsha1署名アルゴリズムのみサポートします。               |
| q-ak             | AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q     | SecretIdフィールド                            |
| q-sign-time      | 1417773892;1417853898                    | 2014/12/5 18:04:52から2014/12/6 16:18:18まで |
| q-key-time       | 1417773892;1417853898                    | 2014/12/5 18:04:52から2014/12/6 16:18:18まで |
| q-header-list    | host;range                               | HTTPヘッダーkeyのリスト                     |
| q-url-param-list |                                          | HTTPパラメータリストはブランクです                        |
| q-signature      | 4b6cbab14ce01381c29032423481ebffd514e8be | コード計算によって取得します                         |

その中で、q-signatureの計算コードは：

```c
$signTime = '1417773892;1417853898';
$keyTime = $signTime;
$signKey = hash_hmac('sha1', $keyTime, 'BQYIM75p8x0iWVFSIgqEKwFprpRSVHlz');
$httpString = "get\n/testfile\n\nhost=examplebucket-1250000000.cos.ap-beijing.myqcloud.com&range=bytes%3D0-3\n";
$sha1edHttpString = sha1($httpString);
$stringToSign = "sha1\n$signTime\n$sha1edHttpString\n";
$signature = hash_hmac('sha1', $stringToSign, $signKey);
```

