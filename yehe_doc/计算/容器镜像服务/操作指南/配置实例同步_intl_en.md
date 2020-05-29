
## Scenario
Tencent Container Registry (TCR) supports the synchronization of container images and Helm charts among different instances in different regions. It also supports single-point pushing and worldwide automatic synchronization and distribution, helping enterprises quickly deploy and update the Tencent Kubernetes Engine (TKE) service in multiple regions worldwide.

The instance synchronization feature allows you to customize synchronization rules and synchronize specified resources in an instance to a specified location of another instance. In particular, you can select the synchronized resource type (container image, Helm chart, or both), filter the synchronized resource paths, and use a regular expression to filter repositories and versions. You can also select whether to overwrite existing images with the same names to prevent the loss of historical data due to overwriting.

## Prerequisites

Before creating and managing a synchronization rule for a TCR Enterprise Edition instance, complete the following tasks:
- [Create an Enterprise Edition instance](https://intl.cloud.tencent.com/document/product/1051/35486).
- If you are using a sub-account, grant the sub-account operation permissions for the corresponding instance in advance. For more information, see Examples of Enterprise Edition Authorization Schemes.

## Procedure
### Creating a synchronization rule
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Instance Synchronization** in the left sidebar.
On the "Instance Synchronization" page, you can view the list of synchronization rules for the current instance. To change the instance, select the desired instance name from the "Instance Name" drop-down list at the top of the page.
2. Click **Create**. In the "Create Instance Synchronization Rule" window, configure the rule based on the following information. See the figure below.

 - **Name**: name of the instance synchronization rule. It can contain lowercase letters, numbers, hyphens (-), periods (.), and underscores (_), and must start with a letter or number.
 - **Description**: rule description.
 - **Source Address**
   - **Source Instance**: the current instance is the source instance. You can return to the "Instance Synchronization" page to change the source instance.
   - **Namespace**: namespace with which the current instance needs to synchronize. Currently, you cannot select all namespaces.
   - **Repository**: synchronized repository. You can use a regular expression to filter repositories. If this parameter is not specified, all repositories in the namespace are selected by default.
   - **Tag**: synchronized tag. You can use a regular expression to filter tags. If this parameter is not specified, all tags in the repositories that meet the requirements are selected by default.
   - **Repository Type**: synchronized resource type. You can synchronize container images and Helm charts simultaneously, or only one of them.
 - **Target Address**
   - **Target Instance**: target instance for data synchronization. You can select any instance on the platform, including instances in other regions and source instances.
   - **Namespace**: namespace where the repository is located after this repository is synchronized to the target instance. If this parameter is not specified, it is set to the namespace with the same name as that in the source instance by default. If such a namespace does not exist, a namespace is created.
 - **Overwrite the image with the same name**: this indicates whether the container image with the same name in the target instance is overwritten. We recommend that you do not overwrite images with the same name.
3. Click **OK** to create the synchronization rule.

### Managing synchronization rules
After a synchronization rule is created, you can view the synchronization rule on the "Instance Synchronization" page. Then, you can perform the following operations to manage synchronization rules. See the figure below.

- **Viewing synchronization logs**: you can click a rule name to view the triggering logs of the rule.
- **Modifying the rule status**: a new instance synchronization rule is enabled by default. You can click the toggle button to enable or disable the rule.
- **Triggering synchronization**: you can click "Sync" in the "Operation" column to manually trigger synchronization. Then, all repositories in the instance that match the rule are scanned and synchronized.
- **Configuring a rule**: you can click "Configuration" in the "Operation" column to re-configure all parameters of the instance synchronization rule.
- **Deleting a rule**: you can click "Delete" in the "Operation" column to delete the instance synchronization rule.

### Viewing synchronization logs
Click the name of an instance synchronization rule to go to the "Triggering Logs" page of this rule, as shown in the figure below.

- **Task ID**: synchronization task ID, which is unique in the instance.
- **Create Time**: time that the synchronization task is created.
- **Time Spent**: time consumed to complete all the synchronization tasks.
- **Success Rate**: resource synchronization completion ratio. Multiple repositories may be synchronized concurrently in the same synchronization task.
- **Number of synced repositories**: number of repositories that need to be synchronized in the current task.
- **Synchronization Status**: task status. If the number of container images and Helm charts that need to be synchronized in a task is large, the task may remain in the synchronizing state for a long time.
