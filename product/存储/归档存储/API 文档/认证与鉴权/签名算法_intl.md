## Signature Description

In CAS, each HTTP request initiated must be **a request with signature**. For a request with signature, a string of ciphertext is computed based on the key provided by Tencent Cloud and the content of the request, and is passed in as Authorization field in HTTP Headers.

CAS determines which requests are allowed and how to control request content and the request validity based on the user-specific access control policy and the signature passed in.

Request restriction and signature access can be applied in the following scenarios:

> Verify the identity of the user: The signature is calculated based on the keys provided by Tencent Cloud, including SecretID and SecretKey.
>
> Verify the transmitted data: The verification information of the data is included in the ciphertext of the signature. If the check value of the passing data does not match the check value in the ciphertext, a failure will be returned for such request. Generally, this can guarantee that, when the request content is hijacked, the error data will not be recorded.
>
> Protect the signature from being used twice: By encrypting the request's validity period in the signature, it is possible to ensure that the client cannot initiate the request after the signature expires, which is also used to prevent any third party from intervening in the use of the signature to protect data security when network is listened in.



## Signature Algorithm

### Overview

In CAS, Authorization field is required in the HTTP request header for each request, which is the most common request authentication method in the HTTP standard definition. Common requests are as follows:

```http
PUT /-/vaults/example HTTP/1.1
Host: cas.ap-chengdu.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=QmFzZTY0IGlzIGEgZ2VuZXJp&q-sign-time=1480932292;1481012292&q-key-time=1480932292;1481012292&q-header-list=host&q-url-param-list=&q-signature=43803ef4a4207299d87bb75d1c739c06cc9406bb
```

The following table lists the information to be passed in the Authorization field:

| Name               | Description                                       |
| ---------------- | ---------------------------------------- |
| q-sign-algorithm | The encryption method of the signature. Tencent Cloud uses HMAC-SHA1 for signature encryption.<br /> Please keep the default value (sha1) for this field |
| q-ak             | SecretID, which identifies the user's identity. You can check it on the Tencent Cloud API Key page. |
|q-sign-time      | The start and end time of the signature validity, which is represented by a 10-digit Unix timestamp, accurate to seconds.<br /> The start and end time are separated before and after by semicolon. |
| q-key-time | Users can define the start and end time of SignKey validity, which is represented by a 10-digit Unix timestamp, accurate to seconds.<br /> The start and end time are separated before and after by semicolon.<br /> Generally, the time range of the q-key-time is greater than or equal to that of q-sign-time. |
| q-header-list    | The list of headers to be verified in ciphertexts, which should be in `lowercase`, `sorted in lexicographical order` and separated with ";". |
| q-header-list    | The list of parameters to be verified in ciphertexts, which should be in `lowercase` and separated with ";". |
| q-signature      | Request verification information encrypted via the HMAC-SHA1 algorithm. |

### Computing signature

Before constructing the signature, you must first obtain the API key pair for the Tencent Cloud account, including SecretID and SecretKey. For more information, see "Monitor & Management - Cloud API Key" in the Tencent Cloud console.

#### Signature composition

-  SignKey: A key string that carries the validity period and is encrypted with HMAC-SHA1 via SecretKey.
-  FormatString: A string formatted according to certain standards from the request.
-  StringToSign: A string containing the verification algorithm, validity period of the request, and FormatString verified by Hash.
-  Signature: Encrypted signature, use the string encrypted with HMAC-SHA1 in SignKey and StringToSign to fill in q-signature.

#### 1. Compute SignKey

In order to protect the security of SecretKey, the request needs to encrypt the SecretKey before transmission. The signature allows users to carry Unix timestamps to limit the effective time of SecretKey.

To enable users to send the key information needed for signature calculation to the untrusted client, SecretKey supports the generation of an irreversible key string encrypted along with the user-specified validity period, and sends it to the untrusted client. The SignKey shall be computed in the following format:

$SignKey =

```
HMAC-SHA1($SecretKey,"<q-key-time>")
```

