>!When granting access permissions to a sub-user or collaborator, please be sure to grant the minimum set of API access permissions needed to satisfy your business needs. There may be data security risks associated with granting excessive access to all of your resources `(resource:*)` or all operations `(action:*)`.


## Overview
When using a temporary key to access COS, the operation permissions required vary depending on the API or series of APIs that you specify.

A COS API access policy is a JSON string. For example, below is a policy that grants the permission to perform uploads (including simple upload, upload using an HTML form, and multipart upload) for objects prefixed with `doc` and downloads for objects prefixed with `doc2` for the bucket `examplebucket-1250000000` in the region "ap-beijing" under the APPID `1250000000`:
```shell
{
	"version": "2.0",
	"statement": [{
			"action": [
				// Upload an object using simple upload 
				"name/cos:PutObject",
				// Upload an object using an HTML form 
				"name/cos:PostObject",
				// Initialize a multipart upload operation 
				"name/cos:InitiateMultipartUpload",
				// List all in-progress multipart upload operations
				"name/cos:ListMultipartUploads",
				// List uploaded parts 
				"name/cos:ListParts",
				// Upload parts 
				"name/cos:UploadPart",
				// Complete a multipart upload operation 
				"name/cos:CompleteMultipartUpload",
				// Abort a multipart upload operation 
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
| version | The policy syntax version. The default is 2.0. |
| effect | Allow or deny |
| resource | Specific data authorized to be operated on. It can be any resource, a resource in a path with a specified prefix, a resource in a specified absolute path, or a combination thereof. |
| action | COS API. You can specify one, several, or all (`*`) COS APIs as needed, e.g. `name/cos:GetService`. **Note that this value is case-sensitive**.       |
| condition | Condition (this value is optional). For more information, see [Condition](https://intl.cloud.tencent.com/document/product/598/10603) |

Examples of access policy settings for each COS API are listed below.

## Service API

### Querying the bucket list

To grant permission to access this API, the `action` field in the policy should be set to `name/cos:GetService`, and the `resource` field should be set to `*`.

#### Samples 

The following policy grants the permission to query a bucket list:

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

The `resource` field for bucket API access policies is outlined in further detail below:

- To allow access to buckets in all regions
the `resource` field should be set to `*`. **Please use this option with caution as it may present data security risks due to excessive permissions**.

- To only allow access to buckets in a specified region, the `resource` field should be configured as shown in the following example:
For example, to grant access to `examplebucket-1250000000` under the APPID `1250000000` in the region `ap-beijing`, the `resource` field should be `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*`.

- To only allow access to a bucket with a specified name in a specified region, the `resource` field should be configured as shown in the following example:
- For example, to grant access to the bucket named `examplebucket-1250000000` under the APPID `1250000000` in the region `ap-beijing`, the `resource` field should be `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/`.

The `action` field for bucket API policies varies by operation. The following section lists several bucket API access policies for your reference.

### Creating a bucket 

To grant permission to access this API, the `action` field in the policy should be set to `name/cos:PutBucket`.

#### Samples 

The following policy grants the user with the APPID `1250000000` permission to create a bucket named `examplebucket-1250000000` in the Beijing region:

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

>?For bucket naming rules, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312).

### Extracting a bucket and its permissions  

To grant permission to access this API, the `action` field in the policy should be set to `name/cos:HeadBucket`.

#### Samples 

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


### Querying objects

To grant permission to access this API, the `action` field in the policy should be set to `name/cos:GetBucket`.

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

To grant permission to access this API, the `action` field in the policy should be set to `name/cos:DeleteBucket`.

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

### Setting a bucket ACL 

To grant permission to access this API, the `action` field in the policy should be set to `name/cos:PutBucketACL`.

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

### Querying a bucket ACL

To grant permission to access this API, the `action` field in the policy should be set to `name/cos:GetBucketACL`.

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

### Setting CORS

To grant permission to access this API, the `action` field in the policy should be set to `name/cos:PutBucketCORS`.

#### Samples 

The following policy grants the permission to set a cross-origin access configuration only for the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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

### Querying a CORS configuration

To grant permission to access this API, the `action` field in the policy should be set to `name/cos:GetBucketCORS`.

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

### Deleting CORS configuration

To grant permission to access this API, the `action` field in the policy should be set to `name/cos:DeleteBucketCORS`.

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

### Setting lifecycle configuration

To grant permission to access this API, the `action` field in the policy should be set to `name/cos:PutBucketLifecycle`.

#### Samples 

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

### Querying a lifecycle configuration

To grant permission to access this API, the `action` field in the policy should be set to `name/cos:GetBucketLifecycle`.

#### Samples 

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

### Deleting a lifecycle configuration

To grant permission to access this API, the `action` field in the policy should be set to `name/cos:DeleteBucketLifecycle`.

#### Samples 

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


## Object API

The `resource` field for object API access policies is outlined in further detail below:

- To grant access to all objects, the `resource` field should be `*`.
- To only grant access to objects in a specified bucket, such as objects in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`, the `resource` field should be `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*`.
- To only grant access to objects with a specified path prefix in a specified bucket, such as objects with the path prefix `doc` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`, the `resource` field should be `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*`.
- To access only an object in a specified absolute path, such as the object in the absolute path `doc/audio.mp3` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`, the `resource` field should be `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/audio.mp3`.


