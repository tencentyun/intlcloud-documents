
## Overview
Tencent Container Registry (TCR) supports the synchronization of container images and Helm charts among different instances in different regions. It also supports single-instance image pushing and worldwide automatic image data synchronization and distribution, helping enterprises quickly deploy and update the Tencent Kubernetes Engine (TKE) service in multiple regions worldwide.

The instance synchronization feature allows you to customize synchronization rules and synchronize specified resources in an instance to a specified location of another instance. In particular, you can select the synchronized resource type (container image, Helm chart, or both), filter the synchronized resource paths, and use a regular expression to filter repositories and tags. You can also select whether to overwrite existing images with the same names to prevent the loss of historical data due to overwriting.

## Prerequisites

Before creating and managing the synchronization configuration of a TCR Enterprise Edition instance, complete the following tasks:
- You have [purchased an Enterprise Edition instance](https://intl.cloud.tencent.com/document/product/1051/39088).
- If you are using a sub-account, you must have granted the sub-account operation permissions for the corresponding instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).

## Directions
### Creating a synchronization rule
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Synchronization** in the left sidebar.
On the "Synchronization" page, you can view the list of synchronization rules for the current instance. To change the instance, select the desired instance name from the "Instance Name" drop-down list at the top of the page.
2. Click **Create**. In the "Create Instance Synchronization Rule" window, configure the rule based on the information shown in the figure below.
![](https://main.qcloudimg.com/raw/6de531925e0b97e02961059d703279c8.png)
 - **Name**: rule name, which is a string of lowercase letters, numbers, and special characters (`-`, `.`, and `_`) and must start with a letter or number.
 - **Description**: rule description.
 - **Sync source**:
    - **Source Instance**: the current instance is the source instance. You can return to the "Synchronization" page to change the source instance.
    - **Namespace**: namespace with which the current instance needs to synchronize. Currently, you cannot select all namespaces.
    - **Repository Name**: synchronized repository. You can use a [regular expression](https://intl.cloud.tencent.com/document/product/1051/35488) to filter repositories. If this parameter is not specified, all repositories in the namespace are selected by default.
    - **Tag**: synchronized tag. You can use a [regular expression](https://intl.cloud.tencent.com/document/product/1051/35488) to filter tags. If this parameter is not specified, all tags in the repositories that meet the requirements are selected by default.
    - **Repository Type**: synchronized resource type. You can synchronize both container images and Helm charts simultaneously or only synchronize one type of resource.
 - **Synchronization Target**:
    - **Target Instance**: target instance for data synchronization. You can select any instance on the platform.
    - **Namespace**: namespace where the repository is located after it is synchronized to the target instance. If this parameter is not specified, it is set to the namespace with the same name as that in the source instance by default. If such a namespace does not exist, a namespace is created.
 - **Image Override**: this indicates whether the container image with the same name in the target instance is overwritten. We recommend that you do not overwrite images with the same name.
3. Click **Confirm** to create the synchronization rule.

### Managing synchronization rules
After a synchronization rule is created, you can view the synchronization rule on the "Synchronization" page. Then, you can perform the operations shown in the figure below to manage synchronization rules.
![](https://main.qcloudimg.com/raw/dc388f24f649bb005bd8dd0df46220ae.png)

- **View Synchronization Logs**: click an instance rule to view triggering logs of the rule. For more information, see [Viewing synchronization logs](#CheckLog).
- **Modify Rule Status**: <img src="https://main.qcloudimg.com/raw/d31873587cb976e1429768b2dc2b0e16.png" style="margin:-6px 0px"> indicates that a rule is enabled, and <img src="https://main.qcloudimg.com/raw/5ba06490364505efc4d698e3adb1064e.png" style="margin:-6px 0px"> indicates that a rule is disabled. Newly created instance synchronization rules are enabled by default, and you can choose whether to disable them.
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
- **Number of synced repositories**: number of repositories that need to be synchronized in the current task.
- **Synchronization Status**: task status. If a large number of container images and Helm charts need to be synchronized in a task, the task may remain in the InProgress state for a long time.



 

 

 

 

 



 

 

 

 

 

  

 

 

 

 

 

 

 

 

 

 

 




