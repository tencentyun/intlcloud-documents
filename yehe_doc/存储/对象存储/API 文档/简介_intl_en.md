COS uses XML APIs, which are lightweight, connectionless, and stateless. By calling XML APIs, you can send requests and accept responses directly through HTTP/HTTPS to interact with the COS backend.

Since COS APIs and TencentCloud APIs use different data transfer frameworks, APIs and SDKs provided by COS are independent of TencentCloud APIs and SDKs. You can find more information in [Operation List](https://intl.cloud.tencent.com/document/product/436/10111) or download SDKs in [SDK Overview](https://intl.cloud.tencent.com/document/product/436/6474) as needed. The guides for TencentCloud APIs and corresponding SDKs do not cover the operational features of COS.

>!
>- By using Tencent Cloud COS APIs, you acknowledge that you have read and agree to the [General Service Level Agreements](https://intl.cloud.tencent.com/document/product/301/12905) and [Service Level Agreement](https://intl.cloud.tencent.com/document/product/436/6227).
>- For more information on the regions where COS is available, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). 
>- Before you use the APIs or SDKs to initiate requests, we recommend you read the [Creating Request Overview](https://intl.cloud.tencent.com/document/product/436/30613) document to learn more about access endpoints, authentication, and how to determine whether an access request is over the private or public network.



## API Overview

For the APIs supported by COS, please see [Operation List](https://intl.cloud.tencent.com/document/product/436/10111).


## Glossary
When using the APIs, you may see some key concepts and terms as detailed below:
<style rel="stylesheet">
table th:nth-of-type(1) {
width: 150px;	
}
table th:nth-of-type(2) {
width:550px;	
}
</style>

| Name | 	Description |
|---|---|
| APPID	| `APPID` of your Tencent Cloud account, which is a unique user-level resource identifier used to access COS and can be obtained on the [API Key Management](https://console.cloud.tencent.com/capi) page in the console. |
| SecretId | Your project ID, which is used for authentication and can be obtained on the [API Key Management](https://console.cloud.tencent.com/capi) page in the console. |
| SecretKey	| Your project key, which can be obtained on the [API Key Management](https://console.cloud.tencent.com/capi) page in the console. |
| Bucket | A bucket is a container used to store data in COS. For more information, please see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). |
| Object | An object is a specific file stored in COS, which is the basic entity of storage. |
| ObjectKey | An object key is the unique ID of an object in a bucket. For more information on object and object key, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). |
| Region | Region information such as ap-beijing, ap-hongkong, and eu-frankfurt. For enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). |
| ACL |	 An access control list (ACL) is a list of access control information for a specified bucket or object. |
| CORS | Cross-origin resource sharing (CORS) refers to HTTP requests where the origin of the resource <br>that initiates the request is different from the origin of the destination resource. |
| Multipart Uploads | Multipart upload mode provided by COS for uploading files in multiple parts |

## Getting Started

Take the following steps to start using COS APIs:

1. Activate the COS service in the [COS Console](https://console.cloud.tencent.com/cos5).
2. Create a bucket in the [COS Console](https://console.cloud.tencent.com/cos5).
3. Get the `APPID` and create `SecretId` and `SecretKey` on the [API Key Management](https://console.cloud.tencent.com/capi) page in the CAM Console.
4. Write a request signature algorithm program or use a server SDK. For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
5. Calculate the signature and call an API to perform an operation.