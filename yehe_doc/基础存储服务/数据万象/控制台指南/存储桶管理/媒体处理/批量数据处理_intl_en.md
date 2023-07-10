## Overview

CI supports batch processing of files stored in COS. You can specify a workflow or an independent job node as the operation of batch data processing.

## Directions

### Creating batch data processing job

1. Log in to the [CI console](https://console.cloud.tencent.com/ci).
2. Click **Bucket Management** on the left sidebar to enter the bucket list.
3. Click **Manage** in the **Operation** column on the right of the target bucket to enter the bucket management page.
4. On the left sidebar, click **Job and Workflow** > **Batch Data Processing**.
5. Click **Create Batch Data Processing Job** to enter the creation page.
6. On the **Create Workflow** page, configure the following items:

  - **Job Name**: It is required and can contain up to 128 letters, digits, underscores (\_), and hyphens (-).
  - **Input Bucket Name**: It is the current bucket by default.
  - **Scope**: Determine the data scope for batch processing, which is the current bucket file list by default.
  - **Time**: Select the default audio/video/image file filter rule or a custom workflow rule. You can also select all files to process all objects in the bucket.
  - **Prefix**: Scan files with the specified prefix to perform operations specified in the processing settings.
  - **Processing Type**: Set operations for data within the specified range. You can select a workflow or independent node. For configurations for independent nodes, see [Job](https://www.tencentcloud.com/document/product/1045/43605).
  - **Select Workflow**: Select the workflow to be executed.


## Viewing batch data processing job result

1. Go to the batch data processing page and click **Execution Result** in the **Operation** column of the target workflow.

2. If the processing type is workflow, clicking **Execution Result** will redirect you to **Execution Record** > **Workflow Execution Result**.
3. If the processing type is independent node, clicking **Execution Result** will redirect you to **Execution Record** > **Job Result**.




