## Overview
This document describes examples of bucket policies used to limit subnets, principals and VPC ID. You can use these bucket policies to control specific access to the bucket and its data. For more information, see [Access Policy Language Overview](https://cloud.tencent.com/document/product/436/18023).
>!
>- When configuring a bucket policy in the COS Console, you need to grant users appropriate permissions to the bucket, for example, getting the bucket location, and listing the bucket permissions.
- The bucket policy size is limited to 20 KB.


### Example 1: Limit the IP range in the subnet to 10.1.1.0/24 and vpcid to aqp5jrc1.
Syntax example:
```
{
  "Statement": [
    {
      "Action": [
        "name/cos:*"
      ],
      "Condition": {
        "ip_equal": {
          "qcs:ip": [
            "10.1.1.0/24"
          ]
        },
        "string_equal": {
          "vpc:requester_vpc": [
            "vpc-aqp5jrc1"
          ]
        }
      },
      "Effect": "deny",
      "Principal": {
        "qcs": [
          "qcs::cam::anyone:anyone"
        ]
      },
      "Resource": [
        "qcs::cos:ap-guangzhou:uid/1251668577:jimmyyantest-1251668577/*"
      ]
    }
  ],
  "version": "2.0"
}
```


### Example 2: Limit vpcid to aqp5jrc1 and specify the principal and bucket.
Syntax example:
```
{
  "Statement": [
    {
      "Action": [
        "name/cos:*"
      ],
      "Condition": {
        "string_equal": {
          "vpc:requester_vpc": [
            "vpc-aqp5jrc1"
          ]
        }
      },
      "Effect": "allow",
      "Principal": {
        "qcs": [
          "qcs::cam::uin/3280754170:uin/100005212150"
        ]
      },
      "Resource": [
        "qcs::cos:ap-beijing:uid/1252921383:x3cmplay-1252921383/*"
      ]
    }
  ],
  "version": "2.0"
}
```

