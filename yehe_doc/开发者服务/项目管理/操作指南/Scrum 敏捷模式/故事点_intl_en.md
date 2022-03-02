This document describes story points in Scrum agile management.

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click **Use Now** to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the project.
3. In the menu on the left, click **Project Collaboration**. 

## Function Overview

Traditional software teams generally estimate their workload in time, while agile teams use story points to estimate the software effort. You can estimate story points using a modified Fibonacci sequence (0, 1⁄2, 1, 2, 3, 5, 8, 13, 20, 40) or T-shirt sizing (XS, S, M, L, XL). Such abstract estimation helps software teams to make better decisions around work effort.

Using CODING Project Collaboration, you can configure the story point field, specify story points, edit story points, and view story points for different types of issues (user stories/requirements/tasks/bugs), and view the total story points of an iteration.

### Configure story points[](#configure)

The story point function is enabled by default when a project is created. To configure the story point estimation method, go to **Project Settings** > **Project Collaboration** > **Agile Features**. The default estimation method is **Modified Fibonacci sequence** and you can change it to **T-shirt size**.

>!Changing the story point estimation method will clear the story point configuration of existing issues. Proceed with caution.
>
![](https://qcloudimg.tencent-cloud.cn/raw/008e99fb12b13bb1a42020762bd3e8ad.png)

### Use story points[](#use)

#### Specify story points[](#enter)

You can configure the story point field when creating a user story, requirement, task, or bug.
![](https://qcloudimg.tencent-cloud.cn/raw/424d000875df01ae0dc1b410f99bd7ff.png)

#### View story points[](#check)

You can view story points configured on the **Pending Planning** page, iteration details page, and the overview and details page of an issue (user story/requirement/task/bug).

**Pending Planning** displays the story points configured for each issue as well as the total story points of all issues in the **backlog** or an iteration.
![](https://qcloudimg.tencent-cloud.cn/raw/f5daf2a85346e22cad4354a2f3ab260e.png)

By default, the story points configured for issues are not displayed on the iteration details page or issue overview page. You can display them and adjust the display priority in **Table Display Settings** in the upper-right corner.
![](https://qcloudimg.tencent-cloud.cn/raw/0e560d6e0170ceefd9501d14937736a3.png)
![](https://qcloudimg.tencent-cloud.cn/raw/30d6b4c4a6607ba9baf9d90ff98b2aee.png)

### More information[](#read-more)

#### Differences between story points and time[](#differences)

Traditional software teams estimate workload with time. Time is an **absolute value** that is usually estimated with historical empirical information.

Agile development teams estimate software effort with story points, a **relative value**. In other words, given two requirements, we can estimate that one is larger than the other, but we are unsure of the exact workload of each requirement.

In practice, both estimation methods have their own advantages and disadvantages in different scenarios. Good estimation practices help teams stay on top of project costs and profitability and reach a consensus on the effort, priority, and value of requirements to be delivered, leading to better business decisions.

#### What is the Fibonacci sequence?[](#Fibonacci-sequence)

Fibonacci sequence: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34...

The recursive relation of this sequence is f(0) = 0, f(1) = 1, f(n) = f(n-1) + f(n-2) (n ≥ 2, n ∈ N*). In other words, except for the first two values (0 and 1), the Nth value is equal to the sum of the previous two ones.

1 = 0 + 1

2 = 1 + 1

3 = 1 + 2

8 = 3 +5

...

#### Why estimate story points with a modified Fibonacci sequence? [](#why)

In agile development, task effort is estimated by comparing story points between tasks. In our modified Fibonacci sequence, the difference between adjacent numbers increases as the numbers increase, allowing us to distinguish tasks by effort. For example, a 34-point requirement is different from a 21-point one, but it would not be very agile to debate over whether a feature is 34 or 35 points.

#### Which story point estimation method should I choose? [](#choose)

-   T-shirt sizing is suited to estimating the size of large user stories with massive requirements in a coarse-grained yet quick way.
-   The modified Fibonacci sequence is suited to estimating the size of small user stories with few requirements in a relatively precise way.

#### How to achieve effective story point estimation [](#effective)

During actual agile development, the estimated number of points may be different from the actual situation due to business uncertainty, new changing factors, and subjective factors. We hope the following suggestions can help you improve story point estimation efficiency:

- **Involve all relevant members in the estimation.** With more comprehensive information comes more mature results. During the estimation process, team members can share their logic, experience, and hypotheses, creating synergy.
- **Reference previous work.** In the iteration retrospective, review and reflect on the accuracy of the estimate to improve the next iteration estimate.
- **Choose the right estimation method for story points.** Estimation methods differ for projects of different types and effort. Popular estimation methods include planning poker, T-shirt size, and dot vote.
