## Overview

Errors may occur when data is being transmitted between the client and the server. Cloud Object Storage (COS) combined with Serverless Cloud Function (SCF) can ensure the integrity of uploaded data through data verification, for example, MD5 verification. When users upload files to COS, SCF will help verify the objects uploaded by the users to ensure the integrity and correctness of the uploaded data.

## Background

None of the existing public cloud object storage services in the industry provides MD5 verification, and after a user uploads a file, the following situations may occur:

- Duplicated files and rising costs
- File errors and lower business efficiency
- File missing


## Solution Strengths

- Visual operation: One-click configuration simplifies the development process without coding, greatly improving R&D efficiency
- Multiple options: MD5, SHA1, SHA256, and CRC64 are available, meeting user requirements in various scenarios
- Automatic execution: Once a file is uploaded to COS, the workflow for calculating the verification code is triggered


## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Create a workflow, customize the format filter rule, and create a custom function node. For detailed directions, see [Configuring Workflow](https://intl.cloud.tencent.com/document/product/436/46408).
![](https://qcloudimg.tencent-cloud.cn/raw/9d4a303445da7e91b5e5dd9cd42585c8.png)
3. In the function node pop-up window, click **Add Function**. 
3. On the SCF creation page, select the template for **COSHashCalculate**.
![](https://qcloudimg.tencent-cloud.cn/raw/dda0680b33565addb4973207941cb6b2.png)
4. Based on the user's file size, configure the execution timeout duration in the basic settings and configure sufficient memory in the advanced settings.
5. Configure the function code. This function template supports the following two environment variables:
  - hashTypeList: Indicates the list of calculation algorithms. This variable is optional. The default value is `["crc64", "md5", "sha1", "sha256"]`.
  - caseType: Indicates the hash case. This variable is optional. The default value is `lowercase`. You can also pass in `uppercase`.
6. Enable permission configuration and bind a role that has the read/write permission of the current bucket. To create an execution role, see [Role and Authorization](https://intl.cloud.tencent.com/document/product/583/38176).
7. Click **Complete**.
8. Go back to the previous workflow page, select the custom transcoding function created just now, and save the workflow.
![](https://qcloudimg.tencent-cloud.cn/raw/86cd43267e8e9a1e84ba7e5227be7f25.png)
9. Upload the file. After the workflow processing is successful, you can see that multiple hash headers are successfully added to the uploaded file.
![](https://qcloudimg.tencent-cloud.cn/raw/b87689705cd3382098796383e2876400.png)  



