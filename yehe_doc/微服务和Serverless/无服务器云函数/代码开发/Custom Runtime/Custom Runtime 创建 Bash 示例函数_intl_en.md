## Overview
This document describes how to create, package, and release a Custom Runtime cloud function to respond to the triggered event. You will learn the development process and operating mechanism of Custom Runtime.

## Directions
Before creating a Custom Runtime cloud function, you need to create a runtime boot file [bootstrap](#bootstrap) and [function file](#hsfile).

<span id="bootstrap"></span>
### Creating a bootstrap file
Bootstrap is a runtime entry bootloader. When Custom Runtime loads a function, it retrieves the file named “bootstrap” and executes the file to start Custom Runtime, which allows developers to develop runtime functions using any programming language and version. Bootstrap must:
 - Have the execute permission.
 - Be able to run in the SCF system environment (CentOS 7.6).

You can refer to the following sample code to create a bootstrap file in a command line terminal. Bash is used as an example in this document.
```
#! /bin/bash
set -euo pipefail

# Initialization - Load the function file.
source ./"$(echo $_HANDLER | cut -d. -f1).sh"

# After the initialization is completed, access the runtime API to report the readiness. 
curl -d " " -X POST -s "http://$SCF_RUNTIME_API:$SCF_RUNTIME_API_PORT/runtime/init/ready"

### Start the loop that listens to events, handles events, and pushes event handling results.
while true
do
  HEADERS="$(mktemp)"
  # Gets event data through long polling
  EVENT_DATA=$(curl -sS -LD "$HEADERS" -X GET -s "http://$SCF_RUNTIME_API:$SCF_RUNTIME_API_PORT/runtime/invocation/next")
  # Invokes a function to handle the event
  RESPONSE=$($(echo "$_HANDLER" | cut -d. -f2) "$EVENT_DATA")
  # Pushes the function handling result
  curl -X POST -s "http://$SCF_RUNTIME_API:$SCF_RUNTIME_API_PORT/runtime/invocation/response"  -d "$RESPONSE"
done
```

#### Sample description
In the preceding sample, Custom Runtime has two phases, the initialization and invocation phases. Initialization is executed only once during the cold start of a function instance. After the initialization, the invocation loop starts, which listens to events, invokes functions for handling, and pushes the handling results.

- **Initialization phase**
For more information, please refer to [Initializing function](https://intl.cloud.tencent.com/document/product/583/38129#.E5.87.BD.E6.95.B0.E5.88.9D.E5.A7.8B.E5.8C.96).
After the initialization, you need to proactively invoke the runtime API to report the readiness to SCF. The sample code is as follows: 
```
# After the initialization, access the runtime API to report the readiness of initialization.
curl -d " " -X POST -s "http://$SCF_RUNTIME_API:$SCF_RUNTIME_API_PORT/runtime/init/ready"
```
Because Custom Runtime is implemented with a custom programming language and version, a standard protocol is needed for the communication between Custom Runtime and SCF. In the current sample, SCF provides runtime APIs and built-in environment variables to Custom Runtime over HTTP. For more information, please see [Environment Variables](https://intl.cloud.tencent.com/document/product/583/32748).
 - `SCF_RUNTIME_API`: runtime API address
 - `SCF_RUNTIME_API_PORT`: runtime API port
- **Initialization logs and exceptions**
For more information, please see [Logs and exceptions](https://intl.cloud.tencent.com/document/product/583/38129#.E6.97.A5.E5.BF.97.E5.8F.8A.E5.BC.82.E5.B8.B8).
- **Invocation phase**
For more information, please see [Function invocation](https://intl.cloud.tencent.com/document/product/583/38129#.E5.87.BD.E6.95.B0.E8.B0.83.E7.94.A8).
 1. After initialization, the invocation loop starts. A function is invoked to listen to events. The sample code is as follows: 
```
# Long-poll events.
  EVENT_DATA=$(curl -sS -LD "$HEADERS" -X GET -s "http://$SCF_RUNTIME_API:$SCF_RUNTIME_API_PORT/runtime/invocation/next")
```
During the long-polling of events, do not set timeout of the GET method. Access the runtime event acquisition API (`/runtime/invocation/next`) to wait for event delivery. If you access this API repeatedly within an invocation, the same event data will be returned. The response body is `event_data`. The response header includes: 
   - `Request_Id`: request ID, identifying the request that triggers function invocation.
   - `Memory_Limit_In_Mb`: function memory limit, in MB.
   - `Time_Limit_In_Ms`: function timeout limit, in milliseconds.
 2. Based on the environment variables, response header information, and event information, construct parameters of the function and start function invocation for event handling. The sample code is as follows:
```
# Invoke a function to handle the event.
  RESPONSE=$($(echo "$_HANDLER" | cut -d. -f2) "$EVENT_DATA")
```
 3. Access the runtime invocation response API to push the function handling result. The first invocation success will be considered as the final event status, which will be locked by SCF. The pushed result cannot be changed. The sample code is as follows:
```
# Push the function handling result.
  curl -X POST -s "http://$SCF_RUNTIME_API:$SCF_RUNTIME_API_PORT/runtime/invocation/response"  -d "$RESPONSE"
```
If an error occurs during function invocation, access the runtime invocation error API to push the error message, which ends the current invocation. The first invocation result will be considered as the final event status, which will be locked by SCF. The pushed result cannot be changed. The sample code is as follows:
```
# Push the function handling error.
  curl -X POST -s "http://$SCF_RUNTIME_API:$SCF_RUNTIME_API_PORT/runtime/invocation/error"  -d "parse event error" 
```
- **Invocation logs and exception**
For more information, please see [Logs and exceptions](https://intl.cloud.tencent.com/document/product/583/38129#.E6.97.A5.E5.BF.97.E5.8F.8A.E5.BC.82.E5.B8.B82).

<span id="hsfile"></span>
### Creating a function file
>? The function file contains the implementation of function logic. The execution method and parameters can be implemented by Custom Runtime.
>
Create `index.sh` in the command line terminal.
```
function main_handler () {
  EVENT_DATA=$1
  echo "$EVENT_DATA" 1>&2;
  RESPONSE="Echoing request: '$EVENT_DATA'"
  echo $RESPONSE
}
```

## Releasing a Function
1. The following shows the directory structure after the [bootstrap](#bootstrap) and [function file](#hsfile) are created.
```
├ bootstrap
└ index.sh
```
2. Run the following command to grant execute permission on the bootstrap file:
>? Windows does not support the `chmod 755` command. Therefore, you need to run the command in Linux or Mac OS.
>
```
$ chmod 755 index.sh bootstrap
```
3. To create and release a function, you can use [Serverless Framework](#Serverless). Alternatively, you can run the following commands to generate a zip package, and use [SDK](#SDK) or [SCF Console](#KZT) to create and release the function.
```
$ zip demo.zip index.sh bootstrap
   adding: index.sh (deflated 23%)
   adding: bootstrap (deflated 46%)
```

   
<span id="Serverless"></span>
### Using Serverless Framework to create and release a function

### Creating a function

1. Install [Serverless Framework](https://intl.cloud.tencent.com/document/product/1040/37034).
2. Configure the `Serverless.yml` file in the [bootstrap](#bootstrap) directory to create the dotnet function.
```
   #Component information
   component: scf # Component name. `scf` is used as an example.
   name: ap-guangzhou_default_helloworld # Instance name.
   #Component parameters
   inputs:
     name: helloworld #Function name.
     src: ./
     description: helloworld blank template function. 
     handler: index.main_handler
     runtime: CustomRuntime
     namespace: default
     region: ap-guangzhou
     memorySize: 128
     timeout: 3
     events: 
       - apigw: 
           parameters:
             endpoints:
               - path: /
                 method: GET
```
>? For more information about the configurations of SCF components, please see [Configuration Documentation](https://github.com/serverless-components/tencent-scf/blob/master/docs/configure.md)。 
>
3. Run the `sls deploy` command to create a cloud function. A successful creation returns the following message:
```
   serverless ⚡framework
   Action: "deploy" - Stage: "dev" - App: "ap-guangzhou_default_helloworld" - Instance: "ap-guangzhou_default_helloworld"   
   functionName: helloworld
   description:  helloworld blank template function.
   namespace:    default
   runtime:      CustomRuntime
   handler:      index.main_handler
   memorySize:   128
   lastVersion:  $LATEST
   traffic:      1
   triggers: 
     apigw: 
       - http://service-xxxxxx-123456789.gz.apigw.tencentcs.com/release/   
   Full details: https://serverless.cloud.tencent.com/apps/ap-guangzhou_default_helloworld/ap-guangzhou_default_helloworld/dev   
   36s › ap-guangzhou_default_helloworld › Success
```
>? For more information, please see [SCF Component](https://intl.cloud.tencent.com/document/product/1040/33164)。

#### Invoking a function

As `events` is set to `apigw` in the `serverless.yml` file, an API gateway is created together with the function. The cloud function can be accessed over this API gateway. If a message similar to the following is returned, the access is successful.
```
Echoing request: 
'{
		"headerParameters":{},
		"headers":{
"accept":"text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9",
		"accept-encoding":"gzip, deflate",
		"accept-language":"zh-CN,zh-TW;q=0.9,zh;q=0.8,en-US;q=0.7,en;q=0.6",
		"cache-control":"max-age=259200",
		"connection":"keep-alive",
		"host":"service-eiu4aljg-1259787414.gz.apigw.tencentcs.com",
		"upgrade-insecure-requests":"1",
		"user-agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.121 Safari/537.36",
		"x-anonymous-consumer":"true",
		"x-api-requestid":"b8b69e08336bb7f3e06276c8c9******",
		"x-api-scheme":"http",
		"x-b3-traceid":"b8b69e08336bb7f3e06276c8c9******",
		"x-qualifier":"$LATEST"},
		"httpMethod":"GET",
		"path":"/",
		"pathParameters":{},
		"queryString":{},
		"queryStringParameters":{},
		"requestContext":{"httpMethod":"GET","identity":{},"path":"/",
		"serviceId":"service-xxxxx",
		"sourceIp":"10.10.10.1",
		"stage":"release"
		}
}'
```


<span id="SDK"></span>
### Using SDK to create and release a function
<span id="creat"></span>
#### Creating a function
Run the following commands to use the Python SDK of SCF to create a function named `CustomRuntime-Bash`.
```
from tencentcloud.common import credential
from tencentcloud.common.profile.client_profile import ClientProfile
from tencentcloud.common.profile.http_profile import HttpProfile
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException 
from tencentcloud.scf.v20180416 import scf_client, models 
from base64 import b64encode
try: 
    cred = credential.Credential("SecretId", "secretKey") 
    httpProfile = HttpProfile()
    httpProfile.endpoint = "scf.tencentcloudapi.com"

    clientProfile = ClientProfile()
    clientProfile.httpProfile = httpProfile
    client = scf_client.ScfClient(cred, "na-toronto", clientProfile) 

    req = models.CreateFunctionRequest()
    f = open('demo.zip', 'r')
    code = f.read()
    f.close()
    
    params = '{\"FunctionName\":\"CustomRuntime-Bash\",\"Code\":{\"ZipFile\":\"'+b64encode(code)+'\"},\"Timeout\":3,\"Runtime\":\"CustomRuntime\",\"InitTimeout\":3}'
    req.from_json_string(params)

    resp = client.CreateFunction(req) 
    print(resp.to_json_string()) 

except TencentCloudSDKException as err: 
    print(err) 
```

#### Special parameters of Custom Runtime

| Parameter | Description | 
|---------|---------|
| `"Runtime":"CustomRuntime"` | Runtime type of Custom Runtime. |
| `"InitTimeout":3` | Initialization timeout period. Custom Runtime adds a configuration of initialization timeout period. The initialization period starts from the boot-time of bootstrap and ends when the runtime API is reported ready. When the initialization period exceeds the timeout period, the execution ends and an initialization timeout error is returned. |
| `"Timeout":3` | Invocation timeout period. This parameter configures the timeout period of function invocation. The invocation period starts from the event delivery time and ends upon the time when the function pushes the handling result to the runtime API. When the invocation period exceeds the timeout period, the execution ends and an invocation timeout error is returned. |


#### Invoking a function
Run the following commands to use the Python SDK of SCF to invoke the [CustomRuntime-Bash function](#creat).
```
from tencentcloud.common import credential
from tencentcloud.common.profile.client_profile import ClientProfile
from tencentcloud.common.profile.http_profile import HttpProfile
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException 
from tencentcloud.scf.v20180416 import scf_client, models 
try: 
    cred = credential.Credential("SecretId", "secretKey") 
    httpProfile = HttpProfile()
    httpProfile.endpoint = "scf.tencentcloudapi.com"

    clientProfile = ClientProfile()
    clientProfile.httpProfile = httpProfile
    client = scf_client.ScfClient(cred, "na-toronto", clientProfile) 

    req = models.InvokeRequest()
    params = '{\"FunctionName\":\"CustomRuntime-Bash\",\"ClientContext\":\"{   \\\"key1\\\": \\\"test value 1\\\",   \\\"key2\\\": \\\"test value 2\\\" }\"}'
    req.from_json_string(params)

    resp = client.Invoke(req) 
    print(resp.to_json_string()) 

except TencentCloudSDKException as err: 
    print(err) 
```
If a message similar to the following is returned, the invocation is successful.
```
{"Result": 
    {"MemUsage": 7417***, 
    "Log": "", "RetMsg": 
    "Echoing request: '{ 
        \"key1\": \"test value 1\", 
        \"key2\": \"test value 2\" 
        }'", 
    "BillDuration": 101, 
    "FunctionRequestId": "3c32a636-****-****-****-d43214e161de", 
    "Duration": 101, 
    "ErrMsg": "", 
    "InvokeResult": 0
    }, 
    "RequestId": "3c32a636-****-****-****-d43214e161de"
}
```

<span id="KZT"></span>

### Using Console to create and release a function
#### Creating a function
1. Log in to the [SCF Console](https://console.cloud.tencent.com/scf) and click **Function Service** in the left sidebar.
2. Choose a region at the top of the **Function Service** page and click **Create** to start creating a function.
3. Set basic information of the function on the **Create Function** page and click **Next**.
    - **Function name**: Enter “CustomRuntime-Bash”.
    - **Runtime environment**: Choose **CustomRuntime**.
    - **Create Method**: Choose **Empty function**.
4. On the **Function configuration** page, set **Submitting Method** and **Function code**.
    - **Submitting Method**: Choose **Local ZIP file**.
    - **Function code**: Choose the `demo.zip`.
    - **Advanced Settings**: Expand **Advanced Settings** and set **Initialization timeout period** as well as other related parameters.
5. Click **Complete**.

#### Invoking a function
1. Log in to the [SCF Console](https://console.cloud.tencent.com/scf) and click **Function Service** in the left sidebar.
2. Choose a region at the top of the **Function Service** page, and click the function to be invoked to go to the function detail page.
3. Navigate to **Function Management** from the left sidebar and then choose the **Function code** tab.
4. Choose **Hello World event template** in **Test Event** and click **Test**.
    The execution result and logs of the invocation will be displayed on the right side of the Console.

