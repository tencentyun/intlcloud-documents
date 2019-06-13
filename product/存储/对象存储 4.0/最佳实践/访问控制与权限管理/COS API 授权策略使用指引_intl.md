## Overview
When COS uses the temporary key service, different permissions should be granted to perform actions on different COS APIs. An action or a set of actions can be specified.

COS API authorization policy is a JSON string. In the following example, the policy grants the permissions to upload any resource in the path with prefix of `test` and the permission to download any resource in the path with prefix of `test2` within the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutObject",
        "name/cos:InitiateMultipartUpload",
        "name/cos:ListParts",
        "name/cos:UploadPart",
        "name/cos:CompleteMultipartUpload",
        "name/cos:AbortMultipartUpload"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    },
    {
      "action": [
        "name/cos:GetObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test2/*"
      ]
    }
  ]
}
```

<a id="policy"></a>
#### Description of policy elements

| Name | Description |
| -------- | ------------------------------------------------------------ |
| version | The version of policy syntax. It defaults to 2.0. |
| effect | Allow and Deny |
| resource | Specific data authorized to be operated on. It can be any resource, a resource in a path with the specified prefix, a resource in the specified absolute path, or a combination thereof. |
| action   | Indicates COS APIs, used to specify an action, a set of actions, or all actions (*) as needed. |
| condition | Optional. For more information, see [Condition](https://intl.cloud.tencent.com/document/product/598/10603#6..E7.94.9F.E6.95.88.E6.9D.A1.E4.BB.B6(condition)). |

The following authorization policies are described in details using COS APIs.

## Service API 

### Get the bucket list

Get the list of buckets: Get Service. To grant this permission, the `action` is `name/cos:GetService`, and the `resource` is `*` in the policy.

#### Example 

The following policy grants the permission to get the list of buckets:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetService"
      ],
      "effect": "allow",
      "resource": [
        "*"
      ]
    }
  ]
}
```

## Bucket API

The `resource` in Bucket API policies can be described as follows:

- To perform operations on a bucket in any region, the `resource` is `*`.
- To perform operations only on a bucket in the specified region, for example, to operate on a bucket in the region `ap-beijing` under the APPID 1253653367, the `resource` is `qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/*`。.
- To perform operations only on a bucket with the specified name in the specified region, for example, to operate on the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367, the `resource` is `qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/`。.



The `action` in Bucket API policies varies with action values. All Bucket API authorization policies are listed below.

### Create a bucket 

This API (Put Bucket) is used to create a bucket. To grant this permission, the `action` in the policy is `name/cos:PutBucket`.

#### Example 

The following policy grants the permission to create a bucket with an arbitrary name in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutBucket"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/*"
      ]
    }
  ]
}
```

### Search for a bucket  

Search for a bucket: Head Bucket. To grant this permission, the `action` in the policy is `name/cos:HeadBucket`.

#### Example 

The following policy grants the permission to search for the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:HeadBucket"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/”
      ]
    }
  ]
}
```

### Query the region information of a bucket

Query the location of a bucket: Get Bucket Location. To grant this permission, the `action` in the policy is `name/cos:GetBucketLocation`。.

#### Example 

The following policy grants the permission to query the location information of the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetBucketLocation"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/”
      ]
    }
  ]
}
```

### Get the object list of a bucket

This API (Get Bucket) is used to get the list of objects in a bucket. To grant this permission, the `action` in the policy is `name/cos:GetBucket`.

#### Example 

The following policy grants the permission to get the object list of the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetBucket"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/*"
      ]
    }
  ]
}
```

### Delete a bucket

This API (Delete Bucket) is used to delete a bucket. To grant this permission, the `action` in the policy is `name/cos:DeleteBucket`.

#### Example 

The following policy grants the permission to delete the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:DeleteBucket"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/”
      ]
    }
  ]
}
```

### Set a bucket ACL 

This API (Put Bucket ACL) is used to set an ACL for a bucket. To grant this permission, the `action` in the policy is `name/cos:PutBucketACL`.

#### Example 

The following policy grants the permission to set an ACL for the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutBucketACL"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/”
      ]
    }
  ]
}
```

### Get the bucket ACL

This API (Get Bucket ACL) is used to get the ACL of a bucket. To grant this permission, the `action` in the policy is `name/cos:GetBucketACL`.

#### Example 

