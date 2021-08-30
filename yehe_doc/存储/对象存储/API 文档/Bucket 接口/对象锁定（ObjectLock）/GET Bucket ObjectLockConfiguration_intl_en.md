## Overview

COS supports locking objects stored in your buckets. This API is used to obtain the object lock configuration that has taken effect.

## Request

#### Sample request

```plaintext
GET /?object-lock HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String 
```

>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body of this request is empty.

 

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

```plaintext
<?xml version="1.0" encoding="UTF-8" ?>
<ObjectLockConfiguration>
      <ObjectLockEnabled>Enabled</ObjectLockEnabled> 
      <Rule> 
           <DefaultRetention>
                 <Days>30</Days> 
           </DefaultRetention> 
      </Rule> 
</ObjectLockConfiguration> 
```



The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| ----------------------- | --------------------------------------------- | --------------------------------------- | ---------- |
| ObjectLockConfiguration | None | Object lock configuration | Container |
| ObjectLockEnabled | ObjectLockConfiguration | Whether object lock is enabled | String |
| Rule | ObjectLockConfiguration | Object lock rule | Containers |
| DefaultRetention | ObjectLockConfiguration.Rule | Default configuration of the retention period (during which an object remains locked) | Containers |
| Days | ObjectLockConfiguration.Rule.DefaultRetention | Default retention period, in days. Value range: 1−36500 | Int |

 

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

 
