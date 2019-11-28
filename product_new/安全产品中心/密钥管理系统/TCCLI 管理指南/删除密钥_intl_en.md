## Overview
The schedule key deletion feature involves the following two APIs:


| API Name | Description | Note |
|---------|---------|---------|
| ScheduleKeyDeletion | Creates a schedule deletion task | The `KeyId` and `PendingWindowInDays` parameters are required for this API. For more information. |
| CancelKeyDeletion | Cancels a schedule deletion task | The `KeyId` parameter is required for this API.|

>If a CMK schedule deletion waiting period is set through the ScheduleKeyDeletion API when the CMK is in disabled status, the CMK will be deleted automatically at the specified time.

The examples below are called with [TCCLI](https://intl.cloud.tencent.com/product/cli), which can also be called with any supported programming languages.

## Examples
#### Creating a schedule deletion task

This example shows you how to delete a disabled CMK in 7 days.
#### Input
```shell
tccli kms ScheduleKeyDeletion --region ap-guangzhou --KeyId 5xxxxx-xxxx-xxxx-xxxx-52xxxxx4 --PendingWindowInDays 7
```

#### Output
If the setting is successful, the ID of the CMK to be deleted and the schedule deletion timestamp will be returned.
```shell
{
	"KeyId": "6xxxxxxx-xxxx-xxxx-xxxx-5xxxxxxxxc09",
    "RequestId": "2bd72d85-f9dd-4465-ae51-beebff54f540",
    "DeletionDate": 1572512542
}
```



#### Canceling a schedule deletion task
This example shows you how to cancel a schedule deletion task, where the CMK is the one used in the above example.

#### Input
```shell
tccli kms CancelKeyDeletion --region ap-guangzhou --KeyId 5xxxxx-xxxx-xxxx-xxxx-52xxxxx
```

#### Output
If the execution is successful, the returned request will contain the ID of the CMK for which the schedule deletion task is successfully canceled.
```shell
{
	"KeyId": "6xxxxxxx-xxxx-xxxx-xxxx-5xxxxxxxxc09",
    "RequestId": "c85473c6-e18d-4a09-9eac-03958dd4714d"
}
```


