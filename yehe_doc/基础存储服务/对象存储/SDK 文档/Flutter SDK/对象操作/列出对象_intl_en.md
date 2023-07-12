## Overview

This document provides an overview of APIs and SDK code samples for listing objects.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket (List Objects)](https://www.tencentcloud.com/document/product/436/30614) | Querying an object list | Queries some or all objects in a bucket |

## Querying an Object List

#### Feature description

This API is used to query some or all the objects in a bucket.

#### Sample 1. Getting the first page of data

```dart
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
String bucket = "examplebucket-1250000000";
try {
  BucketContents bucketContents = await Cos().getDefaultService().getBucket(
      bucket,
      prefix: "dir/", // Prefix match, which is used to specify the address prefix of returned objects.
      maxKeys: 100 // Maximum number of entries returned at a time. Default value: 1000.
  );
  // The data is truncated, and the next page of data needs to be pulled.
  var isTruncated = bucketContents.isTruncated;
  // `nextMarker` indicates the start position of the next page
  var nextMarker = bucketContents.nextMarker;
} catch (e) {
  // An exception will be reported in case of failure. Process the business logic accordingly.
  print(e);
}
```

#### Sample 2. Requesting the next page of data

```dart
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
String bucket = "examplebucket-1250000000";
// `prevPageBucketContents` is the result returned on the previous page, where `nextMarker` indicates the start position of the next page
String prevPageMarker = prevPageBucketContents.nextMarker;
try {
  BucketContents bucketContents = await Cos().getDefaultService().getBucket(
      bucket,
      prefix: "dir/", // Prefix match, which is used to specify the address prefix of returned objects.
      marker: prevPageMarker, // Starting position
      maxKeys: 100 // Maximum number of entries returned at a time. Default value: 1000.
  );
  // The data is truncated, and the next page of data needs to be pulled.
  var isTruncated = bucketContents.isTruncated;
  // `nextMarker` indicates the start position of the next page
  var nextMarker = bucketContents.nextMarker;
} catch (e) {
  // An exception will be reported in case of failure. Process the business logic accordingly.
  print(e);
}
```

#### Sample 3. Getting an object list and subdirectories

```dart
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
String bucket = "examplebucket-1250000000";
// The delimiter is a symbol. If the prefix exists,
// identical paths between the prefix and delimiter will be grouped as together and defined as a common prefix,
// and then all common prefixes are listed. If there is no prefix, the listing starts from the beginning of the path
var delimiter = "/";
try {
  BucketContents bucketContents = await Cos().getDefaultService().getBucket(
      bucket,
      prefix: "dir/", // Prefix match, which is used to specify the address prefix of returned objects.
      delimiter: delimiter,
      maxKeys: 100 // Maximum number of entries returned at a time. Default value: 1000.
  );
  // The data is truncated, and the next page of data needs to be pulled.
  var isTruncated = bucketContents.isTruncated;
  // `nextMarker` indicates the start position of the next page
  var nextMarker = bucketContents.nextMarker;
} catch (e) {
  // An exception will be reported in case of failure. Process the business logic accordingly.
  print(e);
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ------ | ------ |
| bucket | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| prefix | Key prefix to query objects by | String | No   |
| delimiter | Character delimiter used to group object keys. Keys that contain identical paths between the prefix (or, if no prefix is specified, the beginning of the string) and the first delimiter are grouped and defined as a `Prefix` node under `CommonPrefixes`. The grouped object keys will no longer appear in the subsequent object list. For specific scenarios and usage, see the samples above. | String | No |
| encodingType | Indicates the encoding method of the returned value. Valid value: `url`, which means that the returned object keys are URL-encoded (percent-encoded) values. For example, "Tencent Cloud" will be encoded as `%E8%85%BE%E8%AE%AF%E4%BA%91`. | String | No |
| marker | Marker for the starting object key. Object key entries will be returned in UTF-8 lexicographical order, starting from the first object key after the marker. | String | No |
| maxKeys | The maximum number (up to 1,000) of keys returned in the response. Default value: `1000`. Note: This parameter limits the maximum number of keys (the sum of `CommonPrefixes` and `Contents`) COS can return in each `List Objects` response. If not all objects are listed in a single response, COS will return the `NextMarker` node, the value of which can be used to specify `marker` so that the remaining objects can be listed in your next request. | Int | No |

#### Response description

- Success: `BucketContents` is returned, including the list of objects and list information.
-Failure: An error occurs (such as authentication failure), with a `CosXmlClientException` or `CosXmlServiceException` exception reported. For more information, see [Troubleshooting](https://www.tencentcloud.com/document/product/436/53963).

Parameters in the `BucketContents` response body are as follows:

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| name | Bucket name in the format of &lt;BucketName-APPID&gt;, such as `examplebucket-1250000000`. | String |
| encodingType | Encoding type, which corresponds to the `encodingType` parameter in the request. This node will be returned only when the `encodingType` parameter is specified in the request. | String |
| prefix | Matching prefix to filter object keys. This node corresponds to the `Prefix` parameter in the request. | String |
| marker | Marks the object key to start with. Object keys after the marker will be returned in UTF-8 lexicographical order. This node corresponds to the `marker` parameter in the request. | String |
| maxKeys | Maximum number of keys returned in a single response. This node corresponds to the `maxKeys` parameter in the request. | Int |
| delimiter | Delimiter, which corresponds to the `delimiter` parameter in the request and will be returned only if the `delimiter` parameter is specified in the request. | String |
| isTruncated | Whether the returned list is truncated, which is a Boolean value. Valid values: `true`, `false` | Bool |
| nextMarker | This node will be returned only if the returned list is truncated (i.e., the value of `IsTruncated` is `true`). The value of this node is the last object key in the current response. If you need to request subsequent entries, the value can be passed in as the value of the `marker` parameter in the next request. | String |
| contentsList | List of objects | List&lt;Content&gt; |
| commonPrefixesList | The identical paths between the prefix (or, if no prefix is specified, the beginning of the string) and the first delimiter are grouped and defined as a common prefix. This node will be returned only if the `delimiter` parameter is specified in the request. | List&lt;CommonPrefixes&gt; |

`Content` has the following sub-nodes:

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| key | Object key | String |
| lastModified | Last modified time of the object, in ISO 8601 format, for example, `2019-05-24T10:56:40Z` | String |
| eTag | Entity tag of the object. It indicates the content of the object when it is created and can be used to verify whether the object content is changed, such as `"8e0b617ca298a564c3331da28dcb50df"`. The value of `ETag` is not necessarily the MD5 checksum of the object. The value will be different if the uploaded object is encrypted. | String |
| size | Object size in bytes | Int |
| owner | Object owner information | Owner |
| storageClass | Object storage class, such as `STANDARD_IA` and `ARCHIVE`. For enumerated values, see Storage Class.  | String |

`Owner` has the following sub-nodes:

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| id | `APPID` of the object owner	 | String |
| disPlayName | Name of the object owner	 | String |

`CommonPrefixes` has the following sub-nodes:

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| prefix | A single common prefix | String |
