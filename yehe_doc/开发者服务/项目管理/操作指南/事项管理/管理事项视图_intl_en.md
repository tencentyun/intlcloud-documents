This document describes how to use Manage Issue Views in CODING Project Collaboration.

## Open Project

1. Log in to the CODING Console and click **Use Now** to go to CODING page.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the project.
3. Click **Project Collaboration** in the menu on the left.

## Feature Overview[](intro)

You can switch between **Tree View**, **Tile View**, and **Kanban View** on the issue (requirement, task, and bug) list page and in iteration issues to suit your needs. The next time you go to this page, the system will display the last used view by default.
![](https://qcloudimg.tencent-cloud.cn/raw/41092f7e0cffa039d2ea29f261a4bcfb.png)

## Kanban View[](kanban)

### Issue Kanban view[](issue)

In the upper-right corner of the issue list page, you can switch the display mode to Kanban View. Issues will be placed as cards in various Kanban columns, providing an overall view of the project progress and workload at different stages.
![](https://qcloudimg.tencent-cloud.cn/raw/9b852c3f6788fc32a746f9e72b028565.png)

>!Kanban View is unavailable for **All Issues**.
>

In any Kanban columns, you can click the edit icon in the upper-right corner of a card to **follow/unfollow** issues, **copy** issue links or "**open issues in new window**".
![](https://qcloudimg.tencent-cloud.cn/raw/1437308c02623842c921bdbc02a0c114.png)

### Kanban view for iterations[](id:statistics)

On the iteration list page, you can see 4 tabs, that is, **All**, **Requirements**, **Tasks**, and **Bugs**. In the default grouping mode, all statuses of requirements, tasks, and bugs are displayed in three Kanban columns in the **All** tab. You can also [Customize Kanban](#custom) settings.
![](https://qcloudimg.tencent-cloud.cn/raw/faf57763a6a62fea37313c6a4b19176f.png)

If you switch to the Kanban mode **Group by Sub-issue**, sub-tasks of the issues and their parent issues that belong to the current iteration will be displayed.


In this grouping mode, the search conditions only apply to sub-tasks. Available search conditions are as follows:
-   Parent issue type: all, requirements, tasks, and bugs.
-   Sub-task title keywords.
-   Assignee and follower.

![](https://qcloudimg.tencent-cloud.cn/raw/a7230099f7397d15b470efd62a9bb8ff.png)

### Change issue status and column[](id:edit) 

By default, a Kanban view includes three columns: **Not Started**, **In Progress**, and **Completed**. You can drag the cards to change the statuses of issues and the column they belong to. In the Kanban view, you can move a card to different columns, and drag it in a column to change the status.
![](https://qcloudimg.tencent-cloud.cn/raw/03830a04c541696b66d0246b5b566db1.png)

>?The drag operation in the Kanban view requires the permissions to:
> 1. Edit issues;
> 2. Execute the transition of issue statuses;
> 
> For more information about permission configuration, see [Custom User Groups](https://help.coding.net/docs/project-settings/members.html#user-group-customized).

### Customize Kanban[](id:custom)

For each project, you can customize the Kanban view for requirements, tasks, and bugs respectively. In the **Kanban View Settings** in the upper-right corner of the issue list page, you can create, sort, rename, and delete Kanban columns, and drag the issue status to different Kanban columns.
>!Members who have permission to configure **Fields and Processes** can set the Kanban view.

![](https://qcloudimg.tencent-cloud.cn/raw/38ff2ac9a2c40ddd53cd7bca3a731847.png)

1. In the **Kanban View Settings**, select **New Column**, and then enter a name for the new Kanban column.
![](https://qcloudimg.tencent-cloud.cn/raw/9536191f50a7b7bb70ecc360557fd1ca.png)
>!The issue status in a Kanban column cannot be empty. Otherwise, the column will be hidden in the Kanban view. If the desired status is not available, add one to the issue in Project Settings. For more information about how to configure the issue status, see [Custom Workflows](https://intl.cloud.tencent.com/document/product/1133/44768).
> ![](https://qcloudimg.tencent-cloud.cn/raw/0addde3761a77c7b1ca6a21928908a7d.png)
> 
2.  Drag the issue status to the new Kanban column. Kanban columns can also be sorted by dragging.
![](https://qcloudimg.tencent-cloud.cn/raw/0f90025f0cc92aa3b1fc1ff29bb96ecc.png)
![](https://qcloudimg.tencent-cloud.cn/raw/2353ca6dd8a6b389d956f6bc058dac3c.png)
3.  If you want to hide an issue status in a Kanban column, drag this issue status to the bottom.
![](https://qcloudimg.tencent-cloud.cn/raw/a632e523811dbb0264d447529ae01c65.png)
4.  Click **Edit** in the upper-right corner to rename and delete a Kanban column. After you complete all the operations, you can select **Restore Change** to restore the configuration before changes or "Save" to complete the creation. The new Kanban column is displayed in the Kanban view.
![](https://qcloudimg.tencent-cloud.cn/raw/6de17b0d30cfce5774a8e4364a9d6f0a.png)

## Tree View[](id:tree-view)

The tree view displays matching results of this issue in a tree-like structure. The root node is at the top level in the Requirements tree of the current issue.

>!
1.  In the Scrum agile project management mode, the tree view is unavailable to **All Issues**.
2.  In the classic project management mode, the tree view is unavailable to **Tasks** and **Bugs**.

![](https://qcloudimg.tencent-cloud.cn/raw/0454de2b256e578ad73f5a5e00660084.png)
## Tile View[](id:tile-view)

The tile view ignores the hierarchy levels of issues and displays all the issues (including sub-tasks and sub-requirements) matching the search criteria as a list. You can select whether to display sub-issues in the tile view.
![](https://qcloudimg.tencent-cloud.cn/raw/08956d22744f1fbfbd51fd7ec1ed1158.png)

## Custom Issue Header[](id:header)

In the **tree view** and **tile view**, you can click the settings icon in the upper-right corner of the issue list to customize the issue list page.
![](https://qcloudimg.tencent-cloud.cn/raw/34c4bfc0b40c1788c09cd0df9c4240d8.png)

On the configuration page, you can change the display density of fields, show or hide the header fields, and drag fields to adjust display priority as needed. If you select **Restore Default**, the header is reset to the default configuration.
![](https://qcloudimg.tencent-cloud.cn/raw/37d11187348941df391d6011fb1e21f5.png)

On the issue details page, you can drag the borders to adjust the display width of fields. (Each column has a minimum and maximum width.) Changes are saved by default. Any changes you make to the settings apply to your view only, and will not affect other team members' views.
![](https://qcloudimg.tencent-cloud.cn/raw/5619f6a23d68200ca5106f75982880a9.png)
