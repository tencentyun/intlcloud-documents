## Overview

This document provides an overview of APIs and SDK code samples for file processing in CI.

| API | Description |
| ------------------------------------------------------------ | ------------------ |
| [Generating a sync file-to-image preview URL](https://intl.cloud.tencent.com/document/product/1045/47929) | Generates a sync file-to-image preview URL. |
| [Generating a sync file-to-HTML preview URL](https://www.tencentcloud.com/document/product/1045/47938) | Generates a sync file-to-HTML preview URL. |

## Basic operations

### Sync file-to-image/HTML preview

#### Feature description

This API is used to generate a sync file-to-image/HTML preview URL by using different parameters.

#### Method prototype

```java
String GenerateDocPreviewUrl(DocHtmlRequest docJobRequest);
```

#### Parameter description

`DocHtmlRequest` has the following sub-nodes:

| Node Name (Keyword) | Description | Type | Required |
| ------------------| -------------------------------------------------------- | --------- |  --------- |
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| objectKey          | Name of the image file in the COS bucket. The COS bucket is specified by `Host`. For example, if the file is `img.jpg` in the `test` directory in the `examplebucket-1250000000` bucket in Beijing, then `Host` is `examplebucket-1250000000.cos.ap-beijing.myqcloud.com`, and `ObjectKey` is `test/img.jpg`. | String | Yes |
| srcType    | Source data type. Currently, the file conversion feature determines the source data type according to the file extension of the COS object. If the object has no extension, you can set this value. | String | No       |
| page | Number of the page to be converted, which is counted from 1 by default. For spreadsheets, `page` indicates to convert the xth image in the xth sheet. | Int | No |
| dstType | Type of the output target file. Valid values: <ul  style="margin: 0;"><li>`png` (converts to .png image) </li><li>`jpg` (converts to .jpg image) </li><li>`pdf` (converts to .pdf file, where the page number cannot be selected, and the `page` parameter does not take effect.) </li><li>`html` (converts to HTML online file) <br/>If the input file format cannot be recognized, the `jpg` format will be used by default. The default value for the SDK is `html`.</li></ul> | String | No |
| password | Password to open the Office file. If you need to convert a password-protected file, set this field. | String | No |
| comment    | Whether to hide comments and apply track changes. Default value: `0`. <ul  style="margin: 0;"><li>`0`: Hide comments and apply track changes. </li><li>`1`: Show comments and track changes. </li></ul>               | Int  | No       |
| ImageParams | Processing parameters for the output image. All parameters of [basic image processing](https://www.tencentcloud.com/document/product/1045/33694) are supported. To specify multiple parameters, separate them with [pipeline operators](https://intl.cloud.tencent.com/document/product/1045/33727). In this way, the image can be processed by multiple parameters in sequence in the same request.  | String | No       |
| quality | Quality of the generated preview image. Value range: [1, 100]. Default value: `100`. For example, if the value is `100`, the quality of the generated image will be 100%. | Int | No |
| scale       | Scaling parameter of the preview image. Value range: [10, 200]. Default value: `100`. For example, if the value is `200`, the image will be scaled up (enlarged) by 200%.                | Int  | No       |
| imageDpi    | Renders the image based on the specified DPI. This parameter works together with `scale`. Value range: 96–600. Default value: `96`. The width of the output image must be less than 65500 px. | Int | No |


#### Response description

- Success: The preview URL is returned.
- Failure: An error (such as the bucket does not exist) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

```java
//1. Create a request object
DocHtmlRequest request = new DocHtmlRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("markjrzhang-1251704708");
// For conversion to image, `dstType` is `DocHtmlRequest.DocType.jpg`.
request.setDstType(DocHtmlRequest.DocType.html);
request.setObjectKey("1.pptx");
request.setPage("1");
//3. Call the API to get the job response object
String previewUrl = client.GenerateDocPreviewUrl(request);
System.out.println(previewUrl);
```
