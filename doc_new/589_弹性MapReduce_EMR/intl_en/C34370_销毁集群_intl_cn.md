## Scenario
When you no longer need an EMR cluster, you can terminate it in the EMR Console.
>After terminated, the cluster will be retained in the recycle bin for 7 days and can be restored during the period. After 7 days, it will be completely terminated and cannot be restored. Please do so with caution.

## Directions
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr) and select **Cluster List** in the left sidebar.
2. In the **Management** column of the instance, select **More** > **Terminate** to enter the termination page.
![](https://main.qcloudimg.com/raw/5a8f383548d3a97eced0de1f3f41c2c4.png)
3. On the cluster termination page, there are two steps for you to confirm the **termination options** and **confirm the termination**.
>
>- If there is an EIP (an IP with a secondary ENI), the instance will be retained after returned, and the idle IP will continue to incur fees. If you don't need to retain it, please release it on the corresponding resource management page.
>- A terminated instance will be retained in the recycle bin for 7 days. Please back up the data in advance.
>
3. After confirming everything is correct, click **Start Termination** to terminate the cluster.
![](https://main.qcloudimg.com/raw/34d683ba58fad5241e8b64e390d05212.png)
