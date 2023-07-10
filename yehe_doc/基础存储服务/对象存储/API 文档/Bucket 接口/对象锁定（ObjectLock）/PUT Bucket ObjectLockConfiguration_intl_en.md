## Feature Overview

COS supports locking objects stored in your buckets. This API is used to configure object lock for your buckets to meet regulatory requirements.

## Request

#### Sample request

```plaintext
PUT /?object-lock HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String 
```

>? 
> - Host: <BucketName-APPID>.cos.<Region>.myqcloud.com, where <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://www.tencentcloud.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://www.tencentcloud.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://www.tencentcloud.com/document/product/436/7778) for more information)
> 

#### Request headers

This API only uses [Common Request Headers](https://www.tencentcloud.com/document/product/436/7728).

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

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ----------------------- | --------------------------------------------- | ------------------------------------- | ---------- | -------- |
| ObjectLockConfiguration | None | Object lock configuration | Container | Yes |
| ObjectLockEnabled | ObjectLockConfiguration | Whether to enable object lock | String | Yes |
| Rule | ObjectLockConfiguration | Object lock rule | Containers | Yes |
| DefaultRetention | ObjectLockConfiguration.Rule | Default configuration of the retention period (during which an object remains locked) | Containers | Yes |
| Days | ObjectLockConfiguration.Rule.DefaultRetention | Object retention period, in days. Value range: 1−36500 | Int | Yes |

>!
- `ObjectLockEnabled` can be set only to `Enabled`, indicating to enable object lock for the bucket.
- Please note that object lock cannot be disabled once enabled.

## Response

#### Response headers

This API only returns [Common Response Headers](https://www.tencentcloud.com/document/product/436/7729).

#### Response body

The response body is empty.

#### Error codes

This API returns common error responses and error codes. For error codes that are not described below, please see [Error Codes](https://www.tencentcloud.com/document/product/436/7730).

| HTTP Status Code | Error Code | Description |
| :----------- | :---------------- | :----------------------------------------------------------- |
| 409 Conflict | InvalidLockedTime | The period set in `Days` is shorter than the previously configured one. The value must be in the range of 1−36500 (days). |

## Examples

#### Request

The following example sets 1-day object lock for the `examplebucket-1250000000` bucket.

```plaintext
PUT /?object-lock= HTTP/1.1
Host: exmaplebucket-1250000000.cos.ap-beijing.myqcloud.com
Content-Length: 281
Content-Type: application/x-www-form-urlencoded
Authorization: Auth String


<ObjectLockConfiguration>
    <ObjectLockEnabled>Enabled</ObjectLockEnabled>
    <Rule>
        <DefaultRetention>
            <Days>1</Days>
        </DefaultRetention>
    </Rule>
</ObjectLockConfiguration>
```


#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: keep-alive
Date: Fri, 09 Dec 2022 08:17:20 GMT
Server: tencent-cos
x-cos-request-id: NjM5MmVmMTBfNmM0ZTQ0MGJfMjA4****
```







