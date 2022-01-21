
## Error Description
- Symptom 1: the connection utilization was high.
![](https://qcloudimg.tencent-cloud.cn/raw/69734df69d793cce934c05b89a6d83b4.png)
- Symptom 2: connections couldn't be established.

## Common Causes
- Connections leaked.
- The configured maximum number of connections is too low.

## Solution
Check for connection leaks. For third-party network connections, there must be a finally block for execution; otherwise; non-standard code is prone to cause the problem where connections are not released properly.

## Troubleshooting Procedure
### [Modifying code logic](id:xgdmlj)
Check whether connections leaked, and if so, you can release invalid connections and fix non-standard code that leaked connections.

### [Modifying connection configuration](id:xgljpz)
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance details page.
2. In the **Network Info** > **Max Connections** parameter on the instance details page, click **Adjust** to adjust the maximum number of connections.
![](https://qcloudimg.tencent-cloud.cn/raw/ed736808880fdd4f3ad4f86b69e0a617.png)
3. In the pop-up window, adjust the maximum number of connections and click **OK**.

>?If the problem persists, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).
