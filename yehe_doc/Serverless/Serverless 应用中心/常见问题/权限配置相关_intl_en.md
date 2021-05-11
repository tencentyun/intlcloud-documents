### What should I do if "The appid is unavailable for legal reasons." is reported?
This error is caused by overdue account, as it is impossible to create pay-as-you-go resources. Please check whether your account is overdue. This error can be resolved by topping up your account to a positive balance.

### What should I do if "you are not authorized to perform operation resource has no permission" is reported?
This error is caused by the lack of relevant permissions in the account itself or the invocation role `SLS_QcsRole`. Please determine the missing policy according to the error message and then assign it to the account or `SLS_QcsRole` in the [CAM console](https://console.cloud.tencent.com/cam).
Sample error message:
```
 [request id:xxxxx]you are not authorized to perform operation (scf:CreateFunction) resource (qcs::scf:gz:uin/xxxxxx:function/*) has no permission
```
It can be seen from the error message that the permissions of `scf:CreateFunction` are missing, so you need to log in to the console and assign the policy `SCFFullAccess` to the corresponding account or `SLS_QcsRole`.

### What should I do if my sub-account has no permissions?
For more information, please see [Sub-account Permission Configuration](https://github.com/AprilJC/Serverless-Framework-Docs/blob/main/docs/%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/%E6%9D%83%E9%99%90%E9%85%8D%E7%BD%AE%E8%AF%B4%E6%98%8E.md#%E5%AD%90%E8%B4%A6%E5%8F%B7%E6%9D%83%E9%99%90%E9%85%8D%E7%BD%AE).
