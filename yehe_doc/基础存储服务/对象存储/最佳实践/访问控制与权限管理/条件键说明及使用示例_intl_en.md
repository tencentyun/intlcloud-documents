When using access policies to grant permissions, you can specify policy conditions to restrict user access sources and the storage classes of uploaded files as instructed in [Access Policy Language > Overview](https://intl.cloud.tencent.com/document/product/436/18023).

This document provides common examples of using COS condition keys in bucket policies. You can view all the condition keys supported by COS and applicable requests [here](https://intl.cloud.tencent.com/document/product/436/46205).

>? 
>- When using condition keys in writing a bucket policy, comply with the principle of least privilege, add the corresponding condition keys only applicable requests (actions), and avoid using the \* wildcard when specifying the actions. Using the wildcard will cause the requests to fail. For more information about condition keys, see [here](https://intl.cloud.tencent.com/document/product/436/46205).
>- When you create a policy in the CAM console, pay attention to the syntax format. The syntax elements of `version`, `principal`, `statement`, `effect`, `action`, `resource`, and `condition` must all begin with a letter in the same letter case.


## Use Cases of Condition Keys

<span id="RestrictUserAccessIP"></span>
### Restricting user access IPs (qcs:ip)

#### Condition key qcs:ip

You can use the `qcs:ip` condition key to restrict user access IPs. This condition key is applicable to all requests.

#### Example: allowing only user access from specified IPs

The policy in this example allows the sub-account with ID 100000000002 under the root account with ID 100000000001 (APPID: 1250000000) to upload and download objects regarding the `examplebucket-bj` bucket in Beijing region and the `exampleobject` object in the `examplebucket-gz` bucket in Guangzhou region, on condition that the access IP falls within the IP range `192.168.1.0/24` or is `101.226.100.185` or `101.226.100.186`.

```
{
    "version": "2.0",
    "principal":{
        "qcs":[
            "qcs::cam::uin/100000000001:uin/100000000002"
        ]
    },
    "statement": [
        {
            "effect": "allow",
            "action":[
                "name/cos:PutObject",
                "name/cos:GetObject"
            ],
            "resource": [
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-gz-1250000000/exampleobject"
            ],
            "condition":{
                "ip_equal":{
                    "qcs:ip":[
                        "192.168.1.0/24",
                        "101.226.100.185",
                        "101.226.100.186"
                    ]
                }
            }
        }
    ]
}
```

<span id="requester_vpc"></span>
### Restricting VPC IDs (vpc:requester_vpc)

#### Condition key vpc:requester_vpc

You can use the condition key `vpc:requester_vpc` to restrict the `vpcid` of user access. For more information on `vpcid`, see [Virtual Private Cloud](https://www.tencentcloud.com/document/product/215).

#### Example: restricting the VPC ID to aqp5jrc1

The policy in this example allows the sub-account with ID 100000000002 that belongs to the root account with ID 100000000001 (APPID: 1250000000) to access the bucket `examplebucket-1250000000`, on condition that the VPC ID is `aqp5jrc1`.

```
{
  "statement": [
    {
      "action":[
        "name/cos:*"
      ],
      "condition":{
        "string_equal":{
          "vpc:requester_vpc": [
            "vpc-aqp5jrc1"
          ]
        }
      },
      "effect": "allow",
      "principal":{
        "qcs":[
          "qcs::cam::uin/100000000001:uin/100000000002"
        ]
      },
      "resource": [
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*"
      ]
    }
  ],
  "version": "2.0"
}
```

<span id="versionid"></span>
### Allowing access only to the latest or specified version of an object (cos:versionid)

#### Request parameter versionid

The `versionid` request parameter specifies the version number of the object. For more information on versioning, see [Overview](https://intl.cloud.tencent.com/document/product/436/19883). When downloading an object (`GetObject`) or deleting an object (`DeleteObject`), you can use `versionid` to specify the object version to be manipulated. There are three different cases with `versionid`:

- If `versionid` is not carried, requests will apply to the latest version of the object by default.
- If `versionid` is an empty string, this is equivalent to the case where `versionId` is not carried.
- If `versionid` is `"null"`, for objects that are uploaded before versioning is enabled for a bucket, their version numbers will become the `"null"` string after versioning is enabled.


#### Condition key cos:versionid 

You can use the `cos:versionid` condition key to restrict the `versionid` request parameter.


#### Example 1: allowing users to get objects of a specified version

Assume that the root account with UIN 100000000001 that owns the bucket `examplebucket-1250000000` uses the following bucket policy to allow the sub-account with UIN 100000000002 to get objects of a specified version only.

According to the policy, object download requests sent the sub-account with UIN 100000000002 can be successful only when they carry the `versionid` parameter and the value of `versionid` is the version number `Tg0NDUxNTc1NjIzMTQ1MDAwODg`.

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"allow",
            "action":[
                "name/cos:GetObject"
            ],
            "condition":{
                "string_equal":{
                    "cos:versionid":"MTg0NDUxNTc1NjIzMTQ1MDAwODg"
                }
            },
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ]
        }
    ]
}
```

#### Adding a deny policy

If you use the above policy to grant the sub-user permissions, and the sub-user obtains the same permissions without any conditions attached through other means, the broader authorization policy takes effect. For example, if a sub-user is in a user group and the root account grants the GetObject permission to the user group without any conditions attached, the restriction on the version number of the above policy does not take effect.

To cope with this, you can add an explicit deny policy based on the above policy to achieve tighter permission restrictions. The following deny policy specifies that, when a sub-user initiates an object download request that does not carry the `versionid` parameter or that the version number specified by `versionid` is not `MTg0NDUxNTc1NjIzMTQ1MDAwODg`, the request will be denied. Because the priority of the deny policy is higher than other policies, adding a deny policy can avoid permission vulnerabilities to the maximum extent.

```
{
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"allow",
            "action":[
                "name/cos:GetObject"
            ],
            "condition":{
                "string_equal":{
                    "cos:versionid":"MTg0NDUxNTc1NjIzMTQ1MDAwODg"
                }
            },
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ]
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"deny",
            "action":[
                "name/cos:GetObject"
            ],
            "condition":{
                "string_not_equal_if_exist":{
                    "cos:versionid":"MTg0NDUxNTc1NjIzMTQ1MDAwODg"
                }
            },
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ]
        }
    ],
    "version":"2.0"
}
```

#### Example 2: allowing users to get objects of the latest version

Assume that the root account with UIN 100000000001 that owns the bucket `examplebucket-1250000000` uses the following bucket policy to allow the sub-account with UIN 100000000002 to get objects of the latest version only.

According to the policy, if `versionid` is not carried or its value is an empty string, a `GetObject` request will download an object of the latest version by default. Therefore, you can use `string_equal_if_exsit` in the condition:
1. If `versionid` is not carried, it is considered that the condition is met (`True`) by default, the `allow` policy is hit, and requests are allowed.
2. If `versionid` is an empty string (`""`), the `allow` policy will also be hit, and only requests for downloading objects of the latest version will be authorized.
```
	"condition":{
		"string_equal_if_exist":{
			"cos:versionid": ""
		}
	}
