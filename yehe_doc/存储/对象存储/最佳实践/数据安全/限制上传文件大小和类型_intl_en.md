Cloud Object Storage (COS) supports limiting object sizes upon the upload, which allows you to manage storage space flexibly by avoiding uploading objects that are too large or too small to make full use of the bandwidth and storage space. This document gives two samples to describe how to control the objects sizes in a refined way.

## Prerequisites

The samples use the information below:
- APPID of the root account: 1250000000
- Bucket name: examplebucket-1250000000




## Sample 1. Specifying a Size Range During POST Object Uploads

When uploading objects using `POST Object`, you can add `content-length-range` in the HTML form to control the object size in this request as follows:

```plaintext
[ "content-length-range", minNum, maxNum ]
```

Sample:

```plaintext
[ "content-length-range", 1, 10]
```

The JSON-formatted field above is added to policy > conditions in the POST request form. A complete policy with this field carried is as follows:

```plaintext
 {
    "expiration": "2021-12-31T12:00:00Z",
    "conditions": [
        { "bucket": "examplebucket-1250000000" },
        [ "starts-with", "$key", "exampleobject" ],
        { "q-ak": "AKIDQjz3ltompVjBni5LitkWHFlFpwkn****" },
        { "q-sign-algorithm": "sha1" },
        { "q-sign-time": "1567150692;1567157892" },
        [ "content-length-range", 1, 10 ]
    ]
}
```

For more information about how to construct a complete request, please see [POST Object](https://intl.cloud.tencent.com/document/product/436/14690).

#### Response

The following response will be returned as follows if the size of the object is within the specified size range:

```plaintext
HTTP/1.1 204 
Content-Length: 0
Connection: close
Date: Wed, 23 Aug 2020 08:14:53 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Location: http://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject
Server: tencent-cos
x-cos-request-id: NWQ2NzgxMzZfMmViMDJhMDlfY2NjOF84NGQz****
```

The response will fail if the object size is not in the specified range.

If the object is too big, the response is as follows:

```plaintext
HTTP/1.1 400 Bad Request
Content-Type: application/xml
Content-Length: 498
Connection: keep-alive
Date: Wed, 23 Aug 2020 08:14:53 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0****



<?xml version='1.0' encoding='utf-8' ?>
<Error>
        <Code>EntityTooLarge</Code>
        <Message>Condition key content-length-range doesn‘t match the value </Message>
        <Resource>examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject</Resource>
        <RequestId>NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0****</RequestId>
</Error>
```

If the object is too small, the response is as follows:

```plaintext
HTTP/1.1 400 Bad Request
Content-Type: application/xml
Content-Length: 498
Connection: keep-alive
Date: Wed, 23 Aug 2020 08:14:53 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0****



<?xml version='1.0' encoding='utf-8' ?>
<Error>
        <Code>EntityTooSmall</Code>
        <Message>Condition key content-length-range doesn‘t match the value </Message>
        <Resource>examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject</Resource>
        <RequestId>NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0****</RequestId>
</Error>
```



## Sample 2. Specifying a Size Range when Applying for a Temporary Credential

The method used in sample 1 is easy, which requires only one parameter in the HTML form. However, it only supports `POST Object` but not `PUT Object`. Moreover, since the requester can still modify the parameter in requests, uploading objects beyond the specified size range is still possible, making it hard for central management.

To solve the problem above, bucket managers can use the following fields to limit the object size when applying for a temporary key. For COS objects, use the fixed `cos:content_length`.

| Condition Field | Description | Example |
| -------------------------- | ------------ | ------------------------------------------------------------ |
| numeric_greater_than | A number greater than | {"numeric_greater_than": {"cos:content_length": 1}}, <br>The object size must be greater than 1 byte.
| numeric_greater_than_equal | A number greater than or equal to  | {"numeric_greater_than_equal": {"cos:content_length": 1}}, <br>The object size must be greater than or equal to 1 byte. |
| numeric_less_than | A number smaller than | {"numeric_less_than": {"cos:content_length": 1}}, <br>The object must be smaller than 1 bytes. |
| numeric_less_than_equal | A number smaller than or equal to | {"numeric_less_than_equal": {"cos:content_length": 1}}, <br>The object must be smaller than 10 bytes. |

For the complete request sample, please see the <b>Obtaining a Temporary Access Credential</b> API Documentation of STS. A complete policy is as follows:

```plaintext
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cos:PutObject",
                "cos:PostObject",
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],

            "condition": {
                "numeric_greater_than_equal": {"cos:content_length": 1}
                , "numeric_less_than": {"cos:content_length": 10}
            }
        }
    ]
}
```

With the temporary credential obtained using the following policy, you can call the `PUT Object` or `POST Object` API to upload objects to the `examplebucket-1250000000` bucket, with the object sizes limited to [1, 10), in bytes.

>!This policy is only applicable to the `cos:PutObject` and `cos:PostObject` actions. Using other actions such as `cos:GetObject` will fail.
>

This method allows bucket managers or the authentication center to centrally apply for temporary credentials and limit the size during the application, after which the credentials can be distributed to operators or business modules. In this way, object sizes can be controlled, avoiding uploading objects beyond the size range due to parameter modification.

#### Response

If the size of the uploaded object is within the specified range, the upload request will succeed with 200 or 204 returned. Otherwise, 403 will be returned, as shown below:

```plaintext
HTTP/1.1 403 Forbidden
Content-Type: application/xml
Content-Length: 298
Connection: keep-alive
Date: Wed, 23 Aug 2020 08:14:53 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0****
```




