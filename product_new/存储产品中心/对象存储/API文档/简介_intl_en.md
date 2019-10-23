COS uses lightweight and connectionless XML APIs. By calling such APIs, you can directly send requests and accept responses through HTTP/HTTPS to interact with the COS backend.

As different data transfer frameworks are used, COS provides APIs independent of TencentCloud API and standalone SDKs. You can find more information about them in [API Operation List](https://intl.cloud.tencent.com/document/product/436/10111) or download the required SDK in [SDK List](https://intl.cloud.tencent.com/document/product/436/6474). The guides for TencentCloud APIs and corresponding SDKs do not describe the operational features of COS.

>
>- By using Tencent Cloud COS APIs, you have read and agreed to the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248) and [Tencent Cloud Object Storage Service Level Agreement](https://intl.cloud.tencent.com/document/product/436/6227).
For more information on the regions where COS is available, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) 
>- Before using the APIs or SDK to initiate a request, you are recommended to read the [Creating Request Overview](https://intl.cloud.tencent.com/document/product/436/30613) document to learn more about concepts related to request initiation such as domain name and authentication as well as access checks on private and public networks.
>- COS offers two different editions of APIs: XML and JSON. The two editions have different API protocols, but they can access the same data.
>- Tencent Cloud recommends the XML APIs, as legacy JSON APIs no longer provide new features rolled out after 2018.

## Glossary
Below are some main concepts and terms in the documents:
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
| APPID	| A unique resource ID at the user level owned by a developer when accessing COS services, which is used to identify resources |
| SecretId | Developer-owned project ID for authentication purpose |
| SecretKey	| Developer-owned project key |
| Bucket |	A container used to store data in COS |
| Object |	A specific file stored in COS, which is the basic storage entity |
| Region|	Region in the domain name such as ap-beijing, ap-hongkong, and eu-frankfurt. For the enumerated values, see [Available Regions](https://intl.cloud.tencent.com/document/product/436/6224) |
| ACL |	Access Control List, which refers to the access control information list of the specified bucket or object |
| CORS | Cross-origin resource sharing (CORS). <br>This refers to HTTP requests where the origin of the resource that initiates the request is different from the origin of the resource pointed to by the request |
| Multipart Uploads | Multipart upload mode provided by Tencent Cloud COS service for uploading files in parts |


# Getting Started

To use COS APIs, you need to follow these steps first:

1. Activate the COS service in the [COS Console](https://console.cloud.tencent.com/cos5).
2. Create a bucket in the [COS Console](https://console.cloud.tencent.com/cos5).
3. Obtain the APPID, SecretId, and SecretKey on the [Cloud API Key](https://console.cloud.tencent.com/capi) page in the CAM Console.
4. Write a request signature algorithm program (or use any server-side SDK). For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
5. Calculate the signature and call an API to perform an operation.
