This document describes how to configure a custom workflow in CODING Project Collaboration.

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click **Use Now** to go to CODING page.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the project.
3. Click **Project Collaboration** in the menu on the left.

## Feature Overview[](#intro)

A custom workflow can meet unique demands of different teams. You can customize the workflow statuses of all issues (including epics, requirements, tasks, bugs, and sub-issues), and specify a fixed transition mode and unified transition rules. This allows your team to deal with different projects in a consistent way, and ensure efficient collaboration across projects and departments.

This document describes how to customize a workflow for your team through ****Global Status Settings**** and ****Project Workflow Configuration****. The steps are as follows:

1. Create global statuses, and then select proper ones for the workflows in the project;
2. When the workflow configuration is complete, you can select a status for each issue (i.e. epic, user story, requirement, task, and bug) in the project.

## Global Status Settings[](#global)

Since all the issue statuses of your team are determined by global status settings, only members who have **management permissions** in the user group can modify or add custom statuses. Go to **Team Management** > **Permission Configuration** > **User Group**, and then view details on the **Permission Configuration** page of the user group.
![](https://qcloudimg.tencent-cloud.cn/raw/e4144cce3fa6d04828b912578a12dd80.png)

If you have management permissions, go to the homepage of your team, and then select **Feature Settings** from the menu on the left. Click **Project Collaboration** > **Issue Status** to go to the status settings page.
![](https://qcloudimg.tencent-cloud.cn/raw/6742f62d322960d60b6eab4d32da00ea.png)
![](https://qcloudimg.tencent-cloud.cn/raw/c260a3fd10d74e5f4c2226bf6203634c.png)

### Create status[](#create)

To create a custom status, click **Create Status** in the upper-right corner, and then enter a name, type, and description (optional) for the new status. Status name must be unique.
![](https://qcloudimg.tencent-cloud.cn/raw/cc79c5d5badcfb648de491a9a4b06680.png)

### Modify or delete status[](#edit)

You can edit or delete any status in **Action**.
![](https://qcloudimg.tencent-cloud.cn/raw/b58cd9a1104ea63b76883b9a87be20bb.png)

## Project Workflow Configuration[](#project)

Workflow configuration allows you to specify an issue's statuses and transition, which indicates the transition of an issue from the initial status to target status. In a project, select **Project Settings** > **Project Collaboration** > **Issue Types** in the menu on the left.
![](https://qcloudimg.tencent-cloud.cn/raw/7157b6b1994d18f3a0febc62719b737d.png)
You can customize the workflow of an issue in**Workflows**.
![](https://qcloudimg.tencent-cloud.cn/raw/3f2de10aa530db3475ce402c43aa932c.png)

For example, when a requirement is in the **under development** status, you can click the transition to go to the custom target status.
![](https://qcloudimg.tencent-cloud.cn/raw/fa2407e6e0b1f61481373437e6bd681f.png)

The following shows how to customize a workflow in Requirements.

### Set status[](#status)

Statuses are divided into two types: initial and target, which indicate the current stage of an issue.

1. Select **Add Status** in **Workflows**.
![](https://qcloudimg.tencent-cloud.cn/raw/c470dc19e3e2c44ce77e4a1211a822b7.png)
2. You can select the status set in **Global Status Settings** from the dropdown menu on the right of **Status**. If **Allow Any Status to this Status** is enabled when you create a status, all statuses in the project can be switched to this target status.
![](https://qcloudimg.tencent-cloud.cn/raw/7b9d65ee35b9efca4b5168640da0ca6d.png)
3. Click **Add** and the new status will be added in the workflow.
![](https://qcloudimg.tencent-cloud.cn/raw/f331d459c01c99680435f64dc9294f48.png)

### Set transition[](#process)

A transition shows the transition process from an initial status to a target status.

1. Select **Create Transition** in **Workflow**.
![](https://qcloudimg.tencent-cloud.cn/raw/c70443119c23dedc82afb261ff5d07e6.png)
2. Specify an **initial status** and a **target status** for this transition. The transition name defaults to the target status, and can be changed. Then, click **Create**.
![](https://qcloudimg.tencent-cloud.cn/raw/1a7650a7d03c602ee500defeb876fea1.png)
3. You can also create a transition directly in **Any Status**. In this case, the **initial status** and **target status** correspond to the statuses respectively in the row and column of the table. You can only change the **transition name**. Then, click **Create**.
![](https://qcloudimg.tencent-cloud.cn/raw/3a25f636488cabc49fcb0c889b82dae6.png)
![](https://qcloudimg.tencent-cloud.cn/raw/28fede754377eed3ed153d6acdc05717.png)
4. Avoid conflicts when you set a transition. As shown in the figure below, since **Any Status** can be switched to the **Not Started** status, the transition from a specific status to the **Not Started** status is overwritten and only the transition from **Any Status** to **Not Started**.
![](https://qcloudimg.tencent-cloud.cn/raw/54605e9d88c784cff6bbdfe343ecec50.png)
5. Select any transition, and then change the transition name and configure rules in the **Transition Settings** on the right, or delete this transition by clicking the **Delete Transition** button below.
![](https://qcloudimg.tencent-cloud.cn/raw/54605e9d88c784cff6bbdfe343ecec50.png)

### Configure rules[](#rules)

The transition rules can be configured separately for each issue type. Click **Configure Rules** in **Workflow** to set transition rules, or select a status, and then click **Transition Settings** > **Rules** > **+** on the right. A total of four types are available: restrict transition permission, add fields, change assignee, and change field values, respectively. You can learn about these types from their descriptions, and configure them as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/1bb5afc7abfcc27bce14dd2f791abe12.png)
![](https://qcloudimg.tencent-cloud.cn/raw/ca1f6026c1763f9c99b436dc887e67fe.png)

#### Restrict transition permission[](#permission)

By default, all team members have access to all transitions. If the transition permission is restricted, only authorized members can execute the transition.
![](https://qcloudimg.tencent-cloud.cn/raw/c840523a01a3d51403c2c2118a0324de.png)

#### Add fields[](#additional-property)

This rule allows the configuration of more than one field as a form. If this rule is configured, a status change occurs only when members set the required field values.
![](https://qcloudimg.tencent-cloud.cn/raw/ec3aaa2642d778ff242b222638e67c11.png)

#### Change assignee[](#processor)

If this rule is configured, the issue assignee will be automatically changed when a status change occurs.
![](https://qcloudimg.tencent-cloud.cn/raw/828a1845a19f70027070324f783c8247.png)

#### Change field values[](#property-value)

If this rule is configured, the configured field values are automatically changed to the specified values when a status change occurs.
![](https://qcloudimg.tencent-cloud.cn/raw/1bb8241ee2a760a12697be97ee68b88a.png)

**Example 1: You need to change the issue priority to **Low** when a transition changes to the **Completed** status.**

Take the following steps: Click **Configure Rules** > **Change Field Values**. Then, select **Any Status** > **Completed** for the Current Transition field, and change the value of the **Priority** field to **Low**.**
![](https://main.qcloudimg.com/raw/c58eec359ac1f923db16916a4ee3f616.png)

**Example 2: You need to auto-update the progress to 100% when an issue transitions to the **Completed** status.**

Take the following steps: Click **Change Field Values**. Then, select **Any Status** > **Completed** for the Current Transition field, and change the value of the **Progress** field to **100**. Note: Both field and task workflow settings require configuration.
![](https://qcloudimg.tencent-cloud.cn/raw/88233a4d6221caacfce5e672cf049da1.png)

### Workflow view[](#view)

Two view options are available on the workflow configuration page, that is, table view and list view.

-   **Table view**: The first column and first row indicate the initial status and target status respectively. Each grid in the table indicates a **transition** prompted when a status change occurs.
![](https://qcloudimg.tencent-cloud.cn/raw/0b1d6f7a595be48109b2b19545bac8cd.png)
-   **List view**: Each status has a table that shows all the transitions and user permissions involved when the status acts as the initial status.
![](https://qcloudimg.tencent-cloud.cn/raw/8404a642126b4f5e94092b7243a07f8d.png)

## Apply Configuration of Another Project[](#applicate)

In Project Collaboration, you can copy fields and workflow configuration of other projects. The first time you enable Project Collaboration, select "Apply Configuration of Another Project".
![](https://qcloudimg.tencent-cloud.cn/raw/82063d7aef7e48ee0c17ea9423f51376.png)
