Tencent Cloud APIは、各アクセスリクエストを認証します。つまり、各リクエストは、リクエスト者の身元を確認するために共通リクエストパラメータに署名情報（Signature）を含める必要があります。
署名情報は、SecretIdおよびSecretKeyを含むセキュリティ認証情報によって生成されます；ユーザーがまだセキュリティ認証情報を持っていない場合、[クラウドAPI暗号鍵ページ](https://console.cloud.tencent.com/capi)で申請してください。申請しないと、クラウドAPIを呼び出すことができません。

## 1. セキュリティ認証情報の申請
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

## 2. 署名文字列の生成

セキュリティ認証SecretIdとSecretKeyがあれば、署名文字列を生成できます。以下は署名文字列を生成する詳細なプロセスです。

例えば、ユーザーのSecretIdとSecretKeyが次のようになるとします。

* SecretId: AKID**********************0123456789EXAMPLE
* SecretKey: sk0123456789********************EXAMPLE

**注意：これは一例に過ぎません。ユーザーの実際申請したSecretIdとSecretKeyによって操作を続けてください！**

CVMのインスタンスリスト表示（DescribeInstances）リクエストを例として、ユーザーがこのAPIを呼び出すと、そのリクエストパラメータは次のようになります：

| パラメータ名称 | 日本語 | パラメータ値|
|---------|---------|---------|
| Action | メソッド名| DescribeInstances |
| SecretId | 暗号鍵ID | AKID**********************0123456789EXAMPLE |
| Timestamp | 現在のタイムスタンプ | 1465185768 |
| Nonce | ランダムな正の整数 | 11886 |
| Region | インスタンスの所属地域 | ap-guangzhou |
| InstanceIds.0 | 照合待ちのインスタンスID | ins-09dx96dg |
| Offset | オフセット | 0 |
| Limit | 最大許容出力 | 20 |
| Version | APIバージョン番号 | 2017-03-12 |


### 2.1. パラメータの並び替え

まず、すべてのリクエストパラメータを、パラメータ名の辞書順（ASCIIコード）で昇順に並び替えます。注意：1）パラメータ名のみで並び替え、パラメータ値はパラメータ名と一致すれば大丈夫で、並び替えません；2）InstanceIds.2はInstanceIds.12の後に置くように、アルファベット順ではなく、値順でもなく、ASCIIコードで並び替えます。ユーザーは、phpのksort関数など、プログラミング言語の関連するソート関数を使用してこの機能を実行できます。上記のパラメータ例の並び替え結果は次のとおりです：

```
{
    'Action' : 'DescribeInstances',
    'InstanceIds.0' : 'ins-09dx96dg',
    'Limit' : 20,
    'Nonce' : 11886,
    'Offset' : 0,
    'Region' : 'ap-guangzhou',
    'SecretId' : 'AKID**********************0123456789EXAMPLE',
    'Timestamp' : 1465185768,
    'Version': '2017-03-12',
}
```
同じ結果を取得できれば、他のプログラム言語で上記の例のパラメータを並べ替えることも可能です。

### 2.2. リクエスト文字列のつなぎ合わせ

このステップはリクエスト文字列を生成します。
前のステップで並べ替えられたリクエストパラメータを「パラメータ名称」=「パラメータ値」の形式にフォーマットします。例えば、Actionパラメータに対して、そのパラメータ名が「Action」で、パラメータ値が「DescribeInstances」なので、フォーマットされた後に、Action=DescribeInstancesになります。
**注意：「パラメータ値」は元の値であり、URLエンコード値ではありません。**

それから、フォーマットされた各パラメータを「＆」でつなぎ合わせて、最後に生成されたリクエスト文字列は次のとおりです：

```
Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKID**********************0123456789EXAMPLE&Timestamp=1465185768&Version=2017-03-12
```

### 2.3. 署名原文文字列のつなぎ合わせ
このステップで署名原文文字列を生成します。
署名原文文字列は、次のパラメータで構成されています：

1. リクエスト方法：POSTおよびGETの方法をサポートします。ここでGETリクエストを使用します。メソッドはすべて大文字です。
2. リクエストCVM：インスタンスリスト表示（DescribeInstances）のリクエストドメイン名はcvm.tencentcloudapi.comです。実際のリクエストドメイン名は、APIが属するモジュールによって異なりますので、詳細は各APIの説明を参照してください。
3. リクエストパス：現在のバージョンのクラウドAPIのリクエストパスは固定的に/です。
4. リクエスト文字列：つまり前のステップで生成されたリクエスト文字列です。

署名原文列のつなぎ合わせ規則：リクエスト方法 + リクエストCVM +リクエストパス + ? + リクエスト文字列

例のつなぎ合わせ結果：

```
GETcvm.tencentcloudapi.com/?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKID**********************0123456789EXAMPLE&Timestamp=1465185768&Version=2017-03-12
```

### 2.4. 署名文字列の生成
このステップで署名文字列を生成します。
まず、HMAC-SHA1アルゴリズムを使用して前の手順で取得した**署名原文文字列**に署名します。次に、Base64を使用して生成された署名文字列をコーディングして最終署名文字列を取得します。

具体的なコードは次のとおりです。PHP言語を例とします：

```
$secretKey = 'sk0123456789********************EXAMPLE';
$srcStr = 'GETcvm.tencentcloudapi.com/?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKID**********************0123456789EXAMPLE&Timestamp=1465185768&Version=2017-03-12';
$signStr = base64_encode(hash_hmac('sha1', $srcStr, $secretKey, true));
echo $signStr;
```

最後に取得された署名文字列は：

```
EliP9YW3pW28FpsEdkXt/+WcGeI=
```

他のプログラミング言語で開発する場合、上記の例の原文を使用して署名検証を実行でき、取得された署名文字列は例と一致すれば成功します。

## 3. 署名文字列のコーディング

生成された署名文字列はリクエストパラメータとして直接使用することはできません。URLコーディングする必要があります。

前のステップで生成された署名文字列はEliP9YW3pW28FpsEdkXt/+WcGeI=であれば、最終取得された署名文字列リクエストパラメータ（Signature）は：EliP9YW3pW28FpsEdkXt%2f%2bWcGeI%3dです。これは最終的なリクエストURLを生成するために使用されます。

**注意：ユーザーのリクエスト方法はGETであれば、またはリクエスト方法はPOSTで、同時にContent-Typeはapplication/x-www-form-urlencodedであれば、リクエストを送信するときに、すべてのリクエストパラメータの値は、URLエンコードされる必要があります。パラメータ鍵と=記号はエンコードする必要がありません。非ASCII文字はURLエンコード前にUTF-8でエンコードされる必要があります。**

**注意：一部のプログラミング言語のHTTPライブラリは自動的にすべてのパラメータをURLエンコードします。その場合、署名文字列をURLエンコードする必要はありません。URLエンコードを繰り返すと、署名が失敗する可能性があります。**

**注意：他のパラメータ値もエンコードする必要があります。エンコードは[RFC 3986](http://tools.ietf.org/html/rfc3986)を使用します。%XYを使って漢字などの特殊文字に対してパーセントエンコーディングします。その中の「X」と「Y」は16進文字（0-9と大文字アルファベットA-F）で、小文字を使用すればエラーが発生する場合があります。**

## 4. 署名失敗
実際の状況によって、以下の署名失敗のエラーコードがあります。適切に処理してください

| エラーコード | エラー説明|
|----------|---------|
| AuthFailure.SignatureExpire | 署名期限切れ |
| AuthFailure.SecretIdNotFound | 暗号鍵が存在しません |
| AuthFailure.SignatureFailure | 署名エラー |
| AuthFailure.TokenFailure | トークンエラー |
| AuthFailure.InvalidSecretId | 暗号鍵が不正です（クラウドAPI暗号鍵タイプではありません）） |

## 5. 署名のデモ

実際にAPI 3.0を呼び出すときは、対応するTencent Cloud SDK 3.0を使用することをお勧めします。SDKは署名プロセスをカプセル化しており、開発中は製品が提供する特定のAPIのみに集中できます。詳細情報については、[SDKセンター](https://cloud.tencent.com/document/sdk)を参照してください。現在サポートするプログラミング言語は：

* [Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [JavaScript](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [.NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

署名プロセスをより明確に説明するために、実際のプログラミング言語を例として上述の署名プロセスを具体的に実施します。リクエストのドメイン名、呼び出すAPI、およびパラメータの値は、上記の署名プロセスのとおりです。コードは署名プロセスを説明するためのものであり、汎用性がありません。実際の開発ではできるだけSDKを使用してください。

最終に出力されたURLは以下である可能性があります：`https://cvm.tencentcloudapi.com/?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKID**********************0123456789EXAMPLE&Signature=EliP9YW3pW28FpsEdkXt%2F%2BWcGeI%3D&Timestamp=1465185768&Version=2017-03-12`

注意：例の暗号鍵は仮想のものであるため、タイムスタンプはシステムの現在時刻ではないので、このURLをブラウザで開くか、curlなどのコマンドで呼び出されると、認証エラー（署名期限切れ）が返されます。通常返されることができるURLを得るために、SecretIdとSecretKeyを本当の暗号鍵に変更して、システムの現在のタイムスタンプをTimestampとして使う必要があります。

注意：以下の例では、異なるプログラミング言語、そして同じ言語でも、毎回実行されるURLが異なる場合があります。正確さには影響しないので、パラメータの順序が異なっていても構いません。すべてのパラメータがそろっていて、署名が正しく計算されては大丈夫です。

注意：次のコードはAPI 3.0専用であり、他の署名プロセスに直接使用することはできません。古いAPIでも、細かい違いが原因で署名計算エラーが発生する場合があるので、対応する実際のドキュメントを参照してください。

### Java

```java
import java.io.UnsupportedEncodingException;
import java.net.URLEncoder;
import java.util.Random;
import java.util.TreeMap;
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import javax.xml.bind.DatatypeConverter;

public class TencentCloudAPIDemo {
    private final static String CHARSET = "UTF-8";

    public static String sign(String s, String key, String method) throws Exception {
        Mac mac = Mac.getInstance(method);
        SecretKeySpec secretKeySpec = new SecretKeySpec(key.getBytes(CHARSET), mac.getAlgorithm());
        mac.init(secretKeySpec);
        byte[] hash = mac.doFinal(s.getBytes(CHARSET));
        return DatatypeConverter.printBase64Binary(hash);
    }

    public static String getStringToSign(TreeMap<String, Object> params) {
        StringBuilder s2s = new StringBuilder("GETcvm.tencentcloudapi.com/?");
        // 署名するときは、パラメータを辞書順で並べ替える必要がありますが、ここでは順序を保証するためにTreeMapを使用します
        for (String k : params.keySet()) {
            s2s.append(k).append("=").append(params.get(k).toString()).append("&");
        }
        return s2s.toString().substring(0, s2s.length() - 1);
    }

    public static String getUrl(TreeMap<String, Object> params) throws UnsupportedEncodingException {
        StringBuilder url = new StringBuilder("https://cvm.tencentcloudapi.com/?");
        // 実際に要求されたURLのパラメータの順序に関する要件はありません
        for (String k : params.keySet()) {
            // リクエスト列に対してURLエンコードを行う必要があります。keyはすべて英字なので、ここではvalueだけに対してURLエンコードを行います
            url.append(k).append("=").append(URLEncoder.encode(params.get(k).toString(), CHARSET)).append("&");
        }
        return url.toString().substring(0, url.length() - 1);
    }

    public static void main(String[] args) throws Exception {
        TreeMap<String, Object> params = new TreeMap<String, Object>(); // TreeMapは自動的に並び替えます
        // 実際に呼び出すときは乱数を使うべきです。例えば：params.put("Nonce", new Random().nextInt(java.lang.Integer.MAX_VALUE));
        params.put("Nonce", 11886); // 共通パラメータ
        // 実際に呼び出すときはシステム現在時間を使うべきです。例えば：   params.put("Timestamp", System.currentTimeMillis() / 1000);
        params.put("Timestamp", 1465185768); // 共通パラメータ
        params.put("SecretId", "AKID**********************0123456789EXAMPLE"); // 共通パラメータ
        params.put("Action", "DescribeInstances"); // 共通パラメータ
        params.put("Version", "2017-03-12"); // 共通パラメータ
        params.put("Region", "ap-guangzhou"); // 共通パラメータ
        params.put("Limit", 20); // 業務パラメータ
        params.put("Offset", 0); // 業務パラメータ
        params.put("InstanceIds.0", "ins-09dx96dg"); // 業務パラメータ
        params.put("Signature", sign(getStringToSign(params), "sk0123456789********************EXAMPLE", "HmacSHA1")); // 共通パラメータ
        System.out.println(getUrl(params));
    }
}
```

### Python

注意：Python 2環境で実行する場合は、まずrequests依存パッケージ：`pip install requests`をインストールする必要があります。

```python
# -*- coding: utf8 -*-
import base64
import hashlib
import hmac
import time

import requests

secret_id = "AKID**********************0123456789EXAMPLE"
secret_key = "sk0123456789********************EXAMPLE"

def get_string_to_sign(method, endpoint, params):
    s = method + endpoint + "/?"
    query_str = "&".join("%s=%s" % (k, params[k]) for k in sorted(params))
    return s + query_str

def sign_str(key, s, method):
    hmac_str = hmac.new(key.encode("utf8"), s.encode("utf8"), method).digest()
    return base64.b64encode(hmac_str)

if __name__ == '__main__':
    endpoint = "cvm.tencentcloudapi.com"
    data = {
        'Action' : 'DescribeInstances',
        'InstanceIds.0' : 'ins-09dx96dg',
        'Limit' : 20,
        'Nonce' : 11886,
        'Offset' : 0,
        'Region' : 'ap-guangzhou',
        'SecretId' : secret_id,
        'Timestamp' : 1465185768, # int(time.time())
        'Version': '2017-03-12'
    }
    s = get_string_to_sign("GET", endpoint, data)
    data["Signature"] = sign_str(secret_key, s, hashlib.sha1)
    print(data["Signature"])
    # ここでは実際に呼び出します。正常に呼び出した後に課金される可能性があります
    # resp = requests.get("https://" + endpoint, params=data)
    # print(resp.url)
```

