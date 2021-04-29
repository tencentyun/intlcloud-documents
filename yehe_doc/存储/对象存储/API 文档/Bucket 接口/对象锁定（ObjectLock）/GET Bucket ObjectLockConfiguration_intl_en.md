
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

> ?Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)

#### Request headers

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body of this request is empty.

 

## Response

#### Response headers

This API returns only common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

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



Nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| ----------------------- | --------------------------------------------- | ----------------------------------- | ---------- |
| ObjectLockConfiguration | None | Object lock configuration | Container |
| ObjectLockEnabled | ObjectLockConfiguration | Whether object lock is enabled | String |
| Rule | ObjectLockConfiguration | Object lock rule | Containers |
| DefaultRetention | ObjectLockConfiguration.Rule | Default configuration of the retention period (during which an object remains locked) | Containers |
| Days | ObjectLockConfiguration.Rule.DefaultRetention | Default retention period, in days. Value range: 1−36500 | Int |

 

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

 
