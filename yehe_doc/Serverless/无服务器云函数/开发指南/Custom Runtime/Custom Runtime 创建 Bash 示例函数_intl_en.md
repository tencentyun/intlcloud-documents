## Overview
This document describes how to create, package, and publish a Custom Runtime function to respond to triggering events. It also details the Custom Runtime development process and operating mechanism.

## Directions
Before creating a Custom Runtime function, you need to create a runtime [bootstrap file](#bootstrap) and a [function processing file](#hsfile) first.

### Creating bootstrap file<span id="bootstrap"></span>
Bootstrap is a runtime entry bootstrap file. When loading a function, Custom Runtime will search for the file named after the bootstrap and run it to start Custom Runtime. Custom Runtime supports function development and execution in any programming language on any version, which is customized by yourself mainly based on the bootstrap file. The bootstrap should meet the following requirements:
 - It should have the executable permission.
 - It can run on SCF's operating system (CentOS 7.6).

You can create a bootstrap file on the command line by referring to the following sample code, which is implemented based on Bash:
```
#! /bin/bash
set -euo pipefail

# Initialization - load the function file
source ./"$(echo $_HANDLER | cut -d. -f1).sh"

# The initialization is completed. Access the runtime API to report the ready status
curl -d " " -X POST -s "http://$SCF_RUNTIME_API:$SCF_RUNTIME_API_PORT/runtime/init/ready"

### Listening on and invoking function to process event in loop
while true
do
  HEADERS="$(mktemp)"
  # Get events through long polling
  EVENT_DATA=$(curl -sS -LD "$HEADERS" -X GET -s "http://$SCF_RUNTIME_API:$SCF_RUNTIME_API_PORT/runtime/invocation/next")
  # Invoke the function to process the event
  RESPONSE=$($(echo "$_HANDLER" | cut -d. -f2) "$EVENT_DATA")
  # Push the processing result of the function
  curl -X POST -s "http://$SCF_RUNTIME_API:$SCF_RUNTIME_API_PORT/runtime/invocation/response"  -d "$RESPONSE"
done
```

#### Sample file description
In the sample, a function runtime of Custom Runtime is divided into initialization stage and invocation stage. Initialization is executed only once during the cold start of the function execution instance. After the initialization is completed, loop invocation will be implemented to listen on events and invoke the function to process them.

- **Initialization**
For more information on initialization, please see [Function Initialization](https://intl.cloud.tencent.com/document/product/583/38129#.E5.87.BD.E6.95.B0.E5.88.9D.E5.A7.8B.E5.8C.96).
After the initialization, you need to proactively call the initialization readiness API of the runtime to inform SCF. The sample code is as follows:
```
# The initialization is completed. Access the runtime API to report the ready status
curl -d " " -X POST -s "http://$SCF_RUNTIME_API:$SCF_RUNTIME_API_PORT/runtime/init/ready"
```
Here, as Custom Runtime is implemented with your custom programming language and version, it needs to communicate with SCF over a standard protocol. In this example, SCF provides runtime APIs and built-in environment variables over the HTTP protocol. For more information on environment variables, please see [Environment Variables](https://intl.cloud.tencent.com/document/product/583/32748).
 - `SCF_RUNTIME_API`: runtime API address.
 - `SCF_RUNTIME_API_PORT`: runtime API port.
- **Initialization logs and exceptions**
For more information on initialization logs and exception messages, please see [Logs and Exceptions](https://intl.cloud.tencent.com/document/product/583/38129#.E6.97.A5.E5.BF.97.E5.8F.8A.E5.BC.82.E5.B8.B8).
- **Invocation**
For more information on invocation, please see [Function Invocation](https://intl.cloud.tencent.com/document/product/583/38129#.E5.87.BD.E6.95.B0.E8.B0.83.E7.94.A8).
 1. After initialization is completed, the function will be invoked in a loop to listen on and process events. The sample code is as follows:
```
# Get events through long polling
  EVENT_DATA=$(curl -sS -LD "$HEADERS" -X GET -s "http://$SCF_RUNTIME_API:$SCF_RUNTIME_API_PORT/runtime/invocation/next")
```
Do not set the timeout period for event acquisition through long polling. When accessing the event acquisition API of the runtime, block wait event distribution. If this API is repeatedly accessed during an invocation, the same event data will be returned. The response body is the event data (`event_data`), and the response header contains the following information:
   - Request_Id: request ID, which identifies the request triggering function invocation.
   - Memory_Limit_In_Mb: maximum function memory in MB.
   - Time_Limit_In_Ms: function timeout period in milliseconds.
 2. Construct function invocation parameters based on the environment variables, required information in the response header, and event information, and call the function processing program. The sample code is as follows:
```
# Invoke the function to process the event
  RESPONSE=$($(echo "$_HANDLER" | cut -d. -f2) "$EVENT_DATA")
```
 3. Access the runtime response result API to push the processing result of the function. The first invocation success will be considered as the final event status, which will be locked by SCF, and the result cannot be changed after push. The sample code is as follows:
```
# Push the processing result of the function
  curl -X POST -s "http://$SCF_RUNTIME_API:$SCF_RUNTIME_API_PORT/runtime/invocation/response"  -d "$RESPONSE"
```
If an error occurs during function invocation, you can access the runtime API to call the error API so as to push the error message. After the current invocation ends, the first invocation will be considered as the final event status, which will be locked by SCF, and the result will not be changed in subsequent pushes. The sample code is as follows:
```
# Push the processing error of the function
  curl -X POST -s "http://$SCF_RUNTIME_API:$SCF_RUNTIME_API_PORT/runtime/invocation/error"  -d "parse event error" 
```
- **Invocation logs and exceptions**
For more information on invocation logs and exception messages, please see [Logs and Exceptions](https://intl.cloud.tencent.com/document/product/583/38129#.E6.97.A5.E5.BF.97.E5.8F.8A.E5.BC.82.E5.B8.B82).


### Creating function processing file<span id="hsfile"></span>
>? The function processing file contains the specific implementation of the function logic, and its execution method and parameters can be customized through the runtime.
>
Create `index.sh` on the command line.
```
function main_handler () {
  EVENT_DATA=$1
  echo "$EVENT_DATA" 1>&2;
  RESPONSE="Echoing request: '$EVENT_DATA'"
  echo $RESPONSE
}
```

## Publishing Function
1. After the [bootstrap](#bootstrap) file and [function file](#hsfile) are successfully created, the directory structure is as follows:
```
├ bootstrap
└ index.sh
```
2. Run the following command to grant the execution permission of the file and add it to the ZIP package:
```
$ chmod 755 index.sh bootstrap
$ zip demo.zip index.sh bootstrap
  adding: index.sh (deflated 23%)
  adding: bootstrap (deflated 46%)
```
3. After preparing the deployment package, you can create and publish the function through the [SDK](#SDK) or in the [SCF Console](#KZT).

### Using SDK to create and publish function<span id="SDK"></span>
#### Creating function<span id="creat"></span>
Run the following command to create a function named `CustomRuntime-Bash` with the SCF SDK for Python:
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

#### Special Custom Runtime parameter description

| Parameter Type | Description | 
|---------|---------|
| `"Runtime":"CustomRuntime"` | Runtime type of Custom Runtime. |
| `"InitTimeout":3` | Initialization timeout period. For initialization, the timeout control configuration item is added to Custom Runtime, and the timeout period starts at the time when the bootstrap is started and ends at the time when the ready status of the runtime API is reported. After the timeout period elapses, the execution will be ended, and an initialization timeout error will be returned. |
| `"Timeout":3` | Invocation timeout period. In this timeout control configuration item, the timeout period starts at the time when the event is distributed and ends at the time when the function completes event processing and pushes the result to the runtime API. After the timeout period elapses, the execution will be ended, and an invocation timeout error will be returned. |


#### Invoking function
Run the following command to invoke the created [CustomRuntime-Bash function](#creat) with the SCF SDK for Python:
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
If information similar to the following is returned, the invocation is successful.
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
### Creating and publishing function in console<span id="KZT"></span>
#### Creating function
1. Log in to the [SCF Console](https://console.cloud.tencent.com/scf) and click **Function Service** on the left sidebar.
2. Select the region where to create a function at the top of the "Functions" page and click **Create** to enter the function creation process.
3. Enter the basic information of the function on the "Create Function" page and click **Next** as shown below:
![](https://main.qcloudimg.com/raw/963dcca09bc987d7ceaaa0a157e633f6.png)
    - **Function name**: enter "CustomRuntime-Bash".
    - **Runtime environment**: select "CustomRuntime".
    - **Create Method**: select **Empty function**.
4. On the "Function configuration" page, set "Submitting Method" and "Function code" as shown below:
![](https://main.qcloudimg.com/raw/d4d1a942bc082166872916d26605d988.png)
    - **Submitting Method**: select "Local ZIP file".
    - **Function code**: select the `demo.zip` package.
    - Advanced Settings: expand the configuration item and set "Initialization Timeout Period" and other relevant parameters.
5. Click **Complete** to complete function creation.

#### Invoking function
1. Log in to the [SCF Console](https://console.cloud.tencent.com/scf) and click **Function Service** on the left sidebar.
2. Select the region where to invoke a function at the top of the "Function Service" page and click the target function on the list page to enter the function details page.
3. Select **Function Management** on the left and select the **Function code** tab on the "Function Management" page as shown below:
![](https://main.qcloudimg.com/raw/7ba11b77d4198b2eddc98635114a7e48.png)
4. In the test templates of "Test Event", select "Hello World event template" and click **Test** as shown below:
![](https://main.qcloudimg.com/raw/1693c906f23e89e21716f6aed0da9f6e.png)
    The invocation execution result and log will be displayed on the right in the console as shown below:
![](https://main.qcloudimg.com/raw/6e8c639e89451a4ac302531659282d3f.png)

