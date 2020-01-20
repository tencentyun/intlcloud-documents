
Before a client initiates an upload, it needs to apply to the application's signature distribution server for an upload signature which must be carried during the upload operation, so that VOD can verify whether the upload is authorized.


## Signature Generation Steps

1. **Get TencentCloud API key**
Get the security credentials (i.e., `SecretId` and `SecretKey`) required to call the server API in the following steps:
	1. Log in to the console and select **Cloud Products** > **Cloud Access Management** > **[API Key Management](https://console.cloud.tencent.com/cam/capi)** to enter the "API Key Management" page.
	2. Get the TencentCloud API key. If you have not created a key, click **Create Key** to create a pair of `SecretId` and `SecretKey`.
2. **Splice the plaintext string `original`**
Splice the plaintext signature string `original` based on the format requirement of URL QueryString as shown below:
```
secretId=[secretId]&currentTimeStamp=[currentTimeStamp]&expireTime=[expireTime]&random=[random]
```
>
	- `[secretId]`, `[currentTimeStamp]`, `[expireTime]`, and `[random]` in the above `original` should be replaced with actual parameter values.
	- `original` must contain four required parameters (`secretId`, `currentTimeStamp`, `expireTime`, and `random`) and may contain any number of optional parameters. For more information, please see [Signature Parameters](#p2).
	- The parameter values must be URL-encoded; otherwise, `QueryString` parsing may fail.
3. **Convert the plaintext string into a signature** (with code in Java as an example)
	1. Use the `SecretKey` to encrypt the plaintext string `original` with the [HMAC-SHA1](https://www.ietf.org/rfc/rfc2104.txt) algorithm to get `signatureTmp`:
	```java
	 Mac mac = Mac.getInstance("HmacSHA1");
   SecretKeySpec secretKey = new SecretKeySpec(this.secretKey.getBytes("UTF-8"), mac.getAlgorithm());
   mac.init(secretKey);
	 byte[] signatureTmp = mac.doFinal(original.getBytes("UTF-8"));
	```
	> **`signatureTmp` is a byte array encoded with UTF-8 and encrypted with HMAC-SHA1.**
	2. Encode the plaintext string `original` into a byte array with UTF-8, merge the array with `signatureTmp`, and then [Base64-encode](https://tools.ietf.org/html/rfc4648) the combination to get the signature:
```java
String signature = base64Encode(byteMerger(signatureTmp, original.getBytes("utf8")));
```
> **`byteMerger` and `base64Encode` are methods of array merging and Base64-encoding, respectively. For more information, please see [Sample Code of Signature in Java](https://intl.cloud.tencent.com/document/product/266/33923#java-.E7.AD.BE.E5.90.8D.E7.A4.BA.E4.BE.8B).**

## Example of Signature Generation
VOD also provides **sample code for signature generation** and a signature generator for your reference and verification:
- [Upload from client - sample code for signature generation](https://intl.cloud.tencent.com/document/product/266/33923)
- [Upload from client - signature generator](https://video.qcloud.com/signature/ugcgenerate.html)
- [Upload from client - signature checker](https://video.qcloud.com/signature/ugcdecode.html)
		
	
## <span id ="p2"></span>Descriptions of signature parameters
 
| Parameter Name | Required | Type | Description |
| --- | --- | --- | --- | 
| secretId | Yes | String | `SecretId` in the TencentCloud API key. For more information on how to get it, please see [Guide for Upload from Client - Get TencentCloud API Key](https://intl.cloud.tencent.com/document/product/266/33921#p3). |
| currentTimeStamp | Yes | Integer | Current Unix timestamp. |
| expireTime | Yes | Integer | Unix timestamp for signature expiration. <br/>```expireTime = currentTimeStamp + signature validity period```<br/>The maximum value for signature validity period is 7,776,000 (i.e., 90 days). |
| random | Yes | Integer | A 32-digit unsigned random integer, which is a parameter used to construct a plaintext signature string. |
| classId | No | Integer | Video file category. Default value: 0. | 
|<span id ="p3"></span> procedure | No | String | Subsequent task operation on a video, i.e., after a video file is uploaded, task flow operations will be initiated automatically. This parameter value is a task flow template name. VOD supports [creating task flow templates](https://intl.cloud.tencent.com/document/product/266/14058) and naming the templates. | 
| taskPriority | No | Integer | Priority of subsequent video task (only valid if `procedure` is specified). Value range: [-10, 10]. Default value: 0. | 
| taskNotifyMode | No | String | Notification mode for task flow status change (only valid if `procedure` is specified). <li>Finish: an event notification will be initiated only after the task flow is completely executed. </li><li>Change: an event notification will be initiated as soon as the status of a subtask in the task flow changes. </li><li>None: no callback for the task flow will be accepted. </li>Default value: Finish. | 
| sourceContext | No | String | Source context, which is used to pass through the user request information. The [upload callback](https://intl.cloud.tencent.com/document/product/266/33950) API will return the value of this field. It can contain up to 250 characters. |
| oneTimeValid | No | Integer | Whether a signature is valid only for once. For more information, please see [Guide for Upload from Client - One-time Signature](https://intl.cloud.tencent.com/document/product/266/33921#p4). <br>0 (default value): not enabled; 1: enabled. <br>For relevant error codes, please see [One-time Signature Description](#p1). | 
| vodSubAppId | No | Integer | [Subapplication](https://intl.cloud.tencent.com/document/product/266/33987) ID. If this parameter is left empty, `0`, or your Tencent Cloud `AppId`, the manipulated subapplication will be the "primary application". | 
| sessionContext | No | String | Session context, which is used to pass through the user request information. If the `procedure` parameter is specified, the [task flow status change callback](https://intl.cloud.tencent.com/document/product/266/33953) API will return the value of this field. It can contain up to 1,000 characters. |
| storageRegion | No | String | Specifies the storage region. You can add storage regions in the console by yourself. For more information, please see [Upload Storage Settings](https://intl.cloud.tencent.com/document/product/266/18874). This field should be filled in with a [region abbreviation](https://intl.cloud.tencent.com/document/product/266/33910). |

#### <span id ="p1"></span>One-time signature description

- After the one-time signature feature is enabled, the signature server needs to ensure that the signatures distributed to users are different each time (for example, it should be ensured that the `random` parameters in the signatures distributed at the same time are unique); otherwise, a duplicate signature error will occur.
- If an upload fails due to a signature error, a new signature needs to be obtained for retry.
- The error code for signature errors caused by the SDKs for Android and Java is `1001`.



