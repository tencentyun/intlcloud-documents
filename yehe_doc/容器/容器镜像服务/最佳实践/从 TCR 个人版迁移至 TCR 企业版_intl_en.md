## Overview
Currently, TCR provides the Personal Edition and Enterprise Edition services at the same time. The Personal Edition service is for individual developers and only provides basic features for container image storage and distribution. While the Enterprise Edition service is for enterprise users and can provide a secure, dedicated, and high-performance cloud native artifacts hosting and distribution service. For the differences between the two editions, please see [TCR Specifications](https://intl.cloud.tencent.com/document/product/1051/35483).

In order to ensure the data security and availability of the container image that the services rely on, and improve the accelerated distribution of container images in multiple regions, it is necessary to switch the Personal Edition to the Enterprise Edition.

This document describes how the enterprise users can migrate container images and related dependencies from the Personal Edition to the Enterprise Edition.


## Prerequisites
To migrate from the Personal Edition service to the Enterprise Edition, you need to confirm and complete the following preparations:
- The Personal Edition service has been activated and used. The account that operates the migration has the permission to pull all the images in the image registry of the Personal Edition. For how to grant full read/write permissions of the Personal Edition to the sub-account, please see [Example of Authorization Solution of the Personal Edition](https://intl.cloud.tencent.com/document/product/1051/37250).
- You have purchased the [Enterprise Edition Instance](https://cloud.tencent.com/document/product/1141/51110). The account that operates the migration has the permission to push image to this instance. For how to grant the sub-account the permission for pushing the container image and Helm Chart of the corresponding instance, please see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248). It is recommended to grant the full read/write permissions of TCR to the sub-account that configures synchronization.
- The running environment of the migration tool has been configured. It is recommended to perform the migration task in a VPC to increase the migration speed and avoid the cost of public network traffic.
  - Run the migration tool in the VPC: add the VPC where the server of the migration tool is running in the private network access of the target Enterprise Edition instance. For more information, please see [Private Network Access Control](https://intl.cloud.tencent.com/document/product/1051/35492).
  - Run the migration tool in the public network: enable the public network access entry of the target Enterprise Edition instance and open to the internet access. For more information, please see [Public Network Access Control](https://intl.cloud.tencent.com/document/product/1051/35491).

## Directions
### Downloading and installing the migration tool
Run the following command to download and install the migration tool.
```
wget https://github.com/tkestack/image-transfer/releases/download/v1.0.0/image-transfer-linux-amd64.tar.gz
tar -xzvf image-transfer-linux-amd64.tar.gz
cd image-transfer
```


### Initializing the migration tool configuration
1. Configure the authentication configuration file of the image registry “security.yaml”, that is, configure the user names and passwords of the source and target registry. Allow the migration tool to log in to the image registry, and pull and push images in batches.
```
tcr-enterprise-demo.tencentcloudcr.com:
        username: xxx
        password: xxx
ccr.ccs.tencentyun.com:
        username: xxx
        password: xxx
```
   - **Enterprise Edition**: supports temporary and long-term access credentials. Log in to the TCR console and select the [Instance List](https://console.cloud.tencent.com/tcr/instance?rid=1). Select a created Enterprise Edition instance to go to the details page, and create an access credential for the image migration in the **Access Credential** tab. For more information, see [Obtaining an Instance Access Credential](https://intl.cloud.tencent.com/document/product/1051/37253).  
   - **Personal Edition**: only supports the fixed password, which is set when you initialize the migration tool. If you forget the password, you can log in to the TCR console, select **Image Repository** > **[Personal Edition](https://console.cloud.tencent.com/tke2/registry/user?rid=1)**, and click **Reset Password**. In the pop-up window, confirm the user name and reset the password.
2. Configure the Tencent Cloud’s authentication configuration file “secret.yaml”. Refer to the following code to configure Tencent Cloud's `SecretId` and `SecretKey` to allow the migration tool to call TCR related Tencent Cloud APIs to obtain the image list and basic information.
```
tcr:
        secretId: xxx
        secretKey: xxx
ccr:
        secretId: xxx
        secretKey: xxx
```
tcr represents the Enterprise Edition and ccr represents the Personal Edition, sharing a pair of Tencent Cloud `secretId` and `secretKey`. You can view your Tencent Cloud API key in**[Access Key** > **[API Key Management](https://console.cloud.tencent.com/cam/capi)**.

### Running the migration tool
Run the following command in the installation folder of the migration tool:
```
./image-transfer --ccrToTcr=true --routines=5 --securityFile=./security.yaml --secretFile=./secret.yaml --tcrName=tcr-enterprise-demo --retry=3 --tcrRegion=ap-guangzhou --ccrRegion=ap-guangzhou --qps=3000
```

| Parameter | Description | 
|---------|---------|
| ccrToTcr=true | Indicate that the TCR one-click full migration mode is enabled. In this mode, the migration tool will fully migrate the images in the Personal Edition instance to the specified Enterprise Edition instance. | 
| securityFile | Specify security.yaml configuration file. | 
| secretFile | Specify secret.yaml configuration file. | 
| tcrName | Specify the name of the target Enterprise Edition instance. | 
| tcrRegion | Specify the region where the target Enterprise Edition instance is located. | 
| ccrRegion | Specify the region where the source Personal Edition instance registry is located. By default, it is the same as the region of the target Enterprise Edition instance. | 





### Viewing the running results
Because the Personal Edition is fully migrated to the Enterprise Edition by default, and the migration time is directly related to the number and size of the image registry in the current Personal Edition, please wait patiently for the migration.
If the following code is displayed after running, it means that the full migration is successful. Otherwise, please run the migration tool to try again.
```
################# Finished, 0 transfer jobs failed, 0 jobs generate failed #################
```