```
After the explicit deny policy is added, the complete bucket policy is as follows:
```
{
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"allow",
            "action":[
                "name/cos:GetObject"
            ],
            "condition":{
                "string_equal_if_exist":{
                    "cos:versionid":""
                }
            },
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ]
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"deny",
            "action":[
                "name/cos:GetObject"
            ],
            "condition":{
                "string_not_equal":{
                    "cos:versionid":""
                }
            },
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ]
        }
    ],
    "version":"2.0"
}
```

#### Example 3: disallowing users from deleting objects uploaded before versioning is enabled

Your bucket may have some objects uploaded before versioning is enabled, and the version numbers of these objects become "null" after versioning is enabled. Sometimes, you may need to enable additional protection for these objects, for example, to prevent users from permanently deleting these objects, that is, to deny deletion of objects with version numbers.

In the example below, there are two bucket policies:
1. Authorize the sub-account to use `DeleteObject` requests to delete objects in the bucket.
2. Restrict the condition for `DeleteObject` requests. If a `DeleteObject` request carries the request parameter `versionid` with the value `"null"`, the request will be denied.

Therefore, if object A was uploaded to the bucket `examplebucket-1250000000` before versioning is enabled, the version number of object A becomes a "null" string after versioning is enabled.

After the bucket policy is added, object A will be protected. If a `DeleteObject` request initiated by a sub-user to delete object A does not carry a version number, object A will not be permanently deleted because versioning is enabled. Instead, a delete marker will be added for object A. If the request contains the "null" version number of object A, the request will be denied, and object A will not be permanently deleted.

```
{
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"allow",
            "action":[
                "name/cos:DeleteObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ]
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"deny",
            "action":[
                "name/cos:DeleteObject"
            ],
            "condition":{
                "string_equal":{
                    "cos:versionid":"null"
                }
            },
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ]
        }
    ],
    "version":"2.0"
}
```

<span id="content-length"></span>
### Restricting the size of the file to upload (cos:content-length)

#### Request header Content-Length
The length of the content of an HTTP request in bytes defined in RFC 2616 is often used in PUT and POST requests. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Condition key cos:content-length

When uploading an object, you can use the `cos:content-length` condition key to restrict the `Content-Length` request header to limit the file size of the uploaded object. In this way, you can flexibly manage storage space and avoid wasting storage space and network bandwidth by uploading files that are too large or too small.

In the two examples below, the root account with UIN 100000000001 that owns the `examplebucket-1250000000` bucket uses the `cos:content-length` condition key to restrict the value of the `Content-Length` header in upload requests initiated by the sub-account with UIN 100000000002.

#### Example 1: restricting the maximum value of the request header Content-Length

Require that `PutObject` and `PostObject` upload requests carry the `Content-Length` header with a value less than or equal to 10 bytes.

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"allow",
            "action":[
                "name/cos:PutObject",
                "name/cos:PostObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "numeric_less_than_equal":{
                    "cos:content-length":10
                }
            }
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"deny",
            "action":[
                "name/cos:PutObject",
                "name/cos:PostObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "numeric_greater_than_if_exist":{
                    "cos:content-length":10
                }
            }
        }
    ]
}
```

