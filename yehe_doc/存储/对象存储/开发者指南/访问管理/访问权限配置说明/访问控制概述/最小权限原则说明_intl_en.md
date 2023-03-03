## Overview

When using COS, you may need to use a temporary key to grant users permissions to certain resources or operations, configure user policies for your sub-users or collaborators that allow them to help you operate on the resources in COS, or create bucket policies that allow the specified users to perform certain operations on or access certain resources in your bucket. When configuring these permissions, please comply with the **principle of least privilege** in order to ensure the security of your data assets.

The **principle of least privilege** means that when granting permission, you must specify the scope of the permission granted to the **specified user** for performing **what operation** and access **what resource** under **what conditions**.

## Limits
We recommend you strictly follow the principle of least privilege to ensure that a user can only perform the specified operations (such as `action:GetObject`) or access the specified resources (such as `resource:examplebucket-1250000000/exampleobject.txt`). 
To prevent data security risks caused by unexpected and unauthorized operations due to excessive permissions, we strongly recommend you not authorize a user to access all resources (such as `resource:*`) or perform all operations (such as `action:*`).

Below are some potential data security risks:
- Data leakage: If you want to authorize a user to download the specified resources such as `examplebucket-1250000000/data/config.json` and `examplebucket-1250000000/video/` but include `examplebucket-1250000000/*` in the permission policy, then all objects in the bucket can be downloaded without your authorization, leading to unexpected data leakage.
- Data overwriting: If you want to authorize a user to upload `examplebucket-1250000000/data/config.json` and `examplebucket-1250000000/video/` but include `examplebucket-1250000000/*` in the permission policy, then all objects in the bucket can be uploaded without your authorization, which may overwrite unintended objects. To avoid this risk, in addition to following the principle of least privilege, you can retain all versions of data for traceability as instructed in [Overview](https://intl.cloud.tencent.com/document/product/436/19883).
- Permission leakage: If you want to authorize a user to list the objects in the bucket (`cos:GetBucket`) but configured `cos:*` in the permission policy, then all operations on the bucket will be allowed, including reauthorizing the bucket, deleting objects, and deleting the bucket, which puts your data at extremely high risk.


## Usage Guide

Under the principle of least privilege, you should specify the following information in the policy:

- principal: you should specify to which sub-account (user ID required), collaborator (user ID required), anonymous user, or user group to grant permission. This is not needed if you use a temporary key for access.
- statement: enter the corresponding parameters.
	-  effect: you must specify whether the policy is to "allow" or "deny".
	-  action: you must specify the action to allow or deny. It can be one API operation or a set of API operations.
	- resource: You must specify the resource for which permission is granted. A resource is described in a six-segment format. You can set the resource as a specific file, e.g., `exampleobject.jpg` or a directory, e.g., `examplePrefix/*`. Unless needed, do not grant any user the access to all of your resources using the `*` wildcard.
	-  condition: it describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value may contain information such as time and IP address.

### Least privilege guide for temporary keys

When applying for a temporary key, you can set the `policy` field as described in [GetFederationToken](https://intl.cloud.tencent.com/document/product/1150/49452) to grant limited permissions on operations and resources. For more information about how to generate a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).

#### Authorization example

#### Granting a user permission to access the specified object using the SDK for Java

If you want to use the Java SDK to grant a user permission to download the `exampleObject.txt` object in the `examplebucket-1250000000` bucket, the configuration code should be as follows:

```
// Import `java sts sdk` using the integration method with Maven as described on GitHub 
import java.util.*;
import org.json.JSONObject; 
import com.tencent.cloud.CosStsClient;

public class Demo {
    public static void main(String[] args) {
        TreeMap<String, Object> config = new TreeMap<String, Object>();

        try {
            String secretId = System.getenv("secretId");// User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
            String secretKey = System.getenv("secretKey");// User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
            // Replace it with your own SecretId 
            config.put("SecretId", secretId);
            // Replace it with your own SecretKey
            config.put("SecretKey", secretKey);

            // Validity period of the temporary key, in seconds. Default value: 1800; maximum value: 7200
            config.put("durationSeconds", 1800);

            // Replace it with your own bucket
            config.put("bucket", "examplebucket-1250000000");
            // Replace it with the region where your bucket resides
            config.put("region", "ap-guangzhou");

            // Change it to the allowed path prefix (such as "a.jpg", "a/*", or "*"). You can determine the upload path based on your login status.
            // If "*" is entered, you allow the user to access all resources. Unless otherwise necessary, grant the user only the limited permissions that are needed following the principle of least privilege.
            config.put("allowPrefix", "exampleObject.txt");

            // List of key permissions. The following permissions are required for simple upload, upload using a form, and multipart upload. For other permissions, please visit https://cloud.tencent.com/document/product/436/31923
            String[] allowActions = new String[] {
                    // Download data
                    "name/cos:GetObject"
            };
            config.put("allowActions", allowActions);

            JSONObject credential = CosStsClient.getCredential(config);
            // If it succeeds, the temporary key information will be returned and printed out as shown below:
            System.out.println(credential);
        } catch (Exception e){
            // If it fails, an exception will be thrown
            throw new IllegalArgumentException("no valid secret !");
        }
    }
}
```

#### Granting a user permission to access the specified object using API

If you want to use an API to grant a user permission to download the `exampleObject.txt` object in the `examplebucket-1250000000` bucket and all objects in the `examplePrefix` directory, the access policy should be as follows:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action":[
        "name/cos:GetObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/exampleObject.txt",
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/examplePrefix/*"
      ]
    }
  ]
}
```

### Least privilege guide for signatures

You can perform temporary uploads and downloads using pre-signed URLs. Moreover, if you send a valid pre-signed URL to others, he (or she) can upload or download the objects.

>!Both temporary and permanent keys can be used to generate pre-signed URLs. However, you are advised to follow the least privilege principle when [generating a temporary key](https://intl.cloud.tencent.com/document/product/436/14048) and use the temporary key to calculate the signature. Try to avoid using a permanent key that has excessive permissions for the sake of security.

#### Authorization example

#### Granting a user permission to use a pre-signed URL to download an object

Use a temporary key to generate a signed download URL and set it to overwrite some public headers to be returned (such as `content-type` and `content-language`). The Java code sample is as follows:

```java
// Pass in the obtained temporary key (tmpSecretId, tmpSecretKey, sessionToken)
String tmpSecretId = "SECRETID";
String tmpSecretKey = "SECRETKEY";
String sessionToken = "TOKEN";
COSCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);
// Set the bucket region. For abbreviations of COS regions, see https://cloud.tencent.com/document/product/436/6224
// `clientConfig` contains the set methods to set region, HTTPS (HTTP by default), timeout, and proxy. For detailed usage, please see the source code or the FAQs about the SDK for Java.
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// To generate a URL that uses the HTTPS protocol, configure this line (recommended).
// clientConfig.setHttpProtocol(HttpProtocol.https);
// Generate a COS client.
COSClient cosClient = new COSClient(cred, clientConfig);
// Enter the Bucket name in the format of `BucketName-APPID`. 
String bucketName = "examplebucket-1250000000";
// Object key, the unique identifier of the object in the bucket.
String key = "exampleobject";
GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// Set the http header returned for download.
ResponseHeaderOverrides responseHeaders = new ResponseHeaderOverrides();
String responseContentType = "image/x-icon";
String responseContentLanguage = "zh-CN";
// Set the returned header to contain filename information.
String responseContentDispositon = "filename=\"exampleobject\"";
String responseCacheControl = "no-cache";
String cacheExpireStr =
        DateUtils.formatRFC822Date(new Date(System.currentTimeMillis() + 24L * 3600L * 1000L));
responseHeaders.setContentType(responseContentType);
responseHeaders.setContentLanguage(responseContentLanguage);
responseHeaders.setContentDisposition(responseContentDispositon);
responseHeaders.setCacheControl(responseCacheControl);
responseHeaders.setExpires(cacheExpireStr);
req.setResponseHeaders(responseHeaders);
// Setting the signature expiration time (optional). If it is not configured, the signature expiration time in ClientConfig (1 hour) is used by default.
// Set the signature to expire in half an hour.
Date expirationDate = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);
req.setExpiration(expirationDate);
URL url = cosClient.generatePresignedUrl(req);
System.out.println(url.toString());
cosClient.shutdown();
```

### Least privilege guide for user policy

A user policy is a user permission policy created in the [CAM Console](https://console.cloud.tencent.com/cam/policy) to grant a user permission to access certain resources in COS. For more information, please see [Access Policy Language Overview](https://intl.cloud.tencent.com/document/product/436/18023).

#### Authorization example

#### Granting an account permission to access the specified object

If you want to grant an account whose UIN is `100000000001` permission to download the `exampleObject.txt` object in the `examplebucket-1250000000` bucket, the access policy should be as follows:
```shell
{
   "version": "2.0",
   "principal":{
      "qcs":[
         "qcs::cam::uin/100000000001:uin/100000000001"
      ]
   },
    "statement": [
        {
            "action":[
                "name/cos:GetObject"
            ],
            "effect": "allow",
            "resource": [
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000.ap-guangzhou.myqcloud.com/exampleObject.txt"
            ]
        }
    ]
}
```

#### Granting a sub-account permission to access the specified directory

If you want to grant a sub-account whose UIN is `100000000011` (root account UIN: `100000000001`) permission to download the objects in the `examplePrefix` directory in the `examplebucket-1250000000` bucket, the access policy should be as follows:

```shell
{
   "version": "2.0",
   "principal":{
      "qcs":[
         "qcs::cam::uin/100000000001:uin/100000000011"
      ]
   },
    "statement": [
        {
            "action":[
                "name/cos:GetObject"
            ],
            "effect": "allow",
            "resource": [
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000.ap-guangzhou.myqcloud.com/examplePrefix/*"
            ]
        }
    ]
}
```

### Least privilege guide for bucket policy

A bucket policy is an access policy configured for a bucket to allow the specified user to perform certain operations on the bucket and resources in it. For more information, please see [Adding Bucket Policies](https://intl.cloud.tencent.com/document/product/436/30927).

#### Authorization example

#### Granting a sub-account permission to access the specified objects

If you want to grant a sub-account whose UIN is `100000000011` (root account UIN: `100000000001`) permission to download the `exampleObject.txt` object in the `examplebucket-1250000000` bucket and all objects in the `examplePrefix` directory, the access policy should be as follows:

```shell
{
  "Statement":[
    {
      "Action":[
        "name/cos:GetObject"
      ],
      "Effect": "allow",
      "Principal":{
        "qcs":[
          "qcs::cam::uin/100000000001:uin/100000000011"
        ]
      },
      "Resource":[
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/exampleObject.txt",
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/examplePrefix/*"
      ]
    }
  ],
  "version": "2.0"
}
```
