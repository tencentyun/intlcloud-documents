## ES CAM Overview
Cloud Access Management (CAM) is a web-based Tencent Cloud service that helps you securely manage and control access permissions to resources under your Tencent Cloud account. With CAM, you can create, manage and terminate users (user groups) and use identities and policies to control user access to Tencent Cloud resources. For more information on CAM policies and usage, see [here](https://intl.cloud.tencent.com/document/product/598/10601).  

## ES CAM Policies
### General Permission Policy
ES provides two general policies by default:
- Full access policy (QcloudElasticsearchServiceFullAccess), which grants a user permission to create and manage all ES cluster instances. 
- Read-only access policy (QcloudElasticsearchServiceReadOnlyAccess), which grants a user permission to view ES cluster instances but not create, update, or delete them.  

You can log in to the [Policy Management](https://console.cloud.tencent.com/cam/policy) page, select "Elasticsearch Service" in "Service Type", and bind the default policies displayed in the list to accounts as needed.
![](https://main.qcloudimg.com/raw/3555788e9bfc9b81346b614ce32a8673.png)
If the default policies cannot meet your requirements, you can click **Create Custom Policy** to customize the authorization.

### Custom Permission Policy

Types of resources that can be authorized in ES include:

| Resource Type | Resource Description |
| -------- | -------------- |
| instance | `qcs::es:$region:$account:instance/*` |

Below describes the details of resource-level access control supported by each API:

| API Name | Description | Associated with Resource | Resource Description |
| ---|---|---|--- |
| Getting cluster list and information of individual clusters | DescribeInstances| Yes |  `qcs::es:${Region}:uin/${ownerUin}:instance/${instanceId}` |
| Creating a cluster | CreateInstance| No |  `*` |
| Updating a cluster | UpdateInstance| Yes | `qcs::es:${Region}:uin/${ownerUin}:instance/${instanceId}` |
| Restarting a cluster | RestartInstance| Yes | `qcs::es:${Region}:uin/${ownerUin}:instance/${instanceId}` |
| Deleting a cluster | DeleteInstance| Yes |  `qcs::es:${Region}:uin/${ownerUin}:instance/${instanceId}` |
 
Supported regions include:

| Region Name | Region ID |
| :-------- | -------------- |
| Guangzhou | `ap-guangzhou` |

The syntax of a custom policy is as follows:

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "Action"
            ],
            "resource": "Resource",
            "effect": "Effect"
        }
    ]
}
```

- Action: Replace it with the operation to be allowed or denied.
- Resource: Replace it with the resources that you want to authorize the user to manipulate.
- Effect: Replace it with "Allow" or "Deny".

ES currently supports access control management for all APIs except DescribeInstances. You can authorize a sub-account to perform various operations on a cluster under your account such as updating, restarting, and deleting.

#### Custom Permission Sample
To grant an account permission to update the specified cluster, use the following policy syntax:
```
{
    "version": "2.0",
    "statement": [
    	 {
            "action": [
                "es:Describe*"
            ],
            "resource": [
               "qcs::es:ap-guangzhou:uin/$uin:instance/$instanceID"
            ],
            "effect": "allow"
        },
        {
            "action": [
                "vpc:Describe*",
                "vpc:Inquiry*",
                "vpc:Get*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "monitor:*",
                "cam:ListUsersForGroup",
                "cam:ListGroups",
                "cam:GetGroup"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "es:Update*"
            ],
            "resource": [
                "qcs::es:ap-guangzhou:uin/$uin:instance/$instanceID"
            ],
            "effect": "allow"
        }
    ]
}
```