#### Example 2: restricting the minimum value of the request header Content-Length

Require that `PutObject` and `PostObject` upload requests carry the `Content-Length` header with a value not less than 2 bytes.

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"allow",
            "action":[
                "name/cos:PutObject",
                "name/cos:PostObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "numeric_greater_than_equal":{
                    "cos:content-length":2
                }
            }
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"deny",
            "action":[
                "name/cos:PutObject",
                "name/cos:PostObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "numeric_less_than_if_exist":{
                    "cos:content-length":2
                }
            }
        }
    ]
}
```

<span id="content-type"></span>
### Restricting the type of the file to upload (cos:content-type)

#### Request header Content-Type 

`Content-Type` must be an HTTP request content type as defined in RFC 2616 (MIME), such as `application/xml` and `image/jpeg`. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Condition key cos:content-type

You can use the `cos:content-type` condition key to restrict the `Content-Type` request header.


#### Example 1: restricting Content-Type of PutObject requests to "image/jpeg"

Assume that the root account with UIN 100000000001 that owns the `examplebucket-1250000000` bucket uses the `cos:content-type` condition key to restrict the content of the `Content-Type` header in upload requests initiated by the sub-account with UIN 100000000002.

The bucket policy in this example is to restrict that object upload requests (`PutObject`) must carry the `Content-Type` header and with the value `image/jpeg`.

Note that `string_equal` requires that the request must carry the `Content-Type` header with a value exactly the same as the specified value. In a real request, you need to **explicitly specify the Content-Type header of the request**. Otherwise, if your request does not carry the `Content-Type` header, the request will fail. In addition, if you use a certain tool to initiate a request and do not explicitly specify `Content-Type`, the tool may automatically add an unexpected `Content-Type` header to the request, the request may also fail.

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"allow",
            "action":[
                "name/cos:PutObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "string_equal":{
                    "cos:content-type":"image/jpeg"
                }
            }
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"deny",
            "action":[
                "name/cos:PutObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "string_not_equal_if_exist":{
                    "cos:content-type":"image/jpeg"
                }
            }
        }
    ]
}
```

<span id="response-content-type"></span>
### Restricting the file type returned by download request (cos:response-content-type)

#### Request parameter response-content-type

The `GetObject` API allows you to add the `response-content-type` request parameter to specify the value of the `Content-Type` header in the response.

#### Condition key cos:response-content-type

You can use the `cos:response-content-type` condition key to specify whether requests need to carry `response-content-type`.

#### Example 1: restricting the GetObject request parameter response-content-type to be "image/jpeg"

