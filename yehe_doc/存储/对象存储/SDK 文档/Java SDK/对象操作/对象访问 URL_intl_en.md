## Overview

This document provides code samples to generate an object access URL.
The URL generated here shows the path to the object in the COS.

>? The URL generated using this API cannot be used to access **private-read** objects.
>

### Getting an object access URL

#### Method prototype

```java
public URL getObjectUrl(String bucketName, String key);
```

#### Sample request

```java
// Identity information does not need to be verified.
COSCredentials cred = new AnonymousCOSCredentials();

// `ClientConfig` contains the COS client configuration for subsequent COS requests.
ClientConfig clientConfig = new ClientConfig();

// Set the bucket region.
// For more information on COS regions, please visit https://intl.cloud.tencent.com/document/product/436/6224.
clientConfig.setRegion(new Region("COS_REGION"));

// Set the URL generation request protocol, `http` or `https`.
// For 5.6.53 and earlier versions, HTTPS is recommended.
// Starting from 5.6.54, HTTPS is used by default.
clientConfig.setHttpProtocol(HttpProtocol.https);

// Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";

System.out.println(cosclient.getObjectUrl(bucketName, key));
```

#### Parameter description

| Parameter | Description | Type | Required |
| --------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, the unique ID of an object in a bucket. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324#.E5.AF.B9.E8.B1.A1.E9.94.AE) | String | Yes |