The following policy grants the permission to get the ACL for the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetBucketACL"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/”
      ]
    }
  ]
}
```

### Set the cross-origin configuration for a bucket

This API (Put Bucket CORS) is used to set the cross-origin configuration of a bucket. To grant this permission, the `action` in the policy is `name/cos:PutBucketCORS`.

#### Example 

The following policy grants the permission to set the cross-origin configuration for the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutBucketCORS"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/”
      ]
    }
  ]
}
```

### Get the cross-origin configuration of a bucket

This API (Get Bucket CORS) is used to get the cross-origin configuration of a bucket. To grant this permission, the `action` in the policy is `name/cos:GetBucketCORS`.

#### Example 

The following policy grants the permission to get the cross-origin configuration of the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetBucketCORS"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/”
      ]
    }
  ]
}
```

### Delete the cross-origin configuration of a bucket

This API (Delete Bucket CORS) is used to delete the cross-origin configuration of a bucket. To grant this permission, the `action` in the policy is `name/cos:DeleteBucketCORS`.

#### Example 

The following policy grants the permission to delete the cross-origin configuration of the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:DeleteBucketCORS"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/”
      ]
    }
  ]
}
```

### Set the bucket lifecycle

This API (Put Bucket Lifecycle) is used to set the lifecycle for a bucket. To grant this permission, the `action` in the policy is `name/cos:PutBucketLifecycle`.

#### Example 

The following policy grants the permission to set the lifecycle for the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutBucketLifecycle"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/”
      ]
    }
  ]
}
```

### Get the bucket lifecycle

This API (Get Bucket Lifecycle) is used to get the lifecycle of a bucket. To grant this permission, the `action` in the policy is `name/cos:GetBucketLifecycle`.

#### Example 

The following policy grants the permission to get the lifecycle of the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetBucketLifecycle"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/”
      ]
    }
  ]
}
```

### Delete the bucket lifecycle

This API (Delete Bucket Lifecycle) is used to delete the lifecycle of a bucket. To grant this permission, the `action` in the policy is `name/cos:DeleteBucketLifecycle`.

#### Example 

The following policy grants the permission to delete the lifecycle of the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:DeleteBucketLifecycle"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/”
      ]
    }
  ]
}
```

### Get in-progress multipart uploads in a bucket

This API (List Multipart Uploads) is used to get in-progress multipart uploads in a bucket. To grant this permission, the `action` in the policy is `name/cos:ListMultipartUploads`.

#### Example 

The following policy grants the permission to get in-progress multipart uploads in the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:ListMultipartUploads"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/”
      ]
    }
  ]
}
```



## Object API

The `resource` in Object API policies can be described as follows:<br>

- To perform operations on any object, the `resource` is `*`.
- To perform operations only on any object in the specified bucket, for example, to operate on any object in the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367, the `resource` is `qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/*`。.
- To perform operations only on any object in the specified bucket and the path with specified prefix, for example, to operate on any object in the path with prefix of `test` within the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367, the `resource` in the policy is `qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*`.
- To perform operations only on an object in the specified absolute path, for example, to operate on an object in the absolute path `test/audio.mp3` within the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367, the `resource` is `qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/audio.mp3`。.



The `action` in Object API policies varies with action values. All Object API authorization policies are listed below.

### Simple upload

This API (Put Object) is used to upload an object using simple upload. To grant this permission, the `action` in the policy is `name/cos:PutObject`.

#### Example 