Assume that the root account with UIN 100000000001 that owns the `examplebucket-1250000000` bucket uses the following bucket policy to require that `GetObject` requests initiated by the sub-account with UIN 100000000002 carry the `response-content-type` request parameter with the value `image/jpeg`. `response-content-type` is a request parameter and needs to be URL-encoded when the request is initiated (encoded value: `response-content-type=image%2Fjpeg`). Therefore, when you set the policy, "image/jpeg" also needs to be URL-encoded, that is, `image%2Fjpeg` needs to be entered.

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"allow",
            "action":[
                "name/cos:GetObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "string_equal":{
                    "cos:response-content-type":"image%2Fjpeg"
                }
            }
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"deny",
            "action":[
                "name/cos:GetObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "string_not_equal_if_exist":{
                    "cos:response-content-type":"image%2Fjpeg"
                }
            }
        }
    ]
}
```

<span id="secure-transport"></span>
### Allowing only HTTPS requests (cos:secure-transport)

#### Condition key cos:secure-transport

You can use the `cos:secure-transport` condition key to require requests to use the HTTPS protocol.

#### Example 1: restricting download requests to use HTTPS

Assume that the root account with UIN 100000000001 that owns the `examplebucket-1250000000` bucket uses the following bucket policy to allow only HTTPS-based `GetObject` requests sent by the sub-account with UIN 100000000002.

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"allow",
            "action":[
                "name/cos:GetObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "bool_equal":{
                    "cos:secure-transport":"true"
                }
            }
        }
    ]
}
```

#### Example 2: denying any non-HTTPS request

Assume that the root account with UIN 100000000001 that owns the bucket `examplebucket-1250000000` uses the following bucket policy to deny any non-HTTPS requests sent by the sub-account with UIN 100000000002.

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"deny",
            "action":[
                "*"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "bool_equal":{
                    "cos:secure-transport":"false"
                }
            }
        }
    ]
}
```

<span id="x-cos-storage-class"></span>
### Allowing setting a specified storage class (cos:x-cos-storage-class)

#### Request header x-cos-storage-class

You can use the `x-cos-storage-class` request parameter to specify or modify the storage class of an object when uploading the object.

#### Condition key cos:x-cos-storage-class

You can use the `cos:x-cos-storage-class` condition key to restrict the `x-cos-storage-class` request header to restrict storage class modification requests.

COS's storage class fields include `STANDARD`, `MAZ_STANDARD`, `STANDARD_IA`, `MAZ_STANDARD_IA`, `INTELLIGENT_TIERING`, `MAZ_INTELLIGENT_TIERING`, `ARCHIVE`, and `DEEP_ARCHIVE`.

#### Example 1: requiring PutObject requests to set the storage class to STANDARD

Assume that the root account with UIN 100000000001 that owns the `examplebucket-1250000000` bucket uses the following bucket policy to require `PutObject` requests sent by the sub-account with UIN 100000000002 to carry the `x-cos-storage-class` header with the value `STANDARD`.

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"allow",
            "action":[
                "name/cos:PutObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "string_equal":{
                    "cos:x-cos-storage-class":"STANDARD"
                }
            }
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"deny",
            "action":[
                "name/cos:PutObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "string_not_equal_if_exist":{
                    "cos:x-cos-storage-class":"STANDARD"
                }
            }
        }
    ]
}
```

<span id="x-cos-acl"></span>
### Allowing setting a specified bucket/object ACL (cos:x-cos-acl)

#### Request header x-cos-acl

When uploading an object or creating a bucket, you can use the `x-cos-acl` request header to specify an ACL or modify the object or bucket ACL. For more information, see [ACL](https://intl.cloud.tencent.com/document/product/436/30583).

- Preset ACLs for buckets: `private`, `public-read`, `public-read-write`, `authenticated-read`
- Preset ACLs for objects: `default`, `private`, `public-read`, `authenticated-read`, `bucket-owner-read`, `bucket-owner-full-control`

#### Condition key cos:x-cos-acl

You can use the `cos:x-cos-acl` condition key to restrict the `x-cos-acl` request header to restrict object/bucket ACL modification requests.

#### Example 1: the object ACL must be set to private in a PutObject request

Assume that the root account with UIN 100000000001 that owns the `examplebucket-1250000000` bucket uses the following bucket policy to allow the sub-account with UIN 100000000002 to upload private objects only. The policy requires that all `PutObject` requests carry the `x-cos-acl` header with the value `private`.

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"allow",
            "action":[
                "name/cos:PutObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "string_equal":{
                    "cos:x-cos-acl":"private"
                }
            }
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"deny",
            "action":[
                "name/cos:PutObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "string_not_equal_if_exist":{
                    "cos:x-cos-acl":"private"
                }
            }
        }
    ]
}
```

<span id="prefix"></span>
### Allowing listing objects in a specified directory only (cos:prefix)

#### Condition key cos:prefix

You can use the `cos:prefix` condition key to restrict the `prefix` request parameter.


>! If the value of `prefix` contains special characters such as `/`, the value must be URL-encoded before being written into the bucket policy.
>

#### Example 1: allowing listing only objects in a specified directory of the bucket

Assume that the root account with UIN 100000000001 that owns the bucket `examplebucket-1250000000` uses the following bucket policy to restrict the sub-account with UIN 100000000002 to list only the objects in the `folder1` directory of the bucket. The policy requires that all `GetBucket` requests carry the `prefix` parameter with the value `folder1`.


```
{
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"allow",
            "action":[
                "name/cos:GetBucket"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "string_equal":{
                    "cos:prefix":"folder1"
                }
            }
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"deny",
            "action":[
                "name/cos:GetBucket"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "string_equal_if_exist":{
                    "cos:prefix":"folder1"
                }
            }
        }
    ],
    "version":"2.0"
}
```

<span id="tls-version"></span>
### Allowing using the TLS protocol of a specified version only (cos:tls-version)

#### Condition key cos:tls-version

You can use the `cos:tls-version` condition key to restrict the TLS version of HTTPS requests. Its value is of the numeric type and supports floating points, such as 1.0, 1.1, or 1.2.


#### Example 1: authorizing only HTTP requests that use TLS v1.2


|Request Scenario   |Expected Result|
|---|---|
|HTTPS request using TLS v1.0|403, failed|
|HTTPS request using TLS v1.2|200, successful|

A policy example is as follows:

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"allow",
            "action":[
                "*"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "numeric_equal":{
                    "cos:tls-version":1.2
                }
            }
        }
    ]
}
```


