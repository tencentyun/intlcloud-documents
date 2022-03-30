This document describes requirements in Scrum agile management.

## Open Project

1. Log in to the CODING Console and click **Use Now** to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the project.
3. In the menu on the left, click **Project Collaboration**. 

## Function Overview

CODING Project Collaboration provides two issue types: **user stories**and **requirements**. You can quickly break down and assign development tasks. You can create requirements and break down larger ones into smaller sub-requirements. Also, tasks and bugs can be created for or associated with requirements.

The user story is the smallest unit of work in the agile framework. It describes the value brought by software to users and is an important measure for agile requirements. Therefore, **User story** is enabled by default. To enable **requirements**, go to **Project Settings** > **Project Collaboration** > **Issue Types** and click **Add Issue Type** in the upper-right corner. Then, select **Requirement** and click **Add**.

![](https://qcloudimg.tencent-cloud.cn/raw/af4f816a6f2082a4fcfc8600e3e95605.png)

In the following section, we will use a **user story** as an example to demonstrate how to manage requirements.

## Create Requirement[](#create)

1. Open a project and select **Project Collaboration** > **Requirements**. Click **Create User Story** in the upper-right corner of the module and enter a user story title, user story description, and other basic information to create the user story. A good user story includes the following three elements:
 - Role: Who will use this feature?
 - Activity: What feature needs to be fulfilled?
 - Business value: Why is this feature needed? What kind of value will it bring?
![](https://qcloudimg.tencent-cloud.cn/raw/b9064a55c8ec9df8c5a6cbc3c24871c7.png)
2. After creating a user story, you can set the assignee and iteration, [set the story points](https://intl.cloud.tencent.com/document/product/1133/44761), adjust the priority, and set the due date.
![](https://qcloudimg.tencent-cloud.cn/raw/eb91b60d25d57d2003da85e74fb733b0.png)

## Break Down Requirement[](#decompose)

Sub-issues are specific activities carried out to fulfill **requirements** (user story or requirement). You can break down and assign requirements by creating sub-issues under them.

1. On the user story details page, click **Add Sub-Issue**.
![](https://qcloudimg.tencent-cloud.cn/raw/026c94d8622739b5d681cede0dcd76fd.png)
2. Simply enter a title and press Enter to quick create a sub-issue.

You can also select **Create** and click **Full Create** in the dropdown menu (keyboard shortcut: Shift + Enter) and enter details before creating a sub-issue.
![](https://qcloudimg.tencent-cloud.cn/raw/0bc2f825badebe08d9a604be475193ae.png)
3. After you have created the sub-issue, you can view it on the user story details page. You can also view the sub-issue in the **requirement** list.
![](https://qcloudimg.tencent-cloud.cn/raw/5db197420f4e5d2cb6d65b363484fd2f.png)
4. On the user story details page, you can select ****`···`**** to the right of a sub-issue and click **Change Parent Issue** or **Delete** in the menu.
![](https://qcloudimg.tencent-cloud.cn/raw/429b01afafd1be11d98c0f2336eef9d3.png)

## Associate Resource[](#resource)

### Associate bug[](#bugs)

A **requirement** can be associated with multiple bugs in a project, but a bug can only be associated with one ** requirement**. For more information, see [Manage Bugs](https://intl.cloud.tencent.com/document/product/1133/44760).

1. On the user story list page, select **Associate Bug** and click Associate to Existing Bug or quick create a new bug and associate it.
![](https://qcloudimg.tencent-cloud.cn/raw/f48b333c433354bf174a26a8d53eec45.png)
2. You can select ****`···`**** to the right of an associated bug and click **Disassociate** in the menu.
![](https://qcloudimg.tencent-cloud.cn/raw/dfe505fde8de7272057abad9b2dd7e57.png)
Go to the bug details page, and you can view requirements that are currently associated and disassociate or switch between them in the menu on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/ca578d17dd567b61876c467e54f9c567.png)

### Associate with test case[](#cases)

A **requirement** can be associated with existing test cases. On the user story details page, select **** `···`**** at the top and click **Associate to Test Case** in the menu. Search for a test case by its ID or title and then associate it. For more information, see [Test Cases](https://help.coding.net/docs/test-management/cases/create.html).
![](https://qcloudimg.tencent-cloud.cn/raw/bec1aebdf0b93c69c523596e5ccde458.png)

### Reference resources[](#references)

In the Description or Comments on the user story details page, you can use `# + reference ID/title` to select a resource. The resource referenced will be shown in the References list. If the current requirement has been referenced by another resource, the resource will be shown in the Referenced By list of the requirement.

You can also associate a **code commit** with an issue. When committing code, add the `# + reference ID/title` of the issue to the commit information (for example, this is a commit #3). For more information, see [Reference Resources and Upload Attachments](https://intl.cloud.tencent.com/document/product/1133/44770).


## Requirement Status Transition[](#status)

The status of a requirement is the stage in the requirement's lifecycle and is used to organize and track the requirement.

1. After creating a user story, go to the user story details page. The user story status is **Not started** by default. Select options from the dropdown menu on the right to switch its status.
![](https://qcloudimg.tencent-cloud.cn/raw/2020d90ae2f80eaa2f6da29adac21908.png)
2. On the requirement list page, you can switch the status based on the current stage of the user story in the **Status** column.
![](https://qcloudimg.tencent-cloud.cn/raw/547e364a8e9ad69ef19e224df542dc99.png)
3. Click **Project Settings** > **Project Collaboration** > **Issue Types** to set custom user story and requirement workflows. For more information, see [Custom Workflows](https://intl.cloud.tencent.com/document/product/1133/44768).
![](https://qcloudimg.tencent-cloud.cn/raw/7b84c904ad8384fc24b18de7d7cdb7c2.png)

## Requirement View[](#view)

The requirement list is the major workspace for relevant product personnel. You can switch between **Tree View*, **Tile View**, and **Kanban View** to suit your needs. This helps you create a global view of all requirements and their progress in the current project. The next time you go to this page, the system will display the last used view by default.

When there are many requirements, flexibly use the search box and filters to quickly locate the information you need. For more information, see [Manage Issue Views](https://intl.cloud.tencent.com/document/product/1133/44773).
![](https://qcloudimg.tencent-cloud.cn/raw/6c82b27cf6ac701a6caf37ae939ff017.png)

## Version Backtracking[](#backdate)

All changes to a requirement are recorded in the action log. On the details page, select ****`···`**** in the upper-right corner and click **Earlier Versions** in the menu to view all versions by time. Version backtracking allows you to restore an earlier version. For more information, see [Version Management](https://intl.cloud.tencent.com/document/product/1133/44771).
![](https://qcloudimg.tencent-cloud.cn/raw/345295d33524129e1fc3479627e867e0.png)

## Import or Export Requirements[](#import)

You can batch import and export requirements. On the requirement list page, select ****`···`**** in the upper-right corner and import or export user stories and requirements. For more information, see [Import and Export Issues](https://intl.cloud.tencent.com/document/product/1133/44765).
![](https://qcloudimg.tencent-cloud.cn/raw/865d445e5a951267907ba811a49d9f09.png)

## Delete Requirement[](#delete)

On the user story details page, you can select ****`···`**** in the upper-right corner and click **Delete** in the menu. This will not change the status of associated bugs, but all sub-issues of the user story, if any, will be deleted. Proceed with caution.
![](https://qcloudimg.tencent-cloud.cn/raw/57040954f1245c3acbe8d155f4e9644d.png)

If you simply need to delete a sub-issue, on the user story details page or details page of the sub-issue, select ****`···`**** and click **Delete** in the menu.
