>Note:
>When granting API operations permissions to child users or collaborators, be sure to authorize them according to the business needs and the principle of least privilege. If you directly grant sub-users or collaborators all resources (`resource:*`), or all actions (`action:*`) permissions, there is a data security risk due to excessive permission scope.

## Overview
When COS uses the temporary key service, different permissions should be granted to perform actions on different COS APIs. An action or a set of actions can be specified.

A COS API policy is a JSON string. For example, below is a policy to grant the permission to perform upload operations (including simple upload, form upload, and multipart upload) for objects with the path prefix `doc2` in the bucket `examplebucket-1250000000` in the region "ap-beijing" under the APPID `1250000000`:
```shell
{
	"version": "2.0",
	"statement": [{
			"action": [
				// Simple upload 
				"name/cos:PutObject",
				// Form upload 
				"name/cos:PostObject",
				// Multipart upload: initialize multipart upload 
				"name/cos:InitiateMultipartUpload",
				// Multipart upload: list uploaded parts 
				"name/cos:ListParts",
				// Multipart upload: upload parts 
				"name/cos:UploadPart",
				// Multipart upload: complete the upload of all parts 
				"name/cos:CompleteMultipartUpload",
				// Cancel multipart Upload 
				"name/cos:AbortMultipartUpload"
			],
			"effect": "allow",
			"resource": [
				"qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
			]
		},
		{
			"action": [
				// Download 
				"name/cos:GetObject"
			],
			"effect": "allow",
			"resource": [
				"qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc2/*"
			]
		}
	]
}
```

<a id="policy"></a>
#### Description of Policy Elements

| Name | Description |
| -------- | ------------------------------------------------------------ |
| version | Version of policy syntax, which is 2.0 by default |
| effect | Allow and Deny |
| resource | Specific data authorized to be operated on. It can be any resource, resources in a path with the specified prefix, resources in the specified absolute path, or a combination of them |
| action   | Indicates COS APIs, which is used to specify an action, a set of actions, or all actions (*) as needed |
| condition | Condition, which is optional. For more information, see [Condition](https://intl.cloud.tencent.com/document/product/598/10603#6..E7.94.9F.E6.95.88.E6.9D.A1.E4.BB.B6(condition)) |

Examples of policy settings for each COS API are listed below.

## Service APIs 

### Querying Bucket List

The API is GET Service. To grant this permission, the `action` in the policy should be `name/cos:GetService` and the `resource` should be `*`.

#### Example 

The following policy grants the permission to query the list of buckets:

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

## Bucket APIs

The `resource` in Bucket API policies can be described as follows:

- To perform operations on a bucket in any region, the `resource` should be `*`.
- To perform operations only on a bucket in the specified region, for example, to operate on a bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`, the `resource` should be `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*`.
- To perform operations only on a bucket with the specified name in the specified region, for example, to operate on the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`, the `resource` should be `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/`.

The `action` in Bucket API policies varies by operation. All Bucket API policies are listed below.

### Creating a Bucket 

The API is PUT Bucket. To grant this permission, the `action` in the policy should be `name/cos:PutBucket`.

#### Example 

The following policy grants the permission to create a bucket with an arbitrary name in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*"
      ]
    }
  ]
}
```

### Checking a Bucket and Its Permission  

The API is HEAD Bucket. To grant this permission, the `action` in the policy should be `name/cos:HeadBucket`.

#### Example 

The following policy grants the permission to retrieve only the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```


### Querying Object List

The API is GET Bucket. To grant this permission, the `action` in the policy should be `name/cos:GetBucket`.

#### Example 

The following policy grants the permission to query only the list of objects in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```

### Deleting a Bucket

The API is Delete Bucket. To grant this permission, the `action` in the policy should be `name/cos:DeleteBucket`.

#### Example 

The following policy grants the permission to delete only the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```

### Setting Bucket ACL 

The API is Put Bucket ACL. To grant this permission, the `action` in the policy should be `name/cos:PutBucketACL`.

#### Example 

The following policy grants the permission to set an ACL only for the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```

### Querying Bucket ACL

The API is GET Bucket acl. To grant this permission, the `action` in the policy should be `name/cos:GetBucketACL`.

#### Example 

The following policy grants the permission to get the ACL only of the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```

### Setting Cross-origin Access Configuration

The API is PUT Bucket cors. To grant this permission, the `action` in the policy should be `name/cos:PutBucketCORS`.

#### Example 

The following policy grants the permission to set the cross-origin access configuration only for the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```

### Querying Cross-origin Access Configuration

The API is GET Bucket cors. To grant this permission, the `action` in the policy should be `name/cos:GetBucketCORS`.

#### Example 

The following policy grants the permission to query the cross-origin access configuration only of the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```

### Deleting Cross-origin Access Configuration

The API is DELETE Bucket cors. To grant this permission, the `action` in the policy should be `name/cos:DeleteBucketCORS`.

#### Example 

The following policy grants the permission to delete the cross-origin access configuration only of the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```

### Setting Lifecycle

The API is PUT Bucket lifecycle. To grant this permission, the `action` in the policy should be `name/cos:PutBucketLifecycle`.

#### Example 

The following policy grants the permission to set the lifecycle only for the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```

### Querying Lifecycle

The API is GET Bucket lifecycle. To grant this permission, the `action` in the policy should be `name/cos:GetBucketLifecycle`.

#### Example 

The following policy grants the permission to query the lifecycle only of the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```

### Deleting Lifecycle

The API is DELETE Bucket lifecycle. To grant this permission, the `action` in the policy should be `name/cos:DeleteBucketLifecycle`.

#### Example 

The following policy grants the permission to delete the lifecycle only of the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```

### Querying a Multipart Upload