The following policy grants the permission to use simple upload to upload any object under the path with prefix of `test` within the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
 {
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### Multipart upload 

This API is used to upload an object using multipart upload, which includes Initiate Multipart Upload, List Parts, Upload Part, Complete Multipart Upload, and Abort Multipart Upload. To grant these permissions, the `action` in the policy is a collection of `"name/cos:InitiateMultipartUpload","name/cos:ListParts","name/cos:UploadPart","name/cos:CompleteMultipartUpload","name/cos:AbortMultipartUpload"`.

#### Example 

The following policy grants the permission to use multipart upload to upload any object under the path with prefix of `test` within the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:InitiateMultipartUpload",
        "name/cos:ListParts",
        "name/cos:UploadPart",
        "name/cos:CompleteMultipartUpload",
        "name/cos:AbortMultipartUpload"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### Upload via Post

This API (Post Object) is used to upload an object via Post. To grant this permission, the `action` in the policy is `name/cos:PostObject`.

#### Example 

The following policy grants the permission to use the Post method to upload any object in the path with prefix of `test` within the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PostObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### Search for an object

This API (Head Object) is used to search for an object. To grant this permission, the `action` in the policy is `name/cos:HeadObject`.

#### Example 

The following policy grants the permission to search for any object in the path with prefix of `test` within the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:HeadObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### Download an object

This API (Get Object) is used to download an object. To grant this permission, the `action` in the policy is `name/cos:GetObject`.

#### Example 

The following policy grants the permission to download any object in the path with prefix of `test` within the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

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
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### Simple copy

This API (Put Object Copy) is used to copy an object using simple copy. To grant this permission, the `action` of the target object is `name/cos:PutObject`, and the `action` of the source object is `name/cos:GetObject` in the policy.

#### Example 

The following policy grants the permission to use simple copy to copy any object between the path with prefix of `test` and the path with prefix of `test2` within the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    },
    {
      "action": [
        "name/cos:GetObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test2/*"
      ]
    }
  ]
}
```

Where, `"qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test2/*"` is the source object.

### Multipart copy

This API (Upload Part Copy) is used to copy an object using multipart copy. To grant this permission, the `action` of the target object is a collection of `"name/cos:InitiateMultipartUpload","name/cos:ListParts","name/cos:PutObject","name/cos:CompleteMultipartUpload","name/cos:AbortMultipartUpload"`, and the `action` of the source object is `name/cos:GetObject` in the policy.

#### Example 

The following policy grants the permission to use multipart copy to copy any object between the path with prefix of `test` and the path with prefix of `test2` within the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:InitiateMultipartUpload",
        "name/cos:ListParts",
        "name/cos:PutObject",
        "name/cos:CompleteMultipartUpload",
        "name/cos:AbortMultipartUpload"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    },
    {
      "action": [
        "name/cos:GetObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test2/*" 
      ]
    }
  ]
}
```

Where, `"qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test2/*"` is the source object.

### Set the object ACL

This API (Put Object ACL) is used to set an ACL for an object. To grant this permission, the `action` in the policy is `name/cos:PutObjectACL`.

#### Example 

The following policy grants the permission to set an ACL for any object in the path with prefix of `test` within the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutObjectACL"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### Get the object ACL

This API (Put Object ACL) is used to get the ACL of an object. To grant this permission, the `action` in the policy is `name/cos:GetObjectACL`.

#### Example 

The following policy grants the permission to get the ACL of any object in the path with prefix of `test` within the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetObjectACL"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### Options request

This API (Options Object) is used to grant permission to send Options request for an object. To grant this permission, the `action` in the policy is `name/cos:OptionsObject`.

#### Example 

The following policy grants the permission to only send an Options request for any object in the path with prefix of `test` within the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:OptionsObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### Restore an archived object

This API (Post Object Restore) is used to restore an archived object. To grant this permission, the `action` in the policy is `name/cos:PostObjectRestore`.

#### Example 

The following policy grants the permission to restore an archived object in the path with prefix of `test` within the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PostObjectRestore"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### Delete an object

This API (Delete Object) is used to delete an object. To grant this permission, the `action` in the policy is `name/cos:DeleteObject`.

#### Example 

The following policy grants the permission to delete the object `audio.mp3` within the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:DeleteObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/audio.mp3"
      ]
    }
  ]
}
```

### Delete objects in batch

This API (Delete Multiple Objects) is used to delete objects in batch. To grant this permission, the `action` in the policy is `name/cos:DeleteObject`.

#### Example 

The following policy grants the permission to delete the objects `audio.mp3` and `video.mp4` within the bucket `example-1253653367` in the region `ap-beijing` under the APPID 1253653367 in batch:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:DeleteObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/audio.mp3",
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/video.mp4"
      ]
    }
  ]
}
```

## Authorization Policies in Common Scenarios

### Grant full real-write access to all resources
The following policy grants full real-write access to all resources:
```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "*"
      ],
      "effect": "allow",
      "resource": [
        "*"
      ]
    }
  ]
}
```

### Grant the real-only access to all resources
The following policy grants the real-only access to all resources:
```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:Head*",
        "name/cos:Get*",
        "name/cos:List*",
        "name/cos:OptionsObject"
      ],
      "effect": "allow",
      "resource": [
        "*"
      ]
    }
  ]
}
```

### Grant the real-write access to any resource under the path with specified prefix
The following policy grants a user the permission to access files under the path with prefix userID123456 in the bucket example-1253653367, and does not allow the user to perform operations on the files in other paths.
```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "*"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-shanghai:uid/1253653367:prefix//1253653367/example/userID123456/*"
      ]
    }
  ]
}
```


