This document describes plans in classic project management.


## Open Project

1. Log in to the CODING Console and click **Use Now** to go to CODING page.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. In the menu on the left, click **Project Collaboration**.

## Feature Overview

**Plans** show the progress and time view of issues by iterations. Using **Plans**, you can plan iterations, break down requirements, assign tasks, and set task durations in plans to facilitate arrangements for the delivery plans of larger projects.
![](https://qcloudimg.tencent-cloud.cn/raw/032bf0b90a7ba9a1bcae08e7eea61300.png)

### Planning according to iterations[](#plan)

According to the classic project management workflow, after a team has reviewed the requirements and the project leader has approved the development plan, an **iteration* serves as the unit of development schedule plans derived. On the **Plans** page, you can select Create Iteration in the upper-right corner, enter a title, assignee, start time, end time, and iteration goal, and then click **Create**.
![](https://qcloudimg.tencent-cloud.cn/raw/20990a7732ebcd39d3ada36d5a5d073a.png)
If you select **Create and Plan**, you can drag and drop or select created but unplanned issues and add them to the current iteration.
![](https://qcloudimg.tencent-cloud.cn/raw/8d2ff0d446608f49182b35959bde3740.png)
After you have created an iteration, it will be shown in **Plans**. To complete arrangements for the plan, select **+** to create issues (requirements, tasks, and bugs) to add to the iteration. See [Plan Iteration](https://intl.cloud.tencent.com/document/product/1133/44746) for details.
![](https://qcloudimg.tencent-cloud.cn/raw/8fa6e36dc012542fc4b756ba4c4912db.png)

### View plan[](#check)

#### View by filters[](#filter-criteria)

In **Plans**, select **More Filters** at the top to quickly locate specific issues by setting filters. The system automatically saves the filters set for the next search.
![](https://qcloudimg.tencent-cloud.cn/raw/e74480385bcfe93a2109a837f0ab3d35.png)

#### View by time period[](#time-period)

In **Plans**, set the time period using the filter in the upper-right corner to show by day, week, or month. The system automatically saves the filters set for the next search.
![](https://qcloudimg.tencent-cloud.cn/raw/1f8795c3a4a8ea49f2346ea7ef51a38a.png)

### Track plan[](#track)

#### Gantt chart[](#gantt-chart)

In **Plans**, the Gantt chart on the right intuitively shows the completion status of all issues in the entire plan, so managers can assess and manage progress and coordinate lagging issues to ensure the plan stays on track.
![](https://qcloudimg.tencent-cloud.cn/raw/a95b731e17136e72996935fe4788d49a.png)
<dx-alert infotype="explain" title="Color description">

<ul style = "margin-bottom: 0px;">
<li>Completed: green</li>
<li>Incomplete and not progressing: gray</li>
<li>Incomplete but progressing: blue</li>
<li>Issue is incomplete and start and due time have exceeded that of parent issue: orange</li>
<li>Overdue and incomplete: orange</li>
</ul>
</dx-alert>
You can show or hide issue fields to suit your needs.

![](https://qcloudimg.tencent-cloud.cn/raw/ff9edb5b366a4a0977c7a350036e829b.png)

#### View block relationships[](#blocking)

In **Plans**, the Gantt chart to the right of a specific issue will show the block relationships and their numbers, including pre-issues and post-issues with block relationships.
![](https://qcloudimg.tencent-cloud.cn/raw/fb19013da50b3b77ca0035ce4f842658.png)

Select **`···`** > **Unblock** to the right of an issue with a block relationship to remove the issue. Alternatively, you can click **Associate Pre-Issue/Post-Issue** to add an issue with a block relationship.
![](https://qcloudimg.tencent-cloud.cn/raw/4806a6c387af3ae9b994f8b390b0825a.png)

#### View block relationships[](#display)

To show pre-issues and post-issues with block relationships for an issue in **Plans**, select **Block Relationships** at the top to enable the mode and the filters will be automatically cleared. If **Show Dependency Chain** is toggled on, all issue dependencies related to the current issue dependencies will be recursively shown.
![](https://qcloudimg.tencent-cloud.cn/raw/b363d93e91fc594ddbd3ad73f340df4b.png)

### Risk control[](#risk-control)

#### Overdue warning[](#delay-warning)

In **Plans**, a yellow exclamation mark **!** indicates the following: the start time of an issue is earlier than the start time of the parent issue; the due time of an issue exceeds the due time of the parent issue; the start time of an issue is earlier than the end time of the pre-issue; or an issue is N day(s) overdue. The risk and time will be shown to the left of the issue to help teams make timely adjustments to plans.
![](https://qcloudimg.tencent-cloud.cn/raw/e857a679141f7c83d4fe6dc278f7a963.png)

### View settings[](#view)

In **Plans**, you can adjust the number of iterations shown in **View Settings** and sort them by the earliest or latest start time. **Show recently completed iterations** is toggled off by default to simplify the interface and help teams focus on the current iterations. You can toggle on the switch as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/681aa9245878f8e0c6c31f7e5da0eaf5.png)
