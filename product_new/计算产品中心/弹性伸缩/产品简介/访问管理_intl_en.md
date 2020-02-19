## Overview

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) is a web-based Tencent Cloud service that helps you with the security management of access permissions for resources under your Tencent Cloud account. With CAM, you can create, manage, and terminate users or user groups, and can use identity and policy management to control the permissions other users have to use Tencent Cloud resources. Policies can be used to authorize or block the use of specified resources by users to complete specified tasks. When you use CAM, you can associate policies with a user or user group to perform permissions control.

Auto Scaling is already integrated with CAM. You can use CAM to control the permissions for resources related to Auto Scaling.


## Related Concepts

#### CAM users

[CAM users](https://intl.cloud.tencent.com/document/product/598/32633) are entities that you create in Tencent Cloud, and each CAM user is associated with only one Tencent Cloud account. The Tencent Cloud account you register is the **root account**. You can also create **sub-accounts** with different permissions in [Cloud Access Management](https://console.cloud.tencent.com/cam). There are 3 types of sub-accounts: [sub-users](https://intl.cloud.tencent.com/document/product/598/13674), [collaborators](https://intl.cloud.tencent.com/document/product/598/32639), and [message recipients](https://intl.cloud.tencent.com/document/product/598/13667).

#### Policies

[The policy](https://intl.cloud.tencent.com/document/product/598/10601) is the syntax rule used to define and describe one or more permissions. CAM supports two types of policies: preset policy and custom policy.

 - Preset policies: policies created and managed by Tencent Cloud. These are some common permission sets that are frequently used by users, such as full read and write permissions for resources. Preset policies have a wide range of operation objects, coarse operation granularity, and are preset by the system. They cannot be edited by users.
 - Custom policies: policies created by users. These permit fine-grained division of permissions. For example, a usage policy is associated with a sub-account that gives the sub-account management permissions for the scaling groups of Auto Scaling, but no management permissions for TencentDB instances.

#### Resources

[Resource](https://intl.cloud.tencent.com/document/product/598/10606) is an element of policies that describes one or multiple operation objects. For example, the launch configuration and scaling groups of Auto Scaling.

## Preset Policies of Auto Scaling

| Preset policy | Permissions granted |
| :----------------------- | :---------------------------------  |
| QcloudASFullAccess       | After association, full read-write access to Auto Scaling (AS) is obtained  |
| QcloudASReadOnlyAccess   | After association, read-only access to Auto Scaling (AS) is obtained    |


## Authorizable Resource Types

Resource-level permissions specify which resources a user can operate. For example, you can authorize a user to have operation permissions for scaling groups in Guangzhou region.
The resource types of Auto Scaling that can be authorized through CAM are as follows:

| Resource type     | Resource description method in authorization policy                     |
| :----------- | :------------------------------------------- |
| Launch configuration | `qcs::as:$region:$account:launch-configuration/*` |
| Scaling group | `qcs::as:$region:$account:auto-scaling-group/*`   |

The following table lists the resource-level permissions operations APIs that Auto Scaling supports, as well as the resource path supported by each operation.
When setting the resource path, you must modify variable parameters such as  `$region`, `$account`、`$LaunchConfigurationId`, and `$AutoScalingGroupId` according to your actual parameter information. You can also use `*` in the path as a wildcard character.
For information about related concepts in CAM policies such as region, action, account, and resource, see [Element Reference](https://intl.cloud.tencent.com/document/product/598/10603).

| API: action              | Resource path: resource      |
| :------------------------- | :----------------- |
| CreateLaunchConfiguration | `qcs::as:$region:$account:launch-configuration/*` |
| DeleteLaunchConfiguration | `qcs::as:$region:$account:launch-configuration/$LaunchConfigurationId`  |
| DescribeLaunchConfigurations | `qcs::as:$region:$account:launch-configuration/*`<br>`qcs::as:$region:$account:launch-configuration/$LaunchConfigurationId` |
| ModifyLaunchConfigurationAttributes | `qcs::as:$region:$account:launch-configuration/$LaunchConfigurationId` |
| UpgradeLaunchConfiguration | `qcs::as:$region:$account:launch-configuration/$LaunchConfigurationId` |
| CreateAutoScalingGroup | `qcs::as:$region:$account:auto-scaling-group/*` |
| CreateAutoScalingGroupFromInstance | `qcs::as:$region:$account:auto-scaling-group/*` |
| DeleteAutoScalingGroup | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| DescribeAutoScalingGroups | `qcs::as:$region:$account:auto-scaling-group/*`<br>`qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| ModifyAutoScalingGroup | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| ModifyLoadBalancers | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| EnableAutoScalingGroup | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| DisableAutoScalingGroup | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| ModifyDesiredCapacity | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| DescribeAutoScalingActivities | `qcs::as:$region:$account:auto-scaling-group/*`<br>`qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| AttachInstances | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| DetachInstances | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| RemoveInstances | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| DescribeAutoScalingInstances | `qcs::as:$region:$account:auto-scaling-group/*`<br>`qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| SetInstancesProtection | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| CreateScheduledAction | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| DeleteScheduledAction | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| DescribeScheduledActions | `qcs::as:$region:$account:auto-scaling-group/*`<br>`qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| ModifyScheduledAction | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| CreateScalingPolicy | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| DeleteScalingPolicy | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| DescribeScalingPolicies | `qcs::as:$region:$account:auto-scaling-group/*`<br>`qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| ModifyScalingPolicy | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| ExecuteScalingPolicy | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| CreateNotificationConfiguration | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| DeleteNotificationConfiguration | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| DescribeNotificationConfigurations | `qcs::as:$region:$account:auto-scaling-group/*`<br>`qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| ModifyNotificationConfiguration | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| CreateLifecycleHook | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| DeleteLifecycleHook | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| DescribeLifecycleHooks | `qcs::as:$region:$account:auto-scaling-group/*`<br>`qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| UpgradeLifecycleHook | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| CompleteLifecycleAction | `qcs::as:$region:$account:auto-scaling-group/$AutoScalingGroupId` |
| DescribeAccountLimits | `*` |


## Auto Scaling CAM Policy Example

The following section provides specific examples that display how to use CAM to control permissions for Auto Scaling:

- Create policy: Guangzhou region allows access permissions to all scaling groups.
```
# In this example, `$account` must be substituted with the account information
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/as:*"
            ],
            "resource": [
                "qcs::as:ap-guangzhou:$account:auto-scaling-group/*"
            ]
        }
    ]
}
```
- Create policy: Guangzhou region prohibits access permissions to a certain scaling group.
```
# In this example, `$account` must be substituted with the account information, and `$AutoScalingGroupId` must be substituted with the corresponding AutoScalingGroupId.
{
    "version": "2.0",
    "statement": [
        {
            "effect": "deny",
            "action": [
                "name/as:*"
            ],
            "resource": [
                "qcs::as:ap-guangzhou:$account:auto-scaling-group/$AutoScalingGroupId"
            ]
        }
    ]
}
```
- Create policy: all read APIs have access permissions in all regions.	
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/as:Describe*"
            ],
            "resource": [
                "*"
            ]
        }
    ]
}
```
