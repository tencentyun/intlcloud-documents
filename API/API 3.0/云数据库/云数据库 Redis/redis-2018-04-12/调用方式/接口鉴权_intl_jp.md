Tencent Cloud API は、各アクセスリクエストに対して身分認証を行います。つまり、各リクエストはいずれも共通のリクエストパラメータにおいて署名情報（Signature）を含むものとし、それによって請求者の身分を検証します。
署名情報はセキュリティ証明書によって生成され、セキュリティ証明書には SecretId と SecretKey が含まれます。ユーザーがまだセキュリティ証明書を所有していない場合、[クラウド API キー画面](https://console.cloud.tencent.com/capi)から申請してください。申請しない場合、クラウド API インターフェースを呼び出すことはできません。

## 1. セキュリティ証明書の申請
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

## 2. 署名文字列の生成

セキュリティ証明書の SecretId と SecretKey を入手すると、署名文字列を生成することができます。以下は署名文字列を生成する詳細なプロセスです。

ユーザーの SecretId と SecretKey はそれぞれ次の通りです。

* SecretId: AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE
* SecretKey: Gu5t9xGARNpq86cd98joQYCN3EXAMPLE

**注意：これはサンプルです。ユーザーが実際に申請した SecretId と SecretKey に基づいて後続の操作をしてください！**

CVM でインスタンスリスト(DescribeInstances)のリクエストを確認する例では、ユーザーがこのインターフェースを呼び出す時、そのリクエストパラメータは以下のようになります。

| パラメータ名 | 中国語 | パラメータ値|
|---------|---------|---------|
| Action | 方法名| DescribeInstances |
| SecretId | キーId | AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE |
| Timestamp | 現在のタイムスタンプ | 1465185768 |
| Nonce | ランダムな正の整数 | 11886 |
| Region | インスタンスのリージョン | ap-guangzhou |
| InstanceIds.0 | クエリ待ちのインスタンスID | ins-09dx96dg |
| Offset | オフセット量 | 0 |
| Limit | 最大許容出力 | 20 |
| Version | インターフェースバージョン番号 | 2017-03-12 |


### 2.1. パラメータのソート

まず、全てのリクエストパラメータをパラメータ名の辞書（ ASCII コード）に基づいて昇順にソートします。注意：1）パラメータ名をもとにソートして、パラメータ値が対応しているだけでよく、大きさの比は関与しません。2）例えば、InstanceIds.2 を InstanceIds.12 の後ろに並べるというように、アルファベットでも数値でもなく、ASCIIコードに基づいて大きさを比較します。php の ksort 関数のようなプログラミング言語における関連ソート関数を利用することで、この機能を実現できます。上記のサンプルパラメータのソート結果は次の通りです。

```
{
    'Action' : 'DescribeInstances',
    'InstanceIds.0' : 'ins-09dx96dg',
    'Limit' : 20,
    'Nonce' : 11886,
    'Offset' : 0,
    'Region' : 'ap-guangzhou',
    'SecretId' : 'AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE',
    'Timestamp' : 1465185768,
    'Version': '2017-03-12',
}
```
その他のプログラミング言語を使用して開発する場合は、上記のサンプルにおけるパラメータをソートすることができ、得られた結果が一致すれば問題ありません。

### 2.2. リクエスト文字列のステッチング

このステップではリクエスト文字列を生成します。
前ステップでソートしたリクエストパラメータは、“パラメータ名”=“パラメータ値”の形式にフォーマット化されます。例えば、Action パラメータの場合、そのパラメータ名は "Action" 、パラメータ値は"DescribeInstances"です。それにより、フォーマット後は Action=DescribeInstances となります。
**注意：“パラメータ値”は元の値であり、url コーディング後の値ではありません。**

その後、フォーマット化した各パラメータは"&"で連結し、最終的に生成したリクエスト文字列は、次のようになります。

```
Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE&Timestamp=1465185768&Version=2017-03-12
```

### 2.3. 署名の元の文字列をステッチングする
このステップでは署名の元の文字列を生成します。
署名の元の文字列は、以下のいくつかのパラメータから構成されます。

1. リクエスト方法:  POST および GET 方式をサポートしています。ここでは GET を使用してリクエストします。この方法は全て大文字であることに注意してください。
2. マスターのリクエスト:インスタンスリスト(DescribeInstances)のリクエストドメインが、cvm.tencentcloudapi.com であることを確認します。実際のリクエストドメインはインターフェースが属するモジュールにより異なります。詳細については各インターフェースの説明をご覧ください。
3. リクエストパス: 現在のバージョンのクラウド API のリクエストパスは、/ に固定されています。
4. リクエスト文字列: 前ステップで生成したリクエスト文字列です。

署名の元の文字列のステッチングルールは次の通りです。リクエスト方法 + リクエストマスター + リクエストパス + ? + リクエスト文字列

サンプルのステッチング結果は次の通りです。

```
GETcvm.tencentcloudapi.com/?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE&Timestamp=1465185768&Version=2017-03-12
```

### 2.4. 署名文字列の生成
このステップでは署名文字列を生成します。
まず、HMAC-SHA1 アルゴリズムを使用して前ステップで取得した**署名の元の文字列**に署名をします。その後、生成した署名文字列を Base64 でエンコードし、最終的な署名文字列が得られます。

具体的なコードは以下のようになります。PHP 言語を例に説明します。

```
$secretKey = 'Gu5t9xGARNpq86cd98joQYCN3EXAMPLE';
$srcStr = 'GETcvm.tencentcloudapi.com/?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE&Timestamp=1465185768&Version=2017-03-12';
$signStr = base64_encode(hash_hmac('sha1', $srcStr, $secretKey, true));
echo $signStr;
```

最終的に得られた署名の文字列は次の通りです。

```
EliP9YW3pW28FpsEdkXt/+WcGeI=
```

その他のプログラミング言語を使用して開発する場合は、上記の例のうち元の文を使用して署名の認証を行い、得られた署名の文字列が例と一致すれば問題ありません。

## 3. 署名文字列のエンコード

生成した署名文字列は、そのままリクエストパラメータにすることはできません。URL エンコードを実行する必要があります。

前ステップで生成した署名文字列が EliP9YW3pW28FpsEdkXt/+WcGeI= であれば、最終的に得られた署名文字列のリクエストパラメータ（Signature）は、EliP9YW3pW28FpsEdkXt%2f%2bWcGeI%3d であり、最終的なリクエスト URL を生成するために使用されます。

**注意：ユーザーのリクエスト方法が GET である場合、またはリクエスト方法が POST であると同時に Content-Type が application/x-www-form-urlencoded である場合は、リクエスト送信時にはすべてのリクエストパラメータの値に URL エンコードを実行する必要があります。パラメータキーと=符号はエンコードを必要としません。ASCII文字以外の場合、URL エンコードの前に、まず UTF-8 でエンコードする必要があります。**

**注意：一部のプログラミング言語の http ライブラリは、自動ですべてのパラメータを urlencode します。この場合、署名文字列に URL エンコードを行う必要はありません。そうせずに2回 URL エンコードを行うと署名に失敗することがあります。**

**注意：その他のパラメータ値もエンコードを行う必要があります。エンコードには [RFC 3986](http://tools.ietf.org/html/rfc3986)を採用しています。%XY を使用して、漢字のような特殊な文字列にパーセントエンコーディングを行います。そのうち、“X”と“Y”は16進数文字（0～9 およびアルファベット大文字 A～F）とします。小文字を使うとエラーが発生します。**

## 4. 署名失敗
実際の状況により、以下のような署名失敗のエラーコードがあります。状況に応じて対応してください。

| エラーコード | エラーの説明|
|----------|---------|
| AuthFailure.SignatureExpire | 署名が期限切れです |
| AuthFailure.SecretIdNotFound | キーが存在しません |
| AuthFailure.SignatureFailure | 署名エラー |
| AuthFailure.TokenFailure | token エラー |
| AuthFailure.InvalidSecretId | 不正なパスワード（クラウド API キーのタイプではない） |

## 5. 署名のデモンストレーション

実際に API 3.0 を呼び出す場合、付属の Tencent Cloud SDK 3.0のご使用をお勧めします。SDK は署名のプロセスをカプセル化しているため、開発時には、製品が提供する具体的なインターフェースに注目するだけです。詳細については、 [SDK センター](https://cloud.tencent.com/document/sdk)を参照してださい。現在サポートするプログラミング言語には、次のようなものがあります。

* [Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [JavaScript](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [.NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

署名プロセスをよりはっきりと説明するために、実際のプログラミング言語を例に上記の署名プロセスを具体的に実行します。リクエストするドメイン名、呼び出すインターフェースおよびパラメータの値は、すべて上記の署名プロセスに準じます。コードは署名プロセスを説明するためのものであり、汎用性はありません。実際の開発では、可能な限り SDK を使用してください。

最終的に出力する url は、次のようになります。`https://cvm.tencentcloudapi.com/?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE&Signature=EliP9YW3pW28FpsEdkXt%2F%2BWcGeI%3D&Timestamp=1465185768&Version=2017-03-12`

注意：サンプルのキーは架空のものであるため、タイムスタンプもシステムの現在時刻ではありません。そのため、この url をブラウザで開くか、 curl などのコマンドで呼び出した場合、認証エラーである署名の期限切れが返されます。正常に返される url を取得するために、サンプル内の SecretId と SecretKey を修正して本物のキーとし、システムの現在のタイムスタンプを Timestamp にする必要があります。

注意：以下のサンプルにおいて、異なるプログラミング言語では（同じ言語であっても）毎回取得する url は異なる場合があります。パラメータの順序が異なることを意味しますが、正確性には影響しません。すべてのパラメータがあり、署名の計算が正確でさえあれば問題ありません。

注意：以下のコードは API 3.0 にのみ適用されます。たとえ旧バージョンの API であっても、そのまま他の署名プロセスに使用することはできません。細かな差異があるため、署名計算にエラーが発生することがあります。対応する実際のドキュメントに準じてください。

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
        // 署名する際、パラメータを辞書に基づいてソートすることが要求されます。ここでは TreeMap を使用して順序を確実にします
        for (String k : params.keySet()) {
            s2s.append(k).append("=").append(params.get(k).toString()).append("&");
        }
        return s2s.toString().substring(0, s2s.length() - 1);
    }

    public static String getUrl(TreeMap<String, Object> params) throws UnsupportedEncodingException {
        StringBuilder url = new StringBuilder("https://cvm.tencentcloudapi.com/?");
        // 実際にリクエストされたurlにおいてパラメータの順序には要件がありません
        for (String k : params.keySet()) {
            // リクエスト文字列に urlencode を行う必要があります。key はすべてアルファベットの大文字であるため、ここではその value に urlencode を実行するだけです
            url.append(k).append("=").append(URLEncoder.encode(params.get(k).toString(), CHARSET)).append("&");
        }
        return url.toString().substring(0, url.length() - 1);
    }

    public static void main(String[] args) throws Exception {
        TreeMap<String, Object> params = new TreeMap<String, Object>(); // TreeMapは自動でソートできます
        // 実際に呼び出す際、次のようにランダム数を使用するものとします。params.put("Nonce", new Random().nextInt(java.lang.Integer.MAX_VALUE));
        params.put("Nonce", 11886); // 共通パラメータ
        // 実際に呼び出す際、次のようにシステムの現在時間を使用するものとします。   params.put("Timestamp", System.currentTimeMillis() / 1000);
        params.put("Timestamp", 1465185768); // 共通パラメータ
        params.put("SecretId", "AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE"); // 共通パラメータ
        params.put("Action", "DescribeInstances"); // 共通パラメータ
        params.put("Version", "2017-03-12"); // 共通パラメータ
        params.put("Region", "ap-guangzhou"); // 共通パラメータ
        params.put("Limit", 20); // サービスパラメータ
        params.put("Offset", 0); // サービスパラメータ
        params.put("InstanceIds.0", "ins-09dx96dg"); // サービスパラメータ
        params.put("Signature", sign(getStringToSign(params), "Gu5t9xGARNpq86cd98joQYCN3EXAMPLE", "HmacSHA1")); // 共通パラメータ
        System.out.println(getUrl(params));
    }
}
```

### Python

注意：Python 2 環境で実行する場合、先に requests 依存関係パッケージである`pip install requests` をインストールしておく必要があります。

```python
# -*- coding: utf8 -*-
import base64
import hashlib
import hmac
import time

import requests

secret_id = "AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE"
secret_key = "Gu5t9xGARNpq86cd98joQYCN3EXAMPLE"

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
    # ここで実際に呼び出し、成功すると料金が発生します
    # resp = requests.get("https://" + endpoint, params=data)
    # print(resp.url)
```

