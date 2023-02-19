You can start or stop instances. After an instance is stopped, it will no longer receive or forward traffic, perform health checks, or allow ping.
<dx-alert infotype="explain" title="">
The feature is currently in beta test. To try it out, [submit a ticket](https://console.tencentcloud.com/workorder/category).
</dx-alert>



## Use Cases
If you have configured a large number of CLB instances, and some of them are temporarily unused for business considerations but cannot be deleted, you can choose to stop them.
- After an instance is stopped, all its listeners will also be stopped, and it will no longer receive or forward traffic.
- After an instance is started, all its listeners will also be started, and it will receive and forward traffic normally.
- After a listener is stopped, it will no longer receive or forward traffic. After all listeners of an instance are stopped, the instance will be stopped.
- After a listener is started, it will receive and forward traffic normally. After all listeners of an instance are started, the instance will be started.
- After an instance is stopped, if any of its listeners is started, the instance will be started and receive and forward traffic normally with the started listener, while other listeners will remain stopped.


## Restrictions
- This feature is supported only for CLB but not classic CLB.
- This feature is only supported by VPC but not classic network.
- This feature is not supported for TLS 1.3 and earlier.

## Prerequisites
- You have created a [CLB instance](https://intl.cloud.tencent.com/document/product/214/6149).
- You have created a listener.

## Directions
1. Log in to the [CLB console](https://console.cloud.tencent.com/loadbalance).
2. Select a region in the top-left corner of the **Instance management** page, select the target instance in the instance list, and click **More** > **Start** or **More** > **Stop** in the **Operation** column on the right.
3. (Optional) On the **Listener management** tab, find the target listener and click **Start listener** or **Stop listener**.
![]()
