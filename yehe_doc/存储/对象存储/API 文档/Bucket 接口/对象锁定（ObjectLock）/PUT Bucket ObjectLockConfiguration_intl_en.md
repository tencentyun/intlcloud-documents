
## Overview

COS supports locking objects stored in your buckets. This API is used to configure object lock for your buckets to meet regulatory requirements.

## Request

#### Sample request


```plaintext
PUT /?object-lock HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String 
```

> ?Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)

#### Request headers

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).


#### Request body


```shell
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

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ----------------------- | --------------------------------------------- | ----------------------------------- | ---------- | -------- |
| ObjectLockConfiguration | None | Object lock configuration | Container | Yes |
| ObjectLockEnabled | ObjectLockConfiguration | Whether to enable object lock | String | Yes |
| Rule | ObjectLockConfiguration | Object lock rule | Containers | Yes |
| DefaultRetention | ObjectLockConfiguration.Rule | Default configuration of the retention period (during which an object remains locked) | Containers | Yes |
| Days | ObjectLockConfiguration.Rule.DefaultRetention | Object retention period, in days. Value range: 1−36500 | Int | Yes |

 

## Response

#### Response headers

This API returns only common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body is empty.

#### Error codes

This API returns common error responses and error codes. For error codes that are not described below, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).


| HTTP Status Code | Error Code | Description |
| :-------------- | :--------------------------- | :------------------- |
| 409 Conflict | InvalidLockedTime | The period set in `Days` is shorter than the previously configured one. The value must be in the range of 1−36500 (days). |


 

 

 
 

 