>Be sure to grant the minimal set of API access permissions to a sub-user or collaborator. There may be data security risks due to excessive permissions if you grant them the access to all of your resources `(resource:*)` or all operations `(action:*)`.


## Overview
If you use temporary keys to access COS, the operation permissions required vary depending on the one or more COS APIs you specify.

A COS API access policy is a JSON string. For example, below is a policy that grants the permissions to perform uploads (including simple upload, upload using a HTML form, and multipart upload) for objects prefixed with `doc`, and downloads for objects prefixed with `doc2`, both in the bucket `examplebucket-1250000000` in the region "ap-beijing" under the APPID `1250000000`:
```shell
{
	"version": "2.0",
	"statement": [{
			"action": [
				// Upload an object using simple upload 
				"name/cos:PutObject",
				// Upload an object using a HTML form 
				"name/cos:PostObject",
				// Initialize a multipart upload 
				"name/cos:InitiateMultipartUpload",
				// List all in-progress multipart uploads
				"name/cos:ListMultipartUploads",
				// List uploaded parts 
				"name/cos:ListParts",
				// Upload parts 
				"name/cos:UploadPart",
				// Complete a multipart upload 
				"name/cos:CompleteMultipartUpload",
				// Cancel a multipart upload 
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
#### Access policy elements

| Name | Description |
| -------- | ------------------------------------------------------------ |
| version | The version of policy syntax. It defaults to 2.0. |
| effect | Allow and Deny |
| resource | Specific data authorized to be operated on. It can be any resource, a resource in a path with the specified prefix, a resource in the specified absolute path, or a combination thereof. |
| action   | COS API. You can specify one, a combination or all (`*`) of COS APIs as needed, e.g. `name/cos:GetService`. **Note that they are case-sensitive**.       |
| condition | Condition, which is optional. For more information, see [Condition](https://intl.cloud.tencent.com/document/product/598/10603) |

Examples of access policy settings for each COS API are listed below.

## Service API 

### Querying bucket list

The API is GET Service. To grant this permission, the `action` in the policy should be `name/cos:GetService` and the `resource` should be `*`.

#### Samples 

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

## Bucket API

The `resource` in Bucket API policies can be described as follows:

- To perform operations on a bucket in any region, the `resource` should be `*`.
- To perform operations only on a bucket in the specified region, for example, to operate on the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`, the `resource` should be `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*`.
- To perform operations only on a bucket with the specified name in the specified region, for example, to operate on the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`, the `resource` should be `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/`.

The `action` in Bucket API policies varies by operation. All Bucket API access policies are listed below.

### Creating a bucket 

The API is PUT Bucket. To grant this permission, the `action` in the policy should be `name/cos:PutBucket`.

#### Samples 

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```

### Retrieving a bucket and permissions  

The API is HEAD Bucket. To grant this permission, the `action` in the policy should be `name/cos:HeadBucket`.

#### Samples 

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


### Querying object list

The API is GET Bucket. To grant this permission, the `action` in the policy should be `name/cos:GetBucket`.

#### Samples 

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

### Deleting a bucket

The API is Delete Bucket. To grant this permission, the `action` in the policy should be `name/cos:DeleteBucket`.

#### Samples 

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

### Setting bucket ACL 

The API is Put Bucket ACL. To grant this permission, the `action` in the policy should be `name/cos:PutBucketACL`.

#### Samples 

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

### Querying bucket ACL

The API is GET Bucket acl. To grant this permission, the `action` in the policy should be `name/cos:GetBucketACL`.

#### Samples 

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

### Setting cross-origin configuration

The API is PUT Bucket cors. To grant this permission, the `action` in the policy should be `name/cos:PutBucketCORS`.

#### Samples 

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

### Querying cross-origin access configuration

The API is GET Bucket cors. To grant this permission, the `action` in the policy should be `name/cos:GetBucketCORS`.

#### Samples 

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

### Deleting cross-origin configuration

The API is DELETE Bucket cors. To grant this permission, the `action` in the policy should be `name/cos:DeleteBucketCORS`.

#### Samples 

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

### Setting lifecycle

The API is PUT Bucket lifecycle. To grant this permission, the `action` in the policy should be `name/cos:PutBucketLifecycle`.

#### Samples 

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

### Querying lifecycle

The API is GET Bucket lifecycle. To grant this permission, the `action` in the policy should be `name/cos:GetBucketLifecycle`.

