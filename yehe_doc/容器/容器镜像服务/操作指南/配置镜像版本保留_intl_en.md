
## Operation Scenario
Tencent Container Registry (TCR) supports the hosting and distribution of container images and provides an image building feature to enable image building, push, and hosting to be automatically triggered by code changes. If users need to quickly iterate their business apps and adopt an automated assembly line to generate images, large numbers of image tags will be generated continuously, rendering most old image tags unnecessary. If a single image repository contains too many image tags, the burden of tag management is huge, and the quota of image tags in the repository will be used up. Therefore, TCR provides the image tag retention feature to allow users to create custom rules for tag retention. Such rules can be triggered periodically to automatically clear image tags that fall outside the retention scope.

Tag retention rules support two types of retention policies: retaining the latest # tags pushed and retaining the tags pushed within # days, and simulated execution is supported.

## Prerequisites

Before creating and managing an image repository for a TCR Enterprise Edition instance, complete the following tasks:
- [Purchasing Instances](https://intl.cloud.tencent.com/document/product/1051/39088).
- If you are using a sub-account, you must have granted the sub-account operation permissions for the corresponding instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).

## Directions
### Creating tag retention rules
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Tag Retention** in the left sidebar.
On the "Tag Retention" page, you can view the list of tag retention rules for the current instance. To change the instance, select the desired instance name from the "Instance Name" drop-down list at the top of the page.
2. Click **Create**. In the "Create Tag Retention Rule" window, configure the rule based on the following information. See the figure below.
![](https://main.qcloudimg.com/raw/3359204eb8ebdb404bae1b6f05ea4bfc.png)
 - **Instance**: the current instance selected.
 - **Namespace**: the namespace for which the tag retention rule takes effect. Currently, only one rule can be created for a single namespace.
 - **Retained Tags**: by default, all repositories and tags in the namespace are retained and no filter is applied.
 - **Retention Policy**: you can choose between retaining the most recent # tags pushed and retaining the tags pushed within # days and specify the number of tags or days accordingly.
 - **Execution Cycle**: the cycle for executing the tag retention rule: manual, daily, weekly, or monthly execution.
 - **Enable Rule**: by default, the rule is enabled.
3. Click **OK** to create the tag retention rule.

### Managing tag retention rules
1. After successfully creating tag retention rules, you can view the created tag retention rules on the "Tag Retention" page. You can also perform the following operations to manage the rules. See the figure below:
![](https://main.qcloudimg.com/raw/ae516d0b13e062520c3203f04c87831c.png)
- **View the rule execution log**: you can click the name of a rule to view its triggering log. For more information, see [Viewing the execution log](#CheckLog).
- **Configure**: you can reconfigure a tag retention rule but cannot modify the namespace for which it takes effect.
- **Delete**: you can delete a tag retention rule.

<span id="CheckLog"></span>
### Checking the execution log
1. Click the name of a tag retention rule to view the triggering log for the rule, as shown in the figure below:
![](https://main.qcloudimg.com/raw/407ec242f14df1eab9a4dd4fc39cd194.png)
 - **Task ID**: ID of a tag retention task, unique within the instance
 - **Creation Time**: time when a tag retention task was created
 - **Time Spent**: time consumed to complete all the tag retention tasks
 - **Execution Mode**: manual or automatic. You can click "Execute Now" or "Simulate Execution" for manual execution. Automatic execution is based on the cycle specified in the tag retention rule.
 - **Execution Type**: real execution or simulated execution. Simulated execution can be used to confirm whether a rule is effective, but it does not actually clear image tags.
 - **Execution status**: status of task completion
2. You can click a task ID to view the task details and click a specific repository to view its execution log.
