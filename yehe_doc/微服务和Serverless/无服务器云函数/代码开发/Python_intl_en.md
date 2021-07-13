Currently, the following versions of Python programming language are supported:
* Python 2.7
* Python 3.6

## Function Format

The Python function format is generally as follows:
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
* event: this parameter is used to pass the trigger event data.
* context: this parameter is used to pass runtime information to your handler.

## Return and Exception

Your handler can use `return` to return a value. The return value will be handled differently depending on the type of invocation when the function is invoked.
* Sync invocation: when sync invocation is used, the return value will be serialized and returned to the invoker in JSON format. The invoker can get the returned value for subsequent handling. For example, the invoking method of function testing in the console is sync invocation, which can capture the function returned value and display it after the invocation is completed.
* Async invocation: when async invocation is used, since the invoking method returns right after the function is triggered, it will not wait for the function to complete execution, and the returned value of the function will be discarded.

In addition, the returned value will be displayed at the `ret_msg` position in the function log for both sync invocation and async invocation.

You can throw an exception inside the function by using `raise Exception`. The thrown exception will be captured in the function runtime environment and displayed in the log as `Traceback`.

## Log
You can use the `print` or `logging` module in the program to output a log. For example, in the following function:
```python
import logging
logger = logging.getLogger()
logger.setLevel(logging.INFO)
def main_handler(event, context):
    logger.info('got event{}'.format(event))
    print("got event{}".format(event))
    return 'Hello World!'  
```

The output can be viewed at the `log` position in the function log.

## Installing Dependencies

For more information, please see [Dependency Installation](https://intl.cloud.tencent.com/document/product/583/34879).


## Included Libraries and Usage

### COS SDK

SCF's runtime environment already contains the [COS SDK for Python](https://intl.cloud.tencent.com/document/product/436/12269), and the specific versions are `cos_sdk_v5` (recommended) and `cos_sdk_v4`.

The COS SDK can be referenced and used within the code as follows:
- For `cos_sdk_v5`:
```
import qcloud_cos_v5
```
```
from qcloud_cos_v5 import CosConfig 
from qcloud_cos_v5 import CosS3Client
```

- For `cos_sdk_v4`:
```
import qcloud_cos
```
```
from qcloud_cos_v4 import CosClient
from qcloud_cos_v4 import DownloadFileRequest
from qcloud_cos_v4 import UploadFileRequest
```

For more information on how to use the COS SDK, please see [COS SDK for Python](https://intl.cloud.tencent.com/document/product/436/12269).

## Python 2 or 3?
You can choose the desired runtime environment by selecting `Python 2.7` or `Python 3.6` for the runtime environment when creating a function.

You can view Python's official advice on Python 2 or Python 3 selection [here](https://wiki.python.org/moin/Python2orPython3).

- The following libraries are supported in Python 3 cloud runtime:
>If you need to use a library that is not listed below, please install it locally and use it after packaging and uploading it.For more information, please see [Dependency Installation](https://intl.cloud.tencent.com/document/product/583/34879#python-.E8.BF.90.E8.A1.8C.E6.97.B6)
>

| Library Name | Version |
| -------------------------------- |---------------|
| absl-py                |0.2.2|
| asn1crypto              |0.24.0|
| astor                  |0.7.1|
| bleach                   |1.5.0|
| certifi             |2019.3.9|
| cffi                     |1.12.2|
| chardet                   |3.0.4|
| cos-python-sdk-v5       |1.6.6|
| cryptography           |2.6.1|
| dicttoxml             |1.7.4|
| gast                     |0.2.0|
| grpcio                  |1.13.0|
| html5lib           |0.9999999|
| idna                      |2.8|
| iniparse                   |0.4|
| Markdown                 |2.6.11|
| mysqlclient             |1.3.13|
| numpy                    |1.15.0|
| Pillow                    |6.0.0|
| pip                       |9.0.1|
| protobuf                  |3.6.0|
| psycopg2-binary           |2.8.2|
| pycparser                  |2.19|
| pycurl                   |7.43.0|
| PyMySQL                   |0.9.3|
| pytz                     |2019.1|
| qcloud-image              |1.0.0|
| qcloudsms-py              |0.1.3|
| requests                 |2.21.0|
| serverless-db-sdk         |0.0.1|
| setuptools               |28.8.0|
| six                      |1.12.0|
| tencentcloud-sdk-python  |3.0.65|
| tencentserverless         |0.1.4|
| tensorboard               |1.9.0
| tensorflow                |1.9.0
| tensorflow-serving-api    |1.9.0|
| termcolor                 |1.1.0
| urllib3                  |1.24.2
| Werkzeug                 |0.14.1
| wheel                    |0.31.1|

- The following libraries are supported in Python 2 cloud runtime:

| Library Name | Version |
| -------------------------------- |---------------|
| absl-py                      | 0.2.2     |
| asn1crypto                   | 0.24.0    |
| astor                        | 0.7.1     |
| backports.ssl-match-hostname | 3.4.0.2   |
| backports.weakref            | 1.0.post1 |
| bleach                       | 1.5.0     |
| cassdk                       | 1.0.2     |
| certifi                      | 2017.11.5 |
| cffi                         | 1.12.2    |
| chardet                      | 3.0.4     |
| cos-python-sdk-v5            | 1.6.6     |
| cryptography                 | 2.6.1     |
| dicttoxml                    | 1.7.4     |
| enum34                       | 1.1.6     |
| funcsigs                     | 1.0.2     |
| futures                      | 3.2.0     |
| gast                         | 0.2.0     |
| grpcio                       | 1.13.0    |
| html5lib                     | 0.9999999 |
| idna                         | 2.6       |
| iniparse                     | 0.4       |
| ipaddress                    | 1.0.22    |
| Markdown                     | 2.6.11    |
| mock                         | 2.0.0     |
| mysqlclient                  | 1.3.13    |
| nose                         | 1.3.7     |
| numpy                        | 1.14.5    |
| ordereddict                  | 1.1       |
| pbr                          | 4.1.0     |
| Pillow                       | 6.0.0     |
| pip                          | 18        |
| protobuf                     | 3.6.0     |
| psycopg2-binary              | 2.8.2     |
| pyaml                        | 2019.4.1  |
| pycparser                    | 2.19      |
| pycurl                       | 7.43.0.1  |
| pygpgme                      | 0.3       |
| PyMySQL                      | 0.9.3     |
| pytz                         | 2019.1    |
| PyYAML                       | 5.1       |
| qcloud-image                 | 1.0.0     |
| qcloudsms-py                 | 0.1.3     |
| requests                     | 2.18.4    |
| serverless-db-sdk            | 0.0.1     |
| setuptools                   | 39.1.0    |
| six                          | 1.11.0    |
| tencentcloud-sdk-python      | 3.0.65    |
| tencentserverless            | 0.1.4     |
| tensorboard                  | 1.9.0     |
| tensorflow                   | 1.9.0     |
| tensorflow-serving-api       | 1.9.0     |
| termcolor                    | 1.1.0     |
| urlgrabber                   | 3.10.2    |
| urllib3                      | 1.22      |
| Werkzeug                     | 0.14.1    |
| wheel                        | 0.31.1    |


## Related Documents
For more information on how to use relevant features, please see the following documents:
- [Role and Authorization](<https://intl.cloud.tencent.com/document/product/583/31444>)




