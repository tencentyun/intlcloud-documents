## Overview

When using COS, you may need to use a temporary key to grant users permissions to certain resources or operations, configure user policies for your sub-users or collaborators that allow them to help you operate on the resources in COS, or create bucket policies that allow the specified users to perform certain operations on or access certain resources in your bucket. When configuring these permissions, please comply with the **principle of least privilege** in order to ensure the security of your data assets.

The **principle of least privilege** means that when granting permission, you must specify the scope of the permission granted to the **specified user** for performing **what operation** and access **what resource** under **what conditions**.

## Precautions
You are recommended to strictly comply with the principle of least privilege to ensure that a user can only perform the specified operations (e.g., `action:GetObject`) or access the specified resources (e.g., `resource:exampleBucket-APPID/exampleObject.txt`). 
To prevent data security risks caused by unexpected and unauthorized operations with excessive permissions, it is strongly recommended that you avoid authorizing a user to access all resources (e.g., `resource:*`) or perform all operations (e.g., `action:*`).

Below are some potential data security risks:
- Data leakage: if you want to authorize a user to download the specified resources such as `examplebucket-1250000000/data/config.json` and `examplebucket-1250000000/video/` but include `examplebucket-1250000000/*` in the permission policy, then all objects in the bucket can be downloaded without your authorization, leading to unexpected data leakage.
- Data overwriting: if you want to authorize a user to upload `examplebucket-1250000000/data/config.json` and `examplebucket-1250000000/video/` but include `examplebucket-1250000000/*` in the permission policy, then all objects in the bucket can be uploaded without your authorization, which may overwrite unintended objects. To avoid this risk, in addition to following the principle of least privilege, you can retain all versions of data for traceability as instructed in [Versioning Overview](https://intl.cloud.tencent.com/document/product/436/19883).
- Permission leakage: if you want to authorize a user to list the objects in the bucket (`cos:GetBucket`) but configured `cos:*` in the permission policy, then all operations on the bucket will be allowed, including reauthorizing the bucket, deleting objects, and deleting the bucket, which puts your data at extremely high risk.





## Usage Guide

Under the principle of least privilege, you should specify the following information in the policy:

- principal: you should specify to which sub-account (user ID required), collaborator (user ID required), anonymous user, or user group to grant permission. This is not needed if you use a temporary key for access.
- statement: enter the corresponding parameters.
	-  effect: you must specify whether the policy is to "allow" or "deny".
	-  action: you must specify the allowed or denied operation. An operation can be an API (described using the prefix “name”) or a feature set (a set of specific APIs, described using the prefix “permid”).
	-  resource: you must specify the resource authorized by the policy. A resource is described in a six-piece format. You can set the resource scope as the specified file (e.g., `exampleobject.jpg`) or the specified directory (e.g., `examplePrefix/*`). Unless it is required by your business, please do not grant any user access to all resources using the `*` wildcard.
	-  condition: it describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value may contain information such as time and IP address.




### Least privilege guide for temporary key

When applying for a temporary key, you can set the permission policy field (`[Policy](https://cloud.tencent.com/document/product/598/33416)`) to limit the permissions to operations and resources within the specific scope. For more information, please see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).

#### Authorization example

#### Granting a user permission to access the specified object using the SDK for Java

If you want to use the SDK for Java to grant a user permission to download the `exampleObject.txt` object in the `examplebucket-1250000000` bucket, the configuration code should be as follows:

```
// Import `java sts sdk` using the integration method with Maven as described on GitHub 
import java.util.*;
import org.json.JSONObject; 
import com.tencent.cloud.CosStsClient;

public class Demo {
    public static void main(String[] args) {
        TreeMap<String, Object> config = new TreeMap<String, Object>();

        try {
            // Replace with your own SecretId 
            config.put("SecretId", "AKIDHTVVaVR6e3");
            // Replace with your own SecretKey
            config.put("SecretKey", "PdkhT9e2rZCfy6");

            // Validity period of the temporary key in seconds; default value: 1,800s; maximum value: 7,200s
            config.put("durationSeconds", 1800);

            // Replace with your own bucket
            config.put("bucket", "examplebucket-1250000000");
            // Replace with the region where your bucket resides
            config.put("region", "ap-guangzhou");

            // Change it to the allowed path prefix such as `a.jpg`, `a/*`, or`*`. You can determine the specific path to which files can be uploaded based on your login status
            // If "*" is entered, the user will be allowed to access all resources; unless it is required by your business, please grant the user only the corresponding permission based on the principle of least privilege.
            config.put("allowPrefix", "exampleObject.txt");

            // List of key permissions. The following permissions are required for simple upload, upload using a form, and multipart upload. For other permissions, please visit https://cloud.tencent.com/document/product/436/31923
            String[] allowActions = new String[] {
                    // Download data
                    "name/cos:GetObject"
            };
            config.put("allowActions", allowActions);

            JSONObject credential = CosStsClient.getCredential(config);
            // If it succeeds, the temporary key information will be returned and printed out as shown below
            System.out.println(credential);
        } catch (Exception e) {
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
      "action": [
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

### Least privilege guide for user policy

A user policy is a user permission policy created in the [CAM Console](https://console.cloud.tencent.com/cam/policy) to grant a user permission to access certain resources in COS. For more information, please see [Access Policy Language Overview](https://intl.cloud.tencent.com/document/product/436/18023).

#### Authorization example

#### Granting an account permission to access the specified object

If you want to grant an account whose UIN is `100000000001` permission to download the `exampleObject.txt` object in the `examplebucket-1250000000` bucket, the access policy should be as follows:
```shell
{
   "version": "2.0",
   "principal": {
      "qcs": [
         "qcs::cam::uin/100000000001:uin/100000000001"
      ]
   },
    "statement": [
        {
            "action": [
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

If you want to grant a sub-account whose UIN is `100000000011` (root account UNI: `100000000001`) permission to download the objects in the `examplePrefix` directory in the `examplebucket-1250000000` bucket, the access policy should be as follows:

```shell
{
   "version": "2.0",
   "principal": {
      "qcs": [
         "qcs::cam::uin/100000000001:uin/100000000011"
      ]
   },
    "statement": [
        {
            "action": [
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

If you want to grant a sub-account whose UIN is `100000000011` (root account UNI: `100000000001`) permission to download the `exampleObject.txt` object in the `examplebucket-1250000000` bucket and all objects in the `examplePrefix` directory, the access policy should be as follows:

```shell
{
  "Statement": [
    {
      "Action": [
        "name/cos:GetObject"
      ],
      "Effect": "allow",
      "Principal": {
        "qcs": [
          "qcs::cam::uin/100000000001:uin/100000000011"
        ]
      },
      "Resource": [
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/exampleObject.txt",
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/examplePrefix/*"
      ]
    }
  ],
  "version": "2.0"
}
```
