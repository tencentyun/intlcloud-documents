This document describes the "Bugs" feature in classic project management.


## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click **Use Now** to go to CODING page.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the project.
3. In the menu on the left, click **Project Collaboration**.

## Feature Overview

In CODING Project Collaboration, the **Bugs** feature allows a team to keep track of bug information and improve the bug transition and processing efficiency, making large-scale bug management much easier for enterprise users.

## Create Bugs[](#create)

1. Open a project and select **Project Collaboration** > **Bugs**. Click **Create Bug** in the upper-right corner of the module and enter a bug title, bug description, and other basic information to create the bug.
![](https://qcloudimg.tencent-cloud.cn/raw/2ced008b1111ffbd1e53927f935ee780.png)
2. After creation, the bug is in a **To be processed** status by default. On the Bug Details page, you can switch the status, set the assignee, associate a parent requirement, plan its iteration, edit the priority, set the start date, estimate or log time, and add tags.
![](https://qcloudimg.tencent-cloud.cn/raw/4a30426a2e4b7c974fb2c5fd9677413d.jpeg)

## Associate Block Dependency[](#blocking)

In a bug, you can configure an existing issue as a pre-issue or post-issue with a block dependency. On the Bug Details page, select **Block Relationship** on the top, search for an issue by its ID or title, and then associate it. You can switch between **pre-issues and post-issues**. For more information, see [Block Dependency](https://intl.cloud.tencent.com/document/product/1133/44750).
![](https://qcloudimg.tencent-cloud.cn/raw/38e95fb7cd4c3263871a8857d06f2fb3.jpeg)

## Reference Resources[](#references)

In the Description or Comments on the Bug Details page, you can use `# + ID/title to reference` to select a resource. The resource referenced will be shown in the References list. If the current bug has been referenced by another resource, the resource will be shown in the Referenced By list of the bug.
![](https://qcloudimg.tencent-cloud.cn/raw/09d7d476bb4267eeafd0c23fdd7026a9.jpeg)

You can also associate a **code commit** with an issue. When committing code, add the `# + ID/title to reference` of the issue to the commit information (for example, this is a commit #3). See [Reference Resources and Upload Attachments](https://intl.cloud.tencent.com/document/product/1133/44770) for details.


## Bug status transition [](#status)

Bug status refers to the stage of a bug in its lifecycle and provides a way to organize and track bugs and implement bug processing workflows. Bug statuses include "To be processed", "In progress", "To be verified", "Rejected", "Reopened" and "Closed".

1. After **creating a bug** on the bug list page, go to the bug details page. The bug status is **To be processed** by default. Select options from the dropdown menu on the right to switch its status.
![](https://qcloudimg.tencent-cloud.cn/raw/c171d366e19dd6f3a77e0a5fce1af6af.jpeg)
2. On the bug list page, you can switch the status based on the current stage of the bug in the **Status** column.
![](https://qcloudimg.tencent-cloud.cn/raw/5bf56200f55ddb3dd99f273c839d065b.png)
3. Click **Project Settings** > **Project Collaboration** > **Issue Types** > **Bugs**, and then select **Workflows** to set custom bug workflows. For more information, see [Custom Workflows](https://intl.cloud.tencent.com/document/product/1133/44768).


## Bug View[](#view)

On the bug list page, you can switch between **Tile View** and **Kanban View** in the upper-right corner to suit your needs. The next time you go to this page, the system will display the last used view by default. You can use the search bar with filters to quickly find the content you want. For more information, see [Manage Issue Views](https://intl.cloud.tencent.com/document/product/1133/44773).
![](https://qcloudimg.tencent-cloud.cn/raw/fdefd232885fc415bf8ca094bfb734c9.png)

## Version Backtracking[](#backdate)

Changes and modifications to a bug are recorded in the action log. **View the version** to view all earlier versions. Version backtracking allows you to restore an earlier version. For more information, see [Version Management](https://intl.cloud.tencent.com/document/product/1133/44771).
![](https://qcloudimg.tencent-cloud.cn/raw/5341a44ac5ca9416cd65ce50f458756f.jpeg)

## Bug Types and Bug Modules[](#type&module)

### Manage bug types[](#type)

When creating and managing a bug, you can set the bug type.
>? CODING Bug Management provides five bug types by default:
- Functional bug
- UI defect
- Usability defect
- Security defect
- Performance defect


Custom bug types are also supported. Only a **team owner** or **admin** can create bug types. After a bug type is added, the bug type can be used for all projects of a team.

#### Create or use bug types[](#type-create)

1. In a project, select **Project Settings** > **Project Collaboration** > **Issue Types** in the menu on the left, and click **Fields** to the right of **Bugs**.
![](https://qcloudimg.tencent-cloud.cn/raw/ca5f4ecacc56884277f67cc62908ec80.jpeg)
2. In **Issue Types** > **Bugs**, select **Configure Menu Options** to the right of **Bug Type**.
![](https://qcloudimg.tencent-cloud.cn/raw/2564d169c5be55908ede95f9d309420b.png)
3. Enter a name for the new bug type. You can adjust the priorities of bugs through the drag-and-drop operation. Select **Add** and then click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/cea65867443d3d5258e16dd1633278ac.jpeg)
Then, in **Issue Types** > **Bugs**, select **Apply Configuration** to add and apply the bug type.
![](https://qcloudimg.tencent-cloud.cn/raw/2564d169c5be55908ede95f9d309420b.png)
4. When creating a bug or on the bug details page, you can select a new bug type in the **Bug Types** menu on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/264e8e580e7f5ed68bb474afd61d9810.png)

### Manage bug modules[](#type&module)

This feature is used to configure modules to which the bugs belong. Creating different modules allows you to manage and locate bugs easily to suit the needs of professional scenarios. Module data can be shared across projects for more efficient collaboration.

#### Create or use bug modules[](#type-create)

1. In a project, select **Project Settings** > **Project Collaboration** > **Module Settings** in the menu on the left and click **Create Module**.
![](https://qcloudimg.tencent-cloud.cn/raw/68e3cbfd7b91caf525b7837f9a64b886.jpeg)
2. Enter a module name, and then select **Save** to add the bug module.
![](https://qcloudimg.tencent-cloud.cn/raw/2db501d7dbd9a57557226dd6ca8aafbe.jpeg)
In **Module Settings**, click **↑****↓** to the right of each module to adjust the display priority of modules. You can also rename or delete the modules.
![](https://qcloudimg.tencent-cloud.cn/raw/66cbebccefabeeec09630409c58f1e3b.jpeg)
3. When creating a bug or on the bug details page, you can select the module to which the bug will be added from the **Modules** menu on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/afdf44ab4f2380d661846881778f2adc.jpeg)https://qcloudimg.tencent-cloud.cn/raw/4ddb8960be8d0ca1a83e63d2b8572a9d.jpeg

## Delete bugs[](#delete)

On the bug details page, select **`···`** in the upper-right corner and click **Delete** to delete the bug.
![](https://qcloudimg.tencent-cloud.cn/raw/4ddb8960be8d0ca1a83e63d2b8572a9d.jpeg)
