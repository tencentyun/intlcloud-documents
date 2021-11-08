

## Overview

SCF upgraded its log service on January 29, 2021 and was fully connected to Tencent Cloud CLS. The functions created before are gradually migrated by regions. For more information, please see [SCF Log Service Change Notification](https://intl.cloud.tencent.com/zh/document/product/583/39328).

SCF provides two log query methods for functions created after January 29, 2021 and the migrated functions:

- Console: the CLS search and analysis page is embedded in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). On this page, you can search for logs by using query syntax to combine keywords.
- API: you can query function invocation logs by calling the CLS log search API.

> ! 
> - For the structure of logs written by SCF to CLS, please see Log Structure Description.
> - If your function was created before January 29, 2021 and has not been migrated, but you need to use more log analysis features, please see [Log Delivery Configuration (Legacy)](https://intl.cloud.tencent.com/zh/document/product/583/34876) to deliver function invocation logs to Cloud Log Service (CLS).



## Directions

### Query in console

You can use the advanced search feature in the following steps:

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and select **Function Service** on the left sidebar.
2. On the **Function Service** list page, select the name of the function for which to search for logs to enter the **Function Management** page.
3. On the **Function Management** page, select **Log Query** > **Advanced Retrieval**.
4. On the **Advanced Retrieval** page, you can search for logs by using keyword or using query syntax to combine keyword. **For more information on syntax rules, please see [Syntax and Rules](https://intl.cloud.tencent.com/document/product/614/30439).**
5. After configuring the search criteria, you can click **Search and Analysis** on the right, and the results will be returned as shown below:
   ![](https://main.qcloudimg.com/raw/f0f51eecc4e0e034875a5834cb2c4862.png)


### Query via API

The following describes how to get and enter relevant SCF parameters for the CLS log search API.

#### TopicId

1. `TopicId` is the ID of the CLS log topic to which function logs are delivered. Click the **Log Topic** link on the **Function Configuration** page of the target function as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/9db203dd76dff17cde3ee5615cd8d6fd.png)
2. You will be redirected to the CLS console, where you can get the log topic ID as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/11617b65054a1b2b9fa37df516f0f6aa.png)
>?You can also get the `TopicId` in `ClsTopicId` by calling the [GetFunction](https://intl.cloud.tencent.com/document/product/583/18584) API.


#### Query

> !
> - For the meanings of fields in the returned result, please see Log Structure Description.
> - SCF invocation logs are reported in real time. If a request exists but its returned value is empty, it may be because that the function execution has not been completed yet, so the log has not been reported to CLS. Please search again after the function is executed.


#### Getting all invocation logs of a function

Take the function `hello-scf` in the `default` namespace as an example:

```SQL
SCF_Namespace:"default" AND SCF_FunctionName:"hello-scf"
```


#### Getting the invocation logs of a request (RequestId)

Take the request `09c346d3-8417-49c5-8569-xxxxxxxxxxxx` as an example:

```SQL
SCF_RequestId:"09c346d3-8417-49c5-8569-xxxxxxxxxxxx"
```


#### Getting the execution result of a request (RequestId)

The execution result includes the request start time, execution result, execution duration, memory usage, and log level. Take the request `09c346d3-8417-49c5-8569-xxxxxxxxxxxx` as an example:

```SQL
SCF_RequestId:"09c346d3-8417-49c5-8569-xxxxxxxxxxxx" AND SCF_Type:Platform AND SCF_Message:Report*
```

#### Getting the returned value of a request (RequestId)

Take the request `09c346d3-8417-49c5-8569-xxxxxxxxxxxx` as an example:

```SQL
SCF_RequestId:"09c346d3-8417-49c5-8569-xxxxxxxxxxxx" AND SCF_Type:Platform AND SCF_Message:Response*
```

> ! 
> - After SCF logs are connected to CLS, returned data will be retained for functions, which will be written to the `SCF_Message` field in the format of `Response RequestId:xxx RetMsg:xxx` in CLS.
> - The value of `SCF_Message` is limited to 8 KB in length, and excessive parts will be truncated.


#### Getting the list of requests for a function over a period of time

Take the function `hello-scf` with the alias `$DEFAULT` on version `1` in the `default` namespace as an example:

- Get the list of failed requests due to internal errors:
```SQL
SCF_Type:Platform AND SCF_Message:Report* | select SCF_RequestId as requestId, SCF_RetryNum as retryNum,SCF_StartTime as startTime where SCF_FunctionName='hello-scf' and SCF_Namespace='default' and SCF_Qualifier='1' and SCF_Alias:'$DEFAULT' and SCF_StatusCode = 500 order by startTime desc
```
- Get the list of requests that took more than 3 seconds to execute:
```SQL
SCF_Type:Platform AND SCF_Message:Report* | select SCF_RequestId as requestId, SCF_RetryNum as retryNum,SCF_StartTime as startTime where SCF_FunctionName='hello-scf' and SCF_Namespace='default' and SCF_Qualifier='1' and SCF_Alias:'$DEFAULT' and SCF_Duration>3000 order by startTime desc
```
