## Overview

Suppose you want to grant every CAM user the permission to access resources they create; for example, you want a user who created a COS resource to have the access to the resource by default.
If the resource owner (root account) authorizes the resources to the resource creator one by one, the owner needs to write policies for each resource and authorize it to the creator, which leads to high authorization costs. In this case, you can use policy variables to meet your requirements. A policy variable is a placeholder that describes the creator’s sub-account UIN in the resource definition. During authentication, the policy variable will be replaced by the contextual information of the request.
    
The policy for granting resource access permissions to a creator is described as follows: 
```json
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": "cmqqueue:*",
            "resource": "qcs::cmqqueue::uin/1000001:queueName/uin/${uin}/*"
        }
    ]
}
```

- A policy variable carries the creator’s sub-account UIN in every resource path. For example, if a sub-account (with its own UIN being `125000000` and its root account’s UIN being `1000001`) has created a CMQ message queue named `queueName/uin/125000000` in Chengdu region, the resource will be described as follows: 
```
qcs::cmqqueue:ap-chengdu:uin/1000001:queueName/uin/125000000
```

- When the above sub-account accesses this resource, the placeholder of the corresponding policy information will be replaced by the visitor during the authentication process, that is, 
```
qcs::cmqqueue::uin/1000001:queueName/uin/125000000
```

- The resource `qcs::cmqqueue::uin/1000001:queueName/uin/125000000` in the policy can access the resource `qcs::cmqqueue:ap-chengdu:uin/1000001:queueName/uin/125000000` through prefix matching. 

## Location of Policy Variable

**Resource element location**: A policy variable can be in the last segment in a [6-segment resource description](https://intl.cloud.tencent.com/document/product/598/10606).
**Condition element location**: A policy variable can be used in condition values.
    
The following policy indicates that the VPC creator has the access permission:

```json
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
>?The 6-segment resource description of COS is `qcs::cos:$region:uid/$appid:$bucketname-$appid/$ResourcesPath`, in which `$ResourcesPath` indicates the specific resource path. The above policy variable cannot be used in `$ResourcesPath`. A complete 6-segment resource description of a COS bucket is as follows:
>`qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/path_1/path_2/pic.jpeg`

## Policy Variable List

Below is a list of supported policy variables:

| Variable       | Description                                                     |
| ------------ | ------------------------------------------------------------ |
| ${uin} | The current visitor’s sub-account UIN, or the root account UIN (if the visitor is a root account). |
| ${owner_uin} | UIN of the root account to which the current visitor belongs. |
| ${app_id}    | APPID of the root account to which the current visitor belongs. |
