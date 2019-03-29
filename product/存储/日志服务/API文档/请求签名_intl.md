## Preparations

1. Obtain SecretId and SecretKey.
    They are available on the [API Key Management](https://console.cloud.tencent.com/capi) page of the console.
2. Specify the development language:
     Supported languages include but are not limited to Java, PHP, C Sharp, C++, Node.js and Python. You need to specify the HMAC-SHA1 function depending on development languages.

## Signature Content
The HTTP signature request initiated to CLS through the API is passed by using the standard HTTP Authorization header, as shown in the following example:

```
GET /logset?logset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx HTTP/1.1
Host: ap-shanghai.cls.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1510109254;1510109314&q-key-time=1510109254;1510109314&q-header-list=content-type;host&q-url-param-list=logset_name&q-signature=e8b23b818caf4e33f196f895218bdabdbd1f1423
```

The Host field in the request is ${region}.cls.myqcloud.com. Where, "region" is replaced by the region of the CLS service, for example, enter ap-beijing for the Beijing region. For the complete region list, see [Regions](https://cloud.tencent.com/document/product/614/18940).

```
ap-beijing - Beijing
ap-shanghai - Shanghai
ap-guangzhou - Guangzhou
ap-chengdu - Chengdu
```

The signature content in the request is comprised of a number of key=value pairs connected with "&". The format is as follows:

```shell
q-sign-algorithm=[Algorithm]&q-ak=[SecretId]&q-sign-time=[SignTime]&q-key-time=[KeyTime]&q-header-list=[SignedHeaderList]&q-url-param-list=[SignedParamList]&q-signature=[Signature]
```

### Key-Value description

The key-value (Key=Value) pairs in the signature content are described as follows:

<table>
   <tr>
      <th>Key</th>
      <th>Value</th>
      <th>Description</th>
   </tr>
   <tr>
      <td nowrap="nowrap">q-sign-algorithm</td>
      <td>sha1</td>
      <td>Signature algorithm (required). Only sha1 is supported.</td>
   </tr>
   <tr>
      <td>q-ak</td>
      <td>Parameter [SecretId]</td>
      <td>Account's SecretId (required). ID obtained from the console in the preparation above.</td>
   </tr>
   <tr>
      <td>q-sign-time</td>
      <td>Parameter [SignTime]</td>
      <td>Signature start and end time (required), which are UNIX timestamp in seconds and separated a semicolon (;).</td>
   </tr>
   <tr>
      <td>q-key-time</td>
      <td>Parameter [KeyTime]</td>
      <td>It is required, and is the same as q-sign-time.</td>
   </tr>
   <tr>
      <td>q-header-list</td>
      <td>Parameter [SignedHeaderList]</td>
      <td>The key (required) of the HTTP request header that needs adding a signature. The key must be converted to lowercase. Multiple keys must be sorted in lexicographic order and separated by semicolons (;). If you don't want to provide signature in any header, it can be an empty string.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">q-url-param-list</td>
      <td>Parameter [SignedParamList]</td>
      <td>The parameter (required) of the HTTP request URI that needs adding a signature. The key must be converted to lowercase. Multiple keys must be sorted in lexicographic order and separated by semicolons (;). If you don't want to provide signature for any param, it can be an empty string.</td>
   </tr>
   <tr>
      <td>q-signature</td>
      <td>Parameter [Signature]</td>
      <td>Calculated signature content (required) comprised of lowercase letters</td>
   </tr>
</table>


>!For q-sign-time and q-key-time, the end time must be later than the start time. Otherwise, the signature expires immediately.

### Calculation method

Signature calculation involves the following steps:

1. Combine the related information of the HTTP request to the string HttpRequestInfo, according to a certain format.
2. Use the sha1 algorithm to calculate the hash value for HttpRequestInfo, and then combine the hash value with other specified parameters according to a certain format to generate the original string StringToSign.
3. Encrypt the q-key-time using the SecretKey to get the SignKey.
4. Encrypt the StringToSign using the SignKey to generate the Signature.

>!The URL encoded special characters should use uppercase characters. For example, `/` is encoded as `%2F` instead of `%2f`.

#### Combine HttpRequestInfo

HttpRequestInfo consists of Method, Uri, Headers, and Parameters in the HTTP request, as shown below:
```
HttpRequestInfo = Method + "\n"
                + Uri + "\n"
                + FormatedParameters + "\n"
                + FormatedHeaders + "\n"
```

`\n` indicates a newline escape character, and `+` indicates a string concatenation operation. The other parameters are defined as follows:

| Field Name | Description |
| ------------------ | ---------------------------------------- |
| Method | Method (in lowercase letters) used by HTTP requests, such as `get, post` |
| Uri | The name of resource of the HTTP request, excluding the query string, for example, `/logset` |
| FormatedParameters | The serialized string of parameters in the HTTP request's query string, namely the parameters specified in q-url-param-list. If no parameter is specified, an empty string is used. The key and the value are connected with `=`. Different key-value pairs are connected with `&`, and need to be sorted in lexicographical order. The key must be lowercase letters, and the value must be URL encoded. |
| FormatedHeaders | The header of HTTP request, namely the HTTP header specified in q-header-list. If no header is specified, an empty string is used. The key and the value are connected with `=`. Different key-value pairs are connected with `&`, and need to be sorted in lexicographical order. The key must be lowercase letters, and the value must be URL encoded. |

#### Combine StringToSign

StringToSign is composed of the sha1 hash values of q-sign-algorithm, q-sign-time, and HttpRequestInfo, as shown below:
```
StringToSign = q-sign-algorithm + "\n"
             + q-sign-time + "\n"
             + sha1(HttpRequestInfo) + "\n"
```

`\n` indicates a newline escape character. `+` indicates a string concatenation operation. Other parameters have been described above. The sha1 hash of HttpRequestInfo is a lowercase hexadecimal string.

#### Generate SignKey
The API only supports one digital signature algorithm, hmac-sha1 (default). Its pseudo code is as follows:
```
SignKey = Hexdigest(HMAC-SHA1(q-key-time, SecretKey))
```

`HMAC-SHA1` is the encryption algorithm, and `Hexdigest` is the method used for hexadecimal string conversion. The output results of some languages using the encryption algorithm are hexadecimal strings, so conversion is not needed.

#### Generate Signature
The API only supports one digital signature algorithm, hmac-sha1 (default). Its pseudo code is as follows:
```
Signature = Hexdigest(HMAC-SHA1(StringToSign, SignKey))
```

`HMAC-SHA1` is the encryption algorithm, and `Hexdigest` is the method used for hexadecimal string conversion. The output results of some languages using the encryption algorithm are hexadecimal strings, so conversion is not needed.

## Examples

Take the following SecretId and SecretKey as examples:

```
SecretId = "AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX"
SecretKey = "LUSE4nPK1d4tX5SHyXv6tZXXXXXXXXXX"

StartTime = 1510109254
EndTime = 1510109314
```

**Example 1**:
To get logset information, the HTTP request is as follows:
```
GET /logset?logset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx HTTP/1.1
Host: ap-shanghai.cls.myqcloud.com
```

For the above request, if a signature is added in the request header Host, the generated string HttpRequestInfo is:

```
get\n/logset\nlogset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\nhost=ap-shanghai.cls.myqcloud.com\n
```

The original string StringToSign generated using HttpRequestInfo is:

```
sha1\n1510109254;1510109314\n35601c3365a361b62b980fda754318c29862d39c\n
```

Encrypt the q-key-time using the SecretKey to get the SignKey:

```
a4501294d3a835f8dab6caf5c19837dd19eef357
```

Encrypt the StringToSign using the SignKey to generate the Signature:

```
2c53900d3fe8d2e875db8a6af5fe7303ee1567a8
```

The combined signature Authorization is:

```
q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1510109254;1510109314&q-key-time=1510109254;1510109314&q-header-list=host&q-url-param-list=logset_id&q-signature=2c53900d3fe8d2e875db8a6af5fe7303ee1567a8
```

The final request content is:

```
GET /logset?logset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx HTTP/1.1
Host: ap-shanghai.cls.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1510109254;1510109314&q-key-time=1510109254;1510109314&q-header-list=host&q-url-param-list=logset_id&q-signature=2c53900d3fe8d2e875db8a6af5fe7303ee1567a8
```

**Example 2**:
To modify logset information, the HTTP request is as follows:
```
PUT /logset HTTP/1.1
Host: ap-shanghai.cls.myqcloud.com
Content-Type: application/json
Content-Length: 50

{"logset_id":"xxxx-xx-xx-xx-xxxxxxxx","period":30}
```

The md5 value calculated for the body content is:
```
f9c7fc33c7eab68dfa8a52508d1f4659
```

For the above request, if a signature is added in the request header Host, the generated string HttpRequestInfo is:
```
put\n/logset\n\ncontent-md5=f9c7fc33c7eab68dfa8a52508d1f4659&content-type=application%2Fjson&host=ap-shanghai.cls.myqcloud.com\n
```

The original string StringToSign generated using HttpRequestInfo is:
```
sha1\n1510109254;1510109314\n0ca0242c3d50441fda6aa234d31bea7a7a12a1ea\n
```

Encrypt the q-key-time using the SecretKey to get the SignKey:
```
a4501294d3a835f8dab6caf5c19837dd19eef357
```

Encrypt the StringToSign using the SignKey to generate the Signature:
```
85a55e61de42483ba03bffd07a6c01b8d651af51
```

The combined signature Authorization is:
```
q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1510109254;1510109314&q-key-time=1510109254;1510109314&q-header-list=content-md5;content-type;host&q-url-param-list=&q-signature=85a55e61de42483ba03bffd07a6c01b8d651af51
```

The final request content is:
```
PUT /logset HTTP/1.1
Host: ap-shanghai.cls.myqcloud.com
Content-Type: application/json
Content-MD5: f9c7fc33c7eab68dfa8a52508d1f4659
Content-Length: 50
Authorization: q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1510109254;1510109314&q-key-time=1510109254;1510109314&q-header-list=content-md5;content-type;host&q-url-param-list=&q-signature=85a55e61de42483ba03bffd07a6c01b8d651af51

{"logset_id":"xxxx-xx-xx-xx-xxxxxxxx","period":30}
```