The `action` field for Object API access policies varies by operation. All Object API access policies are listed below.

### Uploading an object using simple upload

To grant permission to access this API, the `action` field in the policy should be set to `name/cos:PutObject`.

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

Multipart upload APIs include Initiate Multipart Upload, List Multipart Uploads, List Parts, Upload Part, Complete Multipart Upload, and Abort Multipart Upload. To grant permission for these APIs, the `action` field in the policy should be a collection of `"name/cos:InitiateMultipartUpload","name/cos:ListMultipartUploads",
"name/cos:ListParts","name/cos:UploadPart",
"name/cos:CompleteMultipartUpload","name/cos:AbortMultipartUpload"`.

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

### Querying multipart uploads

To grant the permission to access this API, the `action` field in the policy should be set to `name/cos:ListMultipartUploads`.

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


### Uploading an object using an HTML form

To grant permission to access this API, the `action` field in the policy should be set to `name/cos:PostObject`.

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

### Appending parts

To grant permission to access this API (Append Object), set the `action` field in the policy to `name/cos:AppendObject`.

#### Samples 

The following policy grants permission to use append upload for objects with the path prefix `doc` in the bucket `examplebucket-1250000000` residing in the region `ap-beijing` under the account whose `APPID` is `1250000000`:

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

To grant permission to access this API, the `action` field in the policy should be set to `name/cos:HeadObject`.

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

To grant permission to access this API, the `action` field in the policy should be set to `name/cos:GetObject`.

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

### Copying objects

To grant permission to access this API, the `action` field for the destination object should be set to `name/cos:PutObject` and the `action` field for the source object should be set to `name/cos:GetObject`.

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

### Copying an object part

To grant permission to access this API, the `action` field for the destination object should be a collection of `"name/cos:InitiateMultipartUpload","name/cos:ListParts",
"name/cos:PutObject","name/cos:CompleteMultipartUpload",
"name/cos:AbortMultipartUpload"` and the `action` field for the source object should be set to `name/cos:GetObject`.

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

### Setting an object ACL

To grant permission to access this API, the `action` field in the policy should be set to `name/cos:PutObjectACL`.

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

### Querying an object ACL

To grant permission to access this API, the `action` field in the policy should be set to `name/cos:GetObjectACL`.

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

### Checking CORS configuration

To grant permission to access this API, the `action` field in the policy should be set to `name/cos:OptionsObject`.

#### Samples 

The following policy grants the permission to send an OPTIONS request only for objects with the path prefix `doc` in the bucket `examplebucket-1250000000` in the region `ap-beijing` under the APPID `1250000000`:

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

To grant permission to access this API, the `action` field in the policy should be set to `name/cos:PostObjectRestore`.

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

### Deleting an object

To grant permission to access this API, the `action` field in the policy should be set to `name/cos:DeleteObject`.

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

To grant permission to access this API, the `action` field in the policy should be set to `name/cos:DeleteObject`.

#### Samples 

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

## Common Scenarios

### Granting full read-write permission for all resources
The following policy grants full read-write permission for all resources:
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

### Granting read-only permission for all resources
The following policy grants read-only permission for all resources:
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

### Granting read-write permission for any resource under a specified path with a specified prefix
The following policy grants the permission to access only files under the path with prefix `doc` in the bucket `examplebucket-1250000000` and does not allow any operations on files in other paths:
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