- SecretKey: The SecretKey in the API key pair provided by Tencent Cloud, for example `AKIDZfbOA78asKUYBcXFrJD0a1ICvR98JM`.
- q-key-time: The valid start and end time of the SignKey. The two timestamps are separated before and after by semicolon with 10-digit Unix timestamp, accurate to seconds. For example `1480932292; 1481012292`.

#### 2. Generate FormatString

This string formats the key information in the HTTP request and will be used as the primary part for the encryption signature verification. This can protect the HTTP request during transmission from being tampered by any third party.

To enable the CAS server to verify the request in a fixed format, the key data in the HTTP request needs to be included in the FormatString, with one key element displayed per line. It is generated as follows:

$FormatString = 

```
<FormatMethod>\n
<FormatURI>\n
<FormatParameters>\n
<FormatHeaders>\n
```

-  FormatMethod: The HTTP operation for the request, such as PUT/GET/DELETE, which must be converted to lowercase.
-  For example, when initiating `Get http://cas.ap-chengdu.myqcloud.com`, its FormatMethod is `get`.
-  FormatURI: The URI of the request, that is, the remaining part (usually starting with /) after removing the http://, the domain name, and the parameter in URL (usually starting with ?).
-  For example, for `http://cas.ap-chengdu.myqcloud.com/-/vaults`, the Format URI is `/-/vaults`.
-  FormatParameters: The parameter of the request (starting with ?), which is indicated by `key=value`. The key and value of the parameter must be URL encoded. If there are multiple parameter pairs, use & in between. **The key and value must be converted to lowercase and key is sorted in lexicographical order.**
  - For example, for `http://cas.ap-chengdu.myqcloud.com/-/vaults?limit=2`, the FormatParameters is `limit=2`.
- FormatHeaders: The HTTP header of the request, which is indicated by `key=value`. The key of the header must be in lowercase, and the value must be URL encoded. If there are multiple parameter pairs, use & in between. **Sort keys in lexicographical order**
  - For example, in the header `Host: cas.ap-chengdu.myqcloud.com`, the FormatHeaders is `host=cas.ap-chengdu.myqcloud.com`

#### 3. Compute StringToSign

The string contains the algorithm name and the validity period of the signature, and the FormatString processed by the SHA-1 hash. Thus, it is necessary to generate a FormatString before calculating the StringToSign.

The validity period of the signature in StringToSign is different from the effective time of the SecretKey in SignKey. The validity period can only be used to verify if the request is initiated within the valid time.

-  If the client initiating the request is trusted, the SecretKey can be saved directly on the client, and the same start and end time of validity can be used in both SignKey and StringToSign to ensure the validity of the request.
-  If the client initiating the request is untrusted by default, the SecretKey shall be protected and must not be saved on the client. You can issue SignKey to the client to compute the signature after encrypting the SecretKey and restricting its validity period. The validity period of StringToSign shall be generated by the client when the request is initiated.

The StringToSign is generated in the following format:
$StringToSign =

```
<q-sign-algorithm>\n
<q-sign-time>\n
SHA1Hash($FormatString)\n
```

-  q-sign-algorithm: The encryption algorithm used for signatures. The default is `sha1`.
-  q-sign-time: The start and end time of the request validity period. The two timestamps are separated before and after by semicolon with 10-digit Unix timestamp, accurate to seconds. For example `1480932292; 1481012292`.
-  SHA1Hash($FormatString): An irreversible string that will form part of the FormatString, which is generated by SHA-1 hash algorithm, identifying the key content of the request.

#### 4. Compute signature

The Signature generated here will be placed in the q-signature field to verify the validity of the request content. By using the HMAC-SHA1 algorithm, SignKey is used as the key to encrypt and compute the StringToSign. The Signature is generated in the following format:

$Signature =

```
HMAC-SHA1($SignKey,$StringToSign)
```

##### 5. Generate Authorization

The contents generated in the signature and those in the request to be explicitly identified shall be indicated by `key=value`. Use & between multiple parameter pairs.

The Authorization is generated in the following format (a long string without line breaks):

```
q-sign-algorithm=sha1&
q-ak=<SecretID>&
q-sign-time=<SignTime>&
q-key-time=<KeyTime>&
q-header-list=<SignedHeaderList>&
q-url-param-list=<SignedParameterList>&
q-signature=<Signature>
```


