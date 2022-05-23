## Overview

COS workflow provides a series of processing capabilities for media files such as audios, videos, and images. You can flexibly and quickly create a media processing workflow as needed. To satisfy your needs for customization and guarantee the flexibility, COS workflow offers the custom function feature for you to implement custom logic in SCF by configuring function nodes in a workflow.
To make this feature easier to use, COS workflow provides common function feature templates and integrates their creation to node configuration steps, facilitating subsequent processing of source and output files. Currently, supported basic operations include modifying object attributes, moving objects, and deleting objects.

## Use Cases

- You want to move or transition source files after media processing to reduce the storage costs.
- You want to tag output files or modify their headers after media processing to facilitate subsequent business use.

## Solution Strengths

- Out-of-the-box service: You can use the service after simple configuration, with no need to develop the function logic or care about the complex deployment process.
- Flexible configuration: You can configure nodes of common features as needed to perform different business operations on source and output files.
- Easy extension: You can modify the function logic to meet more customization requirements.

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the target bucket to enter the bucket details page.
4. On the left sidebar, select **Data Processing Workflow** > **Workflow** and click **Create Workflow**.
5. On the workflow creation page, configure the media processing node required by the business such as **Audio/Video Transcoding**. For more information, see Workflow.

6. On the workflow creation page, add the **Custom Function** node and select a required common feature function.

If you haven't created a function of this type, click **Create**.

Create a common feature function as follows:
 1. Enter the basic function configuration: Enter the function name prefix, select **Authorize SCF Service**, and click **Next**.

 2. Configure attributes: Set the storage class and custom header based on the business needs and click **Next**.

 3. Select the object to be processed. You can perform this operation only on the workflow source file.

 4. Click **OK**.
 5. COS workflow encapsulates processes such as function creation, version release, and alias-based stream switch. Wait for the workflow to be created.

7. After the creation, select the function instance just created and click **OK**.

8. Click **Save**.

## Operation Verification

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the target bucket to enter the bucket details page.
4. On the left sidebar, select **Data Processing Workflow** > **Workflow** to enter the workflow management page.
5. Enable the workflow just created, go to the specified bucket, upload a media file, and wait for the workflow to be executed.

6. After the workflow execution is completed:
You can see that media processing succeeded, and the output file was generated.

The storage class and custom header have been set for the source file.


