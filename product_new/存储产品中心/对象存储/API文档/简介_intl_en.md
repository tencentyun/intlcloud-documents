COS uses XML APIs, which are lightweight, connectionless, and stateless. By calling XML APIs, you can send requests and accept responses directly through HTTP/HTTPS to interact with the COS backend.

Since COS APIs and TencentCloud APIs use different data transfer frameworks, APIs and SDKs provided by COS are independent of TencentCloud APIs and SDKs. You can find more information in [API Operation List](https://intl.cloud.tencent.com/document/product/436/10111) or download SDKs in [SDK Overview](https://intl.cloud.tencent.com/document/product/436/6474). The guides for TencentCloud APIs and corresponding SDKs do not cover the operational features of COS.

>
>- By using Tencent Cloud COS APIs, you acknowledge that you have read and agree to the [Tencent Cloud Terms of Service](https://intl.cloud.tencent.com/document/product/301/9248) and [Tencent Cloud Object Storage Service Level Agreement](https://intl.cloud.tencent.com/document/product/436/6227).
For more information on the regions where COS is available, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224). 
>- Before using the APIs or SDKs to initiate a request, you are recommended to read the [Creating Request Overview](https://intl.cloud.tencent.com/document/product/436/30613) document to learn more about access domain name, authentication, and how to determine whether an access is via private or public network.

## Glossary
Below are some main concepts and terms that may come up in the documentation:
<style rel="stylesheet">
table th:nth-of-type(1) {
width: 150px;	
}
table th:nth-of-type(2) {
width:550px;	
}
</style>

| Name |	 Description |
|---|---|
| APPID| A unique resource ID at the user level owned by a developer accessing COS services, which is used to identify resources |
| SecretId | Developer-owned project ID for identity verification |
| SecretKey	| Developer-owned project key |
| Bucket |	A container used to store data in COS |
| Object |	A specific file stored in COS, which is the basic storage entity |
| Region|Region in domain names such as `ap-beijing`, `ap-hongkong`, and `eu-frankfurt`. For enumerated values, see [Regions and Access Domain Names](https://cloud.tencent.com/document/product/436/6224) |
| ACL |Access Control List, a list of access control information for a specified bucket or object |
| CORS | Cross-origin resource sharing (CORS). <br>This refers to HTTP requests where the origin of the resource that initiates the request is different from the origin of the destination resource |
| Multipart Uploads | Multipart upload mode provided by Tencent Cloud COS service for uploading files in parts |


# Getting Started

Take the following steps to start using COS APIs:

1. Activate the COS service in the [COS Console](https://console.cloud.tencent.com/cos5).
2. Create a bucket in the [COS Console](https://console.cloud.tencent.com/cos5).
3. Obtain the APPID, SecretId, and SecretKey on the [Cloud API Key](https://console.cloud.tencent.com/capi) page in the CAM Console.
4. Write a request signature algorithm program or use a server-side SDK. For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
5. Calculate the signature and call an API to perform an operation.