This API is used to query in-progress multipart uploads in a bucket. To grant this permission, the `action` in the policy should be `name/cos:ListMultipartUploads`.

#### Example 

The following policy grants the permission to query in-progress multipart uploads only in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```



## Object APIs

The `resource` in Object API policies can be described as follows:

- To perform operations on any object, the `resource` should be `*`.
- To perform operations only on objects in the specified bucket, for example, to operate on any objects in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`, the `resource` should be `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*`.
- To perform operations only on objects in the specified bucket with the specified path prefix, for example, to operate on any objects in the bucket `examplebucket-1250000000` in the region `ap-beijing` with the path prefix `doc` under the APPID `1250000000`, the `resource` should be `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*`.
- To perform operations only on the object in the specified absolute path, for example, to operate on the object in the absolute path `doc/audio.mp3` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`, the `resource` should be `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/audio.mp3`.


The `action` in Object API policies varies by operation. All Object API policies are listed below.

### Upload an Object using Simple Upload

The API is PUT Object. To grant this permission, the `action` in the policy should be `name/cos:PutObject`.

#### Example 

The following policy grants the permission to use simple upload to upload only objects with the path prefix `doc` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    }
  ]
}
```

### Multipart Upload 

Multipart upload APIs include Initiate Multipart Upload, List Parts, Upload Part, Complete Multipart Upload, and Abort Multipart Upload. To grant these permissions, the `action` in the policy should be a collection of `"name/cos:InitiateMultipartUpload","name/cos:ListParts","name/cos:UploadPart","name/cos:CompleteMultipartUpload","name/cos:AbortMultipartUpload"`.

#### Example 

The following policy grants the permission to use multipart upload to upload only objects with the path prefix `doc` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    }
  ]
}
```

### Uploading an Object Using a Form

The API is POST Object. To grant this permission, the `action` in the policy should be `name/cos:PostObject`.

#### Example 

The following policy grants the permission to use the POST method to upload only objects with the path prefix `doc` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    }
  ]
}
```

### Querying Object Metadata

The API is HEAD Object. To grant this permission, the `action` in the policy should be `name/cos:HeadObject`.

#### Example 

The following policy grants the permission to query objects only with the path prefix `doc` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    }
  ]
}
```

### Downloading an Object

The API is GET Object. To grant this permission, the `action` in the policy should be `name/cos:GetObject`.

#### Example 

The following policy grants the permission to download only objects with the path prefix `doc` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    }
  ]
}
```

### Copying an Object

The API is Put Object Copy. To grant this permission, the `action` of the destination object in the policy should be `name/cos:PutObject` and the `action` of the source object should be `name/cos:GetObject`.

#### Example 

The following policy grants the permission to use multipart copy to copy any objects between the path prefixed with `doc` and the path prefixed with `doc2` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    },
    {
      "action": [
        "name/cos:GetObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc2/*"
      ]
    }
  ]
}
```

Here, `"qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc2/*"` is the source object.

### Copying Parts

The API is Upload Part - Copy. To grant this permission, the `action` of the destination object in the policy should be a collection of `"name/cos:InitiateMultipartUpload","name/cos:ListParts","name/cos:PutObject","name/cos:CompleteMultipartUpload","name/cos:AbortMultipartUpload"` and the `action` of the source object should be `name/cos:GetObject`.

#### Example 

The following policy grants the permission to use multipart copy to copy any objects between the path prefixed with `doc` and the path prefixed with `doc2` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    },
    {
      "action": [
        "name/cos:GetObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc2/*" 
      ]
    }
  ]
}
```

Here, `"qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc2/*"` is the source object.

### Setting Object ACL

The API is Put Object ACL. To grant this permission, the `action` in the policy should be `name/cos:PutObjectACL`.

#### Example 

The following policy grants the permission to set an ACL only for objects with the path prefix `doc` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    }
  ]
}
```

### Querying Object ACL

The API is Get Object ACL. To grant this permission, the `action` in the policy should be `name/cos:GetObjectACL`.

#### Example 

The following policy grants the permission to query the ACL only for objects with the path prefix `doc` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID ·1250000000·:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    }
  ]
}
```

### Pre-requesting Cross-origin Configuration

The API is OPTIONS Object. To grant this permission, the `action` in the policy should be `name/cos:OptionsObject`.

#### Example 

The following policy grants the permission to send an Options request only for objects with the path prefix `doc` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    }
  ]
}
```

### Restoring an Archived Object

The API is Post Object Restore. To grant this permission, the `action` in the policy should be `name/cos:PostObjectRestore`.

#### Example 

The following policy grants the permission to restore an archived object only with the path prefix `doc` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    }
  ]
}
```

### Deleting a Single Object

The API is DELETE Object. To grant this permission, the `action` in the policy should be `name/cos:DeleteObject`.

#### Example 

The following policy grants the permission to delete only the object `audio.mp3` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/audio.mp3"
      ]
    }
  ]
}
```

### Deleting Multiple Objects

The API is DELETE Multiple Objects. To grant this permission, the `action` in the policy should be `name/cos:DeleteObject`.

#### Example 

The following policy grants the permission to delete only the objects `audio.mp3` and `video.mp4` in batches in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/audio.mp3",
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/video.mp4"
      ]
    }
  ]
}
```

## Authorization Policies in Common Scenarios

### Granting Read/Write Access to All Resources
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

### Granting Read-only Access to All Resources
The following policy grants the real-only access to all resources:
```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:HeadObject",
        "name/cos:GetObject",
        "name/cos:ListObject",
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

### Granting Read/Write Access to Resources with the Specified Path Prefix
The following policy grants the permission to access only files under the path with prefix `doc` in the bucket `examplebucket-1250000000` and does not allow performing operations on the files in other paths.
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
        "qcs::cos:ap-shanghai:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    }
  ]
}
```

