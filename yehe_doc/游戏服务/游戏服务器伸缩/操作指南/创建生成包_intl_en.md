## Overview

This document describes how to create an asset package, which will be uploaded to and deployed in GSE for game hosting.

## Directions

1. Log in to the [GSE console](https://console.cloud.tencent.com/gse/asset) and click **Asset** on the left sidebar.
2. Click **Create** in the top-left corner.
3. To create an asset package, you can upload one through the console page or CLI.

### Page upload
Enter the basic package information, including the package name and version. Select the OS and submission mode, upload the code, and click **OK**.
   - Asset Package Name: descriptive name of the asset package to be created, which does not need to be unique and can be modified and updated.
   - Asset Package Version: detailed information of asset package version, which is used to distinguish between different asset package versions.
   - OS: the operating system on which the game server asset package runs. It cannot be modified after the asset package is created.
   - Submission Mode: currently, only local zip packages can be uploaded.
   - Upload Codes: the asset package requires [integrating the gRPC framework](https://intl.cloud.tencent.com/document/product/1055/37418). The asset package directory must contain all the components necessary for running your game server, including executable files, dependency packages, and installation scripts of the game server. All are compressed into a zip package.
     - Game server executable file: a file required for running the game server. The asset package can contain multiple executable files, but only if they are built for the same platform.
     - Dependency package: any file required for running the game server executable file.
     - Installation script: executes the tasks for installing the asset package on the GSE-hosted server. This file must be placed in the root directory of the asset package and will run once during fleet creation. For more information, see [Game Process Launch Configuration](https://intl.cloud.tencent.com/document/product/1055/39885).
   - Tag (optional): the tag is used to manage resources by category from different dimensions. If the existing tag does not meet your requirements, please go to the [Tag](https://console.cloud.tencent.com/tag/taglist) console to create new tags.
![](https://main.qcloudimg.com/raw/e4b2ea4e83d3362e8824587160d0e05a.png)

### CLI upload

#### Step 1: download the script
Click [here](https://uploadasset-1301007756.cos.ap-guangzhou.myqcloud.com/uploadasset.zip?_ga=1.169449890.2037398510.1594263380) to download the `uploadasset.py` script.

#### Step 2: install the script dependency packages
Running the script requires the following two dependency packages.
-  **tencentcloud-sdk-python**
 -  Installation command: `pip install tencentcloud-sdk-python`.
 -  Supported version: TencentCloud API SDK Python V2.7-V3.6. For more information, see [Python SDK](https://intl.cloud.tencent.com/document/product/494/7244).
- **cos-python-sdk-v5**
 - Installation command: `pip install -U cos-python-sdk-v5`.
 - Supported version: For more information, see [Python SDK](https://intl.cloud.tencent.com/document/product/436/12269).

#### Step 3: run the script
**1. Modify the configuration**
Configure your authentication in the script. Replace `secret_id` and `secret_id` with your actual values.

**2. Execute the command**
Execute the following command to run the script:
```
python uploadasset.py  --local_path ./game_folder/
```
You will see `help` after running the command code. Click `help` to view more parameter information.

>?
>1. When you use the CLI to upload the asset package, you can configure the parameter `--local_path` to specify the upload folder path. The script will automatically compress and package the content under this path (only the contents under the path rather than the folder are packaged).
>2. The operating system and bit can be uploaded. The following methods are recommended:
>```
>python uploadasset.py  --local_path ./game_folder/ --os_type=Windows --os_bit=64
> python uploadasset.py  --local_path ./game_folder/ --os_type=CentOS --os_bit=64
> python uploadasset.py  --local_path ./game_folder/ --image_id=img-9qabwvbn
>```