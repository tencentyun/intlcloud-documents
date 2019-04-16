### 準備作業

1.SecretIdとSecretKeyを取得します。
    コンソールの[Cloud APIコンソール](https://console.cloud.tencent.com/capi)ページで取得します。
2.開発言語を決めます。
     サポートされている言語には、Java、PHP、C Sharp、C++、Node.jsとPythonが含まれますが、これらに限定されません。開発言語に応じてHMAC-SHA1機能を指定する必要があります。

## 署名コンテンツ
次の例に示すように、APIを介してCLSに開始されたHTTP署名リクエストについては、標準のHTTP Authorizationヘッダーを使用して渡されます。

```
GET /logset?logset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx HTTP/1.1
Host: ap-shanghai.cls.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1510109254;1510109314&q-key-time=1510109254;1510109314&q-header-list=content-type;host&q-url-param-list=logset_name&q-signature=e8b23b818caf4e33f196f895218bdabdbd1f1423
```

リクエストのHostフィールドは  ${region}.cls.myqcloud.com  で、そのうちregionフィールドはCLS区域です。北京区域を例として、ap-beijingを入力し、完全な区域リストのフォーマットについては、 [地域リスト](https://cloud.tencent.com/document/product/614/18940)を参照してください。

```
ap-beijing - 北京
ap-shanghai - 上海
ap-guangzhou - 广州
ap-chengdu -成都
```

リクエスト内の署名コンテンツは、"＆"でリンクされたいくつかのkey = valueペアで構成されています。フォーマットは次のとおりです。

```shell
q-sign-algorithm=[Algorithm]&q-ak=[SecretId]&q-sign-time=[SignTime]&q-key-time=[KeyTime]&q-header-list=[SignedHeaderList]&q-url-param-list=[SignedParamList]&q-signature=[Signature]
```

### キー値説明

署名コンテンツ内のキー値（Key = Value）のペアは次のように説明されています。

<table>
   <tr>
      <th>キー（Key）</th>
      <th>値（Value）</th>
      <th>意味</th>
   </tr>
   <tr>
      <td nowrap="nowrap">q-sign-algorithm</td>
      <td>sha1</td>
      <td>現在署名アルゴリズムでサポートされているのはsha1だけです</td>
   </tr>
   <tr>
      <td>q-ak</td>
      <td>パラメータ[SecretId]</td>
      <td>アカウントのSecretId（必須）、上記の準備でコンソールから取得したID</td>
   </tr>
   <tr>
      <td>q-sign-time</td>
      <td>パラメータ[SignTime]</td>
      <td>署名の開始時刻と終了時刻（必須）。秒単位のUNIXタイムスタンプで、セミコロン（;）で区切ります。</td>
   </tr>
   <tr>
      <td>q-key-time</td>
      <td>パラメータ[KeyTime]</td>
      <td>その値はq-sign-timeと同じです</td>
   </tr>
   <tr>
      <td>q-header-list</td>
      <td>パラメータ[SignedHeaderList]</td>
      <td>署名を追加する必要があるHTTPリクエストヘッダーのkey（必須）。keyは小文字に変換する必要があります。複数のkeyは辞書順にソートし、セミコロン（;）で区切る必要があります。ヘッダーに署名を付けたくない場合は、空の文字列になります。</td>
   </tr>
   <tr>
      <td nowrap="nowrap">q-url-param-list</td>
      <td>パラメータ[SignedParamList]</td>
      <td>署名を追加する必要があるHTTPリクエストUri部分のパラメータ（必須）。keyは小文字に変換する必要があります。複数のkeyは辞書順にソートし、セミコロン（;）で区切る必要があります。ヘッダーに署名を付けたくない場合は、空の文字列になります。</td>
   </tr>
   <tr>
      <td>q-signature</td>
      <td>パラメータ[Signature]</td>
      <td>必須、計算された署名コンテンツ、小文字</td>
   </tr>
</table>


>!q-sign-timeとq-key-timeに関しては、終了時間は開始時間より長くなり、そうでなければ署名は即座に期限切れになります。

### 計算方法

Signature計算手順

1.HTTPリクエストに関する情報は、文字列HttpRequestInfoとして特定のフォーマットに従ってスプライスされます。
2.sha1アルゴリズムを使用してHttpRequestInfoのハッシュ値を計算してから、そのハッシュ値を特定のフォーマットに従って他の指定されたパラメータと組み合わせて、元の文字列StringToSignを生成します。
3.SignKeyを取得するためにSecretKeyを使用してq-key-timeを暗号化します。
4.SignKeyを使用してStringToSignを暗号化し、Signature署名を生成します。

>!特殊文字のurlencode結果には、`％2f`ではなく`％2F`としてエンコードされた`/`のような大文字を使用するべきです。

#### HttpRequestInfoのつなぎ合わせ

HttpRequestInfoは、HTTPリクエスト内のMethod、Uri、Headers、およびParametersから構成されます。以下のように示す。
```
HttpRequestInfo = Method + "\n"
                + Uri + "\n"
                + FormatedParameters + "\n"
                + FormatedHeaders + "\n"
```

上記の`\n`は改行エスケープ文字を表し、`+`は文字列連結演算を表します。その他のパラメータは次のように定義されます。

| フィールド名                | 意味                                       |
| ------------------ | ---------------------------------------- |
| Method             | HTTPリクエストが使用される方法です。たとえば`get、post`（小文字）などです       |。
| Uri                | HTTPリクエストのリソース名です。query string部分を含みません。たとえば `/logset`です |
| FormatedParameters |  HTTPリクエストのquery string部分のパラメータのシリアル化された文字列、つまりq-url-param-listで指定されたパラメータです。パラメータが指定されていない場合は、空の文字列が使用されます。keyとvalueは`=`でつながれます。異なるキー/値のペアは`＆`で結び付けられており、辞書順にソートする必要があります。keyは小文字で、valueはurlencodeされている必要があります |
| FormatedHeaders    | HTTPリクエストのヘッダー、すなわちq-header-listに指定されたHTTPヘッダーです。指定されていない場合は、空の文字列が使用されます。keyとvalueは`=`でつながれます。異なるキー/値のペアは`＆`で結び付けられており、辞書順にソートする必要があります。keyは小文字で、valueはurlencodeされている必要があります |

##### StringToSignのつなぎ合わせ

StringToSignは、次に示すように、q-sign-algorithm、q-sign-time、およびHttpRequestInfoのsha1ハッシュ値で構成されています。
```
StringToSign = q-sign-algorithm + "\n"
             + q-sign-time + "\n"
             + sha1(HttpRequestInfo) + "\n"
```

上記の`\n`は改行エスケープ文字を表し、`+`は文字列連結演算を表します。その他のパラメータは上記のように説明されます。そのうちHttpRequestInfoのsha1ハッシュは、小文字の16進数文字列です。

#### SignKeyの生成
現在、APIは1つのデジタル署名アルゴリズム、すなわちデフォルトの署名アルゴリズムhmac-sha1のみをサポートしています。その疑似コードは次のようになります。
```
SignKey = Hexdigest(HMAC-SHA1(q-key-time, SecretKey))
```

ここで、`HMAC-SHA1`は暗号化アルゴリズムで、`Hexdigest`は16進数文字列に変換する方法です。一部の言語では、暗号化アルゴリズムの出力は直接16進数文字列であるため、変換は不要です。

#### 署名の生成
現在、APIは1つのデジタル署名アルゴリズム、すなわちデフォルトの署名アルゴリズムhmac-sha1のみをサポートしています。その疑似コードは次のようになります。
```
Signature = Hexdigest(HMAC-SHA1(StringToSign, SignKey))
```

ここで、`HMAC-SHA1`は暗号化アルゴリズムで、`Hexdigest`は16進数文字列に変換する方法です。一部の言語では、暗号化アルゴリズムの出力は直接16進数文字列であるため、変換は不要です。

## 例

署名の説明については、次のSecretIdとSecretKeyを使用します。

```
SecretId = "AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX"
SecretKey = "LUSE4nPK1d4tX5SHyXv6tZXXXXXXXXXX"

StartTime = 1510109254
EndTime = 1510109314
```

**例1**：
Logset情報を取得するためのHTTPリクエストは次のようになります。
```
GET /logset?logset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx HTTP/1.1
Host: ap-shanghai.cls.myqcloud.com
```

上記のリクエストの場合、リクエストヘッダーHostに署名が追加されていると、生成される文字列HttpRequestInfoは次のようになります。

```
get\n/logset\nlogset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\nhost=ap-shanghai.cls.myqcloud.com\n
```

HttpRequestInfoを使用して生成された元の文字列StringToSignは次のようになります。

```
sha1\n1510109254;1510109314\n35601c3365a361b62b980fda754318c29862d39c\n
```

SecretKeyを使用してq-key-timeを暗号化し、取得されたSignKeyは次のようになります。

```
a4501294d3a835f8dab6caf5c19837dd19eef357
```

SignKeyを使用してStringToSignを暗号化し、生成されたSignatureは次のようになります。

```
2c53900d3fe8d2e875db8a6af5fe7303ee1567a8
```

複合署名承認Authorizationは次のようになります。

```
q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1510109254;1510109314&q-key-time=1510109254;1510109314&q-header-list=host&q-url-param-list=logset_id&q-signature=2c53900d3fe8d2e875db8a6af5fe7303ee1567a8
```

最終的なリクエストコンテンツは次のようになります。

```
GET /logset?logset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx HTTP/1.1
Host: ap-shanghai.cls.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1510109254;1510109314&q-key-time=1510109254;1510109314&q-header-list=host&q-url-param-list=logset_id&q-signature=2c53900d3fe8d2e875db8a6af5fe7303ee1567a8
```

**例2**：
logset情報を変更するためのHTTPリクエストは次のようになります。
```
PUT /logset HTTP/1.1
Host: ap-shanghai.cls.myqcloud.com
Content-Type: application/json
Content-Length: 50

{"logset_id":"xxxx-xx-xx-xx-xxxxxxxx","period":30}
```

bodyコンテンツに対して計算されたmd5値は以下のとおりです。
```
f9c7fc33c7eab68dfa8a52508d1f4659
```

上記のリクエストの場合、リクエストヘッダーHostに署名が追加されていると、生成される文字列HttpRequestInfoは次のようになります。
```
put\n/logset\n\ncontent-md5=f9c7fc33c7eab68dfa8a52508d1f4659&content-type=application%2Fjson&host=ap-shanghai.cls.myqcloud.com\n
```

HttpRequestInfoを使用して生成された元の文字列StringToSignは次のようになります。
```
sha1\n1510109254;1510109314\n0ca0242c3d50441fda6aa234d31bea7a7a12a1ea\n
```

SecretKeyを使用してq-key-timeを暗号化し、取得されたSignKeyは次のようになります。
```
a4501294d3a835f8dab6caf5c19837dd19eef357
```

SignKeyを使用してStringToSignを暗号化し、生成されたSignatureは次のようになります。
```
85a55e61de42483ba03bffd07a6c01b8d651af51
```

複合署名承認Authorizationは次のようになります。
```
q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1510109254;1510109314&q-key-time=1510109254;1510109314&q-header-list=content-md5;content-type;host&q-url-param-list=&q-signature=85a55e61de42483ba03bffd07a6c01b8d651af51
```

最終的なリクエストコンテンツは次のようになります。
```
PUT /logset HTTP/1.1
Host: ap-shanghai.cls.myqcloud.com
Content-Type: application/json
Content-MD5: f9c7fc33c7eab68dfa8a52508d1f4659
Content-Length: 50
Authorization: q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1510109254;1510109314&q-key-time=1510109254;1510109314&q-header-list=content-md5;content-type;host&q-url-param-list=&q-signature=85a55e61de42483ba03bffd07a6c01b8d651af51

{"logset_id":"xxxx-xx-xx-xx-xxxxxxxx","period":30}
```


