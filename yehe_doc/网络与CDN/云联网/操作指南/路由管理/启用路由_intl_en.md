This document describes how to enable one or multiple CCN routes.

## Prerequisites
Disable routes: ![](https://qcloudimg.tencent-cloud.cn/raw/83efcec917f2549d9912ee199b68bed2.png)


## Directions
1. Log in to the [CCN console](https://console.cloud.tencent.com/vpc/ccn).
2. In the CCN instance list, click the ID of the CCN for which you want to enable routing to access the details page.
3. Enable the route on the **Route Table** tab:
>!After the route is enabled, if routing rules overlap, match will be performed according to the longest mask rule.
>
  + **Single route**: Click the icon on the right of the disabled route and click **OK** in the **Enable Route** pop-up window.
 ![]()
  + **Multiple routes**: Select multiple disabled routes, click **Enable Route** at the top, and click **OK** in the pop-up window.
 ![]()
If there is a route conflict, the routes will be matched according to the longest mask rule, which may cause an enablement failure. To use a route, disable/delete the original conflicting route first:
![]()
