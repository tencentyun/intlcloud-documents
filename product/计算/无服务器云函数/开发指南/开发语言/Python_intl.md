Currently, the following versions of Python programming language are supported:
* Python 2.7
* Python 3.6

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

When you create an SCF function, you need to specify an execution method. If the Python programming language is used, the execution method is similar to `index.main_handler`, where `index` indicates that the executed entry file is `index.py`, and `main_handler` indicates that the executed entry function is `main_handler`. When submitting the zip code package by uploading the zip file locally or through COS, please make sure that the root directory of the package contains the specified entry file, the file contains the entry function specified by the definition, and the names of the file and function match those entered in the trigger; otherwise, execution will fail as the entry file or entry function cannot be found.

## Input Parameters

The input parameters in the Python environment include event and context, both of which are of the Python dict type.
* event: This parameter is used to pass the trigger event data.
* context: This parameter is used to pass runtime information to your handler.

## Return and Exception

Your handler can use `return` to return a value. The return value will be handled differently depending on the type of call when the function is called.
* Sync call: When sync call is used, the return value will be serialized and returned to the caller in JSON format. The caller can get the return value for subsequent handling. For example, the calling method of function testing in the console is sync call, which can capture the function return value and display it after the call is completed.
* Async call: When async call is used, since the calling method returns right after the function is triggered, it will not wait for the function to complete execution, and the return value of the function will be discarded.

In addition, the return value will be displayed at the `ret_msg` position in the function log for both sync call and async call.

You can throw an exception inside the function using `raise Exception`. The thrown exception will be captured in the function runtime environment and displayed in the log as `Traceback`.

## Log
You can use the `print` or `logging` module in the program to output the log. Therefore, for example, in the following function:
```python
import logging
logger = logging.getLogger()
logger.setLevel(logging.INFO)
def main_handler(event, context):
    logger.info('got event{}'.format(event))
    print("got event{}".format(event))
    return 'Hello World!'  
```

The output can be viewed at the `log` location in the function log.


## Included Library and Usage

### COS SDK

SCF's runtime environment already contains the [COS SDK for Python](https://cloud.tencent.com/document/product/436/6275), and the specific version is `cos_sdk_v4`.

The COS SDK can be referenced and used within the code as follows:
```
import qcloud_cos
```

```
from qcloud_cos import CosClient
from qcloud_cos import DownloadFileRequest
from qcloud_cos import UploadFileRequest
```

For more detailed instructions on how to use the COS SDK, see [COS SDK for Python](https://cloud.tencent.com/document/product/436/6275).

## Python 2 or 3?
You can choose the desired runtime environment by selecting `Python 2.7` or `Python 3.6` for the runtime environment when creating a function.

You can view Python's official advice on Python 2 or Python 3 selection [here](https://wiki.python.org/moin/Python2orPython3).

