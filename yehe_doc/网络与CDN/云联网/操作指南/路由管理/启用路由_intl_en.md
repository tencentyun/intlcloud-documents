This document describes how to enable one or multiple CCN routes.

## Prerequisites
Disable routes: ![](https://qcloudimg.tencent-cloud.cn/raw/83efcec917f2549d9912ee199b68bed2.png)


## Directions
1. Log in to the [CCN console](https://console.cloud.tencent.com/vpc/ccn).
2. In the CCN instance list, click the ID of the CCN for which you want to enable routing to access the details page.
3. Enable the route on the **Route Table** tab:
>! If the routing rules overlap, match according to the longest mask rule
>
  + **Single route**: Click the icon on the right of the disabled route and click **OK** in the **Enable Route** pop-up window.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/64uw610_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230504164423.png)
  + **Multiple routes**: Select multiple disabled routes, click **Enable Route** at the top, and click **OK** in the pop-up window.
 ![](https://staticintl.cloudcachetci.com/yehe/backend-news/2as4310_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230504165355.png)
After it is enabled, if there is no route conflict, the routes will be displayed as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/rhsH220_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230504165521.png)
If there is a route conflict, the route with the longest mask is used. To use this route, disable/delete the original conflicting route first.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/a5Sc595_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230504165757.png)
