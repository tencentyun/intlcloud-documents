
## Tencentserverless SDK Overview
Tencentserverless is a Tencent Cloud SCF SDK that integrates SCF business flow APIs to make it easier to invoke SCF functions. It allows users to invoke a function quickly from a local system, CVM instance, container or function, eliminating the need to encapsulate APIs in a public cloud.

## Features
Tencentserverless SDK has the following features:

* It can invoke functions in a high-performance, low-latency manner.
* It enables quick invocation across functions after the required parameters are entered (it will obtain parameters in environment variables by default, such as region and secretId).
* It supports access with private network domain names.
* It supports session keep-alive.
* It supports cross-region function invocation.
* It supports native invocation methods in Python.

## Quick Start

### Chaining functions

#### Example
>
>- To chain functions in different regions, you must specify regions. For naming rules, see [Region List](https://intl.cloud.tencent.com/document/product/583/17238#Region-List).
>- If no region is specified, functions will be chained within the same region by default.
>- If no namespace is specified, `default` will be used by default.

1. Create a to-be-invoked Python function named "FuncInvoked" in the cloud in the region of **Guangzhou**. The content of the function is as follows:

```python
# -*- coding: utf8 -*-
def main_handler(event, context):
    if 'key1' in event.keys():
        print("value1 = " + event['key1'])
    if 'key2' in event.keys():
        print("value2 = " + event['key2'])
    return "Hello World from the function being invoked"  #return
```
2. Create an invoking Python function named "PythonInvokeTest" in the cloud in the region of **Chengdu**. You can edit the function as needed following two methods:
Method 1: If you do not need to invoke the function frequently, you can use the sample code below:

```python
# -*- coding: utf8 -*-
from tencentserverless.scf import Client
from tencentserverless.exception import TencentServerlessSDKException
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException

def main_handler(event, context):
    print("prepare to invoke a function!")
    
    try:
        data = scf.invoke('FuncInvoked',region="ap-guangzhou",data={"a": "b"})
        print (data)
    except TencentServerlessSDKException as e:
        print (e)
    except TencentCloudSDKException as e:
        print (e)
    except Exception as e:
        print (e)
    return "Already invoked a function!" # return
```
The output is as follows:
```shell
"Already invoked a function!"
```
Method 2: If you need to invoke the function frequently, you can connect to and trigger it via a client with the following sample code:

```python
# -*- coding: utf8 -*-
from tencentserverless.scf import Client
from tencentserverless.exception import TencentServerlessSDKException
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException

def main_handler(event, context):
    scf = Client(region="ap-guangzhou")

    print("prepare to invoke a function!")
    try:
        data = scf.invoke('FuncInvoked',data={"a": "b"})
        # data = scf.FuncInvoked(data={"a": "b"}) # To use the native invocation method in Python, you need to first perform initialization via the client
        print (data)
    except TencentServerlessSDKException as e:
        print (e)
    except TencentCloudSDKException as e:
        print (e)
    except Exception as e:
        print (e)
    return "Already invoked a function!" # return
```
The output is as follows:
```shell
"Already invoked a function!"
```


### Invoking a function locally

#### Preparing for development
- Development environment
Python 2.7 or Python 3.6 has been installed.
- Operating environment
Windows, Linux, or macOS with tencentserverless SDK installed.

>The above development preparations must be completed before functions can be invoked locally. We recommend you upload a function to the cloud after it is developed locally to debug it via chaining functions.


#### Installing via pip (recommended)
Run the following command to install tencentserverless SDK for Python.
```shell
pip install tencentserverless
```
#### Installing via source package
Go to the [GitHub code hosting page](https://github.com/tencentyun/tencent-serverless-python) to download the latest source package, decompress it, and run the following commands in sequence to install.
```shell
cd tencent-serverless-python
python setup.py install
```
#### Configuring tencentserverless SDK for Python
Run the following command to upgrade tencentserverless SDK for Python.
```shell
pip install tencentserverless -U
```
Run the following command to view the information of tencentserverless SDK for Python.
```shell
pip show tencentserverless
```

#### Example
1. Create a to-be-invoked Python function named "FuncInvoked" in the cloud in the region of **Guangzhou**. The content of the function is as follows:

```python
# -*- coding: utf8 -*-
def main_handler(event, context):
    if 'key1' in event.keys():
        print("value1 = " + event['key1'])
    if 'key2' in event.keys():
        print("value2 = " + event['key2'])
    return "Hello World from the function being invoked"  #return
```
2. Create a local file named PythonInvokeTest.py with the following content:

```python
# -*- coding: utf8 -*-
from tencentserverless.scf import Client
from tencentserverless.exception import TencentServerlessSDKException
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException

def main_handler(event, context):
    print("prepare to invoke a function!")
    scf = Client(secret_id="AKIxxxxxxxxxxxxxxxxxxxxxxggB4Sa",secret_key="3vZzxxxxxxxxxxxaeTC",region="ap-guangzhou")# Replace with your own secret_id and secret_key
    try:
        data = scf.invoke('FuncInvoked',data={"a":"b"}) 
		# data = scf.FuncInvoked(data={"a":"b"}) 
		print (data)
    except TencentServerlessSDKException as e:
        print (e)
    except TencentCloudSDKException as e:
        print (e)
    except Exception as e:
        print (e)
    return "Already invoked a function!" # return

main_handler("","")
```
>secret_id and secret_key: Secret ID and secret key of TencentCloud API. You can obtain them or create news ones by logging into the **[CAM Console](https://console.cloud.tencent.com/cam/overview)** and selecting **TencentCloud API Key** > **[API Key Management](https://console.cloud.tencent.com/cam/capi).**
>
Go to the directory where the `PythonInvokeTest.py` file is located and run the following command to view the result.
```shell
python PythonInvokeTest.py
```
The output is as follows:
```shell
prepare to invoke a function!
"Hello World form the function being invoked"
```


## API List
### API Reference
- [Client](#client) (class)
- [invoke](#invoke) (method)
- [TencentserverlessSDKException](#TencentserverlessSDKException) (class)

#### Client
**Method:**
- **\_\_init__** 

 **Parameter information:**

 <table>
	<tr>
	<th>Parameter Name</th> <th>Required</th> <th>Type</th> <th>Description</th>
	</tr>
	<tr>
	<td>region </td> 	<td>No</td> 	<td><code>String</code></td>
		<td>Region information, which is the same as the region where the function invocation resides by default. The region is Guangzhou by default for local invocation.</td>
	</tr>
	<tr>
	<td>secret_id</td> 	<td>No</td> 	<td><code>String</code></td>
		<td>secret_id, which is obtained from the function's environment variable by default <b>and is required for local invocation.</b></td>
	</tr>
	<tr>
	<td>secret_key</td> 	<td>No</td> 	<td><code>String</code></td>
		<td>secret_key, which is obtained from the function's environment variable by default <b>and is required for local invocation.</b></td>
	</tr>
	<tr>
		<td>token</td> 	<td>No</td> 	<td><code>String</code></td>
		<td>Token, which is obtained from the function's environment variable by default.</td>
	</tr>
</table>


- **invoke**

 **Parameter information:**

 <table>
	<tr>
	<th>Parameter Name</th> <th>Required</th> <th>Type</th> <th>Description</th>
	</tr>
	<tr>
		<td>function_name</td> <td>Yes</td> <td><code>String</code></td> 
		<td>Function name.</td>
	</tr>
	<tr>
		<td>qualifier</td> <td>No</td> <td><code>String</code></td>
		<td>Function version. Default value: $LATEST.</td>
	</tr>
	<tr>
		<td>data</td> <td>No</td> <td><code>Object</code></td>
		<td>Input parameter for function execution, which must be an object that can be converted by json.dumps.</td>
	</tr>
	<tr>
		<td>namespace</td> <td>No</td> <td><code>String</code></td>
		<td>Namespace. Default value: default.</td>
	</tr>
</table>


#### invoke
This is used to invoke a function. Currently, only sync invocation is supported.

**Parameter information:**

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| region | No | `String` | Region information, which is the same as the region where function invocation resides by default. The region is Guangzhou by default for local invocation. |
| secret_id | No | `String` | secret_id, which is obtained from the function's environment variable by default **and is required for local invocation**. |
| secret_key | No | `String` | secret_key, which is obtained from the function's environment variable by default **and is required for local invocation**. |
| token | No | `String` | Token, which is obtained from the function's environment variable by default. |
| function_name | Yes | `String` | Function name. |
| qualifier | No | `String` | Function version. Default value: $LATEST. |
| data | No | `String` | Input parameter for function execution, which must be an object that can be converted by json.dumps. |
| namespace | No | `String` | Namespace. Default value: default. |

<span id="TencentserverlessSDKException"></span>
#### TencentserverlessSDKException
**Attributes:**
- [**code**]
- [**message**]
- [**request_id**]
- [**response**]
- [**stack_trace**]

**Methods and descriptions:**

| Method Name | Description |
|---------|---------|
| get_code | Returns the error information|
| get_message | Returns the error information|
|get_request_id |Returns request_id information |
| get_response | Returns response information |
| get_stack_trace | Returns stack_trace information |

