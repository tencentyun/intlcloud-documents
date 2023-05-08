>! 
> - CLS APIs in this document are legacy and not updated any more. They are not supported by new CLS features, so we strongly recommend you use [CLS API 3.0](https://intl.cloud.tencent.com/document/product/614/42757).
> - To create log topics or modify index configurations, use [CLS API 3.0](https://intl.cloud.tencent.com/document/product/614/42757). To collect logs, use the [SDK](https://intl.cloud.tencent.com/document/product/614/45006) specially optimized for log collection.
> 

## Preparations
Code leakage may lead to the leakage of `SecretId` and `SecretKey`, putting all resources under your account at risk. We recommend that you use a key in a more secure manner as instructed in the TencentCloud API key security solution. Below is the sample code.

1. Get SecretId and SecretKey.
   Credentials (SecretId and SecretKey) are available on the [API Key Management] Console (https://console.cloud.tencent.com/capi) .
2. Determine the programming language.
   Determine the HMAC-SHA1 function based on the programming language. CLS provides [signature calculation demos](https://mirrors.tencent.com/install/cls/signature.zip) for C#, C++, Go, Java, Node.js, PHP, and Python.

 When you send an HTTP request to Tencent Cloud CLS, Tencent Cloud API uses the standard HTTP Authorization header to pass authentication information, as shown in the following example:

```shell
GET /logset?logset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx HTTP/1.1
Host: ap-shanghai.cls.tencentyun.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1510109254;1510109314&q-key-time=1510109254;1510109314&q-header-list=content-type;host&q-url-param-list=logset_name&q-signature=e8b23b818caf4e33f196f895218bdabdbd1f1423
```

### Private and public domain names

CLS request domain names divide into private domain names and public domain names:
- A private domain name is in the format of `${region}.cls.tencentyun.com`, which is only valid for access requests from the same region, that is, CVM or Tencent Cloud services access the CLS service in the same region through the private domain name.
- A public domain name is in the format of `${region}.cls.tencentcs.com`. After the access source is connected to the internet, the public domain name of CLS can be accessed under normal circumstances.

The `region` field is the abbreviation of a CLS service region, such as `ap-beijing` for Beijing region. For the complete region list, see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940).

```
ap-beijing - Beijing
ap-shanghai - Shanghai
ap-guangzhou - Guangzhou
ap-chengdu - Chengdu
...
```

### Key-value description

The key-value (Key=Value) pairs are concatenated with "&"in the signature in the following format:

```shell
q-sign-algorithm=[Algorithm]&q-ak=[SecretId]&q-sign-time=[SignTime]&q-key-time=[KeyTime]&q-header-list=[SignedHeaderList]&q-url-param-list=[SignedParamList]&q-signature=[Signature]
```



The key-value (Key=Value) pairs in the signature are described as follows:

<table>
   <tr>
      <th>Key</th>
      <th>Value</th>
      <th>Definition</th>
   </tr>
   <tr>
      <td nowrap="nowrap">q-sign-algorithm</td>
      <td>sha1</td>
      <td>Signature algorithm, which is required and currently can only be `sha1`</td>
   </tr>
   <tr>
      <td>q-ak</td>
      <td>Parameter [SecretId]</td>
      <td>`SecretId` of the account API key, which is required.</td>
   </tr>
   <tr>
      <td>q-sign-time</td>
      <td>Parameter [SignTime]</td>
			<td>Start time and end time of the signature validity period in seconds in the format of Unix timestamp and separated by <code>;</code>, such as 1510109254;1510109314.</td>
   </tr>
   <tr>
      <td>q-key-time</td>
      <td>Parameter [KeyTime]</td>
      <td>Same as the `q-sign-time` value, which is required.</td>
   </tr>
   <tr>
      <td>q-header-list</td>
      <td>Parameter [SignedHeaderList]</td>
      <td>Key of the HTTP request header that needs to be signed, which is required. A key needs to be converted to lowercase, and multiple keys should be sorted in lexicographical order; for example, if there are multiple keys, separate them by <code>;</code>. If you don't want to sign any header, you can enter an empty string.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">q-url-param-list</td>
      <td>Parameter [SignedParamList]</td>
      <td>Parameter of the HTTP request URI that needs to be signed, which is required. A key needs to be converted to lowercase, and multiple keys should be sorted in lexicographical order; for example, if there are multiple keys, separate them with <code>;</code>. If you don't want to sign any parameter, you can enter an empty string.</td>
   </tr>
   <tr>
      <td>q-signature</td>
      <td>Parameter [Signature]</td>
      <td>Calculated signature information in lowercase, which is required.</td>
   </tr>
</table>



> !For `q-sign-time` and `q-key-time`, the end time should be after the start time; otherwise, the signature will expire immediately.

### Calculation method

Signature calculation process:

1. Concatenate the relevant information in the HTTP request into `HttpRequestInfo` according to the specified format.
2. Use the `sha1` algorithm to calculate the hash value of `HttpRequestInfo`, and concatenate other specified parameters into the original string of the signature `StringToSign` in the specified format.
3. The SecretKey is used as a key to hash q-key-time creating SignKey.
4. The SignKey is then used as the key to hash the StringToSign generating the signature.

> !URL-encoded symbols should be in uppercase; for example, `/` should be encoded as `%2F` instead of `%2f`.



#### Step 1. Concatenate the HttpRequestInfo

`HttpRequestInfo` consists of `Method`, `Uri`, `Headers`, and `Parameters` in an HTTP request. It is concatenated in the following way:

```shell
HttpRequestInfo = Method + "\n"
                + Uri + "\n"
                + FormatedParameters + "\n"
                + FormatedHeaders + "\n"
```

`\n` is the newline character, `+` is a string concatenation operator. The other parameters are defined as follows:

| Field Name             | Description                                                        |
| ------------------ | ------------------------------------------------------------ |
| Method             | HTTP request method in lowercase, such as `get` and `post`.              |
| Uri                | The resource name of the HTTP request excluding the query string part, such as `/logset`.  |
| FormatedParameters | The URL-formatted query string parameters, which are the parameters included in the q-url-param-list. If no parameter is specified, use an empty string. The keys (headers) and their values are connected with `=`. Different key-value pairs are connected with `&`, and they need to be sorted in lexicographical order. The key (header) must be lowercase letters, and the value must be URL encoded. |
| FormatedHeaders | The header of HTTP request. That is, the HTTP headers that are included in q-header-list. If no header is specified, use an empty string. The keys (headers) and their values are connected with `=`. Different key-value pairs are connected with `&`, and they need to be sorted in lexicographical order. The key (header) must be lowercase letters, and the value must be URL encoded. |

To get logset information, add request elements into the request as follows:

```shell
GET /logset?logset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx HTTP/1.1
Host: ap-shanghai.cls.tencentyun.com
```

The corresponding `HttpRequestInfo` is as follows:

With request parameter:

```shell
get\n/logset\nlogset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\nhost=ap-shanghai.cls.tencentyun.com\n
```

Without request parameter:

```shell
get\n/logset\n\nhost=ap-shanghai.cls.tencentyun.com\n
```

>?Even without parameters, `\n` cannot be omitted, so `\n\n` is generated.

#### Step 2. Concatenate the StringToSign

`StringToSign` consists of `q-sign-algorithm`, `q-sign-time`, and `sha1` hash value of `HttpRequestInfo`. It is concatenated in the following way:

```shell
StringToSign = q-sign-algorithm + "\n"
             + q-sign-time + "\n"
             + sha1(HttpRequestInfo) + "\n"
```

`\n` is the newline character, `+` is a string concatenation operator. Other parameters which are already mentioned above. Sha1-hashed HttpRequestInfo must be hex-encoded and in lowercase.

> !You need to escape `\n` to a line break first and then perform `sha1` calculation on `HttpRequestInfo`.

The corresponding result is as follows:

```shell
StringToSign = sha1\n1578973108;1578974918\n7be58ef9a64ecca66f96b79dc70d279bd93915cf\n
```

#### Step 3. Generate the SignKey

Tencent Cloud API currently only supports the default signing algorithm hmac-sha1 for message authentication. The following is the pseudocode:

```shell
SignKey = Hexdigest(HMAC-SHA1(q-key-time, SecretKey))
```

Here, `HMAC-SHA1` is the encryption algorithm, and `Hexdigest` is the method for conversion to hexadecimal strings. The output result of the encryption algorithm in some languages is directly a hexadecimal string, so no conversion is required.

The result is as follows:

```shell
SignKey = Hexdigest(HMAC-SHA1(1578973108;1578974918, LUSE4nPK1d4tX5SHyXv6tZXXXXXXXXXX))
```



#### Step 4. Generate the signature

Tencent Cloud API currently only supports the default signing algorithm hmac-sha1 for message authentication. The following is the pseudocode:

```shell
Signature = Hexdigest(HMAC-SHA1(StringToSign, SignKey))
```

Here, `HMAC-SHA1` is the encryption algorithm, and `Hexdigest` is the method for conversion to hexadecimal strings. The output result of the encryption algorithm in some languages is directly a hexadecimal string, so no conversion is required.

The signature is as follows:

```shell
Signature = Hexdigest(HMAC-SHA1(sha1\n1578973108;1578974918\n7be58ef9a64ecca66f96b79dc70d279bd93915cf\n, 100edfdb73b873dae3d94665a2a7505258475486))
```



## Examples

The following SecretId and SecretKey are used in the examples:

```shell
SecretId = "AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX"
SecretKey = "LUSE4nPK1d4tX5SHyXv6tZXXXXXXXXXX"

StartTime = 1578976553
EndTime = 1578978363
```

**Example 1**:
To get logset information, add request elements into the request as follows:

```shell
GET /logset?logset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx HTTP/1.1
Host: ap-shanghai.cls.tencentyun.com
Content-Type: application/json
```

For the above request, after the signature is added to the request header `Host`, the generated string will be:

```shell
HttpRequestInfo=get\n/logset\nlogset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\ncontent-type=application%2Fjson&host=ap-shanghai.cls.tencentyun.com\n
```

The original string of the signature generated based on `HttpRequestInfo` is:

```shell
StringToSign = sha1\n1578976553;1578978363\ne2d0126b61269ef047d9d05b6c385cea0aea9799\n
```

Encrypt `q-key-time` with `SecretKey` to get:

```shell
SignKey = f49255658de17084898d83beaa755b9f0301591f
```

Encrypt `StringToSign` with `SignKey` to generate:

```shell
Signature = 315dfa0d0ce55582145f7800df5eb3e9c88d2f84
```

The final concatenated signature is:

```shell
Authorization = q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1578976553;1578978363&q-key-time=1578976553;1578978363&q-header-list=content-type;host&q-url-param-list=logset_id&q-signature=315dfa0d0ce55582145f7800df5eb3e9c88d2f84
```

The final request is:

```shell
GET /logset?logset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx HTTP/1.1
Host: ap-shanghai.cls.tencentyun.com
Content-Type: application/json
Authorization: q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1578976553;1578978363&q-key-time=1578976553;1578978363&q-header-list=content-type;host&q-url-param-list=logset_id&q-signature=315dfa0d0ce55582145f7800df5eb3e9c88d2f84
```

**Example 2**:
To modify logset information, add request elements into the request as follows:

```shell
PUT /logset HTTP/1.1
Host: ap-shanghai.cls.tencentyun.com
Content-Type: application/json
Content-Length: 50

{"logset_id":"xxxx-xx-xx-xx-xxxxxxxx","period":30}
```

For the above request, after the signature is added to the request header `Host`, the generated string will be:

```shell
HttpRequestInfo = put\n/logset\n\ncontent-type=application%2Fjson&host=ap-shanghai.cls.tencentyun.com\n
```

>?The `uri` parameter is empty, so it is a null character; however, `\n` cannot be omitted, so `\n\n` is generated.

The original string of the signature generated based on `sha1(HttpRequestInfo)` is:

```shell
StringToSign = sha1\n1578976553;1578978363\ne86af9693f3de2047dd10dbe2898ecaf1df00de0\n
```

Encrypt `q-key-time` with `SecretKey` to get:

```shell
SignKey = f49255658de17084898d83beaa755b9f0301591f
```

Encrypt `StringToSign` with `SignKey` to generate:

```shell
Signature = 600aeb5e646d385d7dd9da57ba9b2545cadfaa1c
```

The final concatenated signature is:

```shell
Authorization = q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1578976553;1578978363&q-key-time=1578976553;1578978363&q-header-list=content-type;host&q-url-param-list=&q-signature=600aeb5e646d385d7dd9da57ba9b2545cadfaa1c
```

The final request is:

```shell
PUT /logset HTTP/1.1
Host: ap-shanghai.cls.tencentyun.com
Content-Type: application/json
Content-Length: 50
Authorization: q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1578976553;1578978363&q-key-time=1578976553;1578978363&q-header-list=content-type;host&q-url-param-list=&q-signature=600aeb5e646d385d7dd9da57ba9b2545cadfaa1c
{"logset_id":"xxxx-xx-xx-xx-xxxxxxxx","period":30}
```
