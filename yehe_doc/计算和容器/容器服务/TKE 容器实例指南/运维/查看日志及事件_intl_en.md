

## Overview

Events and logs can help you troubleshoot the issues occur during using container instances. This document describes how to view the logs and events of container instances in the TKE console.


## Viewing Container Logs
You can view the logs of init containers and business containers.
<dx-tabs>
::: Method 1
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/eksci). 
2. On the container instance list page, click **Logs** on the right of the instance for which you want to view the events.
:::
::: Method 2
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/eksci). 
2. On the container instance list page, click the name of the instance for which you want to view the events.
3. On the container instance details page, click **Logs** to view them.
:::
</dx-tabs>







## Viewing Container Instance Events
You can view all events corresponding to the current instance. For common events, see [Event List](#event).
<dx-tabs>
::: Method 1
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/eksci). 
2. On the container instance list page, click **More** > **View Events** on the right of the instance for which you want to view the events.
:::
::: Method 2
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/eksci). 
2. On the container instance list page, click the name of the instance for which you want to view the events.
3. On the container instance details page, click **Events** to view them.
:::
</dx-tabs>

### Event List[](id:event)
The common events and solutions are as follows:

|Content | Level | Description and Solution|
|--|----|---|
|RestartedEksCi | normal | Restart EKSCI successfully.|
|AllocatedEip | normal | Assign an EIP successfully.|
|AssociatedEip | normal | Bind an EIP successfully.|
|ResourceInsufficient | warning | The resource with the specification corresponding to EKSCI of the current region and availability zone has been sold out. Please select another specification for creation or change to another availability zone.|
|RecreatingPodSandbox | warning | PodSandbox recreate after timeout.|
|FailedMountVolume  | warning | Failed to mount a CBS disk or NFS.|
|FailedAllocateEip | warning | Failed to assign an EIP.|
|FailedAssociateEip | warning | Failed to bind an EIP.|

