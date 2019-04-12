## Prerequisites
1. Get SecretId and SecretKey.
    Credentials (SecretId and SecretKey) are available on the [API Key Management] Console (https://console.cloud.tencent.com/capi) .
2. Specify the programming language:
    Supported programming languages include but are not limited to Java, PHP, C Sharp, C++, Node.js and Python. Specify the hash function (SHA1) used in HMAC for the chosen language.

## Signing Tencent Cloud API Requests
When you send a HTTP request to Tencent Cloud CLS, Tencent Cloud API uses the standard HTTP Authorization header to pass authentication information, as shown in the following example: 

```
GET /logset?logset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx HTTP/1.1
Host: ap-shanghai.cls.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1510109254;1510109314&q-key-time=1510109254;1510109314&q-header-list=content-type;host&q-url-param-list=logset_name&q-signature=e8b23b818caf4e33f196f895218bdabdbd1f1423
```

The Host header field in this HTTP request is ${region}.cls.myqcloud.com. "region" specifies the Region of the CLS service, for example, ap-beijing stands for Beijing Region. For a list of supported region, see [Regions](https://cloud.tencent.com/document/product/614/18940).

```
ap-beijing - Beijing
ap-shanghai - Shanghai
ap-guangzhou - Guangzhou
ap-chengdu - Chengdu
```

The key-value (Key=Value) pairs are concatenated with "&"in the signature in the following format:

```shell
q-sign-algorithm=[Algorithm]&q-ak=[SecretId]&q-sign-time=[SignTime]&q-key-time=[KeyTime]&q-header-list=[SignedHeaderList]&q-url-param-list=[SignedParamList]&q-signature=[Signature]
```

### Key-Value description
The key-value (Key=Value) pairs in the signature are described as follows:

<table>
   <tr>
      <th>Key</th>
      <th>Value</th>
      <th>Description</th>
   </tr>
   <tr>
      <td nowrap="nowrap">q-sign-algorithm</td>
      <td>sha1</td>
      <td>Required. The signing algorithm that is used to calculate the signature. Only HMAC-SHA1 is supported.</td>
   </tr>
   <tr>
      <td>q-ak</td>
      <td>Parameter [SecretId]</td>
      <td>Required. Your account's SecretId. See **Prerequisites** to find the information about getting SecretId.</td>
   </tr>
   <tr>
      <td>q-sign-time</td>
      <td>Parameter [SignTime]</td>
      <td>Required. The valid start and end time that you use to define your credential scope.  The time stamps must in UNIX in seconds and are separated by semicolon(;).</td>
   </tr>
   <tr>
      <td>q-key-time</td>
      <td>Parameter [KeyTime]</td>
      <td>Required. The value is the same as the value of q-sign-time.</td>
   </tr>
   <tr>
      <td>q-header-list</td>
      <td>Parameter [SignedHeaderList]</td>
      <td>Required. A list of HTTP request headers that you used to compute the signature. The header names (keys) must be in lexicographic order, lowercase and separated by semicolon(;). An empty string is accepted while not signing the header.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">q-url-param-list</td>
      <td>Parameter [SignedParamList]</td>
      <td>Required. A list of parameter that needs to be added to the  HTTP request URI. The parameters (keys) must be in lexicographic order, lowercase and separated by semicolon(;). An empty string is accepted while not signing the header.</td>
   </tr>
   <tr>
      <td>q-signature</td>
      <td>Parameter [Signature]</td>
      <td>Required. Required. The calculated signature. Must in lowercase.</td>
   </tr>
</table>


>!For q-sign-time and q-key-time, the end time must be later than the start time. Otherwise, the signature expires immediately.

### Signature Calculation

Signature calculation process:

1.  Concatenate the components of the HTTP request authentication information in a standardized format to create a string HttpRequestInfo.
2. Use sha1 hash function to calculate the string HttpRequestInfo, and then combine the resulting hash with other specified parameters in a certain format to generate a StringToSign. 
3. The SecretKey is used as a key to hash q-key-time creating SignKey.
4. The SignKey is then used as the key to hash the StringToSign generating the signature.

>!The URL encoded characters must be in uppercase. For example, `/` is encoded as `%2F` instead of `%2f`.

#### Concatenating HttpRequestInfo

HttpRequestInfo consists of Method, Uri, Headers, and Parameters in the HTTP request, as shown below:
```
HttpRequestInfo = Method + "\n"
                + Uri + "\n"
                + FormatedParameters + "\n"
                + FormatedHeaders + "\n"
```

`\n` is the newline character,  `+` is a string concatenation operator. The other parameters are defined as follows:

| Field Name | Description |
| ------------------ | ---------------------------------------- |
| Method | HTTP request methods (in lowercase), such as `get, post` |
| Uri | The name of resource accessed by the HTTP request, excluding the query string, for example, `/logset` |
| FormatedParameters | The URL-formatted query string parameters, which are the parameters included in the q-url-param-list.  If no paramater is specified, use an empty string. The keys (headers) and their values are connected with `=`. Different key-value pairs are connected with `&`, and they need to be sorted in lexicographical order. The key (header) must be lowercase letters, and the value must be URL encoded. |
| FormatedHeaders | The header of HTTP request. That is, the HTTP headers that are included in q-header-list. If no header is specified, use an empty string. The keys (headers) and their values are connected with `=`. Different key-value pairs are connected with `&`, and they need to be sorted in lexicographical order. The key (header) must be lowercase letters, and the value must be URL encoded. |

#### Creating StringToSign

The StringToSign is combined with the algorithm (q-sign-algorithm), date and time (q-sign-time) and the hashed HttpRequestInfo, as shown below:
```
StringToSign = q-sign-algorithm + "\n"
             + q-sign-time + "\n"
             + sha1(HttpRequestInfo) + "\n"
```

`\n` is the newline character,  `+` is a string concatenation operator. Other parameters which are already mentioned above. Sha1-hashed HttpRequestInfo must be hex-encoded and in lowercase.

#### Generating SignKey
Tencent Cloud API currently only supports the default signing algorithm hmac-sha1 for message authentication. The following is the pseudocode:
```
SignKey = Hexdigest(HMAC-SHA1(q-key-time, SecretKey))
```

`HMAC-SHA1` is the hashing algorithm, and `Hexdigest`  means that hex-encoding is used to encode the digest (binary format hash).  Some programming language do not require that you use hex-encoding as the resulting hash is hex-encoded.

#### Generating Signature
The API only supports one digital signature algorithm, hmac-sha1 (default). Its pseudo code is as follows:
```
Signature = Hexdigest(HMAC-SHA1(StringToSign, SignKey))
```

`HMAC-SHA1` is the hashing algorithm, and `Hexdigest`  means that hex-encoding is used to encode the digest (binary format hash).  Some programming language do not require that you use hex-encoding as the resulting hash is hex-encoded.

## Examples

The following SecretId and SecretKey are used in the examples:

```
SecretId = "AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX"
SecretKey = "LUSE4nPK1d4tX5SHyXv6tZXXXXXXXXXX"

StartTime = 1510109254
EndTime = 1510109314
```

**Example 1**:
To get logset information, add request elements into the request as follows:
```
GET /logset?logset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx HTTP/1.1
Host: ap-shanghai.cls.myqcloud.com
```

For this request, if the HTTP request header Host is signed, the string HttpRequestInfo will be generated as follows:

```
get\n/logset\nlogset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\nhost=ap-shanghai.cls.myqcloud.com\n
```

Use HttpRequestInfo to create a StringToSign::

```
sha1\n1510109254;1510109314\n35601c3365a361b62b980fda754318c29862d39c\n
```

The SecretKey is used as a key to hash q-key-time creating SignKey:

```
a4501294d3a835f8dab6caf5c19837dd19eef357
```

The SignKey is then used as the key to hash the StringToSign generating the Signature:
```
2c53900d3fe8d2e875db8a6af5fe7303ee1567a8
```

The calculated signature is:

```
q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1510109254;1510109314&q-key-time=1510109254;1510109314&q-header-list=host&q-url-param-list=logset_id&q-signature=2c53900d3fe8d2e875db8a6af5fe7303ee1567a8
```

The final request is:

```
GET /logset?logset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx HTTP/1.1
Host: ap-shanghai.cls.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1510109254;1510109314&q-key-time=1510109254;1510109314&q-header-list=host&q-url-param-list=logset_id&q-signature=2c53900d3fe8d2e875db8a6af5fe7303ee1567a8
```

**Example 2**:
To modify logset information, add request elements into the request as follows:
```
PUT /logset HTTP/1.1
Host: ap-shanghai.cls.myqcloud.com
Content-Type: application/json
Content-Length: 50

{"logset_id":"xxxx-xx-xx-xx-xxxxxxxx","period":30}
```

The md5 hashed value in the request Body is:
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

The SecretKey is used as a key to hash q-key-time creating SignKey:
```
a4501294d3a835f8dab6caf5c19837dd19eef357
```

The SignKey is then used as the key to hash the StringToSign generating the Signature:
```
85a55e61de42483ba03bffd07a6c01b8d651af51
```

The calculated signature is:
```
q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1510109254;1510109314&q-key-time=1510109254;1510109314&q-header-list=content-md5;content-type;host&q-url-param-list=&q-signature=85a55e61de42483ba03bffd07a6c01b8d651af51
```

The final request is:
```
PUT /logset HTTP/1.1
Host: ap-shanghai.cls.myqcloud.com
Content-Type: application/json
Content-MD5: f9c7fc33c7eab68dfa8a52508d1f4659
Content-Length: 50
Authorization: q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1510109254;1510109314&q-key-time=1510109254;1510109314&q-header-list=content-md5;content-type;host&q-url-param-list=&q-signature=85a55e61de42483ba03bffd07a6c01b8d651af51

{"logset_id":"xxxx-xx-xx-xx-xxxxxxxx","period":30}
```


