When a TEM application is in failed status, at least one instance is not in **Running** status. This document describes some common instance error statuses and how to troubleshoot the problems.

## Instance Error Status

### CrashLoopBackOff

#### Status description
An application in the instance has a problem while running, and the container failed to start/run.

#### Solution
View the instance logs and troubleshoot the problem based on the **log content**.

![](https://qcloudimg.tencent-cloud.cn/raw/f232dded30fd6e734a7cdd9d6adbdb07.png)

### Error

#### Status description
Similar to `CrashLoopBackOff`, an application in the instance has a problem while running, and the container failed to start/run.

#### Solution
View the instance logs and troubleshoot the problem based on the **log content**.

![](https://qcloudimg.tencent-cloud.cn/raw/f232dded30fd6e734a7cdd9d6adbdb07.png)

### Running Unhealthy: Readiness probe failed

#### Status description
The readiness health check configured for the application failed.

#### Solution
Go to **Application Deployment** > **Health check** and check whether the **Readiness Probe** configuration item of the application is correct.
![](https://qcloudimg.tencent-cloud.cn/raw/0201f789f3433b50d32ba6f5fe2f0f74.png)

### Running Unhealthy: Liveness probe failed

#### Status description
The aliveness health check configured for the application failed.

#### Solution
Go to **Application Deployment** > **Health check** and check whether the **Aliveness Probe** configuration of the application is correct.
![](https://qcloudimg.tencent-cloud.cn/raw/53113c0dcceb186acfeba9388430c4f8.png)

### Running Unhealthy: Readiness check failed according to l4 listener: xxx of CLB xxx. Service: xxx

#### Status description
The access configuration of the application cannot take effect, and the application cannot be accessed.

#### Solution
Go to **Application details** > **Basic information** > **Access configuration** and check whether the port and protocol are correct.
![](https://qcloudimg.tencent-cloud.cn/raw/9f7d2818b7e57b49ad6f5c25e39ec5b6.png)

### PostStartHookError

#### Status description
PostStart configured for the application failed.

#### Solution
Go to **Application Deployment** > **Application start/stop management** and check whether **PostStart** configured for the application can run normally.

![](https://qcloudimg.tencent-cloud.cn/raw/88c7a9bb3124992f4a9573c71ee45e68.png)

### ContainerCreating

#### Status description
The instance container failed to be created.

#### Solution
Go to **Application Deployment** > **Persistent storage** and check whether the application is mounted with a nonexistent data volume. ![](https://qcloudimg.tencent-cloud.cn/raw/828dcb4c0720a5fb7bb4c5439f9a914a.png)

### CreateContainerConfigError

#### Status description
The instance container failed to be configured.

#### Solution
Go to **Application Deployment** > **Environment variable** and check whether the application uses nonexistent configuration.

![](https://qcloudimg.tencent-cloud.cn/raw/7b8bac1611cd55a68030df1c2d232a09.png)

### ImagePullBackOff

#### Status description
The instance image failed to be pulled.

#### Solution
Go to the [TCR console](https://console.cloud.tencent.com/tcr/repository?rid=1) and check whether the image used by the application exists or has been deleted by mistake.
