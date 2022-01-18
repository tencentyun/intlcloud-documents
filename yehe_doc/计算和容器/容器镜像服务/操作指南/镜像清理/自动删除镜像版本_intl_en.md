
## Overview
Tencent Container Registry (TCR) supports the hosting and distribution of container images and provides the image building feature to enable image building, push, and hosting to be automatically triggered by code changes. If customers need to quickly iterate their applications, they can adopt an automated pipeline to generate images. Large number of image tags will be generated continuously, and the old image tags will no longer be used. If a single image repository contains too many image tags, the burden of tag management is huge, and the quota of image tags in the repository will be used up. Therefore, TCR provides the image tag retention feature to allow users to create custom rules for tag retention. Such rules can be triggered periodically to automatically delete the image tags that fall outside the retention scope.

Tag retention rules support two types of retention policies: retaining the latest # tags pushed and retaining the tags pushed within # days, and simulated execution is supported.

## Notes

The tag retention feature only allows users to delete the image tags that are no longer in use based on rules.

## Directions
### Creating tag retention rules
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Tag Retention** in the left sidebar.
On the **Tag Retention** page, you can view the list of tag retention rules for the current instance. To change the instance, select the desired instance name from the "Instance Name" drop-down list at the top of the page.
2. Click **Create Rule**. In the **Create Tag Retention Rules** window, configure the rule based on the following information. See the figure below.
![](https://main.qcloudimg.com/raw/71e1bf8489e40d2e7acbf4e1283047f4.png)
 - **Associated Instance**: the current instance selected.
 - **Namespace**: the namespace for which the tag retention rule will take effect. Currently, only one rule can be created for a single namespace.
 - **Retained Tags**: by default, all repositories and tags in the namespace are retained and no filter is applied.
 - **Retention Rule**: you can choose between **Retain the most recently pushed # tags** and **Retain tags pushed within the last # days** and specify the number of tags or days accordingly.
 - **Execution Period**: the cycle for executing the tag retention rule: manual, daily, weekly, or monthly execution.
 - **Rule Switch**: by default, the rule is enabled.
3. Click **Confirm** to create the tag retention rule.


### Managing tag retention rules
After successfully creating tag retention rules, you can view the created tag retention rules on the **Tag Retention** page. You can also perform the following operations to manage the rules. See the figure below:
![](https://main.qcloudimg.com/raw/ec77b9c7254ab79088aad0449339c5d0.png)

- **View the rule execution log**: you can click the name of a rule to view its triggering log. For more information, see [Viewing execution logs](#CheckLog).
- **Configuration**: you can reconfigure a tag retention rule but cannot modify the namespace for which it takes effect.
- **Delete**: you can delete a tag retention rule.





### Viewing execution logs[](id:CheckLog)
1. Click the name of a tag retention rule to view the triggering log for the rule, as shown in the figure below:
![](https://main.qcloudimg.com/raw/938251f5417f9ed7bbabb0646729930b.png)
 - **Task ID**: ID of a tag retention task, unique within the instance.
 - **Creation Time**: time when a tag retention task was created.
 - **Time Spent**: time consumed to complete all the tag retention tasks.
 - **Execution Method**: manual or automatic. You can click **Execute Now** or **Simulate Execution** for manual execution. Automatic execution is based on the cycle specified in the tag retention rule.
 - **Execution Type**: real execution or simulate execution. Simulate execution can be used to confirm whether a rule is effective, but it does not actually clear image tags.
 - **Execution Status**: status of task completion.
2. You can click a task ID to view the task details and click a specific repository to view its execution log.



## References
You can also use the `CreateTagRetentionRule` API to create the tag retention rules.
