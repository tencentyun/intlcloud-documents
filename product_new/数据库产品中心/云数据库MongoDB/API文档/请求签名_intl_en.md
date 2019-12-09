>This is a legacy API and may be deprecated in the future. It is currently not displayed on the left sidebar. We recommend using [CVM API v3.0](https://intl.cloud.tencent.com/document/api/213/15689), which is more standardized and has much lower access latency.

TencentCloud API authenticates each access request, so each request is required to include the Signature in the common request parameters for user authentication. The signature is generated with the user’s security credentials, which consist of a SecretId and a SecretKey. Users who have no security credentials can apply for one on Tencent Cloud official website; otherwise, you will not be able to call TencentCloud API.

## Applying for Security Credentials
Before using TencentCloud API for the first time, you need to apply for security credentials in **Tencent Cloud Console** > **[API Key Management](https://console.cloud.tencent.com/cam/capi)**. Security credentials consist of a SecretId and a SecretKey.

- **SecretId** is the identity of the requester.
- **SecretKey** is used to encrypt the strings to create a signature so that Tencent Cloud server can validate the identity of the requester.

>SecretKeys are very important. With this credential, you can access and manage the resources in your Tencent Cloud account via API. For security reasons, please keep your keys safe and rotate them regularly, and make sure you delete the old key when a new one is created.


#### How to apply for security credentials

1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com/).
2. Click **Products** and select **Security Credentials** under **Management Tools** to go to the TencentCloud API Key Management page.
![](https://main.qcloudimg.com/raw/2b7614eb462ebe5696276453e35bea5a.png)
3. On the [API Key Management](https://console.cloud.tencent.com/capi) page, click **Create Key** to create a pair of SecretId/SecretKey.

>- A developer account can have up to two pairs of SecretIds/SecretKeys.
> - A developer can add a QQ account as a sub-user and use it to apply for different security credentials in multiple developer consoles
> - A sub-user can only call the specified Tencent Cloud APIs with its security credential.

## Generating a Signature String
After obtaining the security credentials (SecretId and SecretKey), you can generate a signature.

![](https://main.qcloudimg.com/raw/8ee1112aa861f897ddf193ac7490064d.png)

Assume that the SecretId and SecretKey are:
SecretId: AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA
SecretKey: Gu5t9xGARNpq86cd98joQYCN3Cozk1qA

>This example is for demonstration purposes only. Make sure that you proceed with your actual SecretId, SecretKey, and request parameters.

For example, when you call Tencent Cloud CVM's API [Viewing Instance List](https://intl.cloud.tencent.com/document/product/213/9388) (DescribeInstances), the request parameters are as follows:

| Parameter Name | Description | Parameter value |
|---------|---------|---------|
| Action | Method name | DescribeInstances |
| SecretId | Key ID | AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA |
| Timestamp | Current timestamp | 1465185768 |
| Nonce | Random positive integer | 11886 |
| Region | Region where the instance is located | ap-guangzhou |
| SignatureMethod | Signature method | HmacSHA256 |
| InstanceIds.0 | ID of the instance to be queried | ins-09dx96dg |

### 1. Sorting Parameters
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
Any other programming language can be used to sort these parameters as long as the same result is produced.

### 2. Generating Request String
This step generates a request string.
Assign values to the parameters (see the previous step)  by following the logic`"parameter name"="parameter value"`. For example, if the value of `"Action"` is `"DescribeInstances"`, then `Action=DescribeInstances`.

- "Parameter value" is the original value, instead of the URL encoded value.
- If the key of an input parameter contains an underscore, the underscore should be replaced with a `.`; however, underscores in the value do not need to be replaced. For example, `Placement_Zone=CN_GUANGZHOU` should be converted to `Placement.Zone=CN_GUANGZHOU`.

Then, concatenate the formatted parameters with `"&"` to generate the request string (ignore the link breaks here):

```shell
Action=DescribeInstances
&InstanceIds.0=ins-09dx96dg
&Nonce=11886
&Region=ap-guangzhou
&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA
&SignatureMethod=HmacSHA256
&Timestamp=1465185768
```

### 3. Concatenating a Signature Original String
This step generates a signature original string.
The structure for a signature original string is as follows:
> **request method + request host + request path + ? + request string**

The parameters are as detailed below:
**Request method:** Both POST and GET methods are supported. GET is used here. Note that the method name should be in all capital letters.
* **Request host:** This is the host domain name. Request domain name is determined by the product or product module to which the API belongs. For example, the request domain name for the Tencent Cloud CVM API for querying instance list (DescribeInstances) is: `cvm.api.qcloud.com`. For the request domain names of specific products, see the description of each API.
**Request path:** The request path for the product to which the Tencent Cloud API belongs. Each product has a fixed path. For example, the request path for Tencent Cloud CVM is always `/v2/index.php`.
* **Request string:** This is the request string generated in the previous step.


The resulting original signature string in the above example is as follows (ignore the line breaks in the text):
```shell
GETcvm.api.qcloud.com/v2/index.php?Action=DescribeInstances
&InstanceIds.0=ins-09dx96dg
&Nonce=11886
&Region=ap-guangzhou
&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA
&SignatureMethod=HmacSHA256
&Timestamp=1465185768
```

### 4. Generating Signature String
This step generates a signature string.
>There are two ways to calculate a signature: HmacSHA256 and HmacSHA1. Here, a signature string is generated based on the specified signature algorithm (i.e., the `SignatureMethod` parameter). The signature will be calculated with the HmacSHA256 algorithm if `SignatureMethod` is specified as HmacSHA256. In other cases, the signature will be calculated with HmacSHA1.

First, create a hash-based message authentication code (HMAC) that uses HmacSHA256 or HmacSHA1 protocols to sign the string from the previous step, then encode the resulting signature to Base64.

In this example, we use PHP language and calculate the signature using **HmacSHA256** (Note: you can use any other programming languages as long as the resulting signature is the same as the one in this example). The sample code is shown as follows:

```php
$secretKey = 'Gu5t9xGARNpq86cd98joQYCN3Cozk1qA';
$srcStr = 'GETcvm.api.qcloud.com/v2/index.php?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Nonce=11886&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA&SignatureMethod=HmacSHA256&Timestamp=1465185768';
$signStr = base64_encode(hash_hmac('sha256', $srcStr, $secretKey, true));
echo $signStr;
```

The final signature is:

```
0EEm/HtGRr/VJXTAD9tYMth1Bzm3lLHz5RCDv1GdM8s=
```

Similarly, if you specify the signature algorithm as **HmacSHA1**, the code to generate the signature string is as follows:
```php
$secretKey = 'Gu5t9xGARNpq86cd98joQYCN3Cozk1qA';
$srcStr = 'GETcvm.api.qcloud.com/v2/index.php?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Nonce=11886&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA&SignatureMethod=HmacSHA1&Timestamp=1465185768';
$signStr = base64_encode(hash_hmac('sha1', $srcStr, $secretKey, true));
echo $signStr;
```

The final signature is:
```
nPVnY6njQmwQ8ciqbPl5Qe+Oru4=
```


## Encoding Signature String
The signature must be URL encoded.
For example, the signature string `0EEm/HtGRr/VJXTAD9tYMth1Bzm3lLHz5RCDv1GdM8s=` generated in the previous step should be encoded to `0EEm%2FHtGRr%2FVJXTAD9tYMth1Bzm3lLHz5RCDv1GdM8s%3D`. Therefore, the resulting request parameter for the signature string (`Signature`) is `0EEm%2FHtGRr%2FVJXTAD9tYMth1Bzm3lLHz5RCDv1GdM8s%3D`, which will be used to generate the final request URL.

>If you are sending a GET request, all parameters in the request need to be URL encoded.  Please note that some languages may offer auto-URL encoding, and repeated encoding will cause signature verification failure.

## Authentication Failure
The following errors may occur when authentication fails:

| Error Code | Error Type | Error Description |
|---------|---------|---------|
| 4100 | Authentication failed | Make sure the signature added to your request is calculated correctly (see steps above as reference) and  URL encoded.
| 4101 | No API access authorization | The sub-user is not authorized to call this API. Please contact the developer for authorization. |
| 4102 | No authorization to access resources | You are not authorized to access resources used by this API. Check the relevant resource IDs in the `message` field and contact the developer for authorization. </br> |
| 4103 | Non-developer's SecretId cannot be used to call this API | The sub-user's SecretId cannot be used to call this API. Only the developer has the access to this API. |
| 4104 | SecretId does not exist | The SecretId does not exist, or the status of SecretKey is incorrect. Please make sure that the API key is valid and enabled. |
| 4110 | Authentication failed | Permission verification failed. Please make sure that you are granted the permission to access the resources. |
| 4500 | Replay attack error | Please note that the `Nonce` parameter must be unique, and the difference between `Timestamp` and Tencent server time should not be greater than 2 hours. |
