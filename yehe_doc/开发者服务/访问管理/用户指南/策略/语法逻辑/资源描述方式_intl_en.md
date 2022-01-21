The `resource` element describes one or multiple operation objects such as CVM resources and COS buckets. This document describes the resource information in CAM.

### Six-Segment Format
All resources can be described in the following six-segment format. Each service has its own resources and detailed resource definition. For more information on how to specify resources, see the corresponding product documentation in [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).
The six-segment format is defined as follows:
```
qcs:project_id:service_type:region:account:resource
```

- **qcs** is the abbreviation of `qcloud service` and indicates a Tencent Cloud resource, which is required. 
- **project_id** describes the project information, which is only compatible with legacy CAM logic. It is not allowed in the current policy syntax and can be left empty.
- **service_type** describes the abbreviation of a service, such as CVM and CDN. For more information on service abbreviation, see the “Abbreviation in CAM” column in each table in [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588). The value `*` indicates all services. This field is required. 
- **region** describes the region information. If this field is left empty, it indicates all regions. For more information on region naming, see [Region List](https://intl.cloud.tencent.com/zh/document/product/213/31574).
- **account** describes the root account information of the resource owner. Currently, either `uin` or `uid` can be used to describe the resource owner.
 - `uin` is the account ID of the root account, which is expressed in the format of `uin/${uin}`, such as `uin/12345678`.
 - `uid` is the APPID of the root account, which is expressed in the format of `uid/${appid}`, such as `uid/10001234`.
 - If this value is empty, it means the “account” segment is the root account of the user who created the policy.
>?Currently, COS and CAS resource owners can only be described by `uid`, while resource owners of other services can only be described by `uin`.
- **resource** describes the detailed resource information of the specific service.
>?`resource_type` (resource prefix) is the part before the first `/` in the last segment of the 6-segment resource description; for example, in the CVM resource description `qcs::cvm:$region::instance/*`, the resource prefix is `instance`.

  -  This field is required. The resource can be described as follows:
     - It can indicate the ID of a resource in a resource subcategory, such as `instance/ins-abcdefg` for CVM.
```
	<resource_type>/<resource_id> 
```

	 - It can indicate the ID of a resource with a path in a resource subcategory, such as `prefix//10001234/bucket1/object2` for COS. Prefix match at the directory level is supported for this type of description. For example, `prefix//10001234/bucket1/*` indicates all the objects in `bucket1`.
```
	<resource_type>/<resource_path>
```
	 - It can indicate all the resources in a resource subcategory, such as `instance/*`.
```
	<resource_type>/*
```
	 - It can indicate all the resources of a service.
```
	*
```

 -  In certain scenarios, the `resource` element can be described by `*`, and the definitions are as follows. For more information, see the corresponding product documentation.
 -   If the `action` is an operation that needs to be associated with a resource, the resource can be defined as `*`, indicating that all resources are associated.
 - If the `action` is an operation that does not need to be associated with a resource, the resource needs to be defined as `*`.

### Resource Definition for CAM  
CAM resources includes users, user groups, and policies. A CAM resource can be described as follows: 
#### Root account
```
qcs::cam::uin/164256472:uin/164256472
```
Or
```
qcs::cam::uin/164256472:root 
```
#### Sub-account
```    
qcs::cam::uin/164256472:uin/73829520
```
#### Group
```
qcs::cam::uin/164256472:groupid/2340
```
#### All resources
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

### Notes on Resources
- A resource owner is always a root account. The sub-account that creates a resource will not automatically have access to the resource; instead, it must be authorized by the resource owner.
- Services such as COS and CAS support cross-account authorization for resource access. Authorized accounts can pass permissions to their sub-accounts through permission propagation.

### Relevant Documents

For more information on service-specific resource definitions, see the corresponding product documentation in [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588). 
