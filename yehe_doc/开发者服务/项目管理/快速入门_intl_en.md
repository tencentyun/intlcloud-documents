This document describes how to get started with CODING-PM in classic mode.

## Prerequisites
You must activate the CODING DevOps service for your Tencent Cloud account before you can use Coding project management.

## Initialize the Demo Project

1. Go to CODING and click the Project button <img src ="https://main.qcloudimg.com/raw/7531b01c25014beb2754277107fc4ab1.png" style ="margin:0"> on the left, and then click the Create Project button in the upper-right corner of the project list.
2. Select Create a Demo Project.
3. Click Classic Project Management Demo Project.
4. Enter a project name and identifier, and then create the project.

The following example uses a virtual mall, Feiniao Market, to describe how a team can collaborate using classic project management.

## Create Requirements

To gain a foothold in the competitive red ocean of e-commerce, research on potential user groups is essential. Usually, product managers create requirement documentation for products according to pain points in the market or user feedback. You can create a requirement on the **Requirement** page, and upload attachments or reference external resources (MockingBot Prototype) to easily incorporate ideas at any time. The menu on the right of the requirement details page allows you to adjust the priority, type, and due date of a requirement. You can also specify the estimated time and project progress as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/062d694a977e77fca3616bd9f2d062c7.png)

## Coordinate Development Plan

After the requirement research is completed, a requirement pool review meeting is held. After the requirements gathered are discussed and reviewed, the project leader approves the development plan. An **iteration** can serve as the unit of the development plan.
![](https://qcloudimg.tencent-cloud.cn/raw/abad38e9eeed7832a8435c829554fb18.png)

Using this feature, you can split larger plans (including but not limited to development plans) into specific issues (such as requirements and tasks) assigned to specific assignees. All requirements created by the product manager in the early phase can also be seamlessly integrated into the iteration plan.
![](https://qcloudimg.tencent-cloud.cn/raw/1da18253b4a1aa21eeac998e7633d9fa.png)

Requirements can be broken down into sub-requirements or sub-tasks and associated with bugs and test cases. You can configure other resources required to implement a requirement as a pre-issue, check if a requirement is blocked by another issue, reference other requirements or tasks as resources of this issue, or check which resources have referenced this issue.
![](https://qcloudimg.tencent-cloud.cn/raw/2a957ffef62115a1c4c8e7c08303f575.png)

##  Assign Development Tasks
![](https://qcloudimg.tencent-cloud.cn/raw/bcc04eff059fb53133f10bb851888ee3.png)

In an iteration plan, team members can collaborate by creating issues or accepting issues assigned by others. For example, you can break down a requirement to launch a **customer service entry** into development and test tasks. After the development has been completed, you can continue breaking down the requirement into a promotion task and hand it over to the operations department for marketing campaigns.
![](https://qcloudimg.tencent-cloud.cn/raw/542aa1b6f31dad66b83fe50428a2d1dc.png)

##  Implement the Plans

After the various plans have been created and assigned to the specific assignees, in **Workspace** > **My Issues** on the team homepage, team members can view the issues to be completed, merge requests initiated by them or merge requests to be inspected, build tasks in continuous integration, and continuous deployment release orders to be confirmed.
![](https://qcloudimg.tencent-cloud.cn/raw/9b704822cc2a36319ee3cb5b9b2f4cad.png)

For a development task, you can also directly reference merge request records in code repositories. For details, see [Reference Resources and Upload Attachments](https://intl.cloud.tencent.com/document/product/1133/44770). After associating the items, you can see the code commit record and development status in the development task.
![](https://qcloudimg.tencent-cloud.cn/raw/b573b8d04198ede076b6d87c53846c18.png)

In the menu on the right of the issue details page, you can log time by entering the estimated time and time spent on issues. A complete worklog will be automatically created for retrospectives and efficiency analysis after iterations have been completed.
![](https://qcloudimg.tencent-cloud.cn/raw/c71d0c3a21eb3a7b5a3b76d3845286f5.png)

Before leaving work, members can change the status of the daily task to **completed** and update the development progress. The iteration progress will update as each issue progresses.
![](https://qcloudimg.tencent-cloud.cn/raw/5feaca843d458dcc0a7007a737508492.png)

##  Test

The test phase is crucial to the closed development loop. Self-testing by developers usually resolves most common problems, but it is not enough. Testing helps to identify fundamental logic problems and possible missing items during the development process. CODING's built-in automated testing tools, such as Code Scan and Artifact Scan, help testers quickly create a bug and associate requirements or tasks in an iteration after a bug is found.
![](https://qcloudimg.tencent-cloud.cn/raw/bdf75c06002a626a80cb7597d2161f7b.png)

You can also log time and update the progress for a bug. In addition to assigning and entering test tasks in an issue, testers can go to **Test Management** > **Test Case Management** to write test cases.
![](https://qcloudimg.tencent-cloud.cn/raw/a043615a2fbfb19e4034f0fee5ce13ab.png)

In **Test Management** > **Test Plan**, you can configure the iteration of the test in **Edit**.


##  Project Release

After the basic development task has been completed, you can use CODING's continuous integration/deployment services to quickly validate the code.
<dx-alert infotype="explain" title="扩展阅读">
<ul style = "margin-bottom: 0px;">
<li><a href = "https://help.coding.net/docs/ci/start.html">Continuous Integration - Getting Started</a></li>
<li><a href = "https://help.coding.net/docs/cd/start.html">Continuous Deployment - Sample Project</a></li>
</ul>
</dx-alert>

After all iteration plans have been completed, you can go to an iteration to view the status trend and time burndown chart of the iteration in **Overview and Statistics**. Managers can stay on top of their team's progress for the plan.
![](https://qcloudimg.tencent-cloud.cn/raw/2f69e2cbcb88e52454ea10d1cd7a556b.png)

##  Customize Team Workflow

In addition to the default issue statuses, you can customize the workflow of various issues in the issue **Workflow** in **Project Settings** > **Project Collaboration** > **Issue Types**. See [Customize Workflow](https://intl.cloud.tencent.com/document/product/1133/44768) for details.
