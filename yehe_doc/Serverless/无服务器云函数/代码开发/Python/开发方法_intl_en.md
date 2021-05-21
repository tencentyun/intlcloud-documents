## Function Form

The Python function form is generally as follows:

```python
import json

def main_handler(event, context):
    print("Received event: " + json.dumps(event, indent = 2)) 
    print("Received context: " + str(context))
    return("Hello World")
```

## Execution Method

An execution method should be specified when each SCF function is created. The execution method of the Python programming language is similar to `index.main_handler`, where `index` refers to the `index.py` entry file, and `main_handler` refers to the `main_handler` entry function. When submitting the zip code package by uploading a local zip package or uploading it through COS, the root directory of the package should contain the specified entry file and the file should contain the specified entry function. The filename and function name should match those entered in the execution method to ensure successful execution.

## Input Parameters

The input parameters in the Python environment include event and context, both of which are of the Python dict type.

- event: this parameter is used to pass the trigger event data.
- context: this parameter is used to pass runtime information to your handler.

The event parameter varies with trigger or event source. For more information on its data structure, see [Trigger Overview](https://intl.cloud.tencent.com/document/product/583/9705).


## Response

Your handler can use `return` to return a value. The return value will be handled differently depending on the function invocation type.

In the Python environment, a serializable object such as `dict` object can be directly returned:

```python
def main_handler(event, context):
    resp = {
        "isBase64Encoded": false,
        "statusCode": 200,
        "headers": {"Content-Type":"text/html","Key":["value1","value2","value3"]},
        "body": "<html><body><h1>Heading</h1><p>Paragraph.</p></body></html>"
    }
    return(resp)
```

Two methods are available to return values:
- **Sync invocation**: the return value of a sync invocation will be serialized in JSON and returned to the caller for subsequent processing. The function testing in the console is sync invocation, which can capture the function’s return value and display it after the invocation is completed.
- **Async invocation**: the return value of an async invocation will be discarded, since the invocation method responds right after the function is triggered, without waiting for function execution to complete.

>? The return value of both sync and async invocations will be recorded in the function logs.

## Exception Handling

You can throw an exception using `raise Exception` inside the function.

- If the exception is captured and handled before returning without being thrown outside, the function is considered to have been executed. In this case, information specified in the entry function’s `return` will be returned.
The following sample codes show that the function is successfully executed and will return `Hello World`.
```
# -*- coding: utf8 -*-
def main_handler(event, context):
    try:
        print("try exception")
        raise Exception("err msg")
    except Exception as e:
        print(e)
    return("Hello World")
```

- If an exception is not captured before returning, it will be thrown outside the entry function and captured by SCF. In this case, the function is considered to have failed, and an error message will be returned.
The following sample codes show that the function execution fails.
```
# -*- coding: utf8 -*-
def main_handler(event, context):
    print("try exception")
    raise Exception("err msg")
    return("Hello World")
```
The function returns information similar to the following:
```
{
    "errorCode":-1,
    "errorMessage":"user code exception caught",
    "requestId":"a325b967-ef5b-4aa3-a329-c6bb0df72948",
    "stackTrace":"Traceback (most recent call last):\n  File \"/var/user/index.py\", line 4, in main_handler\n    raise Exception(\"err msg\")\nException: err msg",
    "statusCode":430
}
```
The `errorCode` field indicates a code error, and `errorMessage` provides error details. The `stackTrace` field indicates an error stack, and `statusCode` provides error details. For more information about `statusCode`, see [Function Status Code](https://intl.cloud.tencent.com/document/product/583/35311).

