### Use Cases

Suppose you want to grant every CAM user the permission to access resources they create; for example, you want a user that created a COS resource to have the access to the resource by default.
If the resource owner (root account) authorizes the resources to resource creators individually, the owner needs to write policies for each resource and authorize them to creators one by one, which leads to high authorization costs. You can use policy variables to this end. Specifically, in the resource definition of the policy, add a placeholder for the creator information, which is the policy variable. During authentication, the policy variable will be replaced with the contextual information from the request.
    
The policy for granting the read permission to a creator is described as follows:
```
{	 
        "version":"2.0", 
        "statement": [       
         { 
            "effect":"allow", 
            "action":"name/cos:Read*", 
            "resource":"qcs::cos:$region:uid/$appid:prefix//$appid/$bucketname" 
         }
        ]
}
```

- The policy variable carries the creator's `uid` (i.e., `APPID`) in the path of each resource. If the account with the `APPID` of 125000000 creates a bucket named `examplebucket` in the Chengdu region, the corresponding resource description will be as follows:
```
qcs::cos:ap-chengdu:uid/125000000:prefix//125000000/examplebucket
```

- When the user with the `uin` of 125000000 accesses this resource, the placeholder of the corresponding policy information will be replaced with the visitor information during the authentication process, that is:
```
 qcs::cos::uid/125000000:prefix//125000000/examplebucket
```

- The resource `qcs::cos::uid/125000000:prefix//125000000/examplebucket` in the policy can access the resource `qcs::cos:ap-chengdu:uid/125000000:prefix//125000000/examplebucket` through prefix matching.

### Using Policy Variables
    
**Resource Element**: policy variables can be used as the last segment in a [six-segment resource description](https://intl.cloud.tencent.com/document/product/598/10606).
**Condition Element**: policy variables can be used in condition values.
    
The following policy indicates that a VPC creator has the access permission:
```
{  
        "version":"2.0", 
        "statement": [       
         { 
            "effect":"allow", 
            "action":"name/vpc:*", 
            "resource":"qcs::vpc::uin/12357:vpc/*",
            "condition":{"string_equal":{"qcs:create_uin":"${uin}"}} 
         }
      ]
}
```

### Policy Variable List
    
Currently supported policy variables are as follows:

| Name | Description | 
|---------|---------|
| ${uin} | `uin` of the current visitor's sub-account. If the visitor is a root account, this is the `uin` of the root account. | 
| ${owner_uin} | `uin` of the root account to which the current visitor belongs. | 
| ${app_id} | `APPID` of the root account to which the current visitor belongs. | 
