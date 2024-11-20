Tencent Cloud APIは、各アクセスリクエストを認証します。つまり、各リクエストは、リクエスト者の身元を確認するために共通リクエストパラメータに署名情報（Signature）を含める必要があります。
署名情報は、SecretIdおよびSecretKeyを含むセキュリティ認証情報によって生成されます；ユーザーがまだセキュリティ認証情報を持っていない場合、[クラウドAPI暗号鍵ページ](https://console.cloud.tencent.com/capi)で申請してください。申請しないと、クラウドAPIを呼び出すことができません。

## セキュリティ認証情報の申請
クラウドAPIを初めて使用する前に、[クラウドAPI暗号鍵ページ](https://console.cloud.tencent.com/capi)にアクセスしてセキュリティ認証情報を申請してください。
セキュリティ認証情報はSecretIdとSecretKeyを含みます：
* SecretId    API呼び出し元IDを識別するために使用されます
* SecretKey署名文字列とサーバー側の検証署名文字列を暗号化するために使用される暗号鍵。
* <font color='red'>漏洩を避けるために、ユーザーはセキュリティ認証情報を大切に保管する必要があります。</font>

セキュリティ認証情報の具体的な申請手順は以下のとおりです：

1. [Tencent Cloud管理センターコンソール](https://console.cloud.tencent.com/)にログインします。
1. [クラウドAPI暗号鍵](https://console.cloud.tencent.com/capi)のコンソールページに移動します
1. [クラウドAPI暗号鍵](https://console.cloud.tencent.com/capi)ページで、【新規作成】をクリックして、SecretId/SecretKeyのペアを作成できます

注意：開発者アカウントは、最大2組のSecretId/SecretKeyを持つことができます。

## TC3-HMAC-SHA256 署名方法

注意：GET方法では、Content-Type：application/x-www-form-urlencodedプロトコルフォーマットのみがサポートされています。POST方法では、現在Content-Type：application/jsonおよびContent-Type：multipart/form-dataの両方のプロトコルフォーマットがサポートされています。jsonフォーマットはデフォルトですべての業務APIでサポートされます。multipartフォーマットは特定の業務APIでしかサポートされません。この時、このAPIはjsonフォーマットで呼び出されることはできません。詳細については、業務APIドキュメントの説明を参照してください。

これからは、CVMが広州区インスタンスリストを照合することを一例として、署名計算プロセスをステップバイステップで紹介します。インスタンスリストを照合する2つのパラメータ、LimitとOffsetのみを使用しました。GET方法で呼び出します。

例えば、ユーザーのSecretIdとSecretKeyがAKID**********************0123456789EXAMPLEとGu5t9xGARNpq86cd98joQYCN3EXAMPLEです

### 1. 正規リクエスト列のつなぎ合わせ

次のフォーマットで正規リクエスト列（CanonicalRequest）をつなぎ合わせます：

```
CanonicalRequest =
    HTTPRequestMethod + '\n' +
    CanonicalURI + '\n' +
    CanonicalQueryString + '\n' +
    CanonicalHeaders + '\n' +
    SignedHeaders + '\n' +
    HashedRequestPayload
```

- HTTPRequestMethod：HTTPリクエスト方法（GET、POST）、この例ではGETです；
- CanonicalURI：URIパラメータ、API 3.0では固定的にスラッシュです（/）；
- CanonicalQueryString：HTTPリクエストURLにあるクエリ文字列を送信し、POSTリクエストに対して、固定的には空文字列です。GETリクエストに対して、URLにある疑問符（?）後の文字列の内容です。この例の値は：Limit=10&Offset=0です。注意：CanonicalQueryStringはURLコーディング必要です。
- CanonicalHeaders：署名のヘッダー情報は少なくともhostとcontent-typeという2つのヘッダーを含み、カスタムヘッダーも追加して署名に入れて、自分のリクエストの一意性とセキュリティを向上させることもできます。つなぎ合わせ規則：1）ヘッダーkeyとvalueは統一に小文字に変換し、先頭と末尾のスペースを削除して、key:value\nのフォーマットでつなぎ合わせます；2）複数ヘッダーの場合は、ヘッダーkey（小文字）の辞書順に従ってつなぎ合わせます。この例では：`content-type:application/x-www-form-urlencoded\nhost:cvm.tencentcloudapi.com\n`
- SignedHeaders：署名のヘッダー情報は、今回のリクエストの署名にどのヘッダーを入れたかを説明し、それはCanonicalHeadersに含まれるヘッダー内容と一致します。content-typeとhostは必須ヘッダーです。つなぎ合わせ規則：1）ヘッダーkeyを統一に小文字に変換します；2）複数ヘッダーの場合は、ヘッダーkey（小文字）の辞書順に従ってつなぎ合わせ、セミコロン（;）で区切ります。この例では：`content-type;host`
- HashedRequestPayload：リクエスト本文のハッシュ値。計算方法はLowercase(HexEncode (Hash.SHA256(RequestPayload)))です。HTTPリクエストの本文payload全体に対してSHA256ハッシュを作成し、それを16進数でエンコードし、最後にエンコードされた文字列を小文字に変換します。注意：GETリクエストの場合、RequestPayloadは固定的に空文字列です。POSTリクエストの場合、RequestPayloadはHTTPリクエスト本文payloadです。

以上の規則によって、例で取得された正規リクエスト列は以下のとおりです（分かりやすくするために、\n改行符は直接に改行して表示されます。）：
```
GET
/
Limit=10&Offset=0
content-type:application/x-www-form-urlencoded
host:cvm.api.tencentyun.com

content-type;host
e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
```

### 2. 署名する文字列のつなぎ合わせ

以下のフォーマットで署名する文字列をつなぎ合わせます：

```
StringToSign =
    Algorithm + \n +
    RequestTimestamp + \n +
    CredentialScope + \n +
    HashedCanonicalRequest
```

- Algorithm：署名アルゴリズム、現在は固定的にTC3-HMAC-SHA256です；
- RequestTimestamp：リクエストタイムスタンプは。つまり、リクエストヘッダーのX-TC-Timestampの値です。以上のリクエストの例では、値が1539084154です；
- CredentialScope：認証情報範囲、フォーマットはDate/service/tc3_requestです。日付、リクエストするサーバーと終了文字列（tc3_request）が含まれています。DateはUTC標準時間の日付で、その値は共通パラメータX-TC-Timestampによって変換されたUTC標準時間の日付と一致する必要があります；serviceは製品名で、呼び出された製品ドメイン名と一致する必要があります。例えばcvm。以上のリクエストの例では、値が2018-10-09/cvm/tc3_requestです；
- HashedCanonicalRequest：HashedCanonicalRequest：以上のステップでつなぎ合わせによって取得された正規リクエスト列のハッシュ値。その計算方法はLowercase(HexEncode(Hash.SHA256(CanonicalRequest)))です。

以上の規則によって、例で取得された署名する文字列は以下のとおりです（分かりやすくするために、\n改行符は直接に改行して表示されます。）：

```
TC3-HMAC-SHA256
1539084154
2018-10-09/cvm/tc3_request
91c9c192c14460df6c1ffc69e34e6c5e90708de2a6d282cccf957dbf1aa7f3a7
```

### 3. 署名の計算
1）派生署名暗号鍵を計算します。疑似コードは次のとおりです

```
SecretKey = "Gu5t9xGARNpq86cd98joQYCN3EXAMPLE"
SecretDate = HMAC_SHA256("TC3" + SecretKey, Date)
SecretService = HMAC_SHA256(SecretDate, Service)
SecretSigning = HMAC_SHA256(SecretService, "tc3_request")
```

- SecretKey：初期SecretKey；
- Date：CredentialにあるDateフィールド情報です。以上の例では、2018-10-09です；
- Service：CredentialにあるServiceフィールド情報です。以上の例では、cvmです；

2）署名の計算。疑似コードは次のとおりです

```
Signature = HexEncode(HMAC_SHA256(SecretSigning, StringToSign))
```

- SecretSigning：以上の計算で取得された派生署名暗号鍵；
- StringToSign：ステップ2で計算された署名する文字列；

### 4. Authorizationのつなぎ合わせ

以下のフォーマットのようにAuthorizationをつなぎ合わせます：

```
Authorization =
    Algorithm + ' ' +
    'Credential=' + SecretId + '/' + CredentialScope + ', ' +
    'SignedHeaders=' + SignedHeaders + ', '
    'Signature=' + Signature
```

- Algorithm：署名方法、現在は固定的にTC3-HMAC-SHA256です；
- SecretId：暗号鍵ペアにあるSecretId；
- CredentialScope：認証情報の範囲。上記を参照してください；
- SignedHeaders：署名のヘッダー情報。上記を参照てください；
- Signature：署名値

以上の規則によって、例で取得された値は：

```
TC3-HMAC-SHA256 Credential=AKIDEXAMPLE/Date/service/tc3_request, SignedHeaders=content-type;host, Signature=5da7a33f6993f0614b047e5df4582db9e9bf4672ba50567dba16c6ccf174c474
```

最終的な完全な呼び出す情報は次のとおりです：

```
https://cvm.tencentcloudapi.com/?Limit=10&Offset=0

Authorization: TC3-HMAC-SHA256 Credential=AKID**********************0123456789EXAMPLE/2018-10-09/cvm/tc3_request, SignedHeaders=content-type;host, Signature=5da7a33f6993f0614b047e5df4582db9e9bf4672ba50567dba16c6ccf174c474
Content-Type: application/x-www-form-urlencoded
Host: cvm.tencentcloudapi.com
X-TC-Action: DescribeInstances
X-TC-Version: 2017-03-12
X-TC-Timestamp: 1539084154
X-TC-Region: ap-guangzhou
```

### 5. 署名のデモ

#### Java

```
import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.URL;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Map;
import java.util.TimeZone;
import java.util.TreeMap;
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import javax.net.ssl.HttpsURLConnection;
import javax.xml.bind.DatatypeConverter;

import org.apache.commons.codec.digest.DigestUtils;

public class TencentCloudAPITC3Demo {
    private final static String CHARSET = "UTF-8";
    private final static String ENDPOINT = "cvm.tencentcloudapi.com";
    private final static String PATH = "/";
    private final static String SECRET_ID = "AKID**********************0123456789EXAMPLE";
    private final static String SECRET_KEY = "sk0123456789********************EXAMPLE";
    private final static String CT_X_WWW_FORM_URLENCODED = "application/x-www-form-urlencoded";
    private final static String CT_JSON = "application/json";
    private final static String CT_FORM_DATA = "multipart/form-data";

    public static byte[] sign256(byte[] key, String msg) throws Exception {
        Mac mac = Mac.getInstance("HmacSHA256");
        SecretKeySpec secretKeySpec = new SecretKeySpec(key, mac.getAlgorithm());
        mac.init(secretKeySpec);
        return mac.doFinal(msg.getBytes(CHARSET));
    }

    public static void main(String[] args) throws Exception {
        String service = "cvm";
        String host = "cvm.tencentcloudapi.com";
        String region = "ap-guangzhou";
        String action = "DescribeInstances";
        String version = "2017-03-12";
        String algorithm = "TC3-HMAC-SHA256";
        String timestamp = "1539084154";
        //String timestamp = String.valueOf(System.currentTimeMillis() / 1000);
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
        // エラーがないように、タイムゾーンに注意してください
        sdf.setTimeZone(TimeZone.getTimeZone("UTC"));
        String date = sdf.format(new Date(Long.valueOf(timestamp + "000")));

        // ************* ステップ1：正規リクエスト列のつなぎ合わせ *************
        String httpRequestMethod = "GET";
        String canonicalUri = "/";
        String canonicalQueryString = "Limit=10&Offset=0";
        String canonicalHeaders = "content-type:application/x-www-form-urlencoded\n" + "host:" + host + "\n";
        String signedHeaders = "content-type;host";
        String hashedRequestPayload = DigestUtils.sha256Hex("");
        String canonicalRequest = httpRequestMethod + "\n" + canonicalUri + "\n" + canonicalQueryString + "\n"
                + canonicalHeaders + "\n" + signedHeaders + "\n" + hashedRequestPayload;
        System.out.println(canonicalRequest);

        // ************* ステップ2：署名する文字列のつなぎ合わせ *************
        String credentialScope = date + "/" + service + "/" + "tc3_request";
        String hashedCanonicalRequest = DigestUtils.sha256Hex(canonicalRequest.getBytes(CHARSET));
        String stringToSign = algorithm + "\n" + timestamp + "\n" + credentialScope + "\n" + hashedCanonicalRequest;
        System.out.println(stringToSign);

        // ************* ステップ3：署名の計算 *************
        byte[] secretDate = sign256(("TC3" + SECRET_KEY).getBytes(CHARSET), date);
        byte[] secretService = sign256(secretDate, service);
        byte[] secretSigning = sign256(secretService, "tc3_request");
        String signature = DatatypeConverter.printHexBinary(sign256(secretSigning, stringToSign)).toLowerCase();
        System.out.println(signature);

        // ************* ステップ4：Authorizationのつなぎ合わせ *************
        String authorization = algorithm + " " + "Credential=" + SECRET_ID + "/" + credentialScope + ", "
                + "SignedHeaders=" + signedHeaders + ", " + "Signature=" + signature;
        System.out.println(authorization);

        TreeMap<String, String> headers = new TreeMap<String, String>();
        headers.put("Authorization", authorization);
        headers.put("Host", host);
        headers.put("Content-Type", CT_X_WWW_FORM_URLENCODED);
        headers.put("X-TC-Action", action);
        headers.put("X-TC-Timestamp", timestamp);
        headers.put("X-TC-Version", version);
        headers.put("X-TC-Region", region);
    }
}
```

#### Python

```
# -*- coding: utf-8 -*-
import hashlib, hmac, json, os, sys, time
from datetime import datetime

# 暗号鍵パラメータ
secret_id = "AKID**********************0123456789EXAMPLE"
secret_key = "sk0123456789********************EXAMPLE"

service = "cvm"
host = "cvm.tencentcloudapi.com"
endpoint = "https://" + host
region = "ap-guangzhou"
action = "DescribeInstances"
version = "2017-03-12"
algorithm = "TC3-HMAC-SHA256"
timestamp = 1539084154
date = datetime.utcfromtimestamp(timestamp).strftime("%Y-%m-%d")
params = {"Limit": 10, "Offset": 0}

# ************* ステップ1：正規リクエスト列のつなぎ合わせ *************
http_request_method = "GET"
canonical_uri = "/"
canonical_querystring = "Limit=10&Offset=0"
ct = "x-www-form-urlencoded"
payload = ""
if http_request_method == "POST":
    canonical_querystring = ""
    ct = "json"
    payload = json.dumps(params)
canonical_headers = "content-type:application/%s\nhost:%s\n" % (ct, host)
signed_headers = "content-type;host"
hashed_request_payload = hashlib.sha256(payload.encode("utf-8")).hexdigest()
canonical_request = (http_request_method + "\n" +
                     canonical_uri + "\n" +
                     canonical_querystring + "\n" +
                     canonical_headers + "\n" +
                     signed_headers + "\n" +
                     hashed_request_payload)
print(canonical_request)

# ************* ステップ2：署名する文字列のつなぎ合わせ *************
credential_scope = date + "/" + service + "/" + "tc3_request"
hashed_canonical_request = hashlib.sha256(canonical_request.encode("utf-8")).hexdigest()
string_to_sign = (algorithm + "\n" +
                  str(timestamp) + "\n" +
                  credential_scope + "\n" +
                  hashed_canonical_request)
print(string_to_sign)


# ************* ステップ3：署名の計算 *************
# 署名要約関数の計算
def sign(key, msg):
    return hmac.new(key, msg.encode("utf-8"), hashlib.sha256).digest()
secret_date = sign(("TC3" + secret_key).encode("utf-8"), date)
secret_service = sign(secret_date, service)
secret_signing = sign(secret_service, "tc3_request")
signature = hmac.new(secret_signing, string_to_sign.encode("utf-8"), hashlib.sha256).hexdigest()
print(signature)

# ************* ステップ4：Authorizationのつなぎ合わせ *************
authorization = (algorithm + " " +
                 "Credential=" + secret_id + "/" + credential_scope + ", " +
                 "SignedHeaders=" + signed_headers + ", " +
                 "Signature=" + signature)
print(authorization)

# 共通パラメータのリクエストヘッダーへの追加
headers = {
    "Authorization": authorization,
    "Host": host,
    "Content-Type": "application/%s" % ct,
    "X-TC-Action": action,
    "X-TC-Timestamp": str(timestamp),
    "X-TC-Version": version,
    "X-TC-Region": region,
}
```


## 署名失敗

実際の状況によって、以下の署名失敗のエラーコードがあります。適切に処理してください

| エラーコード | エラー説明|
|----------|---------|
| AuthFailure.SignatureExpire | 署名期限切れ |
| AuthFailure.SecretIdNotFound | 暗号鍵が存在しません |
| AuthFailure.SignatureFailure | 署名エラー |
| AuthFailure.TokenFailure | トークンエラー |
| AuthFailure.InvalidSecretId | 暗号鍵が不正です（クラウドAPI暗号鍵タイプではありません）） |

