### Application Scenario

Assume the following scenario: you want to grant every CAM user the permission to access resources they created themselves. For example, a user that created a COS resource would have permission to access that resource by default.
If the resource owner (root account) authorizes the resources to the resource creator individually, the owner needs to write policies for each resource and authorize it to the creator, which leads to high authorization costs. In this type of situation, you can use policy variables to implement your requirements. In the resource definition of the policy, add the creator information described using a placeholder. This placeholder is the policy variable. During authentication, the policy variable will be substituted with the contextual information of the request.
    
The policy for granting read permission to a creator is described as follows:
```
{	 
        "version":"2.0", 
        "statement": [       
         { 
            "effect":"allow", 
            "action":"name/cos:Read*", 
            "resource":"qcs::cos::uid/1238423:prefix/${uin}/*" 
         }
        ]
}
```

- The policy variable of the path of every resource carries the creator’s uin. For example, the user with uin 12356 created a bucket named test. The corresponding resource description method is:
```
qcs::cos::uid/1238423:prefix/12356/test
```

- When the user with uin 12356 accesses this resource, the placeholder of the corresponding policy information will be substituted for that of the visitor during the authentication process, that is:
```
qcs::cos::uid/1238423:prefix/12356/
```

- The resource `qcs::cos::uid/1238423:prefix/12356/` in the policy can access the resource `qcs::cos::uid/1238423:prefix/12356/test` through prefix match.

### Using Policy Variables
    
**Resource Element**: Policy variables can be used as the last piece in the [six-piece resource description method](https://intl.cloud.tencent.com/document/product/598/10606).
**Condition Element**: Policy variables can be used in condition values.
    
The following policy indicates that the VPC creator has access permission:
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
    
At present the supported policy variable list is as follows:

| Name | Description | 
|---------|---------|
| ${uin} | The uin of the current visitor’s sub-account. If the visitor is the root account, this is the uin of the root account. | 
| ${owner_uin} | The uin of the root account to which the current visitor belongs. | 
| ${app_id} | The APPID of the root account to which the current visitor belongs. | 
