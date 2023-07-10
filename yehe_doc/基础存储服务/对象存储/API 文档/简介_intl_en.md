Tencent COS uses XML APIs, which are lightweight, connectionless, and stateless. By calling XML APIs, you can send requests and receive responses directly over HTTP/HTTPS to interact with the COS backend.

COS adopts a data transfer framework different from that of Tencent Cloud. Therefore, APIs and SDKs of COS are independent. For more information, please see the [Operation List](https://intl.cloud.tencent.com/document/product/436/10111) of COS APIs, or download the desired SDKs from [SDK Overview](https://intl.cloud.tencent.com/document/product/436/6474). Note that the guides of Tencent Cloud APIs and the corresponding SDKs do not cover the operations of COS.

>!
>- By using COS APIs, you acknowledge that you have read and agree to the [General Service Level Agreements](https://intl.cloud.tencent.com/document/product/301/12905) and Tencent COS [Service Level Agreement](https://intl.cloud.tencent.com/document/product/436/6227).
>- For more information about the available regions of COS, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). 
>- Before using APIs or SDKs to initiate a request, you are advised to read the [Creating Request Overview](https://intl.cloud.tencent.com/document/product/436/30613) document to learn more about access endpoints, authentication, and how to determine access via a private or public network.
>- For API formats of other Tencent Cloud services, please see [APIs](https://intl.cloud.tencent.com/document/api).



## API Overview

For more information about the APIs supported by COS, please see [Operation List](https://intl.cloud.tencent.com/document/product/436/10111).
<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer (recommended)
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=GetService&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer makes it easy for you to make online API calls, verify signatures, generate SDK code, search for APIs, etc. You can use it to query the request and response of each API call as well as generate sample code for calls.
            </div>
        </div>
    </div>
</div>

## COS Glossary
Terms and concepts you may see when using the APIs are described as follows:
<style rel="stylesheet">
table th:nth-of-type(1) {
width: 150px;	
}
table th:nth-of-type(2) {
width:550px;	
}
</style>

|Name|Description|
|---|---|
| APPID|A unique user-level resource identifier for COS access. It can be obtained at [Manage API Key](https://console.cloud.tencent.com/capi).|
| SecretId | A developer-owned ID used for the project. It can be obtained at [Manage API Key](https://console.cloud.tencent.com/capi).|
| SecretKey| A developer-owned secret key used for the project. It can be obtained at [Manage API Key](https://console.cloud.tencent.com/capi).|
| Bucket | A container used for data storage. For more information, please see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312).|
| BucketName-APPID  | A format used to name the bucket when you use an API or SDK. For example, **examplebucket-1250000000** means the examplebucket belongs to a user with an APPID of 1250000000.   |
| Object | A file stored in COS. It is the basic entity that is stored. |
| ObjectKey | A unique identifier of an object stored in COS. For more information about objects and object keys, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324).|
| Region | Region information. For more information about the enumerated values (such as ap-beijing, ap-hongkong, and eu-frankfurtplease), please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). |
| ACL |Access Control List, a list of access control information for a specified bucket or object. |
| CORS | Cross-origin resource sharing <br>This refers to the HTTP requests for resources from a different endpoint. |
| Multipart Uploads | An upload mode provided by Tencent Cloud COS. |
|  Object Content    |      Binary of the uploaded files. |


## Getting Started

To use the Tencent COS APIs, take the following steps:

1. Activate COS in the [COS console](https://console.cloud.tencent.com/cos5).
2. Create a bucket in the [COS console](https://console.cloud.tencent.com/cos5).
3. In the CAM console, obtain `APPID` at [Manage API Key](https://console.cloud.tencent.com/capi). Then, create `SecretId` and `SecretKey`.
4. Write a request signature algorithm program (or use any server SDK). For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
5. Calculate the signature and call APIs to perform operations.


