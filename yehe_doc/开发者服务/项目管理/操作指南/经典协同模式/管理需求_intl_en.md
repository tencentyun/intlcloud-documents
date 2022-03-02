This document describes requirements in classic project management.

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click **Use Now** to go to CODING page.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. In the menu on the left, click **Project Collaboration**.

A requirement refers to a software feature that users need in order to solve a certain problem or achieve a certain goal. In the **Requirements** module in CODING Classic Project Management, teams can quickly break down and assign development tasks. You can create requirements and break down larger ones into smaller sub-requirements. Also, tasks and bugs can be created for or associated with requirements.

## Create Requirement[](#create)

1. Open any project and select **Project Collaboration** > **Requirements**. Click **Create Requirement** in the upper-right corner of the module and enter a requirement title, requirement description, and other basic information to create the requirement.
![](https://qcloudimg.tencent-cloud.cn/raw/37d35d77d24623c1dcd580a25768c81b.png)
2. After you have created the requirement, you can set the assignee, plan the parent iteration, adjust the priority, and set the start date. Teams can customize the fields and dimensions of requirements to suit their management needs. See [Custom Issue Fields](https://intl.cloud.tencent.com/document/product/1133/447671) for configuration details.
![](https://qcloudimg.tencent-cloud.cn/raw/15cbb620735f11cb21fd104f6674804c.png)

## Break Down Requirement[](#decompose)

Sub-issues (sub-requirements and sub-tasks) are specific activities for achieving requirements. You can break down and assign requirements by creating sub-issues for a requirement.

### Break down sub-requirement[](#sub-requirement)

A requirement can be broken down into sub-requirements, and a sub-requirement can be broken down further. A maximum of 5 levels of sub-requirements are supported. Take note that a requirement can have only one parent requirement at any one time.

1. On the requirement details page, select **Break Down Requirement**.
![](https://qcloudimg.tencent-cloud.cn/raw/30ec16abb81505d53132062a38582bdb.png)
2. You can simply enter a title to quick create a sub-requirement. You can also select **Create** and click **Full Create** in the dropdown menu (keyboard shortcut: Shift + Enter) and enter details before creating a sub-requirement.
![](https://qcloudimg.tencent-cloud.cn/raw/ac8d584e2e37f91af514508d5dfd048b.jpeg)
To associate an existing requirement, do a quick search by issue ID or title.
![](https://qcloudimg.tencent-cloud.cn/raw/28f7055407322085129da278b59723ec.png)
3. After you have created the sub-requirement successfully, you can view it on the details page of the parent requirement. You can also view the sub-requirement in the requirement list.
![](https://qcloudimg.tencent-cloud.cn/raw/8edc5948c5a740f80c2b828cc50cb36a.png)
4. On the requirement details page, select **`···`** to the right of a sub-requirement and click **Create Sub-Requirements** in the menu.
![](https://qcloudimg.tencent-cloud.cn/raw/193b925134dafa101e32b7625e4e097d.png)
Alternatively, on the details page of the sub-requirement, select **Break Down Requirement** at the top to create sub-requirements of the sub-requirement.
![](https://qcloudimg.tencent-cloud.cn/raw/f4c8bd51ebaa380b6ddf7340cab9592c.png)
5. On the requirement details page, you can select **`···`** to the right of a sub-requirement and click **Change Parent Requirement** in the menu.You can also select **Disassociate**.

### Break down sub-task[](#sub-tasks)

A requirement can be broken into sub-tasks. A task can only be associated with one parent requirement at any one time.

1. On the requirement details page, select **Break Down Task**.
![](https://qcloudimg.tencent-cloud.cn/raw/db06d35ef28709b21c062247e7ee6e18.png)
2. You can simply enter a title to quick create a sub-task. You can also select **Create** and click **Full Create** in the dropdown menu (keyboard shortcut: Shift + Enter) and enter details before creating a sub-task. To associate an existing task, do a quick search by issue ID or title.
![](https://qcloudimg.tencent-cloud.cn/raw/ddf61566e193f1149bc6f95f84606489.png)
3. After you have created the sub-task successfully, you can view it on the details page of the parent requirement. You can also view the sub-task in the task list.
![](https://qcloudimg.tencent-cloud.cn/raw/05f105c097bd5f6cae2cb19e7988095c.png)
![](https://qcloudimg.tencent-cloud.cn/raw/68ed0cd14f7c96a080934d7e51c03c1d.png)
4. On the requirement details page, you can select **`···`** to the right of a sub-task and click **Change Parent Requirement** in the menu. You can also select **Disassociate**.


## Associate Resource[](#resource)

### Associate bug[](#bugs)

A requirement can be associated with multiple bugs in a project, but a bug can only be associated with one requirement.

1. On the requirement list page, select **Associate Bug** at the top and click Associate to Existing Bugs or quick create a new bug and associate it.
![](https://qcloudimg.tencent-cloud.cn/raw/663efe34a0cb5bcd981b9d2c13ca4461.png)
2. On the requirement details page, you can select **`···`** to the right of an associated bug and click **Disassociate**. You can also select Disassociate in the menu on the right of the bug details page.
![](https://qcloudimg.tencent-cloud.cn/raw/5f24f2285b544f8e5653356602a4ef7a.png)
You can view requirements that are currently associated and disassociate or switch between them.
![](https://qcloudimg.tencent-cloud.cn/raw/6026ca6ffb9a73d4d6e61c3d6ab47caf.png)
3. On the bug details page, select **`···`** in the upper-right corner and click Convert to Requirement.
![](https://qcloudimg.tencent-cloud.cn/raw/a18e1cdf218fed6698752e0600cf25f2.png)

### Associate with test case[](#cases)

A requirement can be associated with an existing test case. On the requirement details page, select **`···`** at the top and click **Associate to Test Case** in the menu. Search for a test case by its ID or title and then associate it. See [Test Cases](https://help.coding.net/docs/test-management/cases/create.html) for details on creating and managing test cases.
![](https://qcloudimg.tencent-cloud.cn/raw/89a3caf9ab5c34da739bd45f5abf5bc7.png)

### Associate block relationship[](#blocking)

In a requirement, you can configure an existing issue as a pre-issue or post-issue with a block relationship. On the requirement details page, select **`···`** at the top and click **Block Relationship** in the menu. Search for an issue by its ID or title and then associate it. You can switch between **pre-issues and post-issues**. For more information, see [Block Dependency](https://intl.cloud.tencent.com/document/product/1133/44750).
![](https://qcloudimg.tencent-cloud.cn/raw/08b9f74bfa111fa46807b99054376352.png)

### Reference resources[](#references)

In the Description or Comments on the requirement details page, you can use `# + reference ID/title` to select a resource. The resource referenced will be shown in the References list. If the current requirement has been referenced by another resource, the resource will be shown in the Referenced By list of the requirement.
![](https://qcloudimg.tencent-cloud.cn/raw/ffefaa4fb1a94dfcd4e0720907e7d0bd.png)

You can also associate a **code commit** with an issue. When committing code, add the `# + ID/title to reference` of the issue to the commit information (for example, this is a commit #3). See [Reference Resources and Upload Attachments](https://intl.cloud.tencent.com/document/product/1133/44770) for details.


## Transition Requirement Status[](#status)

The status of a requirement is the stage in the requirement's lifecycle and is used to organize and track the requirement. Requirement statuses include the following four by default: "Not started", "Under development", "Under testing", and "Completed".

1. After **creating a requirement** on the requirement list page, go to the requirement details page. The requirement status is **Not started** by default. Select options from the dropdown menu on the right to switch its status.
![](https://qcloudimg.tencent-cloud.cn/raw/9b8342732e5a86a9eacff10bea25c4dc.png)
2. On the requirement list page, you can switch the status to the current stage of the requirement in the **Status** column.
![](https://qcloudimg.tencent-cloud.cn/raw/c420d169cdf3e3e7151258bc70b7f09e.png)
3. Select **Project Settings** > **Project Collaboration** > **Issue Types** > **Requirements**, and then select **Workflows** to set custom requirement workflows. For more information, see [Custom Workflows](https://intl.cloud.tencent.com/document/product/1133/44768).
![](https://qcloudimg.tencent-cloud.cn/raw/cae1423bed3f408d893cbfac1720e474.png)

## Requirement View[](#view)

On the requirement list page, you can switch between **Tree View*, **Tile View**, and **Kanban View** to suit your needs. This is the main working interface for product-related personnel and can help give you an overall idea of all requirements in the current project. When you return to this page, the system will show the last view used by default.

When there are many requirements, you can quickly view the content you need amid the sea of information by using the search bar or filters. For more information, see [Manage Issue Views](https://intl.cloud.tencent.com/document/product/1133/44773).
![](https://qcloudimg.tencent-cloud.cn/raw/84ba59211d8d9f0ce3a6097cd2416bf9.png)

## Version Backtracking[](#backdate)

All changes in a requirement are recorded in the action log. On the details page, select **`···`** in the upper-right corner and click **Earlier Versions** in the menu to view all versions sorted by time. Version backtracking allows you to restore an earlier version. For more information, see [Version Management](https://intl.cloud.tencent.com/document/product/1133/44771).
![](https://qcloudimg.tencent-cloud.cn/raw/e6f5e508b06419a412b22594c5fff570.png)

## Import and Export Requirements[](#import)

You can batch import and export requirements. On the requirement list page, select **`···`** in the upper-right corner and click Import/Export Requirement in the menu. See [Import and Export Issues](https://intl.cloud.tencent.com/document/product/1133/44765) for details.
![](https://qcloudimg.tencent-cloud.cn/raw/d3929d1e93afe61e75bfccb664b4e048.png)

## Delete Requirement[](#delete)

On the requirement details page, you can select **`···`** in the upper-right corner and click **Delete** in the menu. This will not change the status of associated bugs, but all sub-issues (sub-requirements and sub-tasks) of the requirement, if any, will be deleted. Proceed with caution.
![](https://qcloudimg.tencent-cloud.cn/raw/8ddb79041b3322602ddbe3e752506ec1.png)
If you simply need to delete a sub-requirement, sub-task, or bug, on the requirement details page or details page of the sub-requirement, sub-task, or bug, select **`···`** and click **Delete** in the menu.
