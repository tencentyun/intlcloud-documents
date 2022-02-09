## Overview
Access policies can be used to grant access to RUM. They use JSON-based access policy syntax. You can authorize specified principals to perform specified operations on specified RUM resources through the access policy syntax.

The access policy syntax describes the basic elements and usage of the policy. For the description of the policy syntax, see [Permission](https://intl.cloud.tencent.com/zh/document/product/598/10600).

## Policy Syntax
CAM policy:

```
{	 
        "version":"2.0", 
        "statement": 
        [ 
           { 
              "effect":"effect", 
              "action":["action"], 
              "resource":["resource"], 
               "condition": {"key":{"value"}} 
           } 
       ] 
} 

```
#### Element usage
- **version** is required. Currently, only the value "2.0" is allowed.
- **statement** describes the details of one or more permissions. It contains a permission or permission set of multiple other elements such as `effect`, `action`, `resource`, and `condition`. One policy has only one `statement`.
 1. **effect** describes whether the statement result is an "allow" or "explicit deny", which is required.
 2. **action** describes the allowed or denied action (operation). An operation can be an API (prefixed with "name") or a feature set (a set of specific APIs prefixed with "permid"). This element is required.
 3. **resource** describes the details of authorization. A resource is described in a six-segment format. Detailed resource definitions vary by product. For more information on how to specify resources, see the product documentation corresponding to the resource statement you are writing. This element is required.
 4. **condition** describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value may contain information such as time and IP address. Some services allow you to specify additional values in a condition. This element is optional.




### Specifying effect

If access to a resource is not explicitly granted (allowed), then it is implicitly denied. It can also be explicitly denied, which ensures that users cannot access the resource even if they are granted the access permission by other policies. Below is an example of specifying the "allow" effect:

```json
"effect" : "allow"
```

### Specifying action

RUM defines console operations that can be specified in a policy. The specified operations are divided into reading part of APIs (apm:Describe\*) and all APIs (apm:\*) according to the operation nature.

Below is an example of specifying the allowed operations:

```
"action": [
  "name/apm:Describe*"
]
```

### Specifying resource

The `resource` element describes one or more operation objects, such as RUM resources. All resources can use the following six-segment format:

```plaintext
qcs:project_id:service_type:region:account:resource
```

The parameters are as detailed below:

| Parameter | Description | Required |
| ------------ | ------------------------------------------------------------ | -------- |
| qcs | Tencent Cloud service abbreviation, which indicates a service of Tencent Cloud | Yes |
| project_id | Project information, which is only used to enable compatibility with legacy CAM logic and generally can be left empty | No |
| service_type | Product abbreviation, which is `rum` here | Yes |
| region | Region information | Yes |
| account | Root account information of the resource owner, i.e., root account ID in the format of `uin/${OwnerUin}`, such as `uin/100000000001` | Yes |
| resource | Resource details prefixed with `instance` | Yes |

Below is a sample six-segment description of a RUM resource:

```plaintext
"resource":["qcs::rum::uin/1250000000:Instance/rum-vpasY123"]
```

## Use Cases
Grant the read and write permissions of specified resources based on resource ID. The root account ID is `1250000000`:

Sample: granting the sub-user the permission to query the business system (ID: rum-vpasY123).

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "rum:DescribeTawInstances"
            ],
            "resource": [
                "qcs::rum::uin/1250000000:Instance/rum-vpasY123"
            ]
        }
    ]
}
```


### List of APIs supporting resource-level authorization

| API      | Description |
| ------------------------- | -------------------------- |
| DescribeData              | Gets `QueryData`             |
| DescribeError             | Gets homepage error information           |
| DescribeLogList           | Gets the list of CLS logs          |
| DescribeOfflineLogConfigs | Gets the configured offline log listening configuration |
| DescribeOfflineLogRecords | Gets all offline logs       |
| DescribeOfflineLogs       | Gets the specified offline log           |
| DescribeProjects          | Gets the list of projects               |
| DescribePvList            | Gets the list of PVs                |
| DescribeScores            | Gets the list of homepage scores           |
| DescribeTawAreas          | Queries area information               |
| DescribeTawInstances      | Queries business systems               |
| DescribeUvList            | Gets the list of UVs                 |
| DescribeWhitelists        | Gets allowlist             |
| CreateOfflineLogConfig    | Creates offline log listening           |
| CreateProject             | Creates project                   |
| CreateStarProject         | Creates starred project               |
| CreateTawInstance         | Creates business system               |
| CreateWhitelist           | Creates allowlist                 |
| DeleteOfflineLogConfig    | Deletes RUM offline log listening      |
| DeleteOfflineLogRecord    | Deletes offline log           |
