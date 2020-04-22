>When granting subusers or collaborators the permissions to use APIs, be sure to authorize only based on your actual business needs under the principle of least privilege. If you directly grant them the access to all resource `(resource:*)` or all operations `(action:*)`, there will be data security risks due to excessive permissions.


## Overview
When COS uses a temporary key service, different COS API operations require different operation permissions, and one operation or a sequence of operations can be specified.

A COS API authorization policy is a JSON string. For example, to grant the permission to perform uploads (including simple uploads, uploads through form, and multipart uploads) under the path prefix of `doc` and perform downloads under the path prefix of `doc2` in the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:
```shell
{
	"version": "2.0",
	"statement": [{
			"action": [
				// Simple upload operation 
				"name/cos:PutObject",
				// Upload an object through form 
				"name/cos:PostObject",
				// Multipart upload: initializes a multipart upload 
				"name/cos:InitiateMultipartUpload",
				// Multipart upload: lists multipart uploads in progress
				"name/cos:ListMultipartUploads",
				// Multipart upload: lists uploaded parts 
				"name/cos:ListParts",
				// Multipart upload: uploads parts 
				"name/cos:UploadPart",
				// Multipart upload: completes the upload of all parts 
				"name/cos:CompleteMultipartUpload",
				// Cancel multipart upload 
				"name/cos:AbortMultipartUpload"
			],
			"effect": "allow",
			"resource": [
				"qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
			]
		},
		{
			"action": [
				// Download operation 
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
#### Descriptions of authorization policy elements

| Name | Description |
| -------- | ------------------------------------------------------------ |
| version | Policy syntax version. Default value: 2.0 |
| effect   | `allow` or `deny`                |
| resource | Specific data of authorized operations, which can be any resource, resources under a specified path prefix, a resource at a specified absolute path, or a combination of them |
| action   | This parameter refers to a COS API here, which is used to specify one operation, a sequence of operations, or all operations (`*`) as needed       |
|condition| Condition, which is optional. For more information, please see [Condition](https://intl.cloud.tencent.com/document/product/598/10603)  |

Below are sample authorization policies for various COS APIs.

## Service APIs 

### Querying bucket list

The API is `GET Service`. To grant the permission to use it, the `action` in the policy should be `name/cos:GetService` and the `resource` should be `*`.

#### Sample 

To grant the permission to query the bucket list, use the following policy:

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

The `resource` parameter in policies for bucket APIs can be summarized into the following situations:

- To allow operations on buckets in any region, the `resource` in the policy should be `*`.
- To allow operations on a bucket in a specified region, such as the bucket `examplebucket-1250000000` under the `APPID` of `1250000000` in the `ap-beijing` region, the `resource` in the policy should be `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*`.
- To allow operations on a bucket with a specified name in a specified region, such as the bucket named `examplebucket-1250000000` under the `APPID` of `1250000000` in the `ap-beijing` region, the `resource` in the policy should be `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/`.

The value of `action` in policies for bucket APIs varies by operation, including:

### Creating a bucket 

The API is `PUT Bucket`. To grant the permission to use it, the `action` in the policy should be `name/cos:PutBucket`.

#### Sample 

To grant the permission to create a bucket with any name under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

### Checking a bucket and its permission  

The API is `HEAD Bucket`. To grant the permission to use it, the `action` in the policy should be `name/cos:HeadBucket`.

#### Sample 

To grant the permission to check only the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

The API is `GET Bucket`. To grant the permission to use it, the `action` in the policy should be `name/cos:GetBucket`.

#### Sample 

To grant the permission to query the list of objects only in the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

The API is `Delete Bucket`. To grant the permission to use it, the `action` in the policy should be `name/cos:DeleteBucket`.

#### Sample 

To grant the permission to delete only the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

The API is `Put Bucket ACL`. To grant the permission to use it, the `action` in the policy should be `name/cos:PutBucketACL`.

#### Sample 

To grant the permission to set the ACL only for the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

The API is `GET Bucket acl`. To grant the permission to use it, the `action` in the policy should be `name/cos:GetBucketACL`.

#### Sample 

To grant the permission to get the ACL only of the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

### Setting cross-origin access configuration

The API is `PUT Bucket cors`. To grant the permission to use it, the `action` in the policy should be `name/cos:PutBucketCORS`.

#### Sample 

To grant the permission to set the cross-origin access configuration only for the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

The API is `GET Bucket cors`. To grant the permission to use it, the `action` in the policy should be `name/cos:GetBucketCORS`.

#### Sample 

To grant the permission to query the cross-origin access configuration only of the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

### Deleting cross-origin access configuration

The API is `DELETE Bucket cors`. To grant the permission to use it, the `action` in the policy should be `name/cos:DeleteBucketCORS`.

#### Sample 

To grant the permission to delete the cross-origin access configuration only for the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

The API is `PUT Bucket lifecycle`. To grant the permission to use it, the `action` in the policy should be `name/cos:PutBucketLifecycle`.

#### Sample 

To grant the permission to set the lifecycle configuration only for the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

The API is `GET Bucket lifecycle`. To grant the permission to use it, the `action` in the policy should be `name/cos:GetBucketLifecycle`.

#### Sample 

To grant the permission to query the lifecycle configuration only of the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

The API is `DELETE Bucket lifecycle`. To grant the permission to use it, the `action` in the policy should be `name/cos:DeleteBucketLifecycle`.

#### Sample 

To grant the permission to delete the lifecycle configuration only of the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

### Querying a multipart upload

This API is used to query the information of multipart uploads in progress in a bucket. To grant the permission to use it, the `action` in the policy should be `name/cos:ListMultipartUploads`.

#### Sample 

To grant the permission to query multipart uploads in progress only in the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

The `resource` parameter in policies for object APIs can be summarized into the following situations:

- To allow operations on any object, the `resource` in the policy should be `*`.
- To allow operations on any object in a specified bucket, such as any object in the bucket named `examplebucket-1250000000` under the `APPID` of `1250000000` in the `ap-beijing` region, the `resource` in the policy should be `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*`.
- To allow operations on any object under a specified path prefix in a specified bucket, such as any object under the path prefix of `doc` in the bucket `examplebucket-1250000000` under the `APPID` of `1250000000` in the `ap-beijing` region, the `resource` in the policy should be `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*`.
- To allow operations on an object at a specified absolute path, such as the object at the absolute path of `doc/audio.mp3` in the bucket `examplebucket-1250000000` under the `APPID` of `1250000000` in the `ap-beijing` region, the `resource` in the policy should be `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/audio.mp3`.


The value of `action` in policies for object APIs varies by operation, including:

### Simply uploading an object

The API is `PUT Object`. To grant the permission to use it, the `action` in the policy should be `name/cos:PutObject`.

#### Sample 

To grant the permission to perform simple uploads only under the path prefix of `doc` in the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

Multipart upload APIs include `Initiate Multipart Upload`, `List Multipart Uploads`, `List Parts`, `Upload Part`, `Complete Multipart Upload`, and `Abort Multipart Upload`. To grant the permission to use them, the `action` in the policy should be the set of `"name/cos:InitiateMultipartUpload","name/cos:ListMultipartUploads","name/cos:ListParts","name/cos:UploadPart","name/cos:CompleteMultipartUpload","name/cos:AbortMultipartUpload"`.

#### Sample 

To grant the permission to perform multipart uploads only under the path prefix of `doc` in the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

### Uploading an object through form

The API is `POST Object`. To grant the permission to use it, the `action` in the policy should be `name/cos:PostObject`.

#### Sample 

To grant the permission to perform `POST` uploads only under the path prefix of `doc` in the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

The API is `HEAD Object`. To grant the permission to use it, the `action` in the policy should be `name/cos:HeadObject`.

#### Sample 

To grant the permission to query only the objects under the path prefix of `doc` in the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

The API is `GET Object`. To grant the permission to use it, the `action` in the policy should be `name/cos:GetObject`.

#### Sample 

To grant the permission to download only the objects under the path prefix of `doc` in the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

The API is `Put Object Copy`. To grant the permission to use it, the `action` of the destination object and the source object in the policy should be `name/cos:PutObject` and `name/cos:GetObject`, respectively.

#### Sample 

To grant the permission to perform multipart copies between the path prefixes of `doc` and `doc2` in the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

The API is `Upload Part - Copy`. To grant the permission to use it, the `action` of the destination object and the source object in the policy should be the set of `"name/cos:InitiateMultipartUpload","name/cos:ListMultipartUploads","name/cos:ListParts","name/cos:PutObject","name/cos:CompleteMultipartUpload","name/cos:AbortMultipartUpload"` and `name/cos:GetObject`, respectively.

#### Sample 

To grant the permission to perform multipart copies between the path prefixes of `doc` and `doc2` in the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

The API is `Put Object ACL`. To grant the permission to use it, the `action` in the policy should be `name/cos:PutObjectACL`.

#### Sample 

To grant the permission to set the ACL only for the objects under the path prefix of `doc` in the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

The API is `Get Object ACL`. To grant the permission to use it, the `action` in the policy should be `name/cos:GetObjectACL`.

#### Sample 

To grant the permission to query the ACL only of the objects under the path prefix of `doc` in the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

### Pre-requesting cross-origin configuration

The API is `OPTIONS Object`. To grant the permission to use it, the `action` in the policy should be `name/cos:OptionsObject`.

#### Sample 

To grant the permission to perform `OPTIONS` requests only under the path prefix of `doc` in the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

The API is `Post Object Restore`. To grant the permission to use it, the `action` in the policy should be `name/cos:PostObjectRestore`.

#### Sample 

To grant the permission to perform archive restoration only under the path prefix of `doc` in the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

The API is `DELETE Object`. To grant the permission to use it, the `action` in the policy should be `name/cos:DeleteObject`.

#### Sample 

To grant the permission to delete only the object `audio.mp3` in the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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

The API is `DELETE Multiple Objects`. To grant the permission to use it, the `action` in the policy should be `name/cos:DeleteObject`.

#### Sample 

To grant the permission to batch delete only the objects `audio.mp3`and `video.mp4` in the bucket `examplebucket-1250000000` under the `APPID` of `1250000000 ` in the `ap-beijing` region, use the following policy:

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
Tp grant the full access to all resources, use the following policy:
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
Tp grant the read-only access to all resources, use the following policy:
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

### Granting full access to a specified path prefix
To grant a user the access to only files under the path prefix of `doc` in the bucket `examplebucket-1250000000` but not files at other paths, use the following policy:
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

