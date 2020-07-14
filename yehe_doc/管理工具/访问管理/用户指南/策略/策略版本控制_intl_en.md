## Overview
When a custom policy you configured is changed, the system will not overwrite it; instead, it will automatically create a new version. After saving the change, you can configure a default version out of different versions for rapid rollback to different policy versions.
## Granting Permission to Set Default Policy Version
Root accounts and sub-accounts that have permissions to use the `cam:ListPolicies`, `cam:GetPolicy`, and `cam:UpdatePolicy` APIs can configure a default policy version.
Root accounts can use the following policy syntax to grant sub-accounts permission to configure a default policy version:
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
## Setting the default version of custom policy
You can set one of the custom policy versions as the default version to make it the active version. After the configuration, all sub-accounts associated with this custom policy will receive the permissions set on the default version.
1. Log in to the CAM console, and go to [Policies](https://console.cloud.tencent.com/cam/policy).
2. On the policy management page, click the name of the custom policy you want to configure to enter the policy details page.
3. On the policy details page, select **Policy Version**.
4. Locate the version you want to configure, check the box on the left, and click **Save as Default**.

## Rolling back Changes by Using Different Versions
You can roll back your changes by setting the default version of the custom policy. For example, see the following scenario:
You create a custom policy that allows sub-accounts to have read access to CVM instance `ins-1`. When you create the policy, there is only one version of the custom policy (tagged as "v1"). This version is automatically set as the default version, and this policy can work normally.
 
You update this custom policy and add read permission to CVM instance `ins-2`. After the change is saved, the system will create a new policy version (tagged as "v2"). After v2 is set as the default version, sub-accounts feed back that they lack the original CVM management permission. In this case, you can roll back the current policy version to v1. You can set v1 as the default version and restore the sub-account's management permission for the original CVM instance.

You find and correct an error in policy v2, and the system will create another new version of the policy (tagged as "v3"). You can set v3 as the default version to provide the sub-accounts with read permission to both CVM instances `ins-1` and `ins-2`. You can delete the policy v2 which contains the error. 

## Version Limits
Each custom policy can have up to 5 versions. When the number of versions of a custom policy reaches 5, you must delete one or more current versions before you can edit and save a new version. You can delete existing policy versions in the pop-up dialog box in the following two ways:
>- Delete the oldest non-default policy version.
>- Select one or more policy versions to be deleted. You can click **▼** on the left to view the policy syntax of each version to make decisions more conveniently.

>?When a version is deleted, version IDs of the remaining versions will not change. Therefore, version IDs may be discontinuous. For example, if you delete the policy v2 and v4 and then add two new versions, the remaining version IDs may be v1, v3, v5, v6, and v7.
