A policy is a syntactic specification of a user permission set, which accurately describes the authorized resource set, operation set, and authorization conditions.

## [CAM Policy Syntax](id:yufa)
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

The following table describes policy statements.
<table class="table-striped">
<tbody>
<tr><th>Parameter</th><th>Sub-parameter</th><th>Required</th><th>Description</th></tr>
<tr>
<td><b>version</b></td>
<td>N/A</td>
<td>Yes</td>
<td>The only valid value is "2.0".</td></tr>
<tr>    
<td rowspan="4"><b>statement</b></td>
<td>effect</td>    
<td>Yes</td>
<td>It describes whether the statement results in an "allow" or an explicit "deny".</td></tr>
<tr>    
<td>action</td>    
<td>Yes</td>
<td>It describes the allowed or denied operation which can be an API or a feature set (a set of specific APIs prefixed with "permid").</td></tr>
<tr>    
<td>resource</td>    
<td>Yes</td>
<td>It describes the details of authorization. All resources can be described in the six-segment format. Each service has its own resources and detailed resource definition.</td></tr>
<tr>    
<td>condition</td>    
<td>Yes</td>
<td>It specifies the condition for the policy to take effect. A condition consists of the operator, action key, and action value. A condition value may be the time, IP address, etc. Some services allow you to specify additional values in a condition.</td></tr>
</tbody></table>

>? The **statement** element describes the details of one or more permissions. This element contains a permission or permission set of other elements such as `effect`, `action`, `resource`, and `condition`. One policy has only one `statement`.


### [Defining action](id:caozuo)
In a CAM policy statement, you can specify any API operation from any service that supports CAM. APIs prefixed with "mongodb:" should be used for MongoDB, such as mongodb:BackupDBInstance or mongodb:CreateAccountUser.
To specify multiple operations in a single statement, separate them with commas as shown below:
```
"action":["mongodb:action1","mongodb:action2"]
```

You can also specify multiple operations using a wildcard. For example, you can specify all operations whose names begin with "Describe" as shown below:
```
"action":["mongodb:Describe*"]
```

If you want to specify all operations in MongoDB, use a wildcard "*" as shown below:
```
"action"：["mongodb:*"]
```


### [Defining resource](id:lujing)
Each CAM policy statement is resource-specific with a resource path as shown below:
```
qcs:project_id:service_type:region:account:resource
```
- **project_id**: project information, which is only used to enable compatibility with legacy CAM logic and can be left empty.
- **service_type**: product’s abbreviation, for example, `mongodb`.
- **region**: region information, for example, `bj`.
- **account**: the root account of the resource owner, for example, `uin/12345678`.
- **resource**: detailed resource information of each product, for example, `instance/instance_id` or `instance/*`.

You can set `resource` to an instance ID (cmgo-aw6g1g0z) in a statement as shown below:
```
"resource":[ "qcs::mongodb:bj:uin/12345678:instance/cmgo-aw6g1g0z"]
```

You can also use the wildcard "*" to specify all instances that belong to a specific account as shown below:
```
"resource":[ "qcs::mongodb:bj:uin/12345678:instance/*"]
```

If you want to specify all resources or if a specific API operation does not support resource-level permission control, you can use the wildcard "*" in the `resource` element as shown below:
```
"resource": ["*"]
```

If you want to specify multiple resources in a single command, separate them with commas. In the following example, two resources are specified:
```
"resource":["resource1","resource2"]
```

The table below describes the resources that can be used by MongoDB and the corresponding resource description methods, where words prefixed with `$` are placeholders, `region` refers to a region, and `account` refers to an account ID.

| Resource Type | Resource Description Method in Authorization Policy |
| -------- | ------------------------------------------------------------ |
| Instance     | `qcs::mongodb:$region:$account:instance/*`<br>`qcs::mongodb:$region:$account:instance/$instanceId` |
| VPC      | `qcs::vpc:$region:$account:vpc/$vpcId`                       |
| Security group   | `qcs::cvm:$region:$account:sg/$sgId`                         |

## Default Permission Policy of TencentDB for MongoDB
TencentDB for MongoDB supports the following system permission policies.

| **Policy**                  | **Description**                                                     |
| ----------------------------- | ------------------------------------------------------------ |
| `QcloudMongoDBFullAccess`     | TencentDB for MongoDB management permission. A Tencent Cloud sub-account granted with this permission has the same permissions as the root account, including all permissions of console and API operations. |
| `QcloudMongoDBReadOnlyAccess` | Read-Only permission. A Tencent Cloud sub-account granted with this permission only has the read-only permission on all resources of the root account, but does not have any permission of console and API operations. |

