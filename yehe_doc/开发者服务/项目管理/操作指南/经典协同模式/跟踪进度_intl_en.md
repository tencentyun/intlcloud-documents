This document describes progress tracking in classic project management.


## Open Project

1. Log in to the CODING Console and click **Use Now** to go to CODING page.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. In the menu on the left, click **Project Collaboration**.

## Feature Overview

When the various iteration plans are in progress or have been completed, you can go to a specific iteration in the **Iterations** module to view the iteration information, issue statistics, status trend, time burndown chart, and action log in **Overview and Statistics**, to stay on top of your team's progress for the iteration.
![](https://qcloudimg.tencent-cloud.cn/raw/5d65e94edb9753443457ce0281ba7a31.jpeg)

### Iteration details[](#detail)

The iteration details on the left of **Overview and Statistics** shows all information of the iteration. The ** Iteration Info** includes the current iteration phase, iteration duration, progress, estimated time, and other information. In **Issue Statistics**, the total number of issues and number of completed issues in the iteration are shown.
![](https://qcloudimg.tencent-cloud.cn/raw/b3226ccd84601db2df30c4fedf333c37.jpeg)

### Issue status trend[](#trend-chart)

The issue status trend chart in the upper-right corner of **Overview and Statistics** is a stacked area chart showing the change in issue status versus time, highlighting aggregate trends in issues for the development team. You can switch between issues in the dropdown menu. The different area colors indicate different issue statuses, helping teams manage issue progress and make the necessary adjustments to lagging issues.
![](https://qcloudimg.tencent-cloud.cn/raw/891f2fb70da55fd68433ee386d8642c3.jpeg)
<dx-alert infotype="explain" title="Color description">

<ul style = "margin-bottom: 0px;">
<li>Green: Completed</li>
<li>Orange: In progress</li>
<li>Blue: Not started</li>
</ul>
</dx-alert>


### Time burndown chart[](#burndown-chart)

If the estimated time and time spent are logged for issues, the **Time Burndown Chart** in **Overview and Statistics** will show the remaining workload versus time. See [Workload Statistics](https://intl.cloud.tencent.com/document/product/1133/44751) for details on how to use workload statistics.

The time burndown chart starts a day before the iteration start time and shows the total estimated time of all issues. The horizontal axis indicates time and the vertical axis indicates the remaining time. The gray (ideal) line is the expected progress, the blue (actual) line is the actual progress, and the remaining time is computed every day. If you modify the iteration start time on the **Iteration** details page, the start time of the time burndown chart will be updated at the same time.
- If the actual progress fluctuates, but remains below the expected progress in the mid to late stage, the issues are progressing smoothly and will likely be delivered on time.
- If the actual progress remains above the expected progress constantly, the issues are behind schedule and are at risk of delay. You need to adjust the time and iteration plan in time.
![](https://qcloudimg.tencent-cloud.cn/raw/009a9ae57a8635218b25371ac7b4cc46.jpeg)

### Action log[](#activity-log)

The **Action Log** below the **Time Burndown Chart** records all operations for the iteration.
![](https://qcloudimg.tencent-cloud.cn/raw/63c96fb951be4fd17d1866f392fc7046.jpeg)
