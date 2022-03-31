# **Notification on CAM Authentication Upgrade for DBbrain APIs**

According to the security requirements of Tencent Cloud, APIs that are directly accessed now require CAM authentication for access from April 8, 2022. Please grant access permissions for following APIs in the [CAM console](https://console.cloud.tencent.com/cam/policy) before April 8, 2022 so that you can use them normally.

## APIs that require CAM authentication (eight in total)

| API Name                                                     | API Description                           | API Type |
| ------------------------------------------------------------ | ---------------------------------- | -------- |
| [DescribeSlowLogUserHostStats](https://cloud.tencent.com/document/api/1130/57783) | Gets the slow log source address chart       | Resource-level   |
| [DescribeUserSqlAdvice](https://cloud.tencent.com/document/api/1130/57782) | Gets SQL statement optimization suggestions                  | Resource-level   |
| [DescribeMySqlProcessList](https://cloud.tencent.com/document/api/1130/57824) | Gets the real-time thread list                   | Resource-level   |
| [DescribeTopSpaceSchemas](https://cloud.tencent.com/document/api/1130/57793) | Gets the space statistics of top databases           | Resource-level   |
| [DescribeDBDiagEvents](https://cloud.tencent.com/document/api/1130/65947) | Gets the diagnosis event list                   | Operation-level   |
| [DescribeProxySessionKillTasks](https://cloud.tencent.com/document/api/1130/69205) | Queries the status of the session killing task executed by the proxy node  | Resource-level   |
| [DescribeDiagDBInstances](https://cloud.tencent.com/document/api/1130/57798) | Gets the instance list                   | Operation-level   |
| [CreateProxySessionKillTask](https://cloud.tencent.com/document/api/1130/67782) | Creates a task of killing proxy node sessions         | Resource-level   |

## Authorization guide

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
2. Click **Policy** on the left sidebar.

#### Resource-level APIs

Select **Create Custom Policy** > **Create by Policy Generator** to configure policy parameters.

- Service: Select **TencentDB for DBbrain (dbbrain)** 
- Resource: Select either **Specific resources** or **All resources**.

![](https://qcloudimg.tencent-cloud.cn/raw/71f7efac3099ebb476636cd84832ea65.png)

#### Operation-level APIs

Select **Create Custom Policy** > **Create by Policy Generator** to configure policy parameters.

- Service: Select **TencentDB for DBbrain (dbbrain)** 
- Resource: Select **All resources**.

![](https://qcloudimg.tencent-cloud.cn/raw/9f5ac41827be48453c993bb94a421b01.png)

#### The policy that doesn’t need to be modified

If you use the `QcloudDBBRAINFullAccess` authentication policy, you don’t need to modify it.
![](https://qcloudimg.tencent-cloud.cn/raw/49c20eb5e6a258acbb1822bb410a599a.png)

>!Please grant access permissions for related APIs in the [CAM console](https://console.cloud.tencent.com/cam/policy) before April 8 so that you can use these APIs normally. 
If you use the `QcloudDBBRAINFullAccess` authentication policy, you don’t need to modify it.