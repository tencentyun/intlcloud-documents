This document describes iteration statistics in Scrum agile management.


## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click **Use Now** to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the project.
3. In the menu on the left, click **Project Collaboration**. 

## Function Overview

When the various iteration plans are in progress or have been completed, you can go to a specific iteration in the **Iterations** module to view the iteration information, issue statistics, issue status trend chart, story points burndown chart, and issue distribution diagram in **Overview and Statistics**, to stay on top of your team's progress for the iteration.
![](https://qcloudimg.tencent-cloud.cn/raw/3981f7c478cc12d98433cae789d1251b.png)

## Iteration Details[](#detail)

The iteration details on the left of **Overview and Statistics** show all information of the iteration. The ** Iteration Info** includes the current iteration phase, iteration duration, progress, completed story points, and other information. In **Issue Statistics**, the total number of issues and number of completed issues in the iteration are shown.
![](https://qcloudimg.tencent-cloud.cn/raw/9f1464818ea5b3eee18a11422bec638d.png)

## Issue Status Trend Chart[](#trend-chart)

The issue status trend chart in the upper-right corner of **Overview and Statistics** is a stacked area chart showing the change in issue status versus time, highlighting aggregate trends in issues for the development team. You can switch between issues in the dropdown menu. The different area colors indicate different issue statuses, helping teams manage issue progress and make the necessary adjustments to lagging issues.
![](https://qcloudimg.tencent-cloud.cn/raw/663f9be69363bb62d60d6a1f20d2eba1.png)
<dx-alert infotype="explain" title="颜色说明">

<ul style = "margin-bottom: 0px;"><li>Green: Completed</li>
<li>Orange: In progress</li>
<li>Blue: Not started</li></ul>
</dx-alert>



## Story Points Burndown Chart[](#burndown-chart)

If the story point field was specified when an issue was created and the statuses of completed issues have been transitioned appropriately, the **Story Points Burndown Chart** in **Overview and Statistics** will show the remaining story points versus time. For more information, see [Story Points](https://intl.cloud.tencent.com/document/product/1133/44761).

The story points burndown chart starts a day before the iteration start time. The horizontal axis indicates time and the vertical axis indicates the remaining story points. The gray (ideal) line is the expected progress, and the blue (actual) line is the actual progress, and the remaining story points are computed every day. If you modify the iteration start time on the **iteration** details page, the start time of the story points burndown chart will be updated at the same time.
- If the actual progress fluctuates, but remains below the expected progress in the mid to late stage, the issues are progressing smoothly and will likely be delivered on time.
- If the actual progress remains above the expected progress constantly, the issues are behind schedule and are at risk of delay. You need to adjust the story points and iteration plan in time.
![](https://qcloudimg.tencent-cloud.cn/raw/6d140e3aa90680f03a1edc71c32e468e.png)

## Issue Distribution Diagram[](#distribution)

The issue distribution diagram is a horizontal histogram that displays the number of requirements, tasks, and bugs that are **Completed**, **In progress**, and **Not started** in the current iteration, so that teams can quickly get up to speed on the global project progress.
![](https://qcloudimg.tencent-cloud.cn/raw/f61aeacde36ebccbba5e5394c3ba8dde.png)

## Action Log[](#activity-log)

The **action log** below the **issue distribution diagram** records all operations for the iteration.
![](https://qcloudimg.tencent-cloud.cn/raw/1f53712c292f9075095e148a5a85ca0f.png)