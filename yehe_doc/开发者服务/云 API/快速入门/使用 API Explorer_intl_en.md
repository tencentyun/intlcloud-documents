[TencentCloud API Explorer](https://console.cloud.tencent.com/api/explorer) is an automated tool for API call. It currently supports various [Tencent Cloud services](https://intl.cloud.tencent.com/product) such as CVM, VPC, and CBS. Specifically, it can automatically generate SDK code and signature strings in Java, Python, Node.js, PHP, Go and .NET, call APIs online, and send real requests, making SDKs easier to use.



## API Explorer Details

This document describes API Explorer in detail as shown below in order from left to right:
![](https://main.qcloudimg.com/raw/e18e0e4ef4a1dc7d1237881c5ede2f5d.png)

1. **Service area**: all currently supported Tencent Cloud services are listed here.
2. **Service API area**: all feature APIs that are supported under the current service are listed here.
3. **API name**: the name of the selected API is displayed here.
4. **Service version**: there are certain differences between service versions. For more information, please see the API documentation of the specific service. The figure below shows the CVM API version 2017-03-12.
5. **Key pair (`SecretId` and `SecretKey`)**: enter the security credentials of the account, which can be obtained by clicking **View Key**.
>!The API key represents your account identity and granted permissions, which is equivalent to your login password. Do not disclose it to others.
>
6. **Parameters required by signature**: click **More Options** to view the parameters required by various features such as signature string generation and verification. The required parameters may vary by service. For more information, please see the API documentation of the specific service. The parameters required by CVM signature are as follows:
 - **Timestamp (valid only when the generated signature string is verified)**: current UNIX timestamp accurate down to the second, which records when an API request is initiated.
   `Timestamp` must be the same as your current system time, and your system time must be in sync with the UTC time. If the difference between the timestamp and your current system time is greater than five minutes, the request will fail. If your system time is out of sync with the UTC time for a prolonged period, the request will fail, and a signature expiration error will be returned.
 - **Token (valid only when the generated signature string is verified)**: it is used to authenticate the user. The requirements of this parameter may vary by service. If necessary, the way of getting it will be specified. For more information, please see the API documentation of the specific service.
 - **Request method (valid only when the generated signature string is verified)**: a request uses the POST method by default. You can choose an appropriate method according to the specific API document.
 - **Endpoint (valid only when the generated signature string is verified)**: select the access region. Nearby access is used by default.
7. **Parameters required by API**: only the parameters required by the API are displayed, and you can check "View Only Required Parameters" to filter the parameters. The specific parameter description can be viewed by selecting **Parameter Description** on the right.
8. **Feature area**:
 - **Code Generation**: this feature can automatically generate code in multiple languages to make the API easier to use.
 - **Online Call**: after entering the parameters, select **Send Request**, and the system will send the parameters you entered on the left to the corresponding API. This is a real operation, and the system will display related information such as the request result and response headers.
 - **Signature Generation**: this feature can be used to automatically generate signature strings. API 3.0 v3 version is used by default, and you can choose other versions as needed as shown below:
   ![](https://main.qcloudimg.com/raw/3a9c9672e33e26924e4b0b7298ef74e0.png)
9. **Subfeature area**: you can switch languages to generate corresponding code.
10. **Response area**: response information such as the generated code and request result is displayed here.
11. **SDK usage guide**: for more information on the SDK, such as the required environment and sample call, please see the corresponding SDK usage guide.



## Calling API

This document uses the [DescribeZones](https://intl.cloud.tencent.com/document/product/213/35071) API as an example. To use API Explorer to call it, please:

1. Get the private key (`SecretId` and `SecretKey`) and enter them in corresponding fields.
2. Enter the required parameters. You can select **Parameter Description** in the feature area on the right to view the parameters of the specific API.
3. Select **Online Call** > **Send Request** in the feature area on the right and view the request result in the response area.



## Generating signature string

This document uses the [DescribeZones](https://intl.cloud.tencent.com/document/product/213/35071) API as an example. To use API Explorer to generate a signature string, please:

1. Get the private key (`SecretId` and `SecretKey`) and enter them in corresponding fields.
2. (Optional) Enter the parameters required by the signature as needed. If you leave them empty, the system will automatically enter them when generating the signature string.
3. Enter the parameters required by the API. You can select **Parameter Description** in the feature area on the right to view the parameters of the specific API.
4. Select **Signature Generation** > **Generate Signature** in the feature area on the right and view the signing steps and result in the response area.

## FAQs

### How do I use the tool to verify API signatures?

When you encounter the following error message, you can use API Explorer to verify the signature:

```
[TencentCloudSDKException] code:AuthFailure.SecretIdNotFound message:The SecretId is not found, please ensure that your SecretId is correct. requestId:234a93fe-9024-488e-87a8-48e4f3c3548e
```

1. Enter the parameters in API Explorer. Please use variable parameters such as `Timestamp` the same as those used in the incorrect API signature to be verified, and select **Signature Generation** > **Generate Signature** in the feature area.
2. After getting the signing steps and result in the response area, you can compare the data before and after.


### Signature error

If an error occurs during the signing process, the following error codes may be returned. Please resolve the error accordingly:

<table>
<tr>
<th>Error Code</th><th>Error Description</th>
</tr>
<tr>
<td><code>AuthFailure.SignatureExpire</code></td><td>The signature expired.</td>
</tr>
<tr>
<td><code>AuthFailure.SecretIdNotFound</code></td><td>The key does not exist.</td>
</tr>
<tr>
<td><code>AuthFailure.SignatureFailure</code></td><td>Signature error.</td>
</tr>
<tr>
<td><code>AuthFailure.TokenFailure</code></td><td>Token error.</td>
</tr>
<tr>
<td><code>AuthFailure.InvalidSecretId</code></td><td>Invalid key (not TencentCloud API key type).</td>
</tr>
</table>




## Contact Us

- If you encounter any problems during use, you can give us your feedback by selecting **Feedback** in the feature area.
- You can also click <img src="https://main.qcloudimg.com/raw/0a0610eb176a4e0d07eb9b902381c5fc.png" style="margin:-6px 0px"> in the bottom-right corner to query related information in the "Help Center".
