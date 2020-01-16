A function can be queried in the console or through TCCLI.

## Viewing a Function in the Console
1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and select **Functions** on the left.
2. Select the region for which to view functions at the top. In the function list, you can view all the functions in the specified region.
4. The list page includes the function name, monitoring information, function runtime environment, creation time, and modification time.
5. Click the function to enter the details page. It includes the following tabs.
 * Function Configuration: It displays the basic configuration of the function, including function name, runtime environment, configured memory, timeout period, function description, network configuration, and environment variable configuration information.
 * Function Code: It displays the editable function code, execution method, and function submission method. You can test run the function and modify function testing templates on this tab, which displays return values, logs, and execution information of the test runs.
 * Triggers: It displays the configured triggers for the function, and you can configure a trigger on this tab.
 * Logs: It displays the function execution logs, where you can filter logs by certain criteria for display.
 * Monitoring: It displays function execution monitoring information.

## Getting Function Information Through TCCLI
Before starting, you need to install and configure TCCLI by following the instructions in [TCCLI Installation and Configuration](https://intl.cloud.tencent.com/document/product/1013/33463).
The function information can be obtained using the `tccli scf ListFunctions` and `tccli scf GetFunction` commands.

### Getting Function List
The function list can be obtained using the `tccli scf ListFunctions` command. You can use parameters such as `Order`, `Orderby`, `Offset`, `Limit`, or `SearchKey` to filter, sort, or control quantity of the functions.
The sample below gets the function list.
```
$ tccli scf ListFunctions --Limit 3
{
    "TotalCount": 73, 
    "Functions": [
        {
            "ModTime": "2018-09-07 12:10:22", 
            "FunctionName": "testgowin", 
            "AddTime": "2018-09-07 11:59:48", 
            "Namespace": "default", 
            "Runtime": "Go1", 
            "FunctionId": "lam-f7l9o7c6"
        }, 
        {
            "ModTime": "2018-09-06 21:36:40", 
            "FunctionName": "testjava", 
            "AddTime": "2018-09-06 21:36:40", 
            "Namespace": "default", 
            "Runtime": "Java8", 
            "FunctionId": "lam-9hx5q1po"
        }, 
        {
            "ModTime": "2018-09-06 15:29:40", 
            "FunctionName": "testclifunc", 
            "AddTime": "2018-09-05 18:34:32", 
            "Namespace": "default", 
            "Runtime": "Python2.7", 
            "FunctionId": "lam-4ojdz7nq"
        }
    ], 
    "RequestId": "b56181f0-9739-4ed0-8a5d-3295fa9d9025"
}

```

### Getting Function Details
The function details can be obtained using the `tccli scf GetFunction` command, where `FunctionName` is a required parameter indicating the name of the function to be fetched. If the `ShowCode` parameter is used, the entry file code can be outputted.
The sample below gets the function details.
```
$ tccli scf GetFunction --FunctionName testclifunc
{
    "ModTime": "2018-09-06 15:29:40", 
    "CodeError": "", 
    "FunctionName": "testclifunc", 
    "VpcConfig": {
        "SubnetId": "", 
        "VpcId": ""
    }, 
    "Triggers": [
        {
            "ModTime": "2018-09-06 15:47:05", 
            "TriggerDesc": "{\"event\":\"cos:ObjectCreated:*\"}", 
            "Type": "cos", 
            "TriggerName": "api-document-sdk-1253970226.cos.ap-guangzhou.myqcloud.com", 
            "AddTime": "2018-09-06 15:47:05"
        }
    ], 
    "Timeout": 3, 
    "MemorySize": 128, 
    "UseGpu": "FALSE", 
    "CodeSize": 868, 
    "Environment": {
        "Variables": []
    }, 
    "Namespace": "default", 
    "Handler": "index.main", 
    "Role": "", 
    "RequestId": "13232aa6-946c-45ee-9f0f-3c60147d8498", 
    "CodeResult": "", 
    "ErrNo": 0, 
    "Description": "", 
    "Runtime": "Python2.7", 
    "FunctionVersion": "$LATEST", 
    "CodeInfo": ""
}

$ tccli scf GetFunction --FunctionName testclifunc --ShowCode TRUE
{
    "ModTime": "2018-09-06 15:29:40", 
    "CodeError": "", 
    "FunctionName": "testclifunc", 
    "VpcConfig": {
        "SubnetId": "", 
        "VpcId": ""
    }, 
    "Triggers": [
        {
            "ModTime": "2018-09-06 15:47:05", 
            "TriggerDesc": "{\"event\":\"cos:ObjectCreated:*\"}", 
            "Type": "cos", 
            "TriggerName": "api-document-sdk-1253970226.cos.ap-guangzhou.myqcloud.com", 
            "AddTime": "2018-09-06 15:47:05"
        }
    ], 
    "Timeout": 3, 
    "MemorySize": 128, 
    "UseGpu": "FALSE", 
    "CodeSize": 868, 
    "Environment": {
        "Variables": []
    }, 
    "Namespace": "default", 
    "Handler": "index.main", 
    "Role": "", 
    "RequestId": "3025741a-e244-470d-8046-c794c8d9bccc", 
    "CodeResult": "success", 
    "ErrNo": 0, 
    "Description": "", 
    "Runtime": "Python2.7", 
    "FunctionVersion": "$LATEST", 
    "CodeInfo": "# -*- coding: utf8 -*-\nimport json\ndef main_handler(event, context):\n    print(\"Received event: \" + json.dumps(event, indent = 2)) \n    print(\"Received context: \" + str(context))\n    print(\"Hello world\")\n    return(\"Hello World\")"
}


```
