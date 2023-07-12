## Overview

This document provides an overview of the API and sample code for getting an object access URL.

## Getting an Object Access URL

#### Feature description

This API is used to query the URL to access an object. This API does not verify whether the object exists or not.

> ?
>
> - To make the generated object URL a preview URL instead of a download URL, concatenate the `response-content-disposition=inline` parameter to the end of the obtained URL.
> - To make the generated object URL a download URL instead of a preview URL, concatenate the `response-content-disposition=attachment` parameter to the end of the obtained URL.
> - To rename a file during download, concatenate the `filename=(custom file name)` parameter to the end of the obtained URL.
> - If you use a temporary key to generate a pre-signed URL, make sure that the `"name/cos:GetObject"` permission has been added to the `action` for applying for a temporary key.

#### Sample code

Getting the download URL:

[//]: # (.cssg-snippet-get-presign-download-url)

```js
cos.getObjectUrl(
  {
    Bucket: 'examplebucket-1250000000', // Your bucket name. Required. //
    Region: 'COS_REGION', // Bucket region (required), such as ap-beijing //
    Key: 'Profile photo.jpg', // Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. //
    Sign: true, // Get a signed object URL. //
  },
  function (err, data) {
    if (err) return console.log(err);
    /* The URL is the object access URL. */
    var url = data.Url;
    /* Copy the value of `downloadUrl` to the browser and open it, and then download is automatically triggered. */
    var downloadUrl =
      url +
      (url.indexOf('?') > -1 ? '&' : '?') +
      'response-content-disposition=attachment';filename=picture.jpg'; // Add the parameter for a forced download
  }
);
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------------------------------------------------------------------------ | ------- | -------- |
| Bucket  | Bucket name in the format of `BucketName-APPID`. The bucket name entered here must be in this format. | String | Yes |
| Region  | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key     | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| Sign    | Whether to return a signed URL. Default value: `true`. If the object is configured with the private read permission, you still do not have the access permission after you obtain the unsigned URL.                          | Boolean | No   |
| Protocol    | Valid values: `http:` (default value), `https:`. | String | No |
| Domain    | Bucket access domain name. Default value: `{BucketName-APPID}.cos.{Region}.myqcloud.com`. | String | No |
| Method | HTTP request method, such as `GET`, `POST`, `DELETE`, or `HEAD`. Default value: `GET`. | String | No |
| Query     | Request parameters to be included in the signature in the format of `{key: 'val'}`                                         | Object | No   |
| Headers   | Request headers to be included in the signature in the format of `{key: 'val'}`                                         | Object | No   |
| Expires | Signature expiration time in seconds. Default value: `900`. | Number | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| err    | The object returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| data         | The object returned when the request is successful. If an error occurs with the request, this parameter is empty.               | Object |
| - Url | Calculated URL | String |
