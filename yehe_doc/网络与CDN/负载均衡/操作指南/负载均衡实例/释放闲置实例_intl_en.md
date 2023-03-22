When a pay-as-you-go instance is not configured with a listener or bound to a real server seven days after the creation, it’s considered as an idle instance. To reduce unnecessary charges, please release idle instances in time.



## Restrictions
CLB supports batch release of idle instances in the same region only.

## Directions
>!The idle instance data can be cached for one day. Make sure that the instance to be released is not in use to prevent a release error.
>
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance) and click **Idle Instance** on the left sidebar.
2. Select a region in the upper left corner of the idle instance page, find the target instance in the idle instance list, and click **Delete** in the **Operation** column on the right.
3. (Optional) Select all instances on the left side of the idle instance list, and click **Delete** at the top of the page.
4. In the pop-up window, confirm the instance information and click **OK**.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/tUxT437_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230322094617.png" width="70%">
