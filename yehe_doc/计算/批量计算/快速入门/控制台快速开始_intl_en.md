## Getting Started
This document describes how to submit a job with the BatchCompute Console. The steps are detailed below.

### Preparations
Prepare a bucket for [COS](https://intl.cloud.tencent.com/zh/document/product/436). If you haven't created a bucket, create one as instructed in [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).

### Logging in to the Console
Log in to the [BatchCompute Console](https://console.cloud.tencent.com/batch/task). If you have not activated the BatchCompute service, activate it according to the prompts on the BatchCompute Console page.

### Creating a Task Template

1. Select the **Task Template** in the left sidebar, and select a target region, such as "Guangzhou", at the top of the task template page.
2. Click **Create** to enter the "New Task Template" page and create a template, as shown below:
![](https://main.qcloudimg.com/raw/5eaf007532cdb04dc9f359e24a2f6922.png)
The main parameters are described as follows:
 - **Name**: enter a custom name, such as "hello".
 - **Description**: enter a custom description, such as "hello demo".
 - **Compute environment type**:
    - **Existing compute environment**: the existing compute environments are available.
    - **Automatic compute environment**: you don't need to create a fixed computing environment in advance. After the job is submitted, the CVM instance is automatically created to run the task and terminated after the task is completed.
 - **Image**: select an image as needed.
 - **Resource quantity**: such as 1.
 - **Timeout threshold and number of retry attempts**: keep the default values.
3. Click **Next** and configure application information, as shown below:
![](https://main.qcloudimg.com/raw/df04fd8aa361eff74796d40bb7d85171.png)
 - **Execution method**: select "Local".
 - **Stdout log**: For more information on the format, please see [Entering COS & CFS Paths](https://intl.cloud.tencent.com/document/product/599/13996).
 - **Stderr log**: The same as above.
 - **Command line**: echo 'hello, world'.
4. Click **Next** to configure the storage mapping, as shown below:
![](https://main.qcloudimg.com/raw/a9f02dff4b5f84a7253a5b940c5f6e2d.png)
5. Click **Next** to preview the .json file of the task, and click **Save** after confirmation, as shown below:
    ![](https://main.qcloudimg.com/raw/fe380f3cb4e60cd405f623ab70677461.png)
6. View the created templates on the "Task Template" page, as shown below:
![](https://main.qcloudimg.com/raw/56ba751132050eefd71a451cd24aca00.png)

### Submitting a Job
1. Select the **Job** in the left sidebar, and select a target region, such as "Guangzhou", at the top of the Job page.
2. Click **Create** to enter the "New Job" page and configure a job, as shown below:
![](https://main.qcloudimg.com/raw/7aac41e3f597d348daf9aadb2d4f0dd2.png)
 - **Name**: enter a custom name, such as "hello".
 - **Priority**: keep the default value.
 - **Description**: enter a custom description, such as "hello demo".
3. Select the task "hello" on the left side of "Task Flow" and drag the task to the right canvas, as shown below:
![](https://main.qcloudimg.com/raw/023f92bcda936696fd0434eeac1c0765.png)
4. Confirm the configurations in the "Task Details" on the right side of "Task Flow" and click **Save**.
5. You can check the running status of the created job on the "Job" list page, as shown below:
![](https://main.qcloudimg.com/raw/018544b3a1f84fd3e32c141c880b007f.png)
 - Click the job ID and check the running status of task instances under the **Task Running Status** tab.
 - Click **Querying logs** to check the standard outputs and errors of the task instance, as shown below:
![](https://main.qcloudimg.com/raw/3f0f2dab7b34e29cb92a2498911f03eb.png)

## Subsequent Operations
This document only provides a simple example of single-task job, without using the remote storage mapping, and only showing the most basic capabilities to users. You can continue to test the higher-level capabilities of BatchCompute according to the console user guide:
- **Various CVM configurations**: BatchCompute provides a variety of CVM configuration options. You can customize your own CVM configuration based on your business scenario.
- **Execute remote code package**: Technically, BatchCompute can fully satisfy your business needs by combining **custom image and remote code package and command line**.
- **Remote storage mapping**: BatchCompute optimizes storage access and simplifies access to remote storage services into operations in the local file system.
