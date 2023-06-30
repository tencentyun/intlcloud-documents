
This document describes the statuses of a container instance and whether it is billed from its creation to deletion. You can determine whether your current business runs normally based on the status.

## Container Instance Status

All the statuses of a container instance are as described below:

| Instance Status | Description | 
|----------------|---------|
| Pending | The instance is being created.  |
| Running | Indicates that all containers have been created successfully and at least one container is running.  |
| Succeeded | Indicates that all containers have finished running and exited successfully (the `exitCode` of all containers is `0`) and the restart policy is `never` or `onFailure`.  |
| Failed | Indicates that all containers have exited with an exception (the `exitCode` is not `0`) and the restart policy is `never`.  |

>?A restart policy is a behavior performed on the container in an instance. It doesn't mean that the container instance will be restarted. There are three restart policies as described below:
- **Always**: Auto-restarts the container if it is in any status other than `Running`.
- **Never**: Never restarts the container regardless of its status.
- **OnFailure**: Auto-restarts the container when it exits and the `exitCode` is not `0`.

The billing details for each status are as shown below:

![](https://qcloudimg.tencent-cloud.cn/raw/95caa9cabdd7ec6d67e9b2063bcf1113.png)

## Container Status

| Container Status | Description | 
|---------|---------|
| Created  | The container was created successfully.  |
| Running  | The container runs successfully.  |
| Exited  | The container exits after successful or failed (`exitCode` is not `0`) running.|
| Unknown  | The container status is unknown; for example, when the init container hasn't been terminated for a long time.|

