TencentCloud API authenticates each access request, so each request is required to include the `Signature` in the common request parameters for user authentication. The signature is generated with your security credentials, which consist of a `SecretId` and a `SecretKey`. Users who have no security credentials can apply for one on Tencent Cloud official website; otherwise, you will not be able to call TencentCloud API.

## Applying for Security Credentials
Before using TencentCloud API for the first time, you need to apply for security credentials in **Tencent Cloud Console** > **[API Key Management](https://console.cloud.tencent.com/cam/capi)**. Security credentials consist of a `SecretId` and a `SecretKey`.

- **SecretId** is the identity of the requester.
- **SecretKey** is used to encrypt the strings to create a signature so that Tencent Cloud server can validate the identity of the requester.

>!API keys is an important credential for creating TencentCloud API requests. You can access and manage the resources in your Tencent Cloud account via APIs. For the security of your assets and services, please keep the keys private, change them regularly, and delete old keys promptly after creating new ones.


#### How to apply for security credentials

1. Log in to the Tencent Cloud Console and enter the [API Key Management](https://console.cloud.tencent.com/cam/capi) page.
2. On the API Key Management page, click **Create Key** to create a pair of `SecretId/SecretKey`.

>!
> - A developer account can have up to two pairs of `SecretId/SecretKey`.
> - A developer can add a QQ account as a sub-user and use it to apply for different security credentials in multiple developer consoles.
> - A sub-user can only call certain specified TencentCloud APIs with their security credentials.

## Generating a Signature String
With the `SecretId` and `SecretKey`, a signature string can be generated as described below:

![](//mc.qcloudimg.com/static/img/3a3a616ba175bb95be68123d86715e77/image.png)

Assume that the `SecretId` and `SecretKey` are:
SecretId： AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA
SecretKey： Gu5t9xGARNpq86cd98joQYCN3Cozk1qA

>! This example is for demonstration purposes only. Make sure that you proceed with your actual `SecretId`, `SecretKey` and request parameters.

Take Tencent Cloud CVM as an example. If you wish to call the  `DescribeInstances` API to view the instance list, the request parameters are as follows:

| Parameter Name | Description | Parameter Value |
|---------|---------|---------|
| Action | Method name | DescribeInstances |
| SecretId | Key ID | AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA |
| Timestamp | Current timestamp | 1465185768 |
| Nonce | Random positive integer | 11886 |
| Region | Region where the instance resides | ap-guangzhou |
| SignatureMethod | Signature method | HmacSHA256 |
| InstanceIds.0 | ID of the target instance | ins-09dx96dg |

### 1. Sorting parameters
First, sort all request parameters by parameter name in ascending lexicographical order, just like sorting words in a dictionary in ascending alphabetical order or numerical order. That is to say, sort the parameters by their first letters, and then sort the parameters with the same first letter by their second letters, and so on. You can do this with the aid of relevant sorting functions in the programming language, such as the ksort function in PHP. The sorting results of the above sample parameters are as follows:

```shell
{
    "Action" : "DescribeInstances",
    "InstanceIds.0" : "ins-09dx96dg",
    "Nonce" : "11886",
    "Region" : "ap-guangzhou",
    "SecretId" : "AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA",
    "SignatureMethod" : "HmacSHA256",
    "Timestamp" : "1465185768"
}
```
Any other programming languages can be used to sort these parameters as long as the same result is produced.

### 2. Generating request string
This step generates a request string.
Format the request parameters sorted in the previous step into the form of `"parameter name"="value"`. For example, for the `Action` parameter, its parameter name is `"Action"` and its value is `"DescribeInstances"`; therefore, the parameter is formatted into `Action=DescribeInstances`.

>!
- "Parameter value" is the original value instead of the URL-encoded value.
- If the key of an input parameter contains an underscore, the underscore should be replaced with a `.`; however, underscores in `Value` do not need to be replaced. For example, `Placement_Zone=CN_GUANGZHOU` should be converted to `Placement.Zone=CN_GUANGZHOU`.

Then, concatenate the formatted parameters with `"&"` to generate the request string (ignore the line breaks here):

```shell
Action=DescribeInstances
&InstanceIds.0=ins-09dx96dg
&Nonce=11886
&Region=ap-guangzhou
&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA
&SignatureMethod=HmacSHA256
&Timestamp=1465185768
```

### 3. Concatenating an original signature string
This step generates an original signature string.
The structure of original signature string is as follows:
> **request method + request host + request path + ? + request string**

The parameters are as detailed below:
**Request method:** Both POST and GET methods are supported. GET is used here. Note that the method name should be all capitalized.
* **Request host:** This is the host domain name. Request domain name is determined and varies by the product or product module to which the API belongs. For example, the request domain name for the Tencent Cloud CVM API for querying instance list (DescribeInstances) is `cvm.api.qcloud.com`. For the request domain names of specific products, please see the description of each API.
* **Request path:** Request path for the product to which the TencentCloud API belongs. Each product has a fixed request path. For example, the request path for Tencent Cloud CVM is always `/v2/index.php`.
* **Request string**: the request string generated in the previous step.


The resulting original signature string in the above example is as follows: (ignore the line breaks here):
```shell
GETcvm.api.qcloud.com/v2/index.php?Action=DescribeInstances
&InstanceIds.0=ins-09dx96dg
&Nonce=11886
&Region=ap-guangzhou
&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA
&SignatureMethod=HmacSHA256
&Timestamp=1465185768
```

### 4. Generating a signature string
This step generates a signature string.
>| There are two ways to calculate a signature: HmacSHA256 and HmacSHA1. Here, a signature string is generated based on the specified signature algorithm (i.e., the `SignatureMethod` parameter). The signature will be calculated with the HmacSHA256 algorithm if `SignatureMethod` is specified as HmacSHA256. In other cases, the signature will be calculated with HmacSHA1.

First, create a hash-based message authentication code (HMAC) that uses HmacSHA256 or HmacSHA1 protocol to sign the **original signature string** generated in the previous step, and then Base64-encode the resulting signature.

In this example, the PHP programming language is used to calculate the signature string with **HmacSHA256**. You can use any other programming languages as long as the resulting signature is the same as the one in this example. The sample code is shown as follows:

```php
$secretKey = 'Gu5t9xGARNpq86cd98joQYCN3Cozk1qA';
$srcStr = 'GETcvm.api.qcloud.com/v2/index.php?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Nonce=11886&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA&SignatureMethod=HmacSHA256&Timestamp=1465185768';
$signStr = base64_encode(hash_hmac('sha256', $srcStr, $secretKey, true));
echo $signStr;
```

The final signature string is:

```
0EEm/HtGRr/VJXTAD9tYMth1Bzm3lLHz5RCDv1GdM8s=
```

Similarly, if you specify the signature algorithm as **HmacSHA1**, the code to generate the signature string will be as follows:
```php
$secretKey = 'Gu5t9xGARNpq86cd98joQYCN3Cozk1qA';
$srcStr = 'GETcvm.api.qcloud.com/v2/index.php?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Nonce=11886&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA&SignatureMethod=HmacSHA1&Timestamp=1465185768';
$signStr = base64_encode(hash_hmac('sha1', $srcStr, $secretKey, true));
echo $signStr;
```

The final signature string is:
```
nPVnY6njQmwQ8ciqbPl5Qe+Oru4=
```


## Encoding a Signature String
The generated signature string cannot be directly used as a request parameter and needs to be URL-encoded.
For example, the signature string `0EEm/HtGRr/VJXTAD9tYMth1Bzm3lLHz5RCDv1GdM8s=` generated in the previous step should be encoded to `0EEm%2FHtGRr%2FVJXTAD9tYMth1Bzm3lLHz5RCDv1GdM8s%3D`. Therefore, the resulting request parameter for the `Signature` is `0EEm%2FHtGRr%2FVJXTAD9tYMth1Bzm3lLHz5RCDv1GdM8s%3D`, which will be used to generate the final request URL.

>!If you are sending a GET request, all parameters in the request need to be URL-encoded. Please note that some programming languages may offer automatic URL-encoding, and repeated encoding will cause signature verification failure.

## Authentication Failure
The following errors may occur when authentication fails:

| Error Code | Error Type | Error Description |
|---------|---------|---------|
| 4100 | Authentication failed | Authentication failed. Please make sure that the Signature added to your request is calculated correctly (see steps above as reference) and URL-encoded. |
| 4101 | No API access authorization | The sub-user is not authorized to call this API. Please contact the developer for authorization. For more information, please see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602). |
| 4102 | No authorization to access resources | You are not authorized to access resources used by this API. Please check the relevant resource IDs in the `message` field and contact the developer for authorization. </br>For more information, please see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602). |
| 4103 | Non-developer's `SecretId` cannot be used to call this API | The sub-user's `SecretId` cannot be used to call this API. Only the developer has access to this API. |
| 4104 | SecretId does not exist | The `SecretId` does not exist or the status of `SecretKey` is incorrect. Please make sure that the API key is valid and enabled. |
| 4110 | Authentication failed | Permission verification failed. Please make sure that you have the permission to access the resources. |
| 4500 | Replay attack error | The `Nonce` parameter must be unique, and the difference between `Timestamp` and Tencent server time should not be greater than two hours. |
