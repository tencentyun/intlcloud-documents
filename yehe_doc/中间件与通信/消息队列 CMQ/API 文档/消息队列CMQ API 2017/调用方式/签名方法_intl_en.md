TencentCloud API authenticates each access request, that is, each request must include signing information (Signature) in the common request parameters to verify the identity of the user. The signature is generated by the security credentials which consist of a `SecretId` and a `SecretKey`. If you do not have the security credentials yet, you can apply for them at Tencent Cloud's official website; otherwise, you cannot call TencentCloud API.

## Signature Algorithm Description

CMQ allows clients to use two signature algorithms: SHA1 and SHA256, which can be specified in the `SignatureMethod` parameter. If the parameter value is `HmacSHA256`, SHA256 will be used for signature calculation; if this parameter is not specified or its value is not `HmacSHA256`, SHA1 will be used.

## 1. Apply for security credentials
Before using TencentCloud API for the first time, you need to apply for security credentials in the Tencent Cloud Console, which consists of `SecretId` and `SecretKey`. `SecretId` is used to identify the API requester, while `SecretKey` is a key used for signature string encryption and authentication by the server. Please keep your `SecretKey` private and do not disclose it to others.

You can apply for security credentials as follows:

1.1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com/).
1.2. Click **Tencent Cloud Services** and select **[Access Key](https://console.cloud.tencent.com/capi)** under **Management and Audit** to go to the TencentCloud API key management page.
1.3. On the [TencentCloud API Access Key Management](https://console.cloud.tencent.com/capi) page, click **Create** to create a pair of `SecretId/SecretKey`. Each account can have up to two `SecretId/SecretKey` pairs.

## 2. Generate a signature string
With the `SecretId` and `SecretKey`, a signature string can be generated as described below:

Suppose the `SecretId` and `SecretKey` are:
- SecretId: `AKIDPcY*****CVYLn3zT`
- SecretKey: `pPgfLip*****aU7UbQyFFx`

>!This is just an example. To perform actual operations, use your own `SecretId` and `SecretKey`. 

For example, if you call the `SendMessage` API to send a message, the request parameters may be as follows:

| Parameter Name | Description | Value | 
|---------|---------|---------|
| Action | Method name | SendMessage | 
| SecretId | Key ID | `AKIDPcY*****CVYLn3zT` | 
| Timestamp | Current timestamp | 1534154812 | 
|SignatureMethod| Signature algorithm | HmacSHA1|
| Nonce | Random positive integer |2889712707386595659 | 
| queueName | Name of the queue sending message |test1  | 
| RequestClient | Client version | SDK_Python_1.3 |
|clientRequestId|Unique custom ID of client |123***1231|
|delaySeconds|Delay time|0|
|msgBody|Message content to be sent|msg|

As shown above, the request has only five common request parameters (`Action`, `SecretId`, `Timestamp`, `Nonce`, and `SignatureMethod`) instead of the six ones described in "common request parameters". Actually, the sixth parameter `Signature` (signature string) is generated by other parameters (including signaling request parameters) together in the following steps:

### 2.1. Sort parameters
First, sort all request parameters by their names in ascending lexicographical order, just like sorting words in a dictionary in ascending alphabetical or numerical order. That is to say, sort the parameters by their first letters, and then sort the parameters with the same first letter by their second letters and so on. You can do this with the aid of relevant sorting functions in the programming language, such as the `ksort` function in PHP. The sorting results of the above sample parameters are as follows:

```
Action=SendMessage
Nonce=2889712707386595659
RequestClient=SDK_Python_1.3
SecretId=AKIDPcY*****CVYLn3zT
SignatureMethod=HmacSHA1
Timestamp=1534154812
clientRequestId=123***1231
delaySeconds=0
msgBody=msg
queueName=test1

```
Any other programming languages can be used to sort these parameters as long as the same result is produced.

### 2.2. Concatenate a request string
This step generates a request string.
Format the request parameters sorted in the previous step into the form of `parameter=value`. For example, for the `Action` parameter, its parameter is `Action` and its value is `SendMessages`; therefore, the parameter will be formatted into `Action=SendMessage`.
>!
- The `value` is the original value instead of the URL-encoded value.
- If an input parameter contains an underscore, the underscore needs to be replaced with a ".".

Then, concatenate the formatted parameters with `&`. The generated request string will be as follows:

```
Action=SendMessage&Nonce=2889712707386595659&RequestClient=SDK_Python_1.3&SecretId=AKIDPcY*****CVYLn3zT&SignatureMethod=HmacSHA1&Timestamp=1534154812&clientRequestId=123***1231&delaySeconds=0&msgBody=msg&queueName=test1
```

### 2.3. Generate an original signature string
This step generates the original signature string.
The original signature string consists of the following parameters:

- Request method: POST and GET methods are supported. GET is used here for the request. Please note that the method name should be in all capital letters.
- Request domain name: here, suppose the private domain name of the CMQ service in the Guangzhou region `cmq-queue-gz.api.tencentyun.com` is requested.
- Request path: the request path of TencentCloud API is always `/v2/index.php`.
- Request string: the request string generated in the previous step.

The rule for concatenating the original string of the signature is `request method + request server + request path + ? + request string`.

The concatenation result in the example is as follows:

```
POSTcmq-queue-gz.api.tencentyun.com/v2/index.php?Action=SendMessage&Nonce=2889712707386595659&RequestClient=SDK_Python_1.3&SecretId=AKIDPcY*****CVYLn3zT&SignatureMethod=HmacSHA1&Timestamp=1534154812&clientRequestId=123***1231&delaySeconds=0&msgBody=msg&queueName=test1
```

### 2.4. Generate a signature string
This step generates a signature string.
Use the HMAC-SHA1 algorithm to sign the **original signature string** obtained in the previous step, and then Base64-encode the generated signature to get the final signature.

The specific code when PHP is used is as follows:

```
$secretKey = 'pPgfLipfEXZ7VcRzhAMIyPaU7UbQyFFx';
$srcStr = 'POSTcmq-queue-gz.api.tencentyun.com/v2/index.php?Action=SendMessage&Nonce=2889712707386595659&RequestClient=SDK_Python_1.3&SecretId=AKIDPcY*****CVYLn3zT&SignatureMethod=HmacSHA1&Timestamp=1534154812&clientRequestId=123***1231&delaySeconds=0&msgBody=msg&queueName=test1';
$signStr = base64_encode(hash_hmac('sha1', $srcStr, $secretKey, true));
echo $signStr;
```

The obtained signature string is as follows:

```
C16WEtEXsD5v5tnaUMLAbZewXhI=
```

When any other programming language is used for development and the original signature in the example is verified, the same result as described above should be obtained.

## 3. Encode a signature string
>!
- The generated signature string cannot be directly used as a request parameter and needs to be URL-encoded.
- Parameters sent in GET requests have to be URL-encoded.

For example, if the signature string generated in the previous step is `C16WEtEXsD5v5tnaUMLAbZewXhI=`, it will be encoded to `C16WEtEXsD5v5tnaUMLAbZewXhI%3d`, and the final value of the `Signature` request parameter will be `C16WEtEXsD5v5tnaUMLAbZewXhI%3d`, which will be used to generate the final request URL.
The final request string is:
```
clientRequestId=1231231231&Nonce=2889712707386595659&Timestamp=1534154812&msgBody=msg&Action=SendMessage&SignatureMethod=HmacSHA1&RequestClient=SDK_Python_1.3&Signature=C16WEtEXsD5v5tnaUMLAbZewXhI%3D&delaySeconds=0&SecretId=AKIDPcY*****CVYLn3zT&queueName=test1
```
