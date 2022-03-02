This document describes bugs in Scrum agile management.

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click **Use Now** to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the project.
3. In the menu on the left, click **Project Collaboration**. 

## Function Overview

A bug is a failure to meet an initially defined business requirement. Bugs include any such defect except coding errors.

On the CODING platform, you can centrally manage bugs. By recording detailed bug information such as the bug type, assignee, iteration, priority, and module, test engineers can learn about the overall bug handling progress, thereby improving bug transitioning and handling efficiency.

## Create Bugs[](#create)

Open a project and select **Project Collaboration** > **Bugs**. Click **Create Bug** in the upper-right corner and enter a bug title, bug description, and other basic information to quickly create the bug.
![](https://qcloudimg.tencent-cloud.cn/raw/a5b2c292e24ab6bef560fae3f22870b8.png)

## Break Down Bugs[](#decompose)

You can create sub-issues under a bug to break down a large bug.

1. On the bug details page, click **Add Sub-Issue**. You can simply enter a title to quick create a sub-issue.
![](https://qcloudimg.tencent-cloud.cn/raw/6f8f000a45bb3b5c5ffcd4a436f72b46.png)
You can also select **Create** and click **Full Create** in the dropdown menu (keyboard shortcut: Shift + Enter) and enter details before creating a sub-issue.
2. After you have created the sub-issue successfully, you can view it on the bug details page.
![](https://qcloudimg.tencent-cloud.cn/raw/41aba3805f781c2f664072d844525681.png)
You can also view the sub-issue in the **bug** list.
![](https://qcloudimg.tencent-cloud.cn/raw/a0b6d90e90a9ea2de5e5cd12749cfa9e.png)
3. On the bug details page, you can select ****`···`**** to the right of a sub-issue and change the associated parent issue or delete the current sub-issue.
![](https://qcloudimg.tencent-cloud.cn/raw/058239938ecc985af79d004736a5e5a2.png)
4. During actual development scenarios, unexpected bugs may arise due to insufficient planning, or complicated bugs may require lots of work for researching and handling. In this case, enter the bug details page, select ****`···`**** in the upper-right corner, and then convert the bug to a new requirement or change its parent epic.
![](https://qcloudimg.tencent-cloud.cn/raw/704b715d575f1875a43b3de67870386e.png)

## Assign Bugs[](#allocate)

After creating a bug and breaking it down into sub-issues, you can enter the details page to set the iteration and associated requirements, [set the story points](https://intl.cloud.tencent.com/document/product/1133/44761), select the bug type, adjust the priority, set the due date, and specify the assignee.
![](https://qcloudimg.tencent-cloud.cn/raw/7fa1af6f4acf7840535d0f6e02b7b5b9.png)

## Reference Resources[](#references)

In the Description or Comments on the bug details page, you can use `# + reference ID/title` to select a resource. The resource referenced will be shown in the References list. If the current bug has been referenced by another resource, the resource will be shown in the Referenced By list of the bug.
![](https://qcloudimg.tencent-cloud.cn/raw/891f5da03daad273f2f41b9e76c8db2f.png)

You can also associate a **code commit** with an issue. When committing code, add the `# + reference ID/title` of the issue to the commit information (for example, this is a commit #3). See [Reference Resources and Upload Attachments](https://intl.cloud.tencent.com/document/product/1133/44770) for details.


## Bug Status Transition[](#status)

Bug status refers to the stage of a bug in its lifecycle and provides a way to implement bug processing workflows.

1. After creating a bug, the bug status is **To be processed** by default. On the bug details page, select options from the dropdown menu on the right to switch its status.
![](https://qcloudimg.tencent-cloud.cn/raw/d8703ae96e3bbb32ff232b0252117a2e.png)
2. On the bug list page, you can switch the status based on the current stage of the bug in the **Status** column.
![](https://qcloudimg.tencent-cloud.cn/raw/4344193160fbfe2c5c470e83ac956564.png)
3. Click **Project Settings** > **Project Collaboration** > **Issue Types** to set custom bug workflows. For more information, see [Custom Workflows](https://intl.cloud.tencent.com/document/product/1133/44768).

## Bug View[](#view)

The bug list is a list view of all bugs in the project. It is the main workspace for testers and relevant bug assignees. On the bug list page, you can switch between ** Tree View**, **Tile View**, and **Kanban View** to suit your needs. The next time you go to this page, the system will display the last used view by default.

When there are many tasks, flexibly use the search box and filters to quickly locate the information you need. For more information, see [Manage Issue Views](https://intl.cloud.tencent.com/document/product/1133/44773).
![](https://qcloudimg.tencent-cloud.cn/raw/48c1d049e74c5a453dc32067837d017a.png)

## Version Backtracking[](#backdate)

All changes to a bug are recorded in the action log. On the details page, select ****`···`**** in the upper-right corner and click **Earlier Versions** in the menu to view all versions by time. Version backtracking allows you to restore an earlier version. For more information, see [Version Management](https://intl.cloud.tencent.com/document/product/1133/44771).
![](https://qcloudimg.tencent-cloud.cn/raw/eb7520155605d2f2147821e3ec6453b7.png)

## Import or Export Bugs[](#import)

You can batch import and export bugs. On the bug list page, select ****`···`**** in the upper-right corner and import or export bugs. For more information, see [Import and Export Issues](https://intl.cloud.tencent.com/document/product/1133/44765).
![](https://qcloudimg.tencent-cloud.cn/raw/3128b42c0be2b9a08729452708e65ede.png)

## Bug Types and Bug Modules[](#type&module)

### Manage bug types[](#type)

When creating and managing a bug, you can set the bug type. CODING Bug Management provides five bug types by default:
- Functional bug
- UI defect
- Usability defect
- Security defect
- Performance defect

![](https://qcloudimg.tencent-cloud.cn/raw/2fd09fe80cae7a3fccafe8d76bc2e681.png)

Custom bug types are also supported. Only a **team owner** or **admin** can create bug types. After a bug type is added, the bug type can be used for all projects of a team.

#### Create and use bug types[](#type-create)

1. In a project, select **Project Settings** > **Project Collaboration** > **Issue Types**, and click **Fields** to the right of **Bugs**.![](https://qcloudimg.tencent-cloud.cn/raw/4099ec40605102f99a747faf6b48ef00.png)
2. In **Issue Types** > **Bugs**, select **Configure Menu Options** to the right of **Bug Types**.
![](https://qcloudimg.tencent-cloud.cn/raw/f07d1eb53583ad0206bc7dcb3dfd5237.png)
3. Enter a name for the new bug type. You can adjust the priorities of bugs through the drag-and-drop operation.
![](https://qcloudimg.tencent-cloud.cn/raw/a207f0ab4625b071fd3f134e071b5a30.png)
Select **Add** and click **OK**, and then in **Issue Types** > **Bugs**, select **Apply Configuration** to add and apply the bug type.
![](https://qcloudimg.tencent-cloud.cn/raw/183c108e96ccd6b9ccd36a611bd4469a.png)
4. When creating a bug or on the bug details page, you can select a new bug type in the **Bug Types** menu on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/d3ca5f0247d9726dd5213517c29e1b5e.png)

### Manage bug modules[](#module)

This feature is used to configure modules to which the bugs belong. Creating different modules allows you to manage and locate bugs easily to suit the needs of professional scenarios. Module data can be shared across projects for more efficient collaboration.

#### Create and use bug modules[](#module-create)

1. In a project, select **Project Settings** > **Project Collaboration** > **Module Settings** and click **Create Module**.
![](https://qcloudimg.tencent-cloud.cn/raw/0dcb364d263a0e3a0020400cb7ad587d.png)
2. Enter a module name, and then select **Save** to add the bug module.
![](https://qcloudimg.tencent-cloud.cn/raw/9c959230643add00b860f4210648d39f.png)
In **Module Settings**, click **↑****↓** to the right of each module to adjust the display priority of modules. You can also rename or delete the modules.
![](https://qcloudimg.tencent-cloud.cn/raw/713e648825101841c95c8c91e5a77a8a.png)
3. When creating a bug or on the bug details page, you can select the module to which the bug will be added from the **Modules** menu on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/e002ad1c173f42d20fdb23c25f207d19.png)

## Delete Bugs[](#delete)

On the bug details page, you can select ****`···`**** in the upper-right corner and click **Delete** in the menu. Deleting a bug will delete all its sub-issues as well. Proceed with caution.
![](https://qcloudimg.tencent-cloud.cn/raw/6960a45ae690bd1dfcc83aceb75bf427.png)
