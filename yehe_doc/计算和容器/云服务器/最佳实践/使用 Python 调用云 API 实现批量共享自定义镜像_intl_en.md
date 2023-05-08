## Directions
This document describes how to use the Python SDK to call APIs and share custom Cloud Virtual Machine (CVM) images in batches through sub-users. If you have similar needs or want to learn how to use the SDK, refer to this document.


## Prerequisites[](id:preconditions)
- You have created a sub-user and the sub-user has full access to CVM and cloud APIs.
 - For information about how to create a sub-user, see [Creating Sub-User](https://intl.cloud.tencent.com/document/product/598/13674).
 - For information about how to grant permissions to a sub-user, see [Setting Sub-User Permissions](https://intl.cloud.tencent.com/document/product/598/32650). In this document, sub-users are associated with the `QcloudCVMFullAccess` and `QcloudAPIFullAccess` preset policies.
 - For information about how to create a SecretId and a SecretKey for a sub-user, see [Access Key](https://intl.cloud.tencent.com/document/product/598/32675). You need to record and properly save the SecretId and SecretKey.
- There are custom images to be shared. If you need to create custom images, see [Creating a Custom Image](https://www.tencentcloud.com/document/product/213/4942).


## Directions

### Installing Python
1. Run the following command to check whether Python 3.6 or later is installed on the current CVM instance. If yes, skip this step.
```shellsession
python --version
```
2. If Python is not installed on your CVM instance, perform one of the following operations:
 - For a CVM instance on CentOS, run the following command to install Python:
```shellsession
yum install python3
```
 - For a CVM instance on Ubuntu or Debian, run the following command to install Python:
```shellsession
sudo apt install python3
```
 - For a CVM instance on any other operating system, go to the [Python website](https://www.python.org/doc/), download Python 3.6 or later, upload the installation package to the Linux server, decompress the package, and then install Python.
3. After the installation is completed, run the following command to verify the version of Python:
```shellsession
python --version
```

### Writing code
1. Create a `test.py` file on the target machine and enter the following code:
```python
import json
from tencentcloud.common import credential
from tencentcloud.common.profile.client_profile import ClientProfile
from tencentcloud.common.profile.http_profile import HttpProfile
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cvm.v20170312 import cvm_client, models
# By default, the environment variables `TENCENTCLOUD_SECRET_ID` and `TENCENTCLOUD_SECRET_KEY` are read to get the `SecretId` and `SecretKey`.
# For information about more credential management methods, see https://github.com/TencentCloud/tencentcloud-sdk-python#%E5%87%AD%E8%AF%81%E7%AE%A1%E7%90%86
cred = credential.EnvironmentVariableCredential().get_credential()
httpProfile = HttpProfile()
httpProfile.endpoint = "cvm.tencentcloudapi.com"
clientProfile = ClientProfile()
clientProfile.httpProfile = httpProfile
# Nanjing is used in this example. Modify the region according to actual situation. For example, in the case of Shanghai, change the region to `ap-shanghai`.
aria = 'ap-nanjing'
client = cvm_client.CvmClient(cred,aria, clientProfile)
def img_share(img_id,img_name,accountids):
    try:
        req1 = models.ModifyImageSharePermissionRequest()
        params1 = {
            "ImageId": img_id,
            "AccountIds": accountids,
            "Permission": "SHARE"
        }
        req1.from_json_string(json.dumps(params1))

        resp1 = client.ModifyImageSharePermission(req1)
        response1 = json.loads(resp1.to_json_string())
        print(img_name,'Shared successfully!',response1)
    except TencentCloudSDKException as err:
        print(img_name,'Sharing failed!',err)
try:
    req = models.DescribeImagesRequest()
    params = {
        "Filters": [
            {
                "Name": "image-type",
                "Values": ["PRIVATE_IMAGE"]
            }
        ],
        "Limit": 100
    }
    req.from_json_string(json.dumps(params))
    resp = client.DescribeImages(req)
    response = json.loads(resp.to_json_string())
    img_num = response["TotalCount"]
    print('Obtaining the image list...')
    share_config = input('1. Share all images\n\n2. Manually determine the images to share\n\n Enter 1 or 2 and press the Enter key. Default value: 2:') or '2'
    accountids = input('Enter the UINs of users with whom the images are to share, and separate the UINs with commas:').split(",")
    for i in range(img_num):
        basic = response['ImageSet'][i]
        img_id = basic['ImageId']
        img_name = basic['ImageName']
        if share_config == '1':
            img_share(img_id,img_name,accountids)
        elif share_config == '2':
            print('Image ID: ',img_id,'Image name: ',img_name)
            share_choice = input('Whether to share this image y/n:') or 'y'
            if share_choice == 'y':
                img_share(img_id,img_name,accountids)
            elif share_choice == 'n':
                continue
            else:
                print('Please specify a correct option!')
        else:
            print('Please specify a correct option!')
except TencentCloudSDKException as err:
    print(err)
```
 - **SecretId and SecretKey**: Use the SecretId and SecretKey of the created sub-user mentioned in [Prerequisites](#preconditions).
 - **aria**: Use the actual region where the custom images to be shared reside. For more information, see [Common Params](https://www.tencentcloud.com/document/product/213/31574).
2. Run the following command on the target machine to run the code:
```shellesession
python test.py
```
According to the on-screen prompts, enter 1 or 2 (choose to share all images together or to select and share images one by one), and then enter the peer account ID. To obtain the account ID, notify the peer account owner to go to the [Account Information](https://console.cloud.tencent.com/developer) page.
After the images are successfully shared, a corresponding number of RequestID values are returned.

## Relevant API Documents
This document uses the following APIs: [DescribeImages](https://intl.cloud.tencent.com/document/product/213/33272) and [ModifyImageSharePermission](https://www.tencentcloud.com/document/product/213/33268).

