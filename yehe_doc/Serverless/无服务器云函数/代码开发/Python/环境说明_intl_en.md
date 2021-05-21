

## Python Versions
Currently, the following versions of Python programming language are supported:
- Python 2.7
- Python 3.6

When creating a function, you can select a desired runtime environment from `Python 2.7` or `Python 3.6`. Click [here](https://wiki.python.org/moin/Python2orPython3) to view Python's official advice on choosing Python 2 or Python 3.

## Environment Variables

The table below lists environment variables related to built-in Python in a current runtime environment.

| Environment Variable Key | Specific Value or Value Source |
| ------------------------- | ----------------------------- |
| `PYTHONDONTWRITEBYTECODE` | x                             |
| `PYTHONPATH`              | /var/user:/opt                |
| `_`                       | /var/lang/python3/bin/python3 |


For more information on environment variables, see [Environment Variables](https://intl.cloud.tencent.com/document/product/583/32748).



## Included Library and Usage

### COS SDK

SCF's runtime environment already contains the [COS SDK for Python](https://intl.cloud.tencent.com/document/product/436/12269), and specific versions are `cos_sdk_v5` (recommended) and `cos_sdk_v4`.

The COS SDK can be referenced and used within the code as follows:
- For the `cos_sdk_v5` version:
```
import qcloud_cos_v5
```
```
from qcloud_cos_v5 import CosConfig 
from qcloud_cos_v5 import CosS3Client
```

- For the `cos_sdk_v4` version:
```
import qcloud_cos
```
```
from qcloud_cos_v4 import CosClient
from qcloud_cos_v4 import DownloadFileRequest
from qcloud_cos_v4 import UploadFileRequest
```

For more detailed instructions on how to use the COS SDK, see [COS SDK for Python](https://intl.cloud.tencent.com/document/product/436/12269).



### Built-in Libraries

The table below lists the supported SCF libraries in the Python 3 cloud runtime environment.
>? To use a library not listed here, you need to locally install, package, and upload it. For detailed directions, see [Installing Dependent Libraries](https://intl.cloud.tencent.com/document/product/583/34879).
>

|Library Name | Version |
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
| tensorboard               |1.9.0|
| tensorflow                |1.9.0|
| tensorflow-serving-api    |1.9.0|
| termcolor                 |1.1.0|
| urllib3                  |1.24.2|
| Werkzeug                 |0.14.1|
| wheel                    |0.31.1|

The table below lists the supported SCF libraries in the Python 2 cloud runtime environment.

|Library Name | Version |
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



