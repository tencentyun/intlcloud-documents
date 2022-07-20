The `resource` element describes one or multiple operation objects such as CVM resources and COS buckets. This document describes the resource information in CAM.

## Definition of All Resources

- If `resource` is `*`, it indicates all resources; that is, you can grant the `action` (operation) permission of all resources.
- If you want to authorize a Tencent Cloud service at the service level or authorize a service operation at the API level, you need to enter `*` for `resource` to grant the permission of all resources in the Tencent Cloud service or the `action` permission of all resources.

## Definition of One or Multiple Resources

You can describe the permissions of one or multiple resources in the following six-segment format for authorization. Each service has its own resources and detailed resource definition.
The six-segment format is defined as follows:

```
qcs:project_id:service_type:region:account:resource
```

A six-segment resource description contains six fields as detailed below:

| Field     | Description and Valid Values                                                   | Required | Example                                                         |
| ------------ | ------------------------------------------------------------ | -------- | ------------------------------------------------------------ |
| qcs          | Tencent Cloud service abbreviation, which indicates a resource of Tencent Cloud.                | Yes       | qcs                                                          |
| project_id   | Project information, which is only compatible with legacy CAM logic. It cannot be entered in the current policy syntax and can be left empty. | No       | Empty                                                         |
| service_type | <li>Product (service) abbreviation. For more information, see "Abbreviation in CAM" in [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).</li><li>If this field is left empty, it indicates all products.</li> | No       | <li>CVM: cvm</li><li>CDN: cdn</li>           |
| region       | Region information. For more information on region names, see "Region List" in [Common Params](https://intl.cloud.tencent.com/document/product/213/31574).<br/>If this field is left empty, it indicates all regions. | No       | <li>North China (Beijing): ap-beijing</li><li>South China (Guangzhou): ap-guangzhou</li> |
| account      | Root account information of the resource owner. Currently, either `uin` or `uid` can be used to describe the resource owner.<li>`uin` is the root account ID in `uin/${uin}` format.</li><li>`uid` is the root account's `APPID` in `uid/${appid}` format, and only COS and CAS resource owners can be described in this way.</li>If this field is left empty, it indicates the root account of the CAM user creating the policy. | No       | <li>uin: uin/12345678</li><li>uid: uid/10001234 </li>  |
| resource     | Resource details of the product. Currently, you can describe a resource in the following two formats: `resource_type/${resourceid}` and `<resource_type>/<resource_path>`. <li>`resource_type/${resourceid}`: `resourcetype` is the resource prefix, which describes the resource type. `${resourceid}` is the specific resource ID, which can be viewed in the corresponding product console. `*` indicates all resources of this type. </li><li>`<resource_type>/<resource_path>`: `resourcetype` is the resource prefix, which describes the resource type. `<resource_path>` is the resource path. This format supports directory-level prefix match.</li> | Yes       | <li>CVM: instance/ins-1</li><li>TencentDB for MySQL: instanceId/cdb-1</li><li>COS: `prefix//10001234/bucket1/*`, which indicates all files in `bucket1`. Various COS resource types are supported. For more information, see [Working with COS API Authorization Policies](https://intl.cloud.tencent.com/document/product/436/30580).</li> |

## Definition of CAM Resources  

CAM resources include users, user groups, and policies. A CAM resource can be described as follows: 

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

#### Policy

```
qcs::cam::uin/12345678:policyid/*
```

Or

```
qcs::cam::uin/12345678:policyid/12423
```

## Notes on Resources

- A resource owner is always a root account. The sub-account that creates a resource will not automatically have access to the resource without authorization; instead, it must be authorized by the resource owner.
- Services such as COS and CAS support cross-account authorization for resource access. Authorized accounts can pass permissions to their sub-accounts through permission propagation.

## Relevant Documents

For more information on service-specific resource definitions, see the corresponding product documentation in [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588). 
