## Operation Scenarios
[Role](https://intl.cloud.tencent.com/document/product/598/19420) is a virtual identity with a set of permissions provided by [CAM](https://intl.cloud.tencent.com/document/product/598/10583), which is mainly used to grant access permissions of services, operations, and resources in Tencent Cloud to role entities. After these permissions are added to a role, the role can be configured to Tencent Cloud services, allowing the services to perform operations on authorized resources on your behalf.

When creating an SCF function, you may need the permissions to manipulate other Tencent Cloud services. Examples include COS permissions to create and delete COS triggers, API Gateway permissions to create and delete API Gateway triggers, and COS permissions to read zipped code packages.

## Role Details

- Role name: `SCF_QcsRole` 
- Role entity: `service-scf.qcloud.com`
- Role description: default configuration role of SCF. This service role is used to grant the SCF configuration the permissions to connect with other resources in the cloud, including but not limited to code file access and trigger configuration. The preset policy of the configuration role can support basic operations of function execution.
- Role policy: this role has the `QcloudAccessForScfRole` policy that can:
 - Write trigger configuration information to the bucket configuration if a COS trigger is configured. 
 - Read the trigger configuration information from the COS bucket. 
 - Read the code zip package from the bucket when the code is updated through COS. 
 - Create API Gateway services and APIs and publish services if an API Gateway trigger is configured. 

>You can log in to the [CAM Console](https://console.cloud.tencent.com/cam/overview) to view and modify the policy associated with the current configuration role `SCF_QcsRole`; however, modifying the associated policy of the role may cause SCF to fail; therefore, you are not recommended to modify it.
>


## Directions
The `SCF_QcsRole` role is used to grant SCF the permissions to read and manipulate user resources during configuration. If you receive an error for missing role or permission when managing functions (such as using TCCLI or VS Code plugin to update function code), you need to configure the `SCF_QcsRole` role.
>If you are currently a sub-user/collaborator, authorization should be performed by the root account in the following steps. After the authorization is completed, both the root account and sub-user can log in and use the SCF service.
>
1. If you are using SCF for the first time, you will be prompted for service authorization when you open the [SCF Console](<https://console.cloud.tencent.com/scf/index?rid=1>) as shown below:
![](https://main.qcloudimg.com/raw/c30306b710621fc522ea94f9f310fb90.png)
2. Select **Go to CAM** to enter the "Role Management" page and click **Agree to Authorize** to confirm the authorization as shown below:
![](https://main.qcloudimg.com/raw/2b8821b11d01bc42a69da72e822987b8.png)
3. After the authorization is confirmed, the role `SCF_QcsRole` will be automatically created for you as shown below:
![](https://main.qcloudimg.com/raw/cdc5d8421624fa1f8dbdcb9f88fff316.png)

## Appendix
<spoan id="Strategy"></span>
### Notes on user policy update
SCF improved the preset permission policies in April 2020. The preset policies `QcloudSCFFullAccess` and `QcloudSCFReadOnlyAccess` were modified, and the `QcloudAccessForScfRole` policy was added for the configuration role `SCF_QcsRole` as shown below:
- Currently, the preset policy `QcloudSCFFullAccess` has the following permissions:
``` json
{
   "version":"2.0",
   "statement":[
      {
         "action":[
            "scf:*",
            "tag:*",
            "cam:DescribeRoleList",
            "cam:GetRole",
            "cam:ListAttachedRolePolicies",
            "apigw:DescribeServicesStatus",
            "apigw:DescribeService",
            "apigw:DescribeApisStatus",
            "cmqtopic:ListTopicDetail",
            "cmqqueue:ListQueueDetail",
            "cmqtopic:GetSubscriptionAttributes",
            "cmqtopic:GetTopicAttributes",
            "cos:GetService",
            "cos:HeadBucket",
			"cos:HeadObject",
            "vpc:DescribeVpcEx",
            "vpc:DescribeSubnetEx",
            "cls:getTopic",
            "cls:getLogset",
            "cls:listLogset",
            "cls:listTopic",
            "ckafka:List*",
            "ckafka:Describe*",
			"monitor:GetMonitorData",
            "monitor:DescribeBasicAlarmList",
            "monitor:DescribeBaseMetrics",
            "monitor:DescribeSortObjectList",
            "monitor:DescribePolicyConditionList",
            "cdb:DescribeDBInstances"
         ],
         "resource":"*",
         "effect":"allow"
      }
   ]
}
```
- Currently, the preset policy `QcloudSCFReadOnlyAccess` has the following permissions:
``` json
{
   "version": "2.0",
   "statement": [
      {
         "action": [
            "scf:Get*",
            "scf:List*",
            "ckafka:List*",
            "ckafka:Describe*",
            "monitor:GetMonitorData",
            "monitor:DescribeBasicAlarmList",
            "monitor:DescribeBaseMetrics",
            "monitor:DescribeSortObjectList",
            "cam:GetRole",
            "cam:ListAttachedRolePolicies",
            "vpc:DescribeVpcEx",
            "vpc:DescribeSubnetEx",
            "cls:getLogset",
            "cls:getTopic",
            "cls:listTopic",
            "apigw:DescribeService",
            "cmqtopic:GetTopicAttributes",
            "cmqtopic:GetSubscriptionAttributes",
            "cos:HeadBucket",
            "cos:GetService",
            "cos:GetObject"
         ],
         "resource": "*",
         "effect": "allow"
      }
   ]
}
```
- Currently, the preset policy `QcloudAccessForScfRole` has the following permissions:
``` json
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "ckafka:List*",
                "ckafka:Describe*",
                "ckafka:AddRoute",
                "ckafka:CreateRoute",
                "apigw:ReleaseService",
                "apigw:CreateService",
                "apigw:CreateApi",
                "apigw:DeleteApi",
                "cls:*",
                "cos:List*",
                "cos:Get*",
                "cos:Head*",
                "cos:PutBucket",
                "cos:OptionsObject",
                "cmqqueue:*",
                "cmqtopic:*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
The preset policy `QcloudAccessForScfRole` can:
 - Write trigger configuration information to the bucket configuration if a COS trigger is configured. 
 - Read the trigger configuration information from the COS bucket. 
 - Read the code zip package from the bucket when the code is updated through COS. 
 - Create API Gateway services and APIs and publish services if an API Gateway trigger is configured. 
 - Create consumers if a CKafka trigger is configured. 
