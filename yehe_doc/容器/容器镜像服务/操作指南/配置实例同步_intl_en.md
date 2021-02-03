
## Overview
Tencent Container Registry (TCR) supports the synchronization of container images and Helm charts among different instances in different regions. It also supports single-point pushing and worldwide automatic synchronization and distribution, helping enterprises quickly deploy and update the Tencent Kubernetes Engine (TKE) service in multiple regions worldwide.

The instance synchronization feature allows you to customize synchronization rules and synchronize specified resources in an instance to a specified location of another instance. For example, you can select the synchronized resource type (container image, Helm chart, or both), filter the synchronized resource paths, and use a regular expression to filter repositories and versions. You can also select whether to overwrite existing images with the same names to prevent historical data loss due to overwriting.

## Prerequisites

Before creating and managing a synchronization rule for a TCR Enterprise Edition instance, complete the following tasks:
- [Purchasing Instances](https://intl.cloud.tencent.com/document/product/1051/39088).
- If you are using a sub-account, you must grant the sub-account required permissions for the instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).

## Directions
### Creating a synchronization rule
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Instance Synchronization** in the left sidebar.
On the "Instance Synchronization" page, you can view the list of synchronization rules for the current instance. To change the instance, select the desired instance name from the "Instance Name" drop-down list at the top of the page.
2. Click **Create**. In the "Create Instance Synchronization Rule" window, configure the rule based on the following information, as shown in the figure below.
![](https://main.qcloudimg.com/raw/6de531925e0b97e02961059d703279c8.png)
 - **Name**: indicates the instance rule name. It supports lowercase letters, numbers, and three symbols (`-`, `.`, and `_`). It must start with a letter or number.
 - **Description**: indicates the rule description.
 - **Source Address**
    - **Source Instance**: the current instance is the source instance. You can return to the "Instance Synchronization" page to change the source instance.
    - **Namespace**: indicates the namespace to which the current instance needs to synchronize. Currently, you cannot select all namespaces.
    - **Repository**: indicates the synchronized repository. You can use a regular expression to filter repositories. If this parameter is not specified, all repositories in the namespace are selected by default.
    - **Tag**: indicates the synchronized tag. You can use a regular expression to filter tags. If this parameter is not specified, all tags in the repositories that meet the requirements are selected by default.
    - **Repository Type**: indicates the synchronized resource type. You can synchronize container images and Helm charts simultaneously, or only one of them.
 - **Target Address**
    - **Target Instance**: indicates the target instance for data synchronization. You can select any instance on the platform.
    - **Namespace**: indicates the namespace where the repository is located after this repository is synchronized to the target instance. If this parameter is not specified, it is set to the namespace with the same name as that in the source instance by default. If such a namespace does not exist, a namespace is created.
 - **Overwrite the image with the same name**: indicates whether the container image with the same name in the target instance is overwritten. We recommend that you do not overwrite images with the same name.
3. Click **OK** to create the synchronization rule.

### Managing synchronization rules
After a synchronization rule is created, you can view the synchronization rule on the "Instance Synchronization" page. Then, you can perform the following operations to manage synchronization rules, as shown in the figure below:
![](https://main.qcloudimg.com/raw/dc388f24f649bb005bd8dd0df46220ae.png)

- **View synchronization logs**: you can click the name of an instance rule to view its triggering log. For more information, see [Viewing synchronization logs](#CheckLog).
- **Modify rule status**: <img src="https://main.qcloudimg.com/raw/d31873587cb976e1429768b2dc2b0e16.png" style="margin:-6px 0px"> indicates that the rule is enabled. <img src="https://main.qcloudimg.com/raw/5ba06490364505efc4d698e3adb1064e.png" style="margin:-6px 0px"> indicates that the rule is disabled. Newly created instance synchronization rules are enabled by default. You can adjust the rules as needed.
- **Trigger synchronization**: you can manually trigger synchronization. Then, all repositories in the instance that match the rule are scanned and synchronized.
- **Configure**: you can re-configure all parameters of the instance synchronization rule.
- **Delete**: you can delete an instance synchronization rule.
<span id="CheckLog"></span>
### Viewing synchronization logs
Click the name of an instance synchronization rule to view the triggering log of this rule, as shown in the figure below:
![](https://main.qcloudimg.com/raw/2261b918854b7d2d1a86ed40bdfc85bc.png)

- **Task ID**: indicates the synchronization task ID, which is unique in the instance.
- **Create Time**: indicates the time that the synchronization task is created.
- **Time Spent**: indicates the time that is consumed to complete all the synchronization tasks.
- **Success Rate**: indicates the resource synchronization completion ratio. Multiple repositories may be synchronized concurrently in the same synchronization task.
- **Number of synced repositories**: indicates the number of repositories that need to be synchronized in the current task.
- **Synchronization Status**: indicates the task status. If the number of container images and Helm charts that need to be synchronized in a task is large, the task may remain in the  “InProgress” (Synchronizing) state for a long time.
