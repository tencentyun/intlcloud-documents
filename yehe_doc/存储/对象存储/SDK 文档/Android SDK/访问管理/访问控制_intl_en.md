## Overview

This document provides an overview of APIs and SDK code samples related to bucket and object access control lists (ACLs).

**Bucket ACL**

| API | Operation Name | Description |
| ------------------------------------------------------------ | -------------- | --------------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting a bucket ACL | Sets the ACL of a specified bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying a bucket ACL | Queries the ACL of specified bucket |

**Object ACL**

| API | Operation Name | Description |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting an object ACL | Sets an ACL for a specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying an object ACL | Queries the ACL of an object |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).


## Bucket ACLs

### Setting a bucket ACL

#### Feature description

This API is used to set the access control list (ACL) of a specified bucket.

#### Sample code

[//]: # ".cssg-snippet-put-bucket-acl"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketACLRequest putBucketACLRequest = new PutBucketACLRequest(bucket);

// Set the bucket's access permissions
putBucketACLRequest.setXCOSACL("public-read");

// Grant read permission
ACLAccount readACLS = new ACLAccount();
readACLS.addAccount("100000000001", "100000000001");
putBucketACLRequest.setXCOSGrantRead(readACLS);

// Grant write permission 
ACLAccount writeACLS = new ACLAccount();
writeACLS.addAccount("100000000001", "100000000001");
putBucketACLRequest.setXCOSGrantWrite(writeACLS);

// Grant read and write permission
ACLAccount writeandReadACLS = new ACLAccount();
writeandReadACLS.addAccount("100000000001", "100000000001");
putBucketACLRequest.setXCOSReadWrite(writeandReadACLS);

cosXmlService.putBucketACLAsync(putBucketACLRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketACLResult putBucketACLResult = (PutBucketACLResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketACL.java).

### Querying a bucket ACL

#### Feature description

This API is used to query the access control list (ACL) of a specified bucket.

#### Sample code

[//]: # ".cssg-snippet-get-bucket-acl"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketACLRequest getBucketACLRequest = new GetBucketACLRequest(bucket);
cosXmlService.getBucketACLAsync(getBucketACLRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketACLResult getBucketACLResult = (GetBucketACLResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketACL.java).

## Object ACLs

### Setting an object ACL

#### Feature description

This API is used to set an access control list (ACL) for a specified object in a bucket.

#### Sample code

[//]: # ".cssg-snippet-put-object-acl"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
PutObjectACLRequest putObjectACLRequest = new PutObjectACLRequest(bucket,
        cosPath);

// Set the object's access permissions
putObjectACLRequest.setXCOSACL("public-read");

// Grant read permission
ACLAccount readACLS = new ACLAccount();
readACLS.addAccount("100000000001", "100000000001");
putObjectACLRequest.setXCOSGrantRead(readACLS);

// Grant read and write permission
ACLAccount writeandReadACLS = new ACLAccount();
writeandReadACLS.addAccount("100000000001", "100000000001");
putObjectACLRequest.setXCOSReadWrite(writeandReadACLS);

cosXmlService.putObjectACLAsync(putObjectACLRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutObjectACLResult putObjectACLResult = (PutObjectACLResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ObjectACL.java).

### Querying an object ACL

#### Feature description

This API is used to query the ACL of an object.

#### Sample code

[//]: # ".cssg-snippet-get-object-acl"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
GetObjectACLRequest getBucketACLRequest = new GetObjectACLRequest(bucket,
        cosPath);
cosXmlService.getObjectACLAsync(getBucketACLRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetObjectACLResult getObjectACLResult = (GetObjectACLResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```
>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ObjectACL.java).



