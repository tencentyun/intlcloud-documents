## Feature Overview

By using the JS-SDK, you can customize capabilities such as UI, page status, and event listener to deliver a better webpage experience.


## Architecture
![](https://qcloudimg.tencent-cloud.cn/raw/32602ffb3049da778e94b078c25fd967.png)


## Operating Environments

| Platform        | Supported Browsers                                                         | 
| ----------- | ------------------------------------------------------------ | 
| iOS   | Safari, QQ built-in browser, QQ Mini Program, WeChat built-in browser, and WeChat Mini Program                         | 
| Android  | QQ built-in browser, QQ Mini Program, WeChat built-in browser, and WeChat Mini Program                 | 
| Windows   | Chrome, QQ Browser (non-compatibility mode), Edge, Firefox, and Internet Explorer 11      |       
| macOS   | Chrome, Safari, QQ Browser, Edge, and Firefox      |  


## Instructions

### 1. Download a package

Download the latest version of the [JS-SDK package](https://cos-doc-preview-js-sdk-1253960454.file.myqcloud.com/sdk-v0.1.1.zip). For earlier versions, see [Release Notes](https://www.tencentcloud.com/document/product/1045/47943).


### 2. Import the JS-SDK

On the page that needs to call the JS-SDK, import it as follows. In the sample code, `${version}` indicates the version number and should be replaced with the actual version number of your downloaded package.
```plaintext
<script src="sdk-${version}.js"></script>
```

### 3. Get the online file preview URL


#### Option 1. Use the JS-SDK (on v0.1.1 or later) to get

Use the JS-SDK (on v0.1.1 or later) to get the online file preview URL as follows:

```plaintext
var url = await COSDocPreviewSDK.getPreviewUrl( {
      objectUrl: 'https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/test.pptx',
      credentials: {      // If the preview file is private, the request needs to carry the access credential.
          secretId: '',
          secretKey: '',
          authorization: 'q-sign-algorithmxxxxxxxxxxxxxxx',
      },
      copyable: 0,  // Whether the file content can be copied
      htmlwaterword: ''  // Watermark content
})
console.log(url)
```

The configuration items are described as follows:

| Configuration Item  | Description                                                                | Required |  
| ------------- | --------------------------------------------------------------------- | -------- | 
|    objectUrl       | The URL of the object that needs to be previewed, such as `https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/test.pptx`. | Yes      | 
|      credentials     | If the object to be previewed is private, you need to pass in `credentials` as the access credential. You can pass in the calculated [request signature](https://intl.cloud.tencent.com/document/product/1045/33452) (`authorization`) or your `secretId` and `secretKey` (not recommended as placing a permanent key on the frontend has security risks). | No      | 
|     credentials.authorization      | Object download signature. For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/1045/33452). | No      | 
|     credentials.secretId      | Your `secretId`, which can be obtained on the [Manage API Key](https://console.cloud.tencent.com/cam/capi) page in the CAM console. | No      | 
|      credentials.secretKey     | Your `secretKey`, which can be obtained on the [Manage API Key](https://console.cloud.tencent.com/cam/capi) page in the CAM console. | No      |
| copyable          | Whether the file content is copyable. Valid values: `1` (yes), `0` (no).     | No      | 
| htmlwaterword          | Watermark text, which must be URL-safe Base64-encoded as described in [FAQs](https://intl.cloud.tencent.com/document/product/1045/33430) and is empty by default.     | No      | 
| htmlfillstyle          | Watermark RGBA (color and transparency), which must be URL-safe Base64-encoded as described in [FAQs](https://intl.cloud.tencent.com/document/product/1045/33430) and is `rgba(192,192,192,0.6)` by default.  | No      | 
| htmlfront          | Watermark text style, which must be URL-safe Base64-encoded as described in [FAQs](https://intl.cloud.tencent.com/document/product/1045/33430) and is `bold 20px Serif` by default.    | No      | 
| htmlrotate          | Rotation angle in degrees. Value range: 0–360. Default value: `315`. | No | 
| htmlhorizontal          | Horizontal spacing of the watermark text in px. Default value: `50`. | No | 
| htmlvertical          | Vertical spacing of the watermark text in px. Default value: `100`. | No | 


#### Option 2. Directly request to get

##### Sample request

```plaintext
GET /<ObjectKey>?ci-process=doc-preview&dstType=html&weboffice_url=1&sign=AuthString HTTP/1.1 HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
```


##### Request parameters

| Parameter  | Description                                                                | Required |  
| ------------- | --------------------------------------------------------------------- | -------- | 
| ci-process    | Preview parameter, which is fixed at `doc-preview`.                                 | Yes      |  
| dstType       | Preview type. To generate HTML files for preview, enter `html`.        | Yes      |  
| weboffice_url | Whether to get the preview URL. Valid values: `1` (return the preview URL and token information); `2` (return the token information only). If this parameter is not specified, the file will be directly previewed. | No      |  
| tokenuid | Whether to get the token. A token will be generated and returned along with its validity period based on the information passed in such as `tokenuid` and file information. If this parameter is not specified, the token information won't be returned. | No      |  
| sign          | Object download signature, which must be URL-encoded. If the previewed object is privately readable, the signature needs to be passed in. </br>For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/1045/33452). | No      | 
| copyable          | Whether the file content is copyable. Valid values: `1` (yes), `0` (no).     | No      | 
| htmlwaterword          | Watermark text, which must be URL-safe Base64-encoded as described in [FAQs](https://intl.cloud.tencent.com/document/product/1045/33430) and is empty by default.     | No      | 
| htmlfillstyle          | Watermark RGBA (color and transparency), which must be URL-safe Base64-encoded as described in [FAQs](https://intl.cloud.tencent.com/document/product/1045/33430) and is `rgba(192,192,192,0.6)` by default.  | No      | 
| htmlfront          | Watermark text style, which must be URL-safe Base64-encoded as described in [FAQs](https://intl.cloud.tencent.com/document/product/1045/33430) and is `bold 20px Serif` by default.    | No      | 
| htmlrotate          | Rotation angle in degrees. Value range: 0–360. Default value: `315`. | No | 
| htmlhorizontal          | Horizontal spacing of the watermark text in px. Default value: `50`. | No | 
| htmlvertical          | Vertical spacing of the watermark text in px. Default value: `100`. | No | 


##### Sample response

```plaintext
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 478
Date: Thu, 25 Feb 2021 07:44:37 GMT
Status: 200 OK
x-cos-request-id: NjAzNzU1NjVfY2MxZTIzMDlfNzc5NF8yMDQ5****



{
        "PreviewUrl": "https://prvsh.myqcloud.com/office/p/xxxx?_w_provider=XXX"
}
```


### 4. Initialize

During initialization, the JS-SDK will create an iframe under the configured mount node and automatically initialize relevant data and events.
```plaintext
var demo = COSDocPreviewSDK.config({
    url: 'Online file preview URL',  // The online preview URL of the file obtained in step 3
})
// If special processing needs to be performed on the iframe, you can get the DOM object of the iframe as follows:
console.log(demo.iframe)
// File open result
demo.on('fileOpen', function(data) {
    console.log(data.success)
})
```

### 5. Configure the mount node

The mount node is the node mounted when the JS-SDK inserts the iframe. It is configurable during initialization.
```plaintext
<div class="custom-mount"></div>
```
```plaintext
var demo = COSDocPreviewSDK.config({
    url: 'Online file preview URL',    // The online preview URL of the file obtained in step 3
    mount: document.querySelector('.custom-mount')    // Mount node. By default, the `body` node will be mounted to. You can customize the mount node as needed.
})
```
After initialization is completed, the JS-SDK will automatically insert an iframe under the mount node.
```plaintext
<div class="custom-mount">
    <iframe src="..."></iframe>
</div>
```

### 6. Authenticate the token
If no token is used, the signature validity period will be used for authentication by default. Once the signature expires, the file cannot be previewed.
If a token is used for authentication, token authentication and refresh can be performed continuously during preview, and you can control the preview authorization on your own.

![](https://qcloudimg.tencent-cloud.cn/raw/e6063d46f22aa3931a0b61084b698e0b.png)

Token authentication and renewal can be completed in the following three steps. For more information, see the [demo](https://github.com/tencentyun/cos-demo/blob/main/doc-preview/token-refresh-preview.html).


<span id="token"></span>
1. Get the token.
**Request sample**
```plaintext
GET /<ObjectKey>?ci-process=doc-preview&dstType=html&weboffice_url=2&tokenuid=test&sign=AuthString HTTP/1.1 HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
```
**Sample Response**
```plaintext
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 108
Date: Tue, 21 Jun 2022 10:41:10 GMT
Status: 200 OK
x-cos-request-id: NjJiMWEwNDZfMTgyMjYyNjRfYmRlYl9iNTAw****



{
    Token: "ChAJj2vNRiHTc8reToMmJ7T2EJ7FxpUGGhS1mPJanpN03u8PSB17/YKBA/Vo****"
    TokenExpireTime: "1655808670"
}
```
2. Set the token.
>? To avoid frequent token refresh, we recommend you set `timeout` to over 10 minutes. To prevent the refresh request from timing out, the JS-SDK will refresh the token several minutes in advance.
>

```plaintext
var demo = COSDocPreviewSDK.config({
    url: 'Online file preview URL',  // The online preview URL of the file obtained in step 3
})
// Set the token
demo.setToken({
  token: 'yourToken', // Enter the obtained token
  timeout: 10 * 60 * 1000, // Timeout period of the token in milliseconds. To avoid frequent refresh, we recommend you set it to over 10 minutes. The JS-SDK will call the token refresh method `refreshToken` before timeout.
});
```

3. Configure the `refreshToken` method to automatically refresh the token upon timeout.
The `refreshToken` method needs to request the **token refresh method encapsulated on your server**. The server can encapsulate the above token acquisition method (for more information, see [Get the token](#token)).
Taking the server method `http://your.server.com/refreshToken` as an example, configure `refreshToken` as follows:


```plaintext
// Get the token
const refreshToken = () => {
  // Call the method encapsulated on the server to get the token information
  const tokenInfo = await $.get('http://your.server.com/refreshToken')

  // `Promise` or `return { token, timeout }` can be returned.
  return {
    token: tokenInfo.token, // The token to be set, which is required.
    timeout: 10 * 60 * 1000, //  The token timeout period in milliseconds, which is required.
  };
};

var demo = COSDocPreviewSDK.config({
    url: 'Online file preview URL',  
    refreshToken    // Automatic token refresh method
})

// Set the token
demo.setToken({
  token: 'yourToken', // Enter the obtained token
  timeout: 10 * 60 * 1000   // Token timeout period in milliseconds
});

```

## Examples

- For the sample code of online preview of a text file, see the DOC file preview demo at [GitHub](https://github.com/tencentyun/cos-demo/blob/main/doc-preview/doc-to-html-preview.html).
- For the sample code of online preview of a presentation file, see the PPT file preview demo at [GitHub](https://github.com/tencentyun/cos-demo/blob/main/doc-preview/ppt-to-html-preview.html).
- For the sample code of online preview of a spreadsheet file, see the Excel file preview demo at [GitHub](https://github.com/tencentyun/cos-demo/blob/main/doc-preview/xls-to-html-preview.html).
- For the sample code of online preview of a PDF file, see the PDF file preview demo at [GitHub](https://github.com/tencentyun/cos-demo/blob/main/doc-preview/pdf-to-html-preview.html).
- For the sample code of token authentication and renewal, see the token authentication and renewal demo at [GitHub](https://github.com/tencentyun/cos-demo/blob/main/doc-preview/token-refresh-preview.html).
