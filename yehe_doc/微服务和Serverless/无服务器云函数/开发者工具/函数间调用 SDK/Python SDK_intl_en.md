## Tencentserverless SDK Overview

Tencentserverless is a Tencent Cloud SCF SDK that integrates SCF business flow APIs to make it easier to invoke SCF functions. It allows users to invoke a function quickly from a local system, CVM instance, container or function, eliminating the need to encapsulate APIs in a public cloud.

## Features

Tencentserverless SDK has the following features:

* Invokes functions in a high-performance, low-latency manner
* Enables quick invocation across functions after the required parameters are entered (it will obtain parameters in environment variables by default, such as `region` and `SecretId`).
* Supports access with private network domain names.
* Supports session keep-alive.
* Supports cross-region function chaining.
* Supports native invocation methods in Python.

## Quick Start

### Mutual function invocation

#### Samples

>!
>
>- To make functions in different regions invoke each other, you need to specify the region. For the naming rules, please see [Region List](https://intl.cloud.tencent.com/zh/document/api/583/17238).
>- If no region is specified, intra-region mutual function invocation will be used by default.
>- If no namespace is specified, `default` will be used by default.

1. Create an invoked Python function in the cloud named `FuncInvoked` in the **Guangzhou** region with the following content:
``` python
# -*- coding: utf8 -*-

def main_handler(event, context):
	if 'key1' in event.keys():
		print("value1 = " + event['key1'])
	if 'key2' in event.keys():
		print("value2 = " + event['key2'])
	return "Hello World from the function being invoked"  #return

```

2. Create an invoking Python function in the cloud named `PythonInvokeTest` in the **Chengdu** region. You can edit it as needed in the following two methods.

 - Method 1. If you don't need to invoke the function frequently, you can use the following sample code:
<dx-codeblock>
:::  python
from tencentserverless import scf 
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

:::
</dx-codeblock>
The output is as follows:
```shell
"Already invoked a function!"
```

 - Method 2. If you need to invoke the function frequently, you can choose to connect and trigger it through `Client` by using the following sample code:
<dx-codeblock>
:::  python
# -*- coding: utf8 -*-

from tencentserverless import scf 
from tencentserverless.scf import Client
from tencentserverless.exception import TencentServerlessSDKException
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException

def main_handler(event, context):
	#scf = Client(region="ap-guangzhou") # To use this method to establish a `Client` connection, enable the "execution role" feature in the function configuration and select an execution role with the function invocation permission.
	scf = Client(secret_id="AKIxxxxxxxxxxxxxxxxxxxxxxggB4Sa",secret_key="3vZzxxxxxxxxxxxaeTC",region="ap-guangzhou",token=" ")# To use this method to establish a `Client` connection, replace `secret_id` and `secret_key` in the sample code with your actual `secret_id` and `secret_key`. This key pair needs to contain the function invocation permission.
	print("prepare to invoke a function!")
	try:
    	data = scf.invoke('FuncInvoked',data={"a": "b"})
    	# data = scf.FuncInvoked(data={"a": "b"}) # To use Python's native invocation method, perform initialization through `Client` first.
    	print (data)
	except TencentServerlessSDKException as e:
    	print (e)
	except TencentCloudSDKException as e:
    	print (e)
	except Exception as e:
    	print (e)
	return "Already invoked a function!" # return
:::
</dx-codeblock>
The output is as follows:
```shell
"Already invoked a function!"
```
>! `secret_id` and `secret_key`: TencentCloud API key ID and key, which can be obtained or created in **TencentCloud API Key** >  **[API Key Management](https://console.cloud.tencent.com/cam/capi)** in the **[CAM console](https://console.cloud.tencent.com/cam/overview)**.


### Local function invocation

#### Preparations for development

- Development environment
  Python 2.7 or Python 3.6 has been installed.
- Running environment
  Windows, Linux, or macOS with Tencentserverless SDK installed.

>? For local function invocation, you must complete the above preparations. We recommend you develop the function locally and then upload it to the cloud and use mutual function invocation for debugging.



#### Installation through pip (recommended)

Run the following command to install Tencentserverless SDK for Python.

```shell
pip install tencentserverless
```




#### Installation through source package

Go to [GitHub](https://github.com/tencentyun/tencent-serverless-python) to download the latest source package and install it by running the following commands after decompression.

```shell
cd tencent-serverless-python
python setup.py install
```



#### Configuring Tencentserverless SDK for Python

Run the following command to upgrade Tencentserverless SDK for Python.

```shell
pip install tencentserverless -U
```

Run the following command to view the information of Tencentserverless SDK for Python.

```shell
pip show tencentserverless
```

#### Samples

1. Create an invoked Python function in the cloud named `FuncInvoked` in the **Guangzhou** region with the following content:
``` python
# -*- coding: utf8 -*-

def main_handler(event, context):
	if 'key1' in event.keys():
		print("value1 = " + event['key1'])
	if 'key2' in event.keys():
		print("value2 = " + event['key2'])
	return "Hello World from the function being invoked"  #return
```

2. Create a local file named `PythonInvokeTest.py` with the following content:
``` python
# -*- coding: utf8 -*-

from tencentserverless import scf 
from tencentserverless.scf import Client
from tencentserverless.exception import TencentServerlessSDKException
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException

def main_handler(event, context):
	print("prepare to invoke a function!")
	scf = Client(secret_id="AKIxxxxxxxxxxxxxxxxxxxxxxggB4Sa",secret_key="3vZzxxxxxxxxxxxaeTC",region="ap-guangzhou",token=" ")# Replace with your own `secret_id` and `secret_key`
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

Go to the directory where the `PythonInvokeTest.py` file is located and run the following command to view the result.
```python
python PythonInvokeTest.py
```

The output is as follows:
```shell
prepare to invoke a function!"Hello World form the function being invoked"
```

   

## API List

### API Reference

- [Client](#client) (class)
- [invoke](#invoke) (method)
- [TencentserverlessSDKException](#TencentserverlessSDKException) (class)

#### Client

#### Method

- **\_\_init__** 

 **Parameter information:**

 <table>
	<tr>
	<th>Parameter Name</th> <th>Required</th> <th>Type</th> <th>Description</th>
	</tr>
	<tr>
	<td>region </td> 	<td>No</td> 	<td><code>String</code></td>
		<td>Region, which is the same as the region of the function invoking the API and is Guangzhou for local invocations by default.</td>
	</tr>
	<tr>
	<td>secret_id</td> 	<td>No</td> 	<td><code>String</code></td>
		<td>User `SecretId`, which is obtained from the function's environment variable by default and is <b>required for local debugging</b>.</td>
	</tr>
	<tr>
	<td>secret_key</td> 	<td>No</td> 	<td><code>String</code></td>
		<td>User `SecretKey`, which is obtained from the function's environment variable by default and is <b>required for local debugging.</b></td>
	</tr>
	<tr>
		<td>token</td> 	<td>No</td> 	<td><code>String</code></td>
		<td>User `token`, which is obtained from the function's environment variable by default.</td>
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
		<td>Input parameter for function execution, which must be an object that can be processed by `json.dumps`.</td>
	</tr>
	<tr>
		<td>namespace</td> <td>No</td> <td><code>String</code></td>
		<td>Namespace. Default value: default.</td>
	</tr>
</table>




#### invoke

This is used to invoke a function. Currently, only sync invocation is supported.

**Parameter information:**

| Parameter | Required | Type | Description |
| ------------- | -------- | -------- | ------------------------------------------------------------ |
| region        | No       | `String` | Region, which is the same as the region of the function invoking the API and is Guangzhou for local invocations by default. |
| secret_id     | No       | `String` | User `SecretId`, which is obtained from the function's environment variable by default and is **required for local debugging**. |
| secret_key    | No       | `String` | User `SecretKey`, which is obtained from the function's environment variable by default and is **required for local debugging**. |
| token         | No       | `String` | User `token`, which is obtained from the function's environment variable by default.                     |
| function_name | Yes       | `String` | Function name.                                                   |
| qualifier     | No       | `String` | Function version. Default value: $LATEST.                                   |
| data          | No       | `String` | Input parameter for function execution, which must be an object that can be processed by `json.dumps`.                 |
| namespace     | No       | `String` | Namespace. Default value: default.                                   |

[](id:TencentserverlessSDKException)

#### TencentserverlessSDKException

**Attributes:**

- [**code**]
- [**message**]
- [**request_id**]
- [**response**]
- [**stack_trace**]

**Methods and descriptions:**

| Method Name | Description |
| --------------- | --------------------- |
| get_code        | Returns error code |
| get_message     | Returns error message          |
| get_request_id  | Returns `RequestId`   |
| get_response    | Returns `response`    |
| get_stack_trace | Returns `stack_trace` |
