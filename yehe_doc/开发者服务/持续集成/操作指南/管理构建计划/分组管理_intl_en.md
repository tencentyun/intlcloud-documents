---
title: Group Management - CODING Help Center
pageTitle: Group Management
pagePrevTitle: Build node pool
pagePrev: ci/node/pool.html
pageNextTitle: Team Build Template
pageNext: ci/manage/team-template.html
alias: 
-   devops/ci/group.html
-   ci/group.html
---

### Starring and grouping

Build plans can be starred and grouped to help you quickly locate build plans that you are following.

-   Starring

This is a personal setting that only takes effect for the user who has starred a plan. Click the star on a build plan area, and you can view only starred plans in "My Stars" tab.

![](https://qcloudimg.tencent-cloud.cn/raw/1a1303ca9ff03ba1a3fa233bd5471423.png)

- Grouping

This is a global setting that is only accessible to users with permission to "Continuous Integration Management". Members of a project can view the groups and categories configured for build plans and conveniently sort plans.

Click "More" > "Create Group" and enter a group name to create a group.

![](https://qcloudimg.tencent-cloud.cn/raw/410a54716ec18f4a115ec0379663d41a.png)

You can modify group names, change the order, and create and delete groups.

*Note: Deleting a group does not delete the build plans in the group. After you delete a group, the build plans in the group will be categorized as "Not Grouped".*

![](https://qcloudimg.tencent-cloud.cn/raw/e8bf2c03bc0ddfdfb12161a0b76946e8.png)

Click "Batch Sort Build Plans" to enter the build plan sorting page. You can select multiple and move them to the same group at once. Then the selected build plans can be seen a separate group tab after being added.

![](https://qcloudimg.tencent-cloud.cn/raw/f1dd93a0696dab654b38a9f674144a26.png)

### Filtering and sorting

In the search bar on the right of the build plan page, you can filter build plans by name. Select "Filters" > "Only Me". Only the latest build plans triggered by you will be shown. This filter can also be enabled in the build records.

![](https://qcloudimg.tencent-cloud.cn/raw/e90fda6bce3e9cdc8e973ca76c8d0017.png)

You can also sort the build plans by the trigger time of the latest build records.


==== 2020/09/25 ====
