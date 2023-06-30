
## Overview
Tencent Container Registry (TCR) supports the synchronization of container images and Helm Charts among instances in different regions. It also supports single-instance image pushing and worldwide automatic image data synchronization and distribution, helping enterprises quickly deploy and update the container service in multiple regions worldwide.

The instance synchronization feature allows you to customize rules to synchronize specified resources in an instance to a specified location of another instance. In particular, you can select the synchronized resource type (container image, Helm Chart, or both), filter the synchronized resource paths, and use a regular expression to filter repositories and tags. You can also select whether to overwrite existing images with the same names to prevent the loss of historical data due to overwriting. Currently, the instance synchronization feature supports cross-tenant synchronization. You can create a synchronization rule by specifying the instance ID, account ID and access credential of the synchronization target.

## Prerequisites

Before creating and managing the synchronization configuration of a TCR Enterprise instance, you need to complete the following tasks:
- You have [purchased a TCR Enterprise instance](https://intl.cloud.tencent.com/document/product/1051/39088) with standard or premium specification.
- If you are using a sub-account, you must have granted the sub-account operation permissions for the corresponding instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).

## Directions
### Creating a synchronization rule
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Synchronization and Replication** > **Synchronization** in the left sidebar.
2. On the **Synchronization** page, select a region and an instance, and click **Create**.
3. In the **Create Instance Synchronization Rule** window, configure the rule as instructed below.
![](https://main.qcloudimg.com/raw/6de531925e0b97e02961059d703279c8.png)
 - **Name**: rule name, which is a string of lowercase letters, numbers, and special characters ([-._]) and must start with a letter or number.
 - **Description**: rule description.
 - **Sync Source**:
    - **Source Instance**: the current instance is the source instance. You can return to the "Synchronization" page to change the source instance.
    - **Namespace**: namespace with which the current instance needs to synchronize. Currently, you cannot select all namespaces.
    - **Repository Name**: the repository to be synchronized. You can use [regular expression](https://intl.cloud.tencent.com/document/product/1051/35488) to filter. If you do not enter the repository name, the system will select all repositories in the namespace by default.
    - **Tag**: the tag to be synchronized. You can use [regular expression](https://intl.cloud.tencent.com/document/product/1051/35488) to filter. If you do not enter the tag, the system will select all tags in the qualified repositories by default.
    - **Repository Type**: type of the resource to be synchronized. You can choose both **Container Image** and **Helm Chart**, or only one of them.
 - **Synchronization Target**: you can specify whether to enable cross-tenant synchronization. 
<dx-tabs>
::: Disabled
If **Cross-tenant sync** is disabled, the synchronization is between instances under the same tenant. You need to complete the following fields.
- **Target Instance**: target instance for data synchronization. You can select any instance in the root account.
- **Namespace**: namespace where the repository is located after it is synchronized to the target instance. If this parameter is not specified, it is set to the namespace with the same name as that in the source instance by default. If such a namespace does not exist, a namespace is created.
:::
::: Enabled
If **Cross-tenant sync** is enabled, you can sync between instances under different tenants. The following fields are required.
- **Target Instance**: ID of the target instance for data synchronization. You can go to [Instance Management](https://console.cloud.tencent.com/tcr) to obtain it.
- **Namespace**: namespace where the repository is located after it is synchronized to the target instance. If this parameter is not specified, it is set to the namespace with the same name as that in the source instance by default. If such a namespace does not exist, a namespace is created.
- **Account ID**: account ID of the synchronization target. You can obtain it from [Account Info](https://console.cloud.tencent.com/developer).
- **Access Credential**: access credential provided by the target account. See [Obtaining an Instance Access Credential](https://intl.cloud.tencent.com/document/product/1051/37253)
<dx-alert infotype="notice" title="">
1. Please use long-term access credential to ensure that the rule can work properly. Keep the lifecycle of the synchronization rule consistent with that of access credential of newly added synchronization rules under the target account.
2. Please be aware of the risk of unauthorized access. Keep the permissions of access credential consistent with that of the sub-account which creates the credential. It is recommended that you create a new sub-account for cross-tenant synchronization and only grant this sub-account permissions of pushing images. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).
</dx-alert>
:::
</dx-tabs>
 - **Image Override**: this indicates whether the container image with the same name in the target instance is overwritten. We recommend that you do not overwrite images with the same name.
3. Click **OK**.

### Managing synchronization rules
After a synchronization rule is created, you can check it on the **Synchronization** page. Then, you can perform the operations shown in the figure below to manage synchronization rules.
![](https://main.qcloudimg.com/raw/dc388f24f649bb005bd8dd0df46220ae.png)

- **View Synchronization Logs**: click an instance rule to view triggering logs of the rule. For more information, see [Viewing synchronization logs](#CheckLog).
- **Modify Rule Status**: <img src="https://main.qcloudimg.com/raw/d31873587cb976e1429768b2dc2b0e16.png" style="margin:-6px 0px"> indicates that a rule is enabled, and <img src="https://main.qcloudimg.com/raw/5ba06490364505efc4d698e3adb1064e.png" style="margin:-6px 0px"> indicates that a rule is disabled. A newly created synchronization rule is enabled by default, and you can change the status as needed.
- **Trigger Synchronization**: manually trigger synchronization. All repositories in the instance that match the rule are scanned and synchronized.
- **Configuration**: re-configure an instance synchronization rule. You can configure all parameters.
- **Deletion**: delete the instance synchronization rule.

### Viewing synchronization logs[](id:CheckLog)
Click the name of an instance synchronization rule to go to the "Synchronization Logs" page of this rule, as shown in the figure below.
![](https://main.qcloudimg.com/raw/2261b918854b7d2d1a86ed40bdfc85bc.png)
- **Task ID**: synchronization task ID, which is unique in the instance.
- **Creation Time**: time when the synchronization task was created.
- **Time Spent**: time consumed to complete all the synchronization tasks.
- **Success Rate**: resource synchronization completion ratio. Multiple repositories may be synchronized concurrently in the same synchronization task.
- **Number of Synced Repositories**: number of repositories that need to be synchronized in the current task.
- **Synchronization Status**: task status. If a large number of container images and Helm Charts need to be synchronized in a task, the task may remain in the InProgress status for a long time.




## References

You can also use the `ManageReplication` API to manage instance sync.

