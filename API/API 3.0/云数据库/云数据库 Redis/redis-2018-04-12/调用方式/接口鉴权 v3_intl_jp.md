Tencent Cloud API は、各アクセスリクエストに対して身分認証を行います。つまり、各リクエストはいずれも共通のリクエストパラメータにおいて署名情報（Signature）を含むものとし、それによって請求者の身分を検証します。
署名情報はセキュリティ証明書によって生成され、セキュリティ証明書には SecretId と SecretKey が含まれます。ユーザーがまだセキュリティ証明書を所有していない場合、[クラウド API キー画面](https://console.cloud.tencent.com/capi)から申請してください。申請しない場合、クラウド API インターフェースを呼び出すことはできません。

## セキュリティ証明書の申請
最初にクラウド API を使用する前に、[クラウド API キー画面](https://console.cloud.tencent.com/capi)からセキュリティ証明書を申請してください。
セキュリティ証明書には、SecretId と SecretKey が含まれます。
* SecretId    API 呼び出し元 ID を識別するために使用します
* SecretKey 署名文字列とサーバ側の認証署名の文字列の暗号化に使用するキーです。
* <font color='red'>ユーザーは、漏洩がないよう厳格にセキュリティ証明書を保管しなければなりません。</font>

セキュリティ証明書を申請する具体的なステップは以下の通りです。

1. [Tencent Cloud 管理センターコンソール](https://console.cloud.tencent.com/)にログインします。
1. [クラウドAPIキー](https://console.cloud.tencent.com/capi)のコンソール画面に入ります。
1. [クラウドAPIキー](https://console.cloud.tencent.com/capi)画面で【新規作成】をクリックすると、1組の SecretId/SecretKey を作成できます

注意：開発者のアカウントは、最大で2組の SecretId / SecretKey を持つことができます。

## TC3-HMAC-SHA256 署名方法

注意：GET方式については、Content-Type: Application/x-www-form-urlencoded プロトコルフォーマットのみがサポートされています。POST方式については、現在、Content-Type: application/json および Content-Type: multipart/form-data の2種類のプロトコルフォーマットをサポートしています。json 形式は、初期設定の状態ですべてのサービスインターフェースに対応しています。multipart 形式は、特定のサービスインターフェースにのみ対応しています。この場合、そのインターフェースは json フォーマットで呼び出すことはできません。具体的なサービスインターフェースのドキュメントによる説明を参照してください。

次に、CVM で広州エリアのインスタンスリストを照会する場合を例として、署名の計算プロセスを段階ごとに紹介します。ここでは、インスタンスリストを照会する2つのパラメータ、Limit と Offset のみを使用し、GET 方式で呼び出しました。

ユーザーの SecretId と SecretKey が、それぞれ、AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE と Gu5t9xGARNpq86cd98joQYCN3EXAMPLE であると仮定しています

### 1. 正規リクエスト文字列のステッチング

以下のフォーマットに従い、正規リクエスト文字列（CanonicalRequest）をステッチングします：

```
CanonicalRequest =
    HTTPRequestMethod + '\n' +
    CanonicalURI + '\n' +
    CanonicalQueryString + '\n' +
    CanonicalHeaders + '\n' +
    SignedHeaders + '\n' +
    HashedRequestPayload
```

- HTTPRequestMethod：HTTP リクエスト方法（GET、POST ）は、本サンプルでは GET としています。
- CanonicalURI：URI パラメータは、API 3.0 ではスラッシュ（/）に固定しています。
- CanonicalQueryString：HTTP を発起して URL 内の文字列照会をリクエストします。POST リクエストに対しては、空の文字列に固定します。GET リクエストに対しては、URL 内の疑問符（?）の後ろにある文字列の内容とし、本例の値は、Limit=10&Offset=0 とします。注意：CanonicalQueryString は URL エンコードをしている必要があります。
- CanonicalHeaders：署名に関与するヘッダ情報であり、最低でも host と content-type の2つのヘッダを含みます。カスタマイズしたヘッダを追加して署名に関与させ、自らのリクエストの一位性と安全性を高めることもできます。ステッチングルール：1）ヘッダ key は value と統一して小文字に変換します。また、前後のスペースを削除して key:value\n フォーマットに従い接続します。2）複数のヘッダは、ヘッダkey（小文字）の辞書に基づきソートして接続します。この例では、次のようになります。`content-type:application/x-www-form-urlencoded\nhost:cvm.tencentcloudapi.com\n`
- SignedHeaders：署名に関与するヘッダ情報です。このリクエストのどのヘッダが署名に関与しているか説明し、CanonicalHeaders に含まれるヘッダの内容と1つずつ対応します。content-type と host は選択必須のヘッダです。接続ルール：1）ヘッダ key は小文字に統一します。2）複数のヘッダ key（小文字）は辞書に基づきソートして接続し、セミコロン（;）で隔てます。この例では次の通りです。`content-type;host`
- HashedRequestPayload：ボディをリクエストするハッシュ値です。計算方法は Lowercase(HexEncode(Hash.SHA256(RequestPayload)))とし、HTTP リクエストのボディ payload 全体に対して SHA256 ハッシュを行った後、16進数コーディングを実行し、最後にコード文字列をアルファベット小文字に変換します。注意：GET リクエストに対して、RequestPayload は空の文字列に固定されます。POST リクエストに対して、RequestPayload は HTTP リクエストのボディ payload です。

以上のルールに従い、サンプル内で取得した正規リクエスト文字列は次のようになります（分かりやすく表示するために、\n の改行コードは別途新たな行にすることで代替しています）。
```
GET
/
Limit=10&Offset=0
content-type:application/x-www-form-urlencoded
host:cvm.api.tencentyun.com

content-type;host
e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
```

### 2. 署名待ち文字列の接続

以下のフォーマットに従い、署名待ち文字列を接続します。

```
StringToSign =
    Algorithm + \n +
    RequestTimestamp + \n +
    CredentialScope + \n +
    HashedCanonicalRequest
```

- Algorithm：署名アルゴリズム。現在 TC3-HMAC-SHA256 に固定です。
- RequestTimestamp：リクエストタイムスタンプ。リクエストヘッダの X-TC-Timestamp の値です。上記サンプルのリクエストは 1539084154です。
- CredentialScope：証明書の範囲。フォーマットは Date/service/tc3_request とし、日時、リクエストするサービスと終端文字列（tc3_request）を含みます。**Date は UTC 標準時間の日時とし、値は共通パラメータ X-TC-Timestamp と換算した UTC 標準時間の日時と一致する必要があります**。service は製品名とし、cvm のように呼び出す製品のドメインと一致する必要があります。上記サンプルのリクエストのように、値は 2018-10-09/cvm/tc3_request です。
- HashedCanonicalRequest：前述のステップでステッチングして得られた 正規リクエスト文字列のハッシュ値。計算方法は Lowercase(HexEncode(Hash.SHA256(CanonicalRequest)))とします。

注意：

> 1. Date は必ずタイムスタンプ X-TC-Timestamp から計算して取得し、タイムゾーンは UTC+0とします。UTC+8など、システムのローカルタイムゾーンを追加する場合、昼と夜は呼び出しに成功しても、未明の時間の呼び出しは必ず失敗します。タイムスタンプが 1551113065、UTC+8の時間が 2019-02-26 00:44:25 であると仮定した場合でも、計算による Date は UTC+0 の日付を取って 2019-02-25 となり、2019-02-26 とはなりません。
> 2. Timestamp は必ず現在のシステム時間です。また、システム時間と標準時間の同期を行う必要があります。その差が5分を超えた場合、必ず失敗します。長時間にわたり、標準時間と同期しなかった場合、一定時間実行した後にリクエストが失敗する可能性があります（署名の戻りの期限切れエラー）。

以上のルールに従い、サンプル内で取得した署名待ち文字列は次のようになります（分かりやすく表示するために、\n の改行コードは別途新たな行にすることで代替しています）。

```
TC3-HMAC-SHA256
1539084154
2018-10-09/cvm/tc3_request
91c9c192c14460df6c1ffc69e34e6c5e90708de2a6d282cccf957dbf1aa7f3a7
```

### 3. 署名の計算
1）派生の署名キーを計算します。疑似コードは次の通りです

```
SecretKey = "Gu5t9xGARNpq86cd98joQYCN3EXAMPLE"
SecretDate = HMAC_SHA256("TC3" + SecretKey, Date)
SecretService = HMAC_SHA256(SecretDate, Service)
SecretSigning = HMAC_SHA256(SecretService, "tc3_request")
```

- SecretKey：オリジナルの SecretKey。
- Date：Credential の Date フィールド情報。上記サンプルのように、2018-10-09とします。
- Service：Credential の Service フィールド情報。上記サンプルのように cvm とします。

2）署名の計算の疑似コードは以下の通りです

```
Signature = HexEncode(HMAC_SHA256(SecretSigning, StringToSign))
```

- SecretSigning：以上の計算で得られた派生署名キー。
- StringToSign：ステップ2の計算で得られた署名待ち文字列。

### 4. 接続 Authorization

以下のフォーマットに従い、Authorization をステッチングします。

```
Authorization =
    Algorithm + ' ' +
    'Credential=' + SecretId + '/' + CredentialScope + ', ' +
    'SignedHeaders=' + SignedHeaders + ', '
    'Signature=' + Signature
```

- Algorithm：署名方法は、TC3-HMAC-SHA256 に固定です。
- SecretId：キーペア内の SecretId。
- CredentialScope：上記の通り、証明書の範囲。
- SignedHeaders：上記の通り、署名に関するヘッダ情報。
- Signature：署名の値。

上記のルールに従い、サンプル内で得られた値は次の通りです。

```
TC3-HMAC-SHA256 Credential=AKIDEXAMPLE/Date/service/tc3_request, SignedHeaders=content-type;host, Signature=5da7a33f6993f0614b047e5df4582db9e9bf4672ba50567dba16c6ccf174c474
```

最終的に完成した呼び出し情報は以下の通りです。

```
https://cvm.tencentcloudapi.com/?Limit=10&Offset=0

Authorization: TC3-HMAC-SHA256 Credential=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE/2018-10-09/cvm/tc3_request, SignedHeaders=content-type;host, Signature=5da7a33f6993f0614b047e5df4582db9e9bf4672ba50567dba16c6ccf174c474
Content-Type: application/x-www-form-urlencoded
Host: cvm.tencentcloudapi.com
X-TC-Action: DescribeInstances
X-TC-Version: 2017-03-12
X-TC-Timestamp: 1539084154
X-TC-Region: ap-guangzhou
```

### 5. 署名のデモンストレーション

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
    private final static String SECRET_ID = "AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE";
    private final static String SECRET_KEY = "Gu5t9xGARNpq86cd98joQYCN3EXAMPLE";
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
        // タイムゾーンに注意しないと、エラーが発生しやすくなります
        sdf.setTimeZone(TimeZone.getTimeZone("UTC"));
        String date = sdf.format(new Date(Long.valueOf(timestamp + "000")));

        // ************* ステップ 1：正規リクエスト文字列のステッチング *************
        String httpRequestMethod = "GET";
        String canonicalUri = "/";
        String canonicalQueryString = "Limit=10&Offset=0";
        String canonicalHeaders = "content-type:application/x-www-form-urlencoded\n" + "host:" + host + "\n";
        String signedHeaders = "content-type;host";
        String hashedRequestPayload = DigestUtils.sha256Hex("");
        String canonicalRequest = httpRequestMethod + "\n" + canonicalUri + "\n" + canonicalQueryString + "\n"
                + canonicalHeaders + "\n" + signedHeaders + "\n" + hashedRequestPayload;
        System.out.println(canonicalRequest);

        // ************* ステップ 2：署名待ち文字列のステッチング*************
        String credentialScope = date + "/" + service + "/" + "tc3_request";
        String hashedCanonicalRequest = DigestUtils.sha256Hex(canonicalRequest.getBytes(CHARSET));
        String stringToSign = algorithm + "\n" + timestamp + "\n" + credentialScope + "\n" + hashedCanonicalRequest;
        System.out.println(stringToSign);

        // ************* ステップ 3：署名の計算 *************
        byte[] secretDate = sign256(("TC3" + SECRET_KEY).getBytes(CHARSET), date);
        byte[] secretService = sign256(secretDate, service);
        byte[] secretSigning = sign256(secretService, "tc3_request");
        String signature = DatatypeConverter.printHexBinary(sign256(secretSigning, stringToSign)).toLowerCase();
        System.out.println(signature);

        // ************* ステップ 4：Authorization のステッチング *************
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

# キーパラメータ
secret_id = "AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE"
secret_key = "Gu5t9xGARNpq86cd98joQYCN3EXAMPLE"

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

# ************* ステップ 1：正規リクエスト文字列のステッチング *************
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

# *************ステップ 2：署名待ち文字列のステッチング *************
credential_scope = date + "/" + service + "/" + "tc3_request"
hashed_canonical_request = hashlib.sha256(canonical_request.encode("utf-8")).hexdigest()
string_to_sign = (algorithm + "\n" +
                  str(timestamp) + "\n" +
                  credential_scope + "\n" +
                  hashed_canonical_request)
print(string_to_sign)


# ************* ステップ 3：署名の計算 *************
# 署名適用関数の計算
def sign(key, msg):
    return hmac.new(key, msg.encode("utf-8"), hashlib.sha256).digest()
secret_date = sign(("TC3" + secret_key).encode("utf-8"), date)
secret_service = sign(secret_date, service)
secret_signing = sign(secret_service, "tc3_request")
signature = hmac.new(secret_signing, string_to_sign.encode("utf-8"), hashlib.sha256).hexdigest()
print(signature)

# ************* ステップ 4：Authorization のステッチング *************
authorization = (algorithm + " " +
                 "Credential=" + secret_id + "/" + credential_scope + ", " +
                 "SignedHeaders=" + signed_headers + ", " +
                 "Signature=" + signature)
print(authorization)

# 共通パラメータをリクエストヘッダに追加
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

実際の状況により、以下のような署名失敗のエラーコードがあります。状況に応じて対応してください。

| エラーコード | エラーの説明|
|----------|---------|
| AuthFailure.SignatureExpire | 署名が期限切れです |
| AuthFailure.SecretIdNotFound | キーが存在しません |
| AuthFailure.SignatureFailure | 署名エラー |
| AuthFailure.TokenFailure | token エラー |
| AuthFailure.InvalidSecretId | 不正なパスワード（クラウド API キーのタイプではない） |

