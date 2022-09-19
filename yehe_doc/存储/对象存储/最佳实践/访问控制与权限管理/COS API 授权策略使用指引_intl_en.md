>! When granting API access permissions to a sub-user or collaborator, be sure to follow the principle of least privilege and grant the minimum set of permissions necessary to satisfy business needs. There may be data security risks if you grant excessive access to all of your resources `(resource:*)` or all operations `(action:*)`.
>


## Overview

When using a temporary key to access COS, the operation permissions required vary by API or series of APIs that you specify.

A COS API authorization policy is a JSON string. For example, below is a policy that grants the permission to perform uploads (including simple upload, upload through an HTML form, and multipart upload) for objects prefixed with `doc` and downloads for objects prefixed with `doc2` for the bucket `examplebucket-1250000000` in the region "ap-beijing" under the APPID `1250000000`:
```shell
{
	"version": "2.0",
	"statement": [{
			"action": [
				// Upload an object by using simple upload 
				"name/cos:PutObject",
				// Upload an object by using an HTML form 
				"name/cos:PostObject",
				// Initialize a multipart upload 
				"name/cos:InitiateMultipartUpload",
				// List all ongoing multipart uploads
				"name/cos:ListMultipartUploads",
				// List uploaded parts 
				"name/cos:ListParts",
				// Upload parts 
				"name/cos:UploadPart",
				// Complete a multipart upload 
				"name/cos:CompleteMultipartUpload",
				// Abort a multipart upload 
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

## Authorization Policy Elements

| Name | Description |
| -------- | ------------------------------------------------------------ |
| version | Policy syntax version, which is 2.0 by default. |
| effect | Allow or deny. |
| resource | Specific data of the authorized operation, which can be any resources, resources with a specified path prefix, resource in a specified absolute path, or their combination. <br> |
| action | COS API. You can specify one, several, or all (`*`) COS APIs as needed, such as `name/cos:GetService`. **Note that this value is case-sensitive**.       |
| condition | Optional condition. For more information, see [Element Reference](https://intl.cloud.tencent.com/document/product/598/10603). |

Examples of authorization policy settings for each COS API are as listed below.

## Service APIs

### Querying bucket list

To grant access to the `GET Service` API, the `action` field in the policy should be set to `name/cos:GetService`, and the `resource` field to `*`.

#### Sample 

The following policy grants the permission to query the bucket list:

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

The `resource` field for bucket API policies is outlined in further detail below:

- To allow access to buckets in all regions
The `resource` field should be set to `*`. **Use this option with caution as it may present data security risks due to excessive permissions.**
- To allow access only to buckets in a specified region
For example, to grant access to `examplebucket-1250000000` under the APPID `1250000000` in the region `ap-beijing`, the `resource` field should be set to `qcs::cos:ap-beijing:uid/1250000000:*`.
- To allow access only to a bucket with a specified name in a specified region
- For example, to grant access to the bucket named `examplebucket-1250000000` under the APPID `1250000000` in the region `ap-beijing`, the `resource` field should be set to `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*`.

The `action` field in bucket API policies varies by operation. The following lists several bucket API policies for your reference.

### Creating bucket 

To grant access to the `PUT Bucket` API, the `action` field in the policy should be set to name/cos:PutBucket.

#### Sample 

The following policy grants the user with the APPID `1250000000` permission to create a bucket named `examplebucket-1250000000` in Beijing region:

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

>? For bucket naming rules, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312).
>

### Extracting bucket and its permissions  

To grant the access to the `HEAD Bucket` API, the `action` field in the policy should be set to `name/cos:HeadBucket`.

#### Sample 

The following policy grants the permission to extract only the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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

To grant access to the `GET Bucket` API, the `action` field in the policy should be set to `name/cos:GetBucket`.

#### Sample 

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

### Deleting bucket

To grant access to the `Delete Bucket` API, the `action` field in the policy should be set to `name/cos:DeleteBucket`.

#### Sample 

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

To grant access to the `Put Bucket ACL` API, the `action` field in the policy should be set to `name/cos:PutBucketACL`.

#### Sample 

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

To grant access to the `GET Bucket acl` API, the `action` field in the policy should be set to `name/cos:GetBucketACL`.

#### Sample 

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

### Setting CORS configuration

To grant access to the `PUT Bucket cors` API, the `action` field in the policy should be set to `name/cos:PutBucketCORS`.

#### Sample 

The following policy grants the permission to set a CORS configuration only for the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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

### Querying CORS configuration

To grant access to the `GET Bucket cors` API, the `action` field in the policy should be set to `name/cos:GetBucketCORS`.

#### Sample 

The following policy grants the permission to query the CORS configuration only of the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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

### Deleting CORS configuration

To grant access to the `DELETE Bucket cors` API, the `action` field in the policy should be set to `name/cos:DeleteBucketCORS`.

#### Sample 

The following policy grants the permission to delete the CORS configuration only of the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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

### Setting lifecycle configuration

To grant access to the `PUT Bucket lifecycle` API, the `action` field in the policy should be set to `name/cos:PutBucketLifecycle`.

#### Sample 

The following policy grants the permission to set a lifecycle configuration only for the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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

### Querying lifecycle configuration

To grant access to the `GET Bucket lifecycle` API, the `action` field in the policy should be set to `name/cos:GetBucketLifecycle`.

#### Sample 

The following policy grants the permission to query the lifecycle configuration only of the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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

### Deleting lifecycle configuration

To grant access to the `DELETE Bucket lifecycle` API, the `action` field in the policy should be set to `name/cos:DeleteBucketLifecycle`.

#### Sample 

The following policy grants the permission to delete the lifecycle configuration only of the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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


## Object APIs

The `resource` field for object API policies is outlined in further detail below:

- To grant access to all objects, the `resource` field should be set to `*`.
- To grant access only to objects in a specified bucket, such as objects in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`, the `resource` field should be set to `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*`.
- To grant access only to objects with a specified path prefix in a specified bucket, such as objects with the path prefix `doc` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`, the `resource` field should be set to `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*`.
- To grant access only to an object in a specified absolute path, such as the object in the absolute path `doc/audio.mp3` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`, the `resource` field should be set to `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/audio.mp3`.


