
## Preparations

1. Get `SecretId` and `SecretKey`.
   They can be obtained on the [TencentCloud API Key](https://console.cloud.tencent.com/capi) page in the console.
2. Determine the programming language:
   Determine the HMAC-SHA1 function to use based on your development language. CLS provides a [demo for signature calculation](https://mirrors.tencent.com/install/cls/signature.zip) for C#, C++, Go, Java, Node.js, PHP, and Python languages.

An HTTP signature request initiated to CLS through an API is transmitted by using the standard HTTP Authorization header as shown in the following example:

```shell
GET /logset?logset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx HTTP/1.1
Host: ap-shanghai.cls.tencentyun.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1510109254;1510109314&q-key-time=1510109254;1510109314&q-header-list=content-type;host&q-url-param-list=logset_name&q-signature=e8b23b818caf4e33f196f895218bdabdbd1f1423
```

### Private and public domain names

CLS request domain names divide into private domain names and public domain names:
- A private domain name is in the format of `${region}.cls.tencentyun.com`, which is only valid for access requests from the same region, that is, CVM or Tencent Cloud services access the CLS service in the same region through the private domain name.
- A public domain name is in the format of `${region}.cls.tencentcs.com`. After the access source is connected to the internet, the public domain name of CLS can be accessed under normal circumstances.

The `region` field is the abbreviation of a CLS service region, such as `ap-beijing` for the Beijing region. For the complete region list, please see [Region List](https://intl.cloud.tencent.com/document/product/614/18940).

```
ap-beijing - Beijing
ap-shanghai - Shanghai
ap-guangzhou - Guangzhou
ap-chengdu - Chengdu
...
```

### Key-Value description

The signing information in a request is composed of multiple `key=value` pairs concatenated by `&` in the following format:

```shell
q-sign-algorithm=[Algorithm]&q-ak=[SecretId]&q-sign-time=[SignTime]&q-key-time=[KeyTime]&q-header-list=[SignedHeaderList]&q-url-param-list=[SignedParamList]&q-signature=[Signature]
```



The key-value (Key=Value) pairs constituting the signing information above are described as follows:

<table>
   <tr>
      <th>Key</th>
      <th>Value</th>
      <th>Description</th>
   </tr>
   <tr>
      <td nowrap="nowrap">q-sign-algorithm</td>
      <td>sha1</td>
      <td>Signature algorithm, which is required and currently supports only `sha1`</td>
   </tr>
   <tr>
      <td>q-ak</td>
      <td>Parameter [SecretId]</td>
      <td>`SecretId` of account API key, which is required</td>
   </tr>
   <tr>
      <td>q-sign-time</td>
      <td>Parameter [SignTime]</td>
			<td>Start time and end time of signature validity period in seconds in the format of Unix timestamp and separated with <code>;</code>, such as 1510109254;1510109314</td>
   </tr>
   <tr>
      <td>q-key-time</td>
      <td>Parameter [KeyTime]</td>
      <td>Same as the `q-sign-time` value, which is required</td>
   </tr>
   <tr>
      <td>q-header-list</td>
      <td>Parameter [SignedHeaderList]</td>
      <td>Key of the HTTP request header that needs to be signed, which is required. A key needs to be converted to lowercase, and multiple keys should be sorted in lexicographical order; for example, if there are multiple keys, separate them with <code>;</code>. If you don't want to sign any header, you can enter an empty string</td>
   </tr>
   <tr>
      <td nowrap="nowrap">q-url-param-list</td>
      <td>Parameter [SignedParamList]</td>
      <td>Parameter of the HTTP request URI that needs to be signed, which is required. A key needs to be converted to lowercase, and multiple keys should be sorted in lexicographical order; for example, if there are multiple keys, separate them with <code>;</code>. If you don't want to sign any parameter, you can enter an empty string</td>
   </tr>
   <tr>
      <td>q-signature</td>
      <td>Parameter [Signature]</td>
      <td>Calculated signing information in lowercase, which is required</td>
   </tr>
</table>



> !For `q-sign-time` and `q-key-time`, the end time should be after the start time; otherwise, the signature will expire immediately.

### Calculation method

Signature calculation steps:

1. Concatenate the relevant information in the HTTP request into `HttpRequestInfo` according to the specified format.
2. Use the `sha1` algorithm to calculate the hash value of `HttpRequestInfo`, and concatenate other specified parameters into the original string of the signature `StringToSign` according to the specified format.
3. Use `SecretKey` to encrypt `q-key-time` to get `SignKey`.
4. Use `SignKey` to encrypt `StringToSign` to generate `Signature`.

> !URL-encoded special symbols should be in uppercase; for example, `/` should be encoded as `%2F` instead of `%2f`,



#### Step 1. Concatenate HttpRequestInfo

`HttpRequestInfo` consists of `Method`, `Uri`, `Headers`, and `Parameters` in the HTTP request. It is concatenated in the following way:

```shell
HttpRequestInfo = Method + "\n"
                + Uri + "\n"
                + FormatedParameters + "\n"
                + FormatedHeaders + "\n"
```

The `\n` above indicates a line break escape character, `+` indicates a string concatenation operation, and other parameters are defined as follows:

| Field Name | Description |
| ------------------ | ------------------------------------------------------------ |
| Method             | HTTP request method in lowercase, such as `get` and `post`              |
| Uri                | Resource name of HTTP request excluding the query string part, such as `/logset`  |
| FormatedParameters | String generated by serializing parameters in the HTTP request query string, i.e., the parameters specified in `q-url-param-list`. If there is no need to specify this parameter, use an empty string. Key and value are concatenated with `=`, and different key-value pairs are concatenate with `&`, which need to be sorted in lexicographic order. Key is in lowercase, and value needs to be URL-encoded |
| FormatedHeaders    | HTTP request headers, i.e., HTTP headers specified in `q-header-list`. If there is no need to specify this parameter, use an empty string. Key and value are concatenated with `=`, and different key-value pairs are concatenate with `&`, which need to be sorted in lexicographic order. Key is in lowercase, and value needs to be URL-encoded |

To get logset information, the HTTP request is as follows:

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

#### Step 2. Concatenate StringToSign

`StringToSign` is composed of `q-sign-algorithm`, `q-sign-time`, and sha1 hash value of `HttpRequestInfo`. It is concatenated in the following way:

```shell
StringToSign = q-sign-algorithm + "\n"
             + q-sign-time + "\n"
             + sha1(HttpRequestInfo) + "\n"
```

The `\n` above indicates a line break escape character, `+` indicates a string concatenation operation, and other parameters have been described above, where the sha1 hash value of `HttpRequestInfo` is a hexadecimal lowercase string.

> !You need to escape `\n` to a line break first and then perform `sha1` calculation on `HttpRequestInfo`.

The corresponding result is as follows:

```shell
StringToSign = sha1\n1578973108;1578974918\n7be58ef9a64ecca66f96b79dc70d279bd93915cf\n
```

#### Step 3. Generate SignKey

Currently, the API only supports one digital signature algorithm, i.e., the default signature algorithm `hmac-sha1`. The pseudo code is as follows:

```shell
SignKey = Hexdigest(HMAC-SHA1(q-key-time, SecretKey))
```

Here, `HMAC-SHA1` is the encryption algorithm, and `Hexdigest` is the method for conversion to hexadecimal string. The output result of the encryption algorithm in some languages is directly a hexadecimal string, so no conversion is required.

The corresponding result is as follows:

```shell
SignKey = Hexdigest(HMAC-SHA1(1578973108;1578974918, LUSE4nPK1d4tX5SHyXv6tZXXXXXXXXXX))
```



#### Step 4. Generate Signature

Currently, the API only supports one digital signature algorithm, i.e., the default signature algorithm `hmac-sha1`. The pseudo code is as follows:

```shell
Signature = Hexdigest(HMAC-SHA1(StringToSign, SignKey))
```

Here, `HMAC-SHA1` is the encryption algorithm, and `Hexdigest` is the method for conversion to hexadecimal string. The output result of the encryption algorithm in some languages is directly a hexadecimal string, so no conversion is required.

The corresponding signature is as follows:

```shell
Signature = Hexdigest(HMAC-SHA1(sha1\n1578973108;1578974918\n7be58ef9a64ecca66f96b79dc70d279bd93915cf\n, 100edfdb73b873dae3d94665a2a7505258475486))
```



## Sample

`SecretId` and `SecretKey` are used as an example below to describe the signature:

```shell
SecretId = "AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX"
SecretKey = "LUSE4nPK1d4tX5SHyXv6tZXXXXXXXXXX"

StartTime = 1578976553
EndTime = 1578978363
```

**Sample 1**:
To get logset information, the HTTP request is as follows:

```shell
GET /logset?logset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx HTTP/1.1
Host: ap-shanghai.cls.tencentyun.com
Content-Type: application/json
```

For the above request, after the signature is added in the request header `Host`, the generated string will be:

```shell
HttpRequestInfo=get\n/logset\nlogset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\ncontent-type=application%2Fjson&host=ap-shanghai.cls.tencentyun.com\n
```

The original string of the signature generated according to `HttpRequestInfo` is:

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

The final request content is:

```shell
GET /logset?logset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx HTTP/1.1
Host: ap-shanghai.cls.tencentyun.com
Content-Type: application/json
Authorization: q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1578976553;1578978363&q-key-time=1578976553;1578978363&q-header-list=content-type;host&q-url-param-list=logset_id&q-signature=315dfa0d0ce55582145f7800df5eb3e9c88d2f84
```

**Sample 2**:
To modify logset information, the HTTP request is as follows:

```shell
PUT /logset HTTP/1.1
Host: ap-shanghai.cls.tencentyun.com
Content-Type: application/json
Content-Length: 50

{"logset_id":"xxxx-xx-xx-xx-xxxxxxxx","period":30}
```

For the above request, after the signature is added in the request header `Host`, the generated string will be:

```shell
HttpRequestInfo = put\n/logset\n\ncontent-type=application%2Fjson&host=ap-shanghai.cls.tencentyun.com\n
```

>?The `uri` parameter is empty, so it is a null character; however, `\n` cannot be omitted, so `\n\n` is generated.

The original string of the signature generated according to `sha1(HttpRequestInfo)` is:

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

The final request content is:

```shell
PUT /logset HTTP/1.1
Host: ap-shanghai.cls.tencentyun.com
Content-Type: application/json
Content-Length: 50
Authorization: q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1578976553;1578978363&q-key-time=1578976553;1578978363&q-header-list=content-type;host&q-url-param-list=&q-signature=600aeb5e646d385d7dd9da57ba9b2545cadfaa1c
{"logset_id":"xxxx-xx-xx-xx-xxxxxxxx","period":30}
```