#### Example 2: rejecting HTTP requests that use TLS earlier than v1.2

|Request Scenario   |Expected Result|
|---|---|
|HTTPS request using TLS v1.0|403, failed|
|HTTPS request using TLS v1.2|200, successful|


A policy example is as follows:


```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"allow",
            "action":[
                "*"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "numeric_greater_than_equal":{
                    "cos:tls-version":1.2
                }
            }
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"deny",
            "action":[
                "*"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "numeric_less_than_if_exist":{
                    "cos:tls-version":1.2
                }
            }
        }
    ]
}
```


<span id="request_tag"></span>
### Forcibly setting a specified bucket tag when creating a bucket (qcs:request_tag)

>?
>The `request_tag` condition key is only applicable to `PutBucket` and `PutBucketTagging` operations but not `GetService`, `PutObject`, or `PutObjectTagging`.
>


#### Condition key qcs:request_tag

You can use the `qcs:request_tag` condition key to restrict that a user must include a specified bucket tag when initiating a `PutBucket` or `PutBucketTagging` request.

#### Example: restricting that a user must include a specified bucket tag when creating a bucket 

Many users may manage their buckets using bucket tags. The following policy example indicates that the user can get authorization only after the user sets the specified bucket tags `<a,b>` and `<c,d>` when creating a bucket.

Multiple bucket tags can be set. Different bucket tag keys/values and tag quantities will be used as different combinations. Assume that multiple parameter values carried by the user in the request form set A and multiple parameter values specified in the condition form set B. With this condition key, the user can use different combinations of qualifiers `for_any_value` and `for_all_value` to indicate different meanings.
- `for_any_value:string_equal` indicates that the request takes effect if A and B have an intersection.
- `for_all_value:string_equal` indicates that the request takes effect if A is a subset of B.

If `for_any_value:string_equal` is used, the corresponding policy and request are as shown below:

|Request Scenario     |Expected Result|
|---|---|
|PutBucket, request header `x-cos-tagging: a=b&c=d`|200, successful|
|PutBucket, request header `x-cos-tagging: a=b`|200, successful|
|PutBucket, request header `x-cos-tagging: a=b&c=d&e=f`|200, successful|

A policy example is as follows:

```
{
    "version": "2.0",
    "statement": [
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect": "allow",
            "action":[
                "name/cos:PutBucket"
            ],
            "resource": "*",
            "condition":{
                "for_any_value:string_equal": {
                    "qcs:request_tag": [
                        "a&b",
                        "c&d"
                    ]
                }
            }
        }
    ]
}
```


If `for_all_value:string_equal` is used, the corresponding policy and request are as shown below:



|Request Scenario   |Expected Result|
|---|---|
|PutBucket, request header `x-cos-tagging: a=b&c=d`|200, successful|
|PutBucket, request header `x-cos-tagging: a=b`|200, successful|
|PutBucket, request header `x-cos-tagging: a=b&c=d&e=f`|403, failed|


A policy example is as follows:

```
{
    "version": "2.0",
    "statement": [
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect": "allow",
            "action":[
                "name/cos:PutBucket"
            ],
            "resource": "*",
            "condition":{
                "for_all_value:string_equal": {
                    "qcs:request_tag": [
                        "a&b",
                        "c&d"
                    ]
                }
            }
        }
    ]
}
```



