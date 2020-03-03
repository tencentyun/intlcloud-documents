A resource description identifies one or multiple operation objects including CVM resources and COS buckets. This document introduces CAM resource descriptions.

### Six-piece format
All resources can be described using the following six-piece format. Every product has its own resources and detailed resource definition. For more information on how to specify resource information, see the corresponding product documentation.
The six-piece format is defined as follows:
```
qcs:project_id:service_type:region:account:resource
```

- **qcs**: qcloud service abbreviation. This refers to Tencent Cloud resources. This field is required.   
- **project_id**: indicates the project information and is only compatible with the earlier CAM logic. Such information is prohibited to be entered by the current policy syntax.  
- **service_type**: indicates the abbreviated product type, e.g. CVM and CDN. For more information about product, see the corresponding product documentation. The value `*` indicates all the products. This field is required.  
- **region**: describes the region information. If the field is left empty, it indicates all regions. At present, two types of naming methods are supported. For more information about the newest naming method for regions, see [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/213/6091). The existing naming method for Tencent Cloud regions is as follows:

| Region Abbreviation | Region | 
|:---------:|:---------:|
| gz | Guangzhou | 
| sh | Shanghai |
| bj | Beijing |
| ca | Canada |
| sg | Singapore |
| hk | Hong Kong (China) |
| cd | Chengdu |
| de | Germany |

- **account**: indicates the root account information of the resource owner. At present, either `uin` or `uid` can be used to describe the resource owner.
 - uin is the account ID of the root account. It is expressed in the format `uin/${uin}`, e.g. `uin/12345678`.
 - uid is the APPID of the root account. It is expressed in the format `uid/${appid}`, e.g. `uid/10001234`.
 - If this value is empty, the account will be taken to be the root account of the user that created the policy.
 
 >  At present, the resource owners of COS and CAS services can only be described using `uid`, and resource owners of other services can only be described using `uin`.
- **resource**: describes the details of the specific product resource.
	- This field is required. The resource can be described as follows:
     - Indicates the ID of a resource under a sub-resource type. For example, `instance/ins-abcdefg` of a VPC product.
```
	<resource_type>/<resource_id> 
```
	 - Indicates the ID of a resource with a path under a sub-resource type. For example, `prefix//10001234/bucket1/object2` of a COS product. Prefix match at the directory level is supported for this type of description. For example, `prefix//10001234/bucket1/*` indicates all the objects under bucket1.
```
	<resource_type>/<resource_path>
```
	 - Indicates all the resources under a sub-resource type, such as `instance/*`.
```
	<resource_type>/*
```
	 - Indicates all the resources under a product.
	 ```
	*
	```

 - In certain scenarios, resource elements can be described with `*`, and the definitions are as follows. For more information, see the corresponding product documentation.
 - For actions that require association with resources, "resource" defined as `*` indicates that all resources are associated.
 - If the action does not require association with resources, "resource" is defined as `*` in all cases.

### Resource definition for CAM  
CAM resources includes users, user groups, and policies. A CAM resource can be described as follows: 
#### Root account:
```
qcs::cam::uin/164256472:uin/164256472
```
Or
```
qcs::cam::uin/164256472:root 
```
#### Sub-account:
```    
qcs::cam::uin/164256472:uin/73829520
```
#### Group:
```
qcs::cam::uin/164256472:groupid/2340
```
#### All resources:
```
*
```
#### Policy:
```
qcs::cam::uin/12345678:policyid/*
```
Or
```
qcs::cam::uin/12345678:policyid/12423
```

### Notes on resources
- The resource owner will always be the root account. The sub-account that creates the resource will not be permitted to access it without authorization from the root account.
- Services such as COS and CAS support authorization of cross-account resource access permissions. Authorized accounts can pass permissions to their sub-accounts through permission propagation.

### Related documentation

For more information about individual products’ resource definition details, see the corresponding product documentation in [CAM-enabled Cloud Services](https://intl.cloud.tencent.com/document/product/598/10588). 
