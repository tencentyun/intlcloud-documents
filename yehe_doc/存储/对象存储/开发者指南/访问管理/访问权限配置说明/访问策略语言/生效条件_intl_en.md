## Overview

Conditions are part of the access policy language. A complete condition includes the following elements:
- Condition key: Specifies the type of the condition, for example, user access source IP and authorization time.
- Condition operator: Specifies the condition determination method.
- Condition value: Specifies the value of the condition key.

For more information, see [Conditions](https://www.tencentcloud.com/document/product/598/10608) of Access Management.

>? 
>- When using condition keys to write a bucket policy, follow the principle of least privilege, add the corresponding condition keys only to applicable requests (actions), and avoid using the \* wildcard when specifying the actions. Using the wildcard will cause the requests to fail.
>- When you create a policy in the CAM console, pay attention to the syntax format. The syntax elements of `version`, `principal`, `statement`, `effect`, `action`, `resource`, and `condition` must all begin with a letter in the same letter case.


## Condition Example

In the following bucket policy example, the condition specifies that the `cos:PutObject` authorization operation can be completed only in the 10.217.182.3/24 or 111.21.33.72/24 IP range. In the condition:
- The **condition key** is `qcs:ip`, indicating that the condition type is IP.
- The **condition operator** is `ip_equal`, indicating that the condition determination method is to determine whether IP addresses match.
- The **condition value** is the `["10.217.182.3/24","111.21.33.72/24"]` array, listing the specified values for condition determination. If the user's IP is in any of the specified IP ranges in the array, the condition is determined as true.

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/1250000000:uin/1250000001"
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
                "ip_equal":{
                    "qcs:ip":[
                        "10.217.182.3/24",
                        "111.21.33.72/24"
                    ]
                }
            }
        }
    ]
}
```

## Condition Keys Supported by COS


>? Currently, the `tls-version` condition key is supported only in the Beijing region. It will be supported in other regions later. 
>


COS supports two types of condition keys: condition keys applicable to all requests, including IP, VPC, and HTTPS, and condition keys from request headers and request parameters and generally applicable only to requests that need to carry the request headers or request parameters. For the descriptions and use cases of these condition keys, see [Descriptions and Use Cases of Condition Keys](https://intl.cloud.tencent.com/document/product/436/46206).

>? Conditions and condition keys are applicable only to the access management of user requests. When the lifecycle and bucket replication rules are valid, actions such as deletion and replication are initiated by COS rather than users and therefore are not in the applicable scope of condition keys.
>

### Condition keys applicable to all requests

Condition keys applicable to all requests are `qcs:ip`, `qcs:vpc`, and `cos:secure-transport`, which indicate the source IP range of the request, source VPC ID of the request, and whether the request uses HTTPS, respectively.

| Condition Key | Applicable Request | Meaning | Type |
|:----------|:----------|:----------|:----------|
|[cos:secure-transport](https://intl.cloud.tencent.com/document/product/436/46206#secure-transport) | All requests | Whether the request uses HTTPS |  Boolean  |
|[qcs:ip](https://intl.cloud.tencent.com/document/product/436/46206#RestrictUserAccessIP) | All requests | Source IP range of the request |  IP|
|[qcs:vpc](https://intl.cloud.tencent.com/document/product/436/46206#requester_vpc) | All requests | Source VPC ID of the request  | String  |
|[cos:tls-version](https://intl.cloud.tencent.com/document/product/436/46206#tls-version) |All HTTPS requests| TLS version used by HTTPS requests |Numeric|


### Condition keys from request headers and request parameters

Because different requests have different request headers (`Header`) and request parameters (`Param`), condition keys from request headers and request parameters are applicable only to requests that contain such request headers or request parameters.

For example, the condition key `cos:content-type` is applicable to upload requests (such as `PutObject`) that need to use the request header `Content-Type`, while the condition key `cos:response-content-type` is applicable only to `GetObject` requests because only `GetObject` requests support the request parameter `response-content-type`.

The table below lists the condition keys from request headers and request parameters and the corresponding applicable requests.


| Condition Key   | Applicable Request | Check Request Header or Request Parameter | Type |
|:----------|:----------|:----------|:----------|
|[cos:x-cos-storage-class](https://intl.cloud.tencent.com/document/product/436/46206#x-cos-storage-class) |PutObject<br>PostObject<br>InitiateMultipartUpload<br>AppendObject | Request header: `x-cos-storage-class` |String|
|[cos:versionid](https://intl.cloud.tencent.com/document/product/436/46206#versionid) |GetObject<br>DeleteObject<br>PostObjectRestore<br>PutObjectTagging<br>GetObjectTagging<br>DeleteObjectTagging<br>HeadObject | Request parameter: `versionid` |String|
|[cos:prefix](https://intl.cloud.tencent.com/document/product/436/46206#prefix) |GetBucket (List Objects)<br>GET Bucket Object versions<br>List Multipart Uploads<br>ListLiveChannels | Request parameter: `prefix` |String|
|[cos:x-cos-acl](https://intl.cloud.tencent.com/document/product/436/46206#x-cos-acl) |PutObject<br>PostObject<br>PutObjectACL<br>PutBucket<br>PutBucketACL<br>AppendObject<br>Initiate Multipart Upload | Request header: `x-cos-acl` |String|
|[cos:content-length](https://intl.cloud.tencent.com/document/product/436/46206#content-length) | This request header has a wide applicable scope, typically requests with request bodies. | Request header: `Content-Length` |Numeric|
|[cos:content-type](https://intl.cloud.tencent.com/document/product/436/46206#content-type) | This request header has a wide applicable scope, typically requests with request bodies. | Request header: `Content-Type` |String|
|[cos:response-content-type](https://intl.cloud.tencent.com/document/product/436/46206#response-content-type) |GetObject | Request parameter: `response-content-type` |String|
|[qcs:request_tag](https://intl.cloud.tencent.com/document/product/436/46206#request_tag) |PutBucket<br>PutBucketTagging |Request header: x-cos-tagging<br>Request parameter: tagging|String|



## Condition Operators

COS supports the following condition operators, which are applicable to condition keys of the String, Numeric, Boolean, and IP types.

| Condition Operator | Description | Type |
|:----------|:----------|:----------|
|string_equal | String equal to (case-sensitive) |String |
|string_not_equal | String not equal to (case-sensitive) |String |
|string_like |String similar to (case-sensitive). Currently, wildcards (*) can be prefixed or suffixed to the string, for example, `image/*`. |String |
|ip_equal | IP equal to |IP |
|ip_not_equal | IP not equal to |IP |
|numeric_equal | Number equal to |Numeric |
|numeric_not_equal | Number not equal to |Numeric |
|numeric_greater_than | Number greater than |Numeric |
|numeric_greater_than_equal | Number greater than or equal to |Numeric |
|numeric_less_than | Number less than |Numeric |
|numeric_less_than_equal | Number less than or equal to |Numeric |

### _if_exist

You can add `_if_exist` to the end of all the preceding condition operators to form new condition operators, such as `string_equal_if_exist`. The differences between condition operators with and without `_if_exist` are as follows:

- For a condition operator without `_if_exist`, such as `string_equal`, it is considered that the condition is met (`False`) by default if the request does not contain the specified request header or parameter.
- For a condition operator with `_if_exist`, such as `string_equal_if_exist`, it is considered that the condition is met (`True`) by default if the request does not contain the specified request header or parameter.

## License request example


### Example 1: allow downloading objects of a specified version

In the bucket policy in this example, `Effect` is `allow`, allowing `GetObject` requests where the request parameter `versionid` is `MTg0NDUxNTc1NjIzMTQ1MDAwODg`. According to the `allow` authorization policy, if the condition is met (`True`), the request will be allowed; if the condition is not met (`False`), the request will not be allowed and will fail.

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/1250000000:uin/1250000001"
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

The table below lists the condition meeting and request allowing details of the condition operators `string_equal` and `string_equal_if_exist`.

| Condition Operator | Request | Condition Met | Request Allowed |
|:----------|:----------|:----------|:----------|
|string_equal | Without `versionid` |FALSE | No |
|string_equal_if_exist | Without `versionid` |TRUE | Yes |
|string_equal | With `versionid`, whose value is specified |TRUE | Yes |
|string_equal_if_exist | With `versionid`, whose value is specified |TRUE | Yes |
|string_equal | With `versionid`, whose value is not specified |FALSE | No |
|string_equal_if_exist | With `versionid`, whose value is not specified |FALSE | No |

### Example 2: disallow downloading objects of a specified version

In the bucket policy in this example, `Effect` is `deny`, disallowing `GetObject` requests where the request parameter `versionid` is `MTg0NDUxNTc1NjIzMTQ1MDAwODg`. According to the `deny` authorization policy, if the condition is met (`True`), the request will fail; if the condition is not met (`False`), the request will not be denied.

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/1250000000:uin/1250000001"
                ]
            },
            "effect":"deny",
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

The table below lists the condition meeting and request denial details of the condition operators `string_equal` and `string_equal_if_exist`.

| Condition Operator | Request | Condition Met | Request Denied |
|:----------|:----------|:----------|:----------|
|string_equal | Without `versionid` |FALSE | No |
|string_equal_if_exist | Without `versionid` |TRUE | Yes |
|string_equal | With `versionid`, whose value is specified |TRUE | Yes |
|string_equal_if_exist | With `versionid`, whose value is specified |TRUE | Yes |
|string_equal | With `versionid`, whose value is not specified |FALSE | No |
|string_equal_if_exist | With `versionid`, whose value is not specified |FALSE | No |


## Notes

### Special characters require URL encoding

Special characters in request parameters all require URL encoding, and therefore bucket policies that use condition keys from the request parameters require URL encoding as well. For example, if you are to use the `cos:response-content-type` condition key in a bucket policy, the condition value `image/jpeg` must be encoded (URL encoding) into `image%2Fjpeg` before it is entered into the bucket policy.

### Principle of least privilege and no \* wildcard

When using condition keys, comply with the principle of least privilege, add only actions for which you want to set permissions, and avoid using the \* wildcard. Misuse of the \* wildcard may cause some requests to fail. In the example below, requests other than `GetObject` do not support using the request parameter `response-content-type`.

For "deny + string_equal_if_exist", if the condition key does not exist in the request, it is considered `True` by default. Therefore, when you initiate requests such as `PutObject` and `PutBucket`, the `deny` statement will be met and the requests will be denied.

For "allow + string_equal", if the condition key does not exist in the request, it is considered `False` by default. Therefore, when you initiate requests such as `PutObject` and `PutBucket`, the `allow` statement will not be met and the requests will not be allowed.

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/1250000000:uin/1250000001"
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
                "string_equal":{
                    "cos:response-content-type":"image%2Fjpeg"
                }
            }
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/1250000000:uin/1250000001"
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
                "string_not_equal_if_exist":{
                    "cos:response-content-type":"image%2Fjpeg"
                }
            }
        }
    ]
}
```

Alternatively, you can use "allow + string_equal_if_exist" and "deny + string_not_equal" to allow requests without the `response-content-type` request parameter.

For "deny + string_equal", if the condition key does not exist in the request, it is considered `False` by default. Therefore, when you initiate requests such as `PutObject` and `PutBucket`, the `deny` statement will not be met and the requests will not be denied.

For "allow + string_equal_if_exist", if the condition key does not exist in the request, it is considered `True` by default. Therefore, when you initiate requests such as `PutObject` and `PutBucket`, the `allow` statement will be met and the requests will be allowed.

However, if you use condition operators in this way, you will not be able to restrict whether a `GetObject` request carries the `response-content-type` request parameter. A `GetObject` request without the `response-content-type` request parameter will be allowed by default like other requests. Only when the `GetObject` request carries the `response-content-type` request parameter, you can use your specified condition to check whether the content of the request parameter is the same as what you expect to implement conditional authorization.

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/1250000000:uin/1250000001"
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
                "string_equal_if_exist":{
                    "cos:response-content-type":"image%2Fjpeg"
                }
            }
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/1250000000:uin/1250000001"
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
                "string_not_equal":{
                    "cos:response-content-type":"image%2Fjpeg"
                }
            }
        }
    ]
}
```


Therefore, the more secure way is to comply with the principle of least privilege and restrict the action to `GetObject` requests without using the \* wildcard.

As shown in the example policy below, the policy condition strictly specifies that authorization is performed only for `GetObject` requests carrying the `response-content-type` request parameter with value `image%2Fjpeg`.

Other requests are not affected by the policy in this example, and can be authorized separately based on the principle of least privilege.

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/1250000000:uin/1250000001"
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
                    "qcs::cam::uin/1250000000:uin/1250000001"
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


