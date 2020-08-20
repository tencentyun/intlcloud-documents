## ES CAM Overview
Cloud Access Management (CAM) is a web-based Tencent Cloud service that helps you securely manage and control access permissions to resources under your Tencent Cloud account. With CAM, you can create, manage, and terminate users (user groups) and use identities and policies to control user access to Tencent Cloud resources. For more information on CAM policies and usage, please see [CAM Policy](https://intl.cloud.tencent.com/document/product/598/10601).  

## ES CAM Policies
### General permission policy
ES provides two general policies by default:
- Full access policy (QcloudElasticsearchServiceFullAccess), which grants a user permission to create and manage all ES cluster instances. 
- Read-only access policy (QcloudElasticsearchServiceReadOnlyAccess), which grants a user permission to view ES cluster instances but not create, update, or delete them.  

You can log in to the [Policy Management](https://console.cloud.tencent.com/cam/policy) page, select "Elasticsearch Service" in "Service Type", and bind the default policies displayed in the list to accounts as needed.
![](https://main.qcloudimg.com/raw/3555788e9bfc9b81346b614ce32a8673.png)
If the default policies cannot meet your requirements, you can click **Create Custom Policy** to customize the authorization.

### Custom permission policy

Types of resources that can be authorized in ES include:

| Resource Type | Resource Description |
| -------- | -------------- |
| instance | `qcs::es:$region:$account:instance/*` |

Below describes the details of resource-level access control supported by each API:

| API Name | Description | Associated with Resource | Resource Description |
| ---|---|---|--- |
| Getting cluster list and information of individual clusters | DescribeInstances| Yes |  `qcs::es:${Region}:uin/${ownerUin}:instance/${instanceId}` |
| Creating cluster | CreateInstance| No |  `*` |
| Updating cluster | UpdateInstance| Yes | `qcs::es:${Region}:uin/${ownerUin}:instance/${instanceId}` |
| Restarting cluster | RestartInstance| Yes | `qcs::es:${Region}:uin/${ownerUin}:instance/${instanceId}` |
| Deleting cluster | DeleteInstance| Yes |  `qcs::es:${Region}:uin/${ownerUin}:instance/${instanceId}` |
| Updating plugin |  UpdatePlugins    | Yes |  `qcs::es:${Region}:uin/${ownerUin}:instance/${instanceId}` |

Supported regions include:
<table>
<thead>
<tr>
<th align="left">Region</th>
<th align="left">Name</th>
<th>Region ID</th>
</tr>
</thead>
<tbody><tr>
<td align="left" rowspan="2">South China</td>
<td align="left">Guangzhou</td>
<td><code>ap-guangzhou</code></td>
</tr>
<tr>
<td align="left">Qingyuan</td>
<td><code>ap-qingyuan</code></td>
</tr>
<tr>
<td align="left" rowspan="2">East China</td>
<td align="left">Shanghai</td>
<td><code>ap-shanghai</code></td>
</tr>
<tr>
<td align="left">Nanjing</td>
<td><code>ap-nanjing</code></td>
</tr>
<tr>
<td align="left">North China</td>
<td align="left">Beijing</td>
<td><code>ap-beijing</code></td>
</tr>
<tr>
<td align="left" rowspan="2">Southwest China</td>
<td align="left">Chengdu</td>
<td><code>ap-chengdu</code></td>
</tr>
<tr>
<td align="left">Chongqing</td>
<td><code>ap-chongqing</code></td>
</tr>
<tr>
<td align="left">Hong Kong/Macao/Taiwan</td>
<td align="left">Hong Kong (China)</td>
<td><code>ap-hongkong</code></td>
</tr>
<tr>
<td align="left">Southeast Asia Pacific</td>
<td align="left">Singapore</td>
<td><code>ap-singapore</code></td>
</tr>
<tr>
<td align="left">South Asia Pacific</td>
<td align="left">Mumbai</td>
<td><code>ap-mumbai</code></td>
</tr>
<tr>
<td align="left" rowspan="2">Northeast Asia Pacific</td>
<td align="left">Seoul</td>
<td><code>ap-seoul</code></td>
</tr>
<tr>
<td align="left">Tokyo</td>
<td><code>ap-tokyo</code></td>
</tr>
<tr>
<td align="left">West US</td>
<td align="left">Silicon Valley</td>
<td><code>na-siliconvalley</code></td>
</tr>
<tr>
<td align="left">East US</td>
<td align="left">Virginia</td>
<td><code>na-ashburn</code></td>
</tr>
<tr>
<td align="left">North America</td>
<td align="left">Toronto</td>
<td><code>na-toronto</code></td>
</tr>
<tr>
<td align="left">Europe</td>
<td align="left">Frankfurt</td>
<td><code>eu-frankfurt</code></td>
</tr>
</tbody></table>

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

- Action: replace it with the operation to be allowed or denied.
- Resource: replace it with the resources that you want to authorize the user to manipulate.
- Effect: replace it with "allow" or "deny".

ES currently supports access control management for all APIs except `DescribeInstances`. You can authorize a sub-account to perform various operations on a cluster under your account such as updating, restarting, and deleting.

#### Custom permission sample
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
