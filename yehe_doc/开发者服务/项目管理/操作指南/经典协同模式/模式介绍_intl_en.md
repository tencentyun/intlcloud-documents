This document describes the classic project management mode in CODING Project Collaboration.

## Open Project

1. Log in to the CODING Console and click **Use Now** to go to CODING page.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. In the menu on the left, click **Project Collaboration**.

## Feature Overview

Classic project management is a concept relative to Scrum agile project management. It is mainly suited to teams using traditional project management approaches. Traditional project management is based on plans and centered on requirements, resources, and time. Personnel assignments and scheduling take place after requirements are established. In the course of a project, risks are actively tracked and controlled.

Coding **Classic Project Management** aims to address challenges in traditional project management:

**Centralized collaboration**: Information on different stages and functions is gathered on a single platform.
**Global view**: Project progress is summarized in Plans so you can stay on top of multiple iterations.
**Project progress**: Track progress in Plans and Iterations for transparent processes and control over progress.
**Resource management**: View the tasks of members at any time in Plans, and assign and coordinate personnel.
**Quality control**: Track test and bug resolution progress with test and bug management.

![](https://qcloudimg.tencent-cloud.cn/raw/db202780d6325804c2dbc0b8271e10eb.png)

The following example uses a virtual mall, Feiniao Market, to describe how a team can collaborate using classic project management.

### Enable classic project management mode[](#start)

When starting Project Collaboration for the first time, select **Classic Project Management**.
![](https://qcloudimg.tencent-cloud.cn/raw/4ce14c1b568e9140e4c27cf0d7715f7f.jpeg)

### Create requirement[](#create)

To gain a foothold in the competitive red ocean of e-commerce, research on potential user groups is essential. Usually, product managers create requirement documentation for products according to pain points in the market or user feedback. You can create a requirement on the **Requirement** page, and upload attachments or reference external resources (MockingBot Prototype) to easily incorporate ideas at any time. The menu on the right of the requirement details page allows you to adjust the priority, type, and due date of a requirement. You can also specify the estimated time and project progress as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/9db3e2c62316527a0c6914261e83952e.png)

### Coordinate development plan[](#coordinate)

After the requirement research is completed, a requirement pool review meeting is held. After the requirements gathered are discussed and reviewed, the project leader approves the development plan. An **iteration** can serve as the unit of the development plan.
![](https://qcloudimg.tencent-cloud.cn/raw/25e49b3ec650ba29e33d137ba34e1842.png)

Using this feature, you can split larger plans (including but not limited to development plans) into specific issues (such as requirements and tasks) assigned to specific assignees. All requirements created by the product manager in the early phase can also be seamlessly integrated into the iteration plan.
![](https://qcloudimg.tencent-cloud.cn/raw/fc1e72752621604f76037e375d187c75.png)

Requirements can be broken down into sub-requirements or sub-tasks and associated with bugs and test cases. You can configure other resources required to implement a requirement as a pre-issue, check if a requirement is blocked by another issue, reference other requirements or tasks as resources of this issue, or check which resources have referenced this issue.
![](https://qcloudimg.tencent-cloud.cn/raw/8b6cfa6052f601540b9291d10d9fa442.png)

### Assign development task[](#allocate)
![](https://qcloudimg.tencent-cloud.cn/raw/262a26c0d7e68a094e1fece88dcff845.png)

In an iteration plan, team members can collaborate by creating issues or accepting issues assigned by others. For example, you can break down a requirement to launch a **customer service entry** into development and test tasks. After the development has been completed, you can continue breaking down the requirement into a promotion task and hand it over to the operations department for marketing campaigns.
![](https://qcloudimg.tencent-cloud.cn/raw/ac512ef190952d5d80cff65440d99ef3.png)

### Execute plan[](#execution)

After the various plans have been created and assigned to the specific assignees, in **Workspace** > **My Issues** on the team homepage, team members can view the issues to be completed, merge requests initiated by them or merge requests to be inspected, build tasks in continuous integration, and continuous deployment release orders to be confirmed.
![](https://qcloudimg.tencent-cloud.cn/raw/91f0bb56758bd47d112f10271d274ab9.png)

For a development task, you can also directly reference merge request records in code repositories. For details, see [Reference Resources and Upload Attachments](https://intl.cloud.tencent.com/document/product/1133/44770). After associating the items, you can see the code commit record and development status in the development task.
![](https://qcloudimg.tencent-cloud.cn/raw/5867eb177e95944e3053c5d312d5fb82.png)

In the menu on the right of the issue details page, you can log time by entering the estimated time and time spent on issues. A complete worklog will be automatically created for retrospectives and efficiency analysis after iterations have been completed.
![](https://qcloudimg.tencent-cloud.cn/raw/64cadcfc3d927cfb3c633fbed494093b.png)

Before leaving work, members can change the status of the daily task to **completed** and update the development progress. The iteration progress will update as each issue progresses.
![](https://qcloudimg.tencent-cloud.cn/raw/3985e0590da44d207a274f611aa0c9e2.png)

### Test stage[](#test)

The test phase is crucial to the closed development loop. Self-testing by developers usually resolves most common problems, but it is not enough. Testing helps to identify fundamental logic problems and possible missing items during the development process. CODING's built-in automated testing tools, such as Code Scan and Artifact Scan, help testers quickly create a bug and associate requirements or tasks in an iteration after a bug is found.
![](https://qcloudimg.tencent-cloud.cn/raw/e92fc22b75d4a369948f124303cfe420.png)

You can also log time and update the progress for a bug. In addition to assigning and entering test tasks in an issue, testers can go to [**Test Management**](https://help.coding.net/docs/test-management/start.html) > **Test Case Management** to write test cases.
![](https://qcloudimg.tencent-cloud.cn/raw/ab767bad626a5d3855db81c8839f47c0.png)

In **Test Management** > **Test Plan**, you can configure the iteration of the test in **Edit**.


### Project launch[](#launched)

After the basic development task has been completed, you can use CODING's continuous integration/deployment services to quickly validate the code.
<dx-alert infotype="explain" title="扩展阅读"><ul style = "margin-bottom: 0px;">
<li><a href = "https://help.coding.net/docs/ci/start.html">Continuous Integration - Getting Started</a></li>
<li><a href = "https://help.coding.net/docs/cd/start.html">Continuous Deployment - Sample Project</a></li></ul>
</dx-alert>
After all iteration plans have been completed, you can go to an iteration to view the status trend and time burndown chart of the iteration in **Overview and Statistics**. Managers can stay on top of their team's progress for the plan.
<img src = "https://qcloudimg.tencent-cloud.cn/raw/ed799f3ac918f09fdd263000ed53f6c9.png" style="width: 100%">


### Custom team workflows[](#customize-workflow)

In addition to the default issue statuses, you can customize the workflow of various issues in the issue **Workflow** in **Project Settings** > **Project Collaboration** > **Issue Types**. See [Customize Workflow](https://intl.cloud.tencent.com/document/product/1133/44768) for details.