#### Samples 

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

### Deleting lifecycle

The API is DELETE Bucket lifecycle. To grant this permission, the `action` in the policy should be `name/cos:DeleteBucketLifecycle`.

#### Samples 

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

### Querying multipart uploads

This API is used to query in-progress multipart uploads in a bucket. To grant this permission, the `action` in the policy should be `name/cos:ListMultipartUploads`.

#### Samples 

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



## Object API

The `resource` in Object API policies can be described as follows:

- To perform operations on any object, the `resource` should be `*`.
- To perform operations only on objects in the specified bucket, for example, to operate on any objects in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`, the `resource` should be `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*`.
- To perform operations only on objects in the specified bucket with the specified path prefix, for example, to operate on any objects in the bucket `examplebucket-1250000000` in the region `ap-beijing` with the path prefix `doc` under the APPID `1250000000`, the `resource` should be `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*`.
- To perform operations only on the object in the specified absolute path, for example, to operate on the object in the absolute path `doc/audio.mp3` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`, the `resource` should be `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/audio.mp3`.


The `action` in Object API policies varies by operation. All Object API access policies are listed below.

### Upload an object using simple upload

The API is PUT Object. To grant this permission, the `action` in the policy should be `name/cos:PutObject`.

#### Samples 

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

### Multipart upload 

Multipart upload APIs include Initiate Multipart Upload, List Multipart Uploads, List Parts, Upload Part, Complete Multipart Upload, and Abort Multipart Upload. To grant these permissions, the `action` in the policy should be a collection of `"name/cos:InitiateMultipartUpload","name/cos:ListMultipartUploads","name/cos:ListParts","name/cos:UploadPart","name/cos:CompleteMultipartUpload","name/cos:AbortMultipartUpload"`.

#### Samples 

The following policy grants the permission to use multipart upload to upload only objects with the path prefix `doc` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:InitiateMultipartUpload",
        "name/cos:ListMultipartUploads",
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

### Uploading an object using a HTML form

The API is POST Object. To grant this permission, the `action` in the policy should be `name/cos:PostObject`.

#### Samples 

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

### Querying object metadata

The API is HEAD Object. To grant this permission, the `action` in the policy should be `name/cos:HeadObject`.

#### Samples 

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

### Downloading an object

The API is GET Object. To grant this permission, the `action` in the policy should be `name/cos:GetObject`.

#### Samples 

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

### Copying an object

The API is Put Object Copy. To grant this permission, the `action` of the destination object in the policy should be `name/cos:PutObject` and the `action` of the source object should be `name/cos:GetObject`.

#### Samples 

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

### Copying parts

The API is Upload Part - Copy. To grant this permission, the `action` of the destination object in the policy should be a collection of `"name/cos:InitiateMultipartUpload","name/cos:ListParts","name/cos:PutObject","name/cos:CompleteMultipartUpload","name/cos:AbortMultipartUpload"` and the `action` of the source object should be `name/cos:GetObject`.

#### Samples 

The following policy grants the permission to use multipart copy to copy any objects between the path prefixed with `doc` and the path prefixed with `doc2` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:InitiateMultipartUpload",
        "name/cos:ListMultipartUploads",
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

### Setting object ACL

The API is Put Object ACL. To grant this permission, the `action` in the policy should be `name/cos:PutObjectACL`.

#### Samples 

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

#### Samples 

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

### Configuring pre-flight request for cross-origin access

The API is OPTIONS Object. To grant this permission, the `action` in the policy should be `name/cos:OptionsObject`.

#### Samples 

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

### Restoring an archived object

The API is Post Object Restore. To grant this permission, the `action` in the policy should be `name/cos:PostObjectRestore`.

#### Samples 

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

### Deleting a single object

The API is DELETE Object. To grant this permission, the `action` in the policy should be `name/cos:DeleteObject`.

#### Samples 

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

### Deleting multiple objects

The API is DELETE Multiple Objects. To grant this permission, the `action` in the policy should be `name/cos:DeleteObject`.

#### Samples 

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

## Scenarios

### Granting full real-write access to all resources
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

### Granting the read-only access to all resources
The following policy grants the read-only access to all resources:
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

### Grant the read-write access to any resource under the path with specified prefix
The following policy grants the permission to access only files under the path with prefix `doc` in the bucket `examplebucket-1250000000` and does not allow any operations on files in other paths.
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

