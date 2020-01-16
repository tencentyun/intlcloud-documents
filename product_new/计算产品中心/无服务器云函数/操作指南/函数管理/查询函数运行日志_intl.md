Function execution logs can be queried on the console or through TCCLI, and many filtering methods can be used to get the desired logs.

## Querying Function Execution Logs in the Console
1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and select Functions on the left.
2. Select the region for which to view functions at the top. Click the name of a function in the function list to enter the function details page.
4. Open the function log tab to query the function execution logs. You can view all logs, success logs, and failure logs by choosing the function execution result at the top left. Logs with the specified request ID can be queried in the query window at the top right.

## Querying Function Execution Logs Through TCCLI
Before starting, you need to install and configure TCCLI by following the instructions in [TCCLI Installation and Configuration](https://intl.cloud.tencent.com/document/product/1013/33463).
Function execution logs can be queried using the `tccli scf GetFunctionLogs` command, and parameters such as `Order`, `Orderby`, `Offset`, `Limit`, `Filter`, `FunctionRequestId`, `StartTime`, and `EndTime` can be used to filter, sort, control quantity of, and exactly query the logs.

```
$ tccli scf GetFunctionLogs --FunctionName testclifunc --Filter '{"RetCode":"not0"}'
{
    "TotalCount": 7, 
    "Data": [
        {
            "MemUsage": 262144, 
            "RetCode": 1, 
            "RetMsg": "'module' object has no attribute 'main'", 
            "Log": "", 
            "BillDuration": 100, 
            "InvokeFinished": 1, 
            "RequestId": "1610407c-b1a8-11e8-b879-525400c7c826", 
            "StartTime": "2018-09-06 15:40:11", 
            "Duration": 0.686, 
            "FunctionName": "testclifunc"
        }
    ], 
    "RequestId": "777efde3-bb38-420e-bced-e558ca856976"
}


$ tccli scf GetFunctionLogs --FunctionName testclifunc --Limit 3
{
    "TotalCount": 7, 
    "Data": [
        {
            "MemUsage": 126976, 
            "RetCode": 0, 
            "RetMsg": "{\"key2\": \"test value 2\", \"key1\": \"test value 1\"}", 
            "Log": "hello world\n{'key2': 'test value 2', 'key1': 'test value 1'}\n", 
            "BillDuration": 100, 
            "InvokeFinished": 1, 
            "RequestId": "ad97ab22-b56a-11e8-b955-525400c7c826", 
            "StartTime": "2018-09-11 10:30:41", 
            "Duration": 0.783, 
            "FunctionName": "testclifunc"
        }, 
        {
            "MemUsage": 3579904, 
            "RetCode": 0, 
            "RetMsg": "{\"key2\": \"test value 2\", \"key1\": \"test value 1\"}", 
            "Log": "hello world\n{'key2': 'test value 2', 'key1': 'test value 1'}\n", 
            "BillDuration": 100, 
            "InvokeFinished": 1, 
            "RequestId": "ab989c45-b56a-11e8-b787-5254001df6c6", 
            "StartTime": "2018-09-11 10:30:38", 
            "Duration": 0.824, 
            "FunctionName": "testclifunc"
        }, 
        {
            "MemUsage": 126976, 
            "RetCode": 0, 
            "RetMsg": "{\"test\": \"value\"}", 
            "Log": "hello world\n{'test': 'value'}\n", 
            "BillDuration": 100, 
            "InvokeFinished": 1, 
            "RequestId": "ba54a7cc-b569-11e8-b955-525400c7c826", 
            "StartTime": "2018-09-11 10:23:53", 
            "Duration": 1.049, 
            "FunctionName": "testclifunc"
        }
    ], 
    "RequestId": "eee1f44f-2422-49a8-b300-b93c4304ba26"
}

```
