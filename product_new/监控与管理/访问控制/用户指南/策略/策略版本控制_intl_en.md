## Overview
When the custom policy operations you’ve configured change, the system does not overwrite the original policy. It automatically creates a new version instead. After saving, you can configure a default version by using different versions, rapidly rolling back to different policy versions.
## Configuring Permissions of Default Policy Versions
The root account or sub accounts that have cam:ListPolicies, cam:GetPolicy, and cam:UpdatePolicy API permissions can configure default policy versions.
Root accounts can use the following policy syntax to give sub accounts permission to configure the default policy version:
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/cam:ListPolicies",
                "name/cam:GetPolicy",
                "name/cam:UpdatePolicy"
            ],
            "resource": [
                "*"
            ]
        }
    ]
}
```
## Configuring the Default Version of Custom Policies
You can set one of the custom policy versions as the default version to make it the active version. After setup, all sub accounts that are associated with this custom policy will receive the current default version permissions.
1. Log in to the CAM console, and go to [Policies](https://console.cloud.tencent.com/cam/policy).
2. In the policy management page, click the name of the custom policy you want to configure to go to the policy details page.
3. In the policy details page, click **Policy Versions**.
4. Find the version you want to configure, select the box on the left, and click **Save as Default** to complete setting the custom policy default version.

## Rolling Back Changes by Using Different Versions
You can roll back your changes by setting the default version of the custom policy. For example, see the following scenario:
You create a custom policy that allows sub accounts to have CVM **ins-1** read permission. When you create the policy, there is only one version of the custom policy (labeled **Version 1**). This version is automatically set as the default version. This policy can operate normally.

You update this custom policy and add read permissions to CVM **ins-2**. After saving, the system will create a new policy version (labeled **Version 2**). After setting **Version 2** as the default version, the sub account responds that it lacks service management permissions. In this situation, you can roll back the current policy version to policy version **Version 1**. You can set **Version 1** as the default version and restore the sub account’s management permissions for the original CVM.

After finding and correcting the error in policy version **Version2**, the system will create another new version of this policy, labeled **Version 3**. You can set **Version 3** as the default version to provide the sub accounts with read permission to both CVM **ins-1** and CVM **ins-2**. You can delete the policy version **Version 2** which contains an error. 

## Version Limits
Each custom policy can have at most 5 versions. When the number of versions of the custom policy reaches 5, you must delete one or more of the current versions before you can edit and save a new policy version. You can select one of the following two methods to delete existing policy versions from the popup prompt window:
>- Delete the oldest, non-default policy version.
>- Select the policy version to be deleted. You can select multiple versions. You can click **▼** in the left side to view the policy syntax of each version to facilitate your decision.

>When you delete a version, the version labels of the remaining versions will not change. That is, the version labels may become non-continuous. For example, if you delete policy versions **Version2** and **Version4** and then add two new versions, the remaining version labels may be **Version1**, **Version3**, **Version5**, **Version6**, and **Version7**.
