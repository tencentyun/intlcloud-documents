## Overview

This document provides an overview of APIs and SDK code samples for media buckets.

| API | Operation |  Description |
| ------------------------------------------------------------ | --------------------------|---------------------------- |
| [DescribeMediaBuckets](https://intl.cloud.tencent.com/document/product/436/46909) | Querying media processing activation status | Queries buckets with media processing enabled   |

## Querying Media Processing Activation Status

#### Feature description

This API is used to query buckets with media processing enabled.

>! The COS JavaScript SDK version must be at least v1.3.1.


#### Sample code
```js
var config = {
  // Replace with your own bucket information
  Bucket: 'examplebucket-1250000000', /* Bucket (required) */
  Region: 'COS_REGION', /* Bucket region (required) */
};
var host = 'ci.' + config.Region + '.myqcloud.com';
var url = 'https://' + host + '/mediabucket';
cos.request({
    Bucket: config.Bucket,
    Region: config.Region,
    Method: 'GET',
    Key: 'mediabucket', /** Fixed value (required) */
    Url: url,
    Query: {
        pageNumber: '1', /** Page number (optional) */
        pageSize: '10', /** Number of entries per page (optional) */
        // regions: 'ap-chengdu', /** Region (optional), such as 'ap-beijing'. To specify multiple values, separate them with commas, such as 'ap-shanghai,ap-beijing'. */
        // bucketNames: 'test-1250000000', /** Bucket name (optional), such as 'test-1250000000'. To specify multiple values, separate them with commas, such as 'test1-1250000000,test2-1250000000'. Exact search is supported. */
        // bucketName: 'test', /** Bucket name prefix for prefix search (optional), such as 'test'. To specify multiple values, separate them with commas, such as 'test1,test2'. */
    }
}, function (err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| :------- | :----------------------------------------------------------- | :----- | :------- |
| Bucket | Bucket name in the format of `BucketName-APPID`. | String  | Yes   |
| Region  | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key                        | Fixed value: mediabucket. | String   | Yes   |
| PageNumber | Page number.                                          | String | No   |
| PageSize   | Number of entries per page.                                        | String | No   |
| Regions     |  Region information, such as `ap-shanghai` and `ap-beijing`. To specify multiple regions, separate them with commas. For more information, see [Regions and Domain Names](https://intl.cloud.tencent.com/document/product/1045/33423). | String |  No    |
| BucketNames | Bucket name. To specify multiple bucket names, separate them with commas. Exact search is supported. | String | No |
| BucketName  | Bucket name prefix for prefix search.        | String |  No       |


#### Callback function description

```
function(err, data) { ... }
```

| Parameter  | Description                                               | Type             |
| ------------ | ------------------------------------------------------------ | ------ |
| err    | The object returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers. | Object |
| data         | The object returned when the request is successful. If an error occurs with the request, this parameter is empty.               | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers. | Object |
| - Response       | Response result. | Object |
| - - RequestId          | Unique ID of the request.                   | String    |
| - - TotalCount         | Total number of media buckets.                | String       |
| - - PageNumber         | Current page number, which is the same as `pageNumber` in the request. | String       |
| - - PageSize           | Number of entries per page, which is the same as `pageSize` in the request.   | String       |
| - - MediaBucketList    | Media bucket list.                | Object |
| - - - BucketId           | Bucket ID.               | String |
| - - - Name               | Bucket name, which is the same as `BucketId`. | String |
| - - - Region             | Region.              | String |
| - - - CreateTime         | Creation time.                | String |