The `action` field in object API policies varies by operation. All object API policies are as listed below.

### Uploading object by using simple upload

To grant access to the `PUT Object` API, the `action` field in the policy should be set to `name/cos:PutObject`.

#### Sample 

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

Multipart upload APIs include `Initiate Multipart Upload`, `List Multipart Uploads`, `List Parts`, `Upload Part`, `Complete Multipart Upload`, and `Abort Multipart Upload`. To grant access to these APIs, the `action` field in the policy should be a collection of `"name/cos:InitiateMultipartUpload","name/cos:ListMultipartUploads","name/cos:ListParts","name/cos:UploadPart","name/cos:CompleteMultipartUpload","name/cos:AbortMultipartUpload"`.

#### Sample 

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

### Querying multipart upload

To grant access to this API, the `action` field in the policy should be set to `name/cos:ListMultipartUploads`.

#### Sample 

The following policy grants the permission to query ongoing multipart uploads only in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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


### Uploading object by using HTML form

To grant access to the `POST Object` API, the `action` field in the policy should be set to `name/cos:PostObject`.

#### Sample 

The following policy grants the permission to use the `POST` method to upload only objects with the path prefix `doc` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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

### Appending parts

To grant access to the `Append Object` API, the `action` field in the policy should be set to `name/cos:AppendObject`.

#### Sample 

The following policy grants permission to append parts to objects with the path prefix `doc` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

```shell
 {
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:AppendObject"
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

To grant access to the `HEAD Object` API, the `action` field in the policy should be set to `name/cos:HeadObject`.

#### Sample 

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

### Downloading object

To grant access to the `GET Object` API, the `action` field in the policy should be set to `name/cos:GetObject`.

#### Sample 

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

### Copying object

To grant access to the `Put Object Copy` API, the `action` field for the destination object should be set to `name/cos:PutObject`, and the `action` field for the source object should be set to `name/cos:GetObject`.

#### Sample 

The following policy grants the permission to use multipart copy to copy objects from the path prefixed with `doc` to the path prefixed with `doc2` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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

### Copying part

To grant access to the `Upload Part - Copy` API, the `action` field for the destination object should be a collection of `"name/cos:InitiateMultipartUpload","name/cos:ListMultipartUploads","name/cos:ListParts","name/cos:PutObject","name/cos:CompleteMultipartUpload","name/cos:AbortMultipartUpload"`, and the `action` field for the source object should be set to `name/cos:GetObject`.

#### Sample 

The following policy grants the permission to use multipart copy to copy objects from the path prefixed with `doc` to the path prefixed with `doc2` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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

To grant access to the `Put Object ACL` API, the `action` field in the policy should be set to `name/cos:PutObjectACL`.

#### Sample 

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

### Querying object ACL

To grant access to the `Get Object ACL` API, the `action` field in the policy should be set to `name/cos:GetObjectACL`.

#### Sample 

The following policy grants the permission to query the ACL only of objects with the path prefix `doc` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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

### Checking CORS configuration

To grant access to the `OPTIONS Object` API, the `action` field in the policy should be set to `name/cos:OptionsObject`.

#### Sample 

The following policy grants the permission to send an `OPTIONS` request only for objects with the path prefix `doc` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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

### Restoring archived object

To grant access to the `Post Object Restore` API, the `action` field in the policy should be set to `name/cos:PostObjectRestore`.

#### Sample 

The following policy grants the permission to restore archived objects only with the path prefix `doc` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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

### Deleting object

To grant access to the `DELETE Object` API, the `action` field in the policy should be set to `name/cos:DeleteObject`.

#### Sample 

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

To grant access to the `DELETE Multiple Objects` API, the `action` field in the policy should be set to `name/cos:DeleteObject`.

#### Sample 

The following policy grants the permission to batch delete only the objects `audio.mp3` and `video.mp4` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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

## Authorization Policies for Common Scenarios

### Granting full access to all resources
The following policy grants full access to all resources:
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

### Granting read-only access to all resources
The following policy grants read-only access to all resources:
```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:HeadObject",
        "name/cos:GetObject",
        "name/cos:GetBucket",
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

### Granting read-write access to resources with specified path prefix
The following policy grants the permission to access only files with the path prefix `doc` in the bucket `examplebucket-1250000000` and does not allow any operations on files in other paths:
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

