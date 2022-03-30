This document describes how to configure custom issue types in CODING Project Management.

## Open Project

1. Log in to the CODING Console and click **Use Now** to go to CODING page.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the project.
3. Click **Project Collaboration** in the menu on the left.

## Feature Overview[](#intro)

An issue type is the subject in project collaboration. For example, a requirement and a task can both be referred to as an **issue type**. You can add an issue type called **Maintenance**, modify its type icon, and then specify its [fields](https://intl.cloud.tencent.com/document/product/1133/44767) and [workflows](https://intl.cloud.tencent.com/document/product/1133/44768) in the project. Issue types can be categorized as team-level (or global) and project-level types. You need to define the global issue types first, and then apply them to projects.

## Global Issue Type[](#global)

The global issue type list shows all the issue types in a team. Issue types are divided into built-in types and custom types. The icon and name of a built-in type (such as epic, requirement, task, bug, user story, and sub-issue) cannot be changed.

**User Story** is a new built-in type. As the smallest unit of work in an agile framework, it describes the value brought by software to users.
![](https://qcloudimg.tencent-cloud.cn/raw/e349dfa40ac29c49888165f9563243fc.png)

>?When creating a custom issue type, you can select an icon for it, and add a description. The custom issue type can be copied, and a replica of it is created automatically.
>
Custom requirements and custom tasks can be created for custom issue types, which can be manually deleted when they are disassociated with the project.
![](https://qcloudimg.tencent-cloud.cn/raw/8be37bb6186bc153951fed7a31989bc9.png)

## Project-level Issue Type[](#project)

Click **Project Settings** > **Project Collaboration** to add a created global issue type.
![](https://qcloudimg.tencent-cloud.cn/raw/747707706573ada56d374cb1066ffd35.png)

>! The [agile mode](https://intl.cloud.tencent.com/document/product/1133/44754) automatically introduces the sub-issue type, while the [classic mode](https://intl.cloud.tencent.com/document/product/1133/44744) doesn't support the epic type and the sub-issue type.
>


## Issue Type Configuration[](#global)

You can set hierarchy levels, fields, and workflows for issue types.

### Hierarchy levels[](#level)

In the classic collaboration mode, you can set hierarchy levels for **user stories**, **requirements**, and **custom requirements**.
![](https://qcloudimg.tencent-cloud.cn/raw/502e029a1e28b2e221b834c81d80abf0.png)

After hierarchy levels are defined, multiple issue types are available when you break down a requirement to suit your workflows.
![](https://qcloudimg.tencent-cloud.cn/raw/1b730df218d3a64bf8c3b566c71b440f.png)

### Configure field[](#attributes)

Fields are used to **describe** the current status, due date, assignee, priority, and other information of the issue. Basic field information (such as title, description, attachment, and associated resources) is not included. All the fields on the field configuration page are shown on the issue details page and can be used in search and filters. For more information, see [Custom Issue Fields](https://intl.cloud.tencent.com/document/product/1133/44767).
![](https://qcloudimg.tencent-cloud.cn/raw/8b0045f76b2a605848caba1d4fa55f81.png)

### Configure workflow[](#workflow)

Custom workflows can be designed for both agile and classic modes to meet unique demands of different teams. More importantly, global workflow statuses allow you to define consistent statuses and improve collaboration efficiency across projects and departments. See [Custom Workflows](https://intl.cloud.tencent.com/document/product/1133/44768) for details.
![](https://qcloudimg.tencent-cloud.cn/raw/1d2c0eafd0226e3899f5a2202943a9f1.png)
