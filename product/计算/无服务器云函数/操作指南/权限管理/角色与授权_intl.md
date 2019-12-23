## Overview

[Role](https://intl.cloud.tencent.com/document/product/598/19420) is a virtual identity with a set of permissions provided by [CAM](https://intl.cloud.tencent.com/document/product/598/10583), which is mainly used to grant access permissions of services, actions and resources in Tencent Cloud to role carriers. After these permissions are added to a role, the role can be configured to Tencent Cloud services, allowing the services to perform operations on authorized resources on your behalf.

## Role and Permission

SCF create, authorize, and use different roles by asking for your authorization regarding two kinds of roles and their associated policies. The role carrier is always `product service-scf.qcloud.com`, which means that only the SCF service will use the role and the policies owned by the role to complete related operations.
- Configuring role "SCF_QcsRole": It is used to complete the operations of the corresponding resource when the function is configured. Examples include COS permissions for COS trigger creation and deletion, API Gateway permissions for API Gateway trigger creation and deletion, and permissions for reading the zip package of code file in COS.
- Executing role "QCS_SCFExcuteRole": It is used to allow the code to operate the corresponding resource when the function is executed. For example, if you have read and write operations of COS files in your code, you can grant the code access to COS files by adding COS read and write permissions to this role.

### Configuring Role

The configuring role is used to authorize the SCF service to read and operate your resources during the configuration process.
- Role name: SCF_QcsRole 
- Role carrier: Product service-scf.qcloud.com
- Role description: The default configuring role in SCF This service role is used to grant the SCF configuration the permissions to connect with other resources in the cloud, including but not limited to code file access and trigger configuration.

Currently, this role has the following policies:

| Default policy | Policy type | Usage |
| --- | --- | --- |
| QcloudAPIGWFullAccess | Preset | Used to create API Gateway service and API and publish service when an API Gateway trigger is configured. |
| QcloudCOSDataReadOnly | Preset | Used to read the code zip package from the bucket when the code is updated using COS. |
| QcloudCOSBucketConfigRead | Preset | Used to read the trigger configuration information from the COS bucket. |
| QcloudCOSBucketConfigWrite | Preset | Used to write trigger configuration information to the bucket configuration when a COS trigger is configured. |


### Executing Role

The executing role is used to grant the function code permissions to read and operate resources during execution.
- Default role name: QCS_SCFExcuteRole 
- Role carrier: Product service-scf.qcloud.com
- Role description: The default operating role in SCF This service role is used to grant SCF the basic permissions to operate other resources in the cloud during execution.

Currently, this role has the following policies:

| Default policy | Policy type | Usage |
| --- | --- | --- |
| QcloudSCFFullAccess | Preset | Used to allow the code to access and call other functions under the same account during execution. |
| QcloudCLSFullAccess | Preset | Used to write a function execution log to CLS when the function is executed. |

In addition to using the default executing role directly, you can create a role by yourself, set the role carrier as SCF, and configure policies for it. After that, you can use the custom role when creating a function or modifying function configuration. By using a custom role, you have more flexible and autonomous control over the permissions and operational resources your function code gets during execution.

## Using a Role

### Using Configuring Role

When you access the console, if the SCF service has permissions to access the corresponding resources, the authorization request page will pop up automatically. You can complete automatic creation of the role and add default permissions to the role by clicking "Confirm authorization".

If you manage and configure SCF through TCCLI or APIs rather than the console, there will be an error returned when you perform relevant operations that require authorization. For example, when you update the function code through a COS bucket, if there is no role named `SCF_QcsRole` or preset policy "QcloudCOSDataReadOnly" in the role under the account used, an error will be prompted for this operation. You can add a role named `SCF_QcsRole` in the account used, authorize it to `product service-scf.qcloud.com`, and configure the preset policies as listed above to authorize the configuring role.


### Using Executing Role

When the SCF service is triggered, the executing role will be automatically used. According to the instructions in [Using a Role](https://intl.cloud.tencent.com/document/product/598/19419), the SCF service will obtain the temporary credentials corresponding to the role through the API used to obtain the temporary role credentials in the service backend when the function is triggered, and configure such credentials to the runtime environment of the function in the form of environment variables. Temporary variables set in the runtime environment include `TENCENTCLOUD_SECRETID`, `TENCENTCLOUD_SECRETKEY`, and `TENCENTCLOUD_SESSIONTOKEN`. You can follow the instructions in [Using an Environment Variable](https://cloud.tencent.com/document/product/583/30228#.E4.BD.BF.E7.94.A8.E7.8E.AF.E5.A2.83.E5.8F.98.E9.87.8F) to read the corresponding value based on the environment variable key.

The environment variables for temporary credentials are described below:

| Environment variable key | Environment variable value example | Description |
| --- | --- | --- |
| TENCENTCLOUD_SECRETID | AKIDRVI54XXn10r58oZpmzbBOnwt47xO1LRv | Used as the SecretId of the API request |
| TENCENTCLOUD_SECRETKEY | 3t0SYPHRIpjmAAUPfKM8b4yXnff4Aq56 | Used as the SecretKey of the API request |
| TENCENTCLOUD_SESSIONTOKEN | 289986df622a1fdbe0d29ee2b642c904d8d670df40001 | Used as the Token of the API request |

Below is an example of environment variables used in a snippet of Python code that uses COS:
```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging
import os

logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user profile, including secretId and secretKey
secret_id = os.environ.get('TENCENTCLOUD_SECRETID')      # Use the secretId in the environment variable
secret_key = os.environ.get('TENCENTCLOUD_SECRETKEY')    # Use the secretKey in the environment variable
region = 'ap-beijing-1'     
token = os.environ.get('TENCENTCLOUD_SESSIONTOKEN')      # Use the token in the environment variable as the token to be passed in when the temporary key is used
scheme = 'https'          
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)

# 2. Get the client object
client = CosS3Client(config)
```
