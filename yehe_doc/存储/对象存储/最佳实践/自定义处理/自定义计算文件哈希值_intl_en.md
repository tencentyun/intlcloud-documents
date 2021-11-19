## Overview

Errors may occur when data is being transmitted between the client and the server. Cloud Object Storage (COS) combined with Serverless Cloud Function (SCF) can ensure the integrity of uploaded data through data verification, for example, MD5 verification. When users upload files to COS, SCF will help verify the objects uploaded by the users to ensure the integrity and correctness of the uploaded data.

## Background

None of the existing public cloud object storage services in the industry provides MD5 verification, and after a user uploads a file, the following situations may occur:

- Duplicated files and rising costs
- File errors and lower business efficiency
- File missing


## Solution Strengths

- Visual operation: one-click configuration simplifies the development process without coding, greatly improving R&D efficiency
- Multiple options: MD5, SHA1, SHA256, and CRC64 are available, meeting user requirements in various scenarios
- Automatic execution: once a file is uploaded to COS, the workflow for calculating the verification code is triggered


## Directions


1. Log in to the [COS console](https://console.cloud.tencent.com/cos5), create a workflow, customize a format filter rule, and create a custom function node.

2. In the function node pop-up window, click **Add Function**.
     
3. On the SCF creation page, select the **Calculate COS object hash** template.

4. Based on the user's file size, configure the execution timeout period in the basic settings and configure sufficient memory in the advanced settings.
5. Configure the function code. This function template supports the following two environment variables:
  - hashTypeList: indicates the list of calculation algorithms. This variable is optional. The default value is `["crc64", "md5", "sha1", "sha256"]`.
  - caseType: indicates the hash case. This variable is optional. The default value is `lowercase`. You can also pass in `uppercase`.
6. Enable permission configuration and bind a role that has the read/write permission of the current bucket. If you need to create an execution role, see [Role and Authorization](https://intl.cloud.tencent.com/document/product/583/38176).
7. Click **Finish**.
8. Go back to the previous workflow page, select the custom transcoding function created just now, and save the workflow.

9. Upload the file. After the workflow processing is successful, you can see that multiple hash headers are successfully added to the uploaded file.




