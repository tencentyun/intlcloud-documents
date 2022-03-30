This document describes tasks in classic project management.


## Open Project

1. Log in to the CODING Console and click **Use Now** to go to CODING page.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. In the menu on the left, click **Project Collaboration**.


Tasks are a common medium of team collaboration. You can create different projects according to your work scenarios and plan work in projects using tasks. After you have created a task in **Project Collaboration** > **Tasks**, you can adjust the priority, set the due date and estimated time, and track the progress. You can also start a discussion at any time and place with other participants in the task in Comments, and track all task history with the task details.


## Create Task[](#create)

1. Open any project and select **Project Collaboration** > **Tasks**. Click **Create Task** in the upper-right corner of the module and enter a task title, task description, and other basic information to create the task.
![](https://qcloudimg.tencent-cloud.cn/raw/fc52b3ecc75c195f012a7eb9034dde88.png)
2. After you have created the task, you can perform detailed operations such as setting the assignee, associating a parent requirement, planning the parent iteration, adjusting the priority, setting the start date, estimating or logging time, and adding tags.


## Associate Block Dependency[](#blocking)

In a task, you can configure an existing issue as a pre-issue or post-issue with a block relationship. On the Task Details page, select **Block Relationship** at the top, search for an issue by its ID or title, and then associate it. You can switch between **pre-issues and post-issues**. For more information, see [Block Dependency](https://intl.cloud.tencent.com/document/product/1133/44750).
![](https://qcloudimg.tencent-cloud.cn/raw/e450e3833da75f5aa67811bfacf23ee2.jpeg)

## Reference Resources[](#references)

In the Description or Comments on the Task Details page, you can use `# + reference ID/title` to select a resource. The resource referenced will be shown in the References list. If the current task has been referenced by another resource, the resource will be shown in the Referenced By list of the task.
![](https://qcloudimg.tencent-cloud.cn/raw/df9c372b26be25fa3bcdb31fefa2af7e.jpeg)
You can also associate a **code commit** with an issue. When committing code, add the `# + ID/title to reference` of the issue to the commit information (for example, this is a commit #3). See [Reference Resources and Upload Attachments](https://intl.cloud.tencent.com/document/product/1133/44770) for details.


## Transition Task Status[](#status)

The status of a task is the stage in the task's lifecycle and is used to organize and track the task. Task statuses include the following three by default: "Not started", "In progress", and "Completed".


1. After **creating a task** on the task list page, go to the task details page. The task status is **Not started** by default. Select options from the dropdown menu on the right to switch its status.
![](https://qcloudimg.tencent-cloud.cn/raw/62ffa95db8050c6b515d923391fe9d4c.png)
2. On the task list page, you can switch the status to the current stage of the task in the **Status** column.
![](https://qcloudimg.tencent-cloud.cn/raw/bde1610678c20e60170a8ea680725637.png)
3. Click **Project Settings** > **Project Collaboration** > **Issue Types** > **Tasks**, and then select **Workflows** to set custom task workflows. For more information, see [Custom Workflows](https://intl.cloud.tencent.com/document/product/1133/44768).


## Task View[](#view)

On the task list page, you can switch between **Tile View** and **Kanban View** in the upper-right corner to suit your needs. When you return to this page, the system will show the last view used by default. You can quickly view the content you need amid the sea of information by using the search bar or filters. See [Manage Issue Views](https://intl.cloud.tencent.com/document/product/1133/44773) for details on managing issue views.
![](https://qcloudimg.tencent-cloud.cn/raw/0c9e851b08948169881d3614e73907a1.jpeg)

## Version Backtracking[](#backdate)

Changes and modifications to a task are recorded in the action log. View all earlier versions by time through **View the version**. Version backtracking allows you to restore an earlier version. For more information, see [Version Management](https://intl.cloud.tencent.com/document/product/1133/44771).
![](https://qcloudimg.tencent-cloud.cn/raw/168263161111eef0094914c829733c21.png)

## Delete Task[](#delete)

On the task details page, select **`···`** in the upper-right corner and click **Delete** to delete the task.
![](https://qcloudimg.tencent-cloud.cn/raw/dc06fbd0f32bb61e5042d5a82a0b7b76.jpeg)
