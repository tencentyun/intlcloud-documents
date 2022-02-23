## Access Acquisition by Root Account
### Overview

As TI Platform needs to access the APIs of other Tencent Cloud services (such as COS) at runtime, it needs to be authorized to create a service role.

### Prerequisites

[Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).

>？
> After you sign up, the system will create a root account for you by default, which is used to quickly access Tencent Cloud resources.

### Directions

1. Log in to the TI Platform console with the **root account**, and you will be prompted to create a service role to access other Tencent Cloud resources in order to use TI Platform normally.

![](https://qcloudimg.tencent-cloud.cn/raw/13d217e54e6103dd649d210c223ba587.png)

2. Click **Authorize** to enter the CAM console for authorization. Click **Agree**, and TI Platform will be assigned a service role to access your resources.

![](https://qcloudimg.tencent-cloud.cn/raw/aaef43fa7fa7ad812c9773d0e8b7f404.png)


## Access Acquisition by Sub-account

1. A sub-account or collaborator account can log in to TI Platform. The root account can grant them the permission to manage access.

2. TI Platform offers the following three preset policies for the root account to easily grant commonly used permissions to a sub-account in the CAM console. For detailed directions, see [Creating and Authorizing Sub-account](https://intl.cloud.tencent.com/document/product/598/40985):

| Preset Policy Name                                         | Feature Description                                                     |
| ---------------------------------------------------- | ------------------------------------------------------------ |
| QcloudTIONEFullAccessContainMultiservice             | Full access to TI Platform, including read-only access to certain Tencent Cloud services (such as CAM, Tag, CM, and CloudAudit). Sub-accounts/Collaborators assigned this policy can use all features of TI Platform. |
| QcloudTIONEResouceGroupFullAccessContainMultiservice | Full access to the resource group management module of TI Platform, including read-only access to other modules of the platform and certain Tencent Cloud services (such as CAM, Tag, CM, and CloudAudit). Sub-accounts/Collaborators assigned this policy have read-only access to TI Platform and full access to the resource group management module. |
| QcloudTIONEReadOnlyAccessContainMultiservice         | Read-Only access to TI Platform and other Tencent Cloud services (such as CAM, Tag, CM, and CloudAudit). Sub-accounts/Collaborators assigned this policy have read-only access to TI Platform.  |

3. If the preset policies described above cannot meet the permission control requirements of the root account for sub-accounts, the root account can use a custom policy to authorize sub-accounts as instructed in [Permission and Policy](https://intl.cloud.tencent.com/document/product/598/10600). The following lists resources and operations supported for authorization:

- Resource list

| Module       | Resource | Resource Description Method in Authorization Policy                                      |
| ---------- | ------------ | ---------------------- | ------------------------------------------------------------ |
| Training | Training task      | qcs::tione:$region:$account:trainingtask/${trainingTaskId}   |
| Notebook   | Notebook | qcs::tione:$region:$account:notebook/${notebookId}           |
| Model Repository | Model | qcs::tione:$region:$account:model/${modelId}                 |
| Model Services   | Service group    | qcs::tione:$region:$account:servicegroup/${servicegroupid}   |
| Data Labeling | Personal labeling task | qcs::tione:$region:$account:personalannotationtask/${personalannotationtaskid} |
| Data Center   | Dataset             | qcs::tione:$region:$account:dataset/${datasetId}             |
| Resource group management | Resource group           | qcs::tione:$region:$account:resourcegroup/${resourcegroupId} |

- Operation list (TBD - the list of all APIs connected to CAM by the R&D team)

4. TI Platform has been connected to Tencent Cloud Tag. If you have already created tags for resources and want to grant a sub-account access to resources with one or multiple tags, you need to create a custom policy through **[authorization by tag](https://console.cloud.tencent.com/cam/policy/createByTag)** as instructed in [Creating Custom Policy](https://intl.cloud.tencent.com/document/product/598/35596).