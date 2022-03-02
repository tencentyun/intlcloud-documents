This document describes tasks in Scrum agile management.

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click **Use Now** to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the project.
3. In the menu on the left, click **Project Collaboration**. 

## Function Overview

Facilitating team collaboration, tasks refer to specific activities carried out to achieve a certain goal. Generally, a task can be completed in one iteration. In an iteration, any number of tasks may be completed.

Go to **Project Collaboration** > **Tasks** and create a task. Then, you can set its assignee, iteration, story points, and priority. One task can be associated with other issues, or broken down into several sub-issues for flexible task assignment. In addition, you can start a discussion at any time and place with the assignee of the task in Comments, and track all task history with the task details.

## Create Tasks[](#create)

1. Open a project and select **Project Collaboration** > **Tasks**. Click **Create Task** in the upper-right corner of the module and enter a task title, task description, and other basic information to create the task.
![](https://qcloudimg.tencent-cloud.cn/raw/4eccb97de8c902e4f8ce92d42243f76c.png)
1. After creating a task, you can set the assignee and iteration, [set the story points](https://intl.cloud.tencent.com/document/product/1133/44761), adjust the priority, and set the due date on the task details page.
![](https://qcloudimg.tencent-cloud.cn/raw/9e66efc9d31b08a98d12f9f02f0ea588.png)

## Break Down Tasks[](#decompose)

Agile development is a mode of development that focuses on quick iterations and delivery. As the workload during the duration of an iteration should be small, you can break down tasks into smaller sub-issues to improve development efficiency, thereby ensuring on-time delivery as expected.

1. On the task details page, click **Add Sub-Issue**.
![](https://qcloudimg.tencent-cloud.cn/raw/ae93d6d097e71762b2a27e4a7209c072.png)
1. You can simply enter a title to quick create a sub-issue.

3. You can also select **Create** and click **Full Create** in the dropdown menu (keyboard shortcut: Shift + Enter) and enter details before creating a sub-issue.
![](https://qcloudimg.tencent-cloud.cn/raw/7b67b9c2d29c465a019beba55732cd5c.png)
1. After you have created the sub-issue, you can view it on the task details page.
![](https://qcloudimg.tencent-cloud.cn/raw/346c888c01196d9e67c906430f72feba.png)
3. You can also view the sub-issue in the **task** list.
![](https://qcloudimg.tencent-cloud.cn/raw/a5435c7c917d5dc013c1d783ca7dafd8.png)
1. On the task details page, you can select **`···`** to the right of a sub-issue and change the associated parent issue or delete the current sub-issue.


## Reference Resources[](#references)

In the Description or Comments on the task details page, you can use `# + reference ID/title` to select a resource. The resource referenced will be shown in the References list. If the current task has been referenced by another resource, the resource will be shown in the Referenced By list of the task.
![](https://qcloudimg.tencent-cloud.cn/raw/0f18fa152fe53e683ce1390d42f0bebf.png)
You can also associate a **code commit** with an issue. When committing code, add the `# + reference ID/title` of the issue to the commit information (for example, this is a commit #3). For more information, see [Reference Resources and Upload Attachments](https://intl.cloud.tencent.com/document/product/1133/44770).


## Task Status Transition[](#status)

The status of a task is the stage in the task's lifecycle and is used to organize and track the task.

1. After creating a task, go to the task details page. The task status is **Not started** by default. Select options from the dropdown menu on the right to switch its status.
![](https://qcloudimg.tencent-cloud.cn/raw/dbee70ac0699de8ddfcae241d2e4c5f7.png)
1. On the task list page, you can switch the status based on the current stage of the task in the **Status** column.
![](https://qcloudimg.tencent-cloud.cn/raw/4a3678f12e7b9583a9c2f05cfb337666.png)
1. Click **Project Settings** > **Project Collaboration** > **Issue Types** to set custom task workflows. For more information, see [Custom Workflows](https://intl.cloud.tencent.com/document/product/1133/44768).

## Task View[](#view)

On the task list page, you can switch between **Tree View**, **Tile View**, and **Kanban View** to suit your needs. The next time you go to this page, the system will display the last used view by default.

When there are many tasks, flexibly use the search box and filters to quickly locate the information you need. For more information, see [Manage Issue Views](https://intl.cloud.tencent.com/document/product/1133/44773).
![](https://qcloudimg.tencent-cloud.cn/raw/1051120a5cb716188b686f13e9c2329d.png)

## Version Backtracking[](#backdate)

All changes to a task are recorded in the action log. On the details page, select **`···`** in the upper-right corner and click **Earlier Versions** in the menu to view all versions by time. Version backtracking allows you to restore an earlier version. For more information, see [Version Management](https://intl.cloud.tencent.com/document/product/1133/44771).
![](https://qcloudimg.tencent-cloud.cn/raw/3a60cc22ed9ce0d61bae256f158c00ce.png)

## Import or Export Tasks[](#import)

You can batch import and export tasks. On the task list page, select **`···`** in the upper-right corner and import or export tasks. For more information, see [Import and Export Issues](https://intl.cloud.tencent.com/document/product/1133/44765).
![](https://qcloudimg.tencent-cloud.cn/raw/4a95bdecf48ed66fea78c907567cfd2b.png)

## Delete Tasks[](#delete)

On the task details page, you can select **`···`** in the upper-right corner and click **Delete** in the menu. Deleting a task will delete all its sub-issues as well. Proceed with caution.
![](https://qcloudimg.tencent-cloud.cn/raw/433fc2bc8a8e8356700fa8b1e3a3fd96.png)