The system permission policy `QcloudMongoDFullAccess` is as follows:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "monitor:GetMonitorData",
                "monitor:DescribeBaseMetrics",
                "mongodb:*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

The system permission policy `QcloudMongoDBReadOnlyAccess` is as follows:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "monitor:GetMonitorData",
                "monitor:DescribeBaseMetrics",
                "mongodb:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

## Custom Permission Policy of TencentDB for MongoDB
Currently, TencentDB for MongoDB supports custom policies for the following resource-level permissions.

>?TencentDB API operations not listed here do not support resource-level permissions. You can still authorize a user to perform such a TencentDB API operation, but you must specify * as the resource element of the policy statement. 

<table class="table-striped">
<tbody>
<tr><th>action Name</th><th>Permission</th><th>resource Description</th></tr>
<tr>
<td>BackupDBInstance</td>
<td>Back up a database instance</td>
<td>
    <ul>
       <li>qcs::mongodb:$region:$account:instance/*</li>
       <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>	
<tr>
<td>CreateAccountUser</td>
<td>Create an account</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>	
<tr>
<td>CreateDBInstanceHour</td>
<td>Create a pay-as-you-go TencentDB instance</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>DeleteAccountUser</td>
<td>Delete an account</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>DescribeAccountUsers</td>
<td>Query user information of an account</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>DescribeBackupAccess</td>
<td>Get the permission to download instance backups</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>DescribeBackupRules</td>
<td>Query the backup rules of a TencentDB instance</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>DescribeClientConnections</td>
<td>Query the number of client connections</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>DescribeDBBackups</td>
<td>Query the instance backup list</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>DescribeDBBackups</td>
<td>Query the instance backup list</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>DescribeDBInstances</td>
<td>Query the database instance list</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>DescribeInstanceDB</td>
<td>Query the database table information of an instance</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>DescribeSlowLog</td>
<td>Query the information of slow query logs</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>DescribeSlowLogPattern</td>
<td>Query the statistics of slow query logs</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>DescribeSpecInfo</td>
<td>Query the purchasable specifications of TencentDB instances</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>ExchangeInstance</td>
<td>Replace an instance with a temp instance</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>IsolateDBInstance</td>
<td>Isolate a TencentDB instance</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>ModifyDBInstanceSpec</td>
<td>Adjust the configuration of a TencentDB instance</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>OfflineIsolatedDBInstance</td>
<td>Eliminate an isolated TencentDB instance</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr> 
<tr>
<td>RemoveCloneInstance</td>
<td>Delete a temp instance</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>RenameInstance</td>
<td>Rename an instance</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr> 
<tr>
<td>ResizeOplog</td>
<td>Resize the oplog of an instance</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr> 
<tr>
<td>RestartInstance</td>
<td>Restart an instance</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>RestoreDBInstance</td>
<td>Restore a database instance</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>SetAccountUserPrivilege</td>
<td>Set user permissions</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>SetInstanceFormal</td>
<td>Promote a temp instance to primary instance</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>SetInstanceMaintenance</td>
<td>Set maintenance time for an instance</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>SetPassword</td>
<td>Set a password</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>SetReadOnlyToNormal</td>
<td>Promote a read-only instance to primary instance</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>TerminateDBInstanceHour</td>
<td>Terminate a pay-as-you-go instance</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
<tr>
<td>UpgradeDBInstanceHour</td>
<td>Upgrade a pay-as-you-go instance</td>
<td>
    <ul>
        <li>qcs::mongodb:$region:$account:instance/*</li>
        <li>qcs::mongodb:$region:$account:instance/$instanceId</td></li>
    </ul>
</td></tr>
</tbody>
</table>


### Custom permission policy example
If you want to grant an account the `CreateDBInstance` and `CreateAccountUser` permissions on the "cmgo-aw6g****" instance, you can create a policy as follows:
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "mongodb:CreateDBInstance",
                "mongodb:CreateAccountUser"
            ],
            "resource": [
                "qcs::mongodb::uin/100001540306:instanceId/cmgo-aw6g****"
            ],
            "condition": {
                "ip_equal": {
                    "qcs:ip": [
                        "10.0.0.4"
                    ]
                }
            }
        }
    ]
}
```

### Creating a custom permission policy
You can create a custom policy on the [Policy](https://console.cloud.tencent.com/cam/policy) page in the CAM console. For detailed directions, see [Creating Custom Policy](https://intl.cloud.tencent.com/document/product/598/35596).

