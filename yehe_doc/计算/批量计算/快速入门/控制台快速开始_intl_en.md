## Quick Start
This document describes how to submit a job in the BatchCompute Console. The steps are as follows:
### Preparations
Prepare a [COS](https://intl.cloud.tencent.com/document/product/436) bucket. If you haven't created a bucket yet, create one as instructed in [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).

### Logging in to [console](https://console.cloud.tencent.com/batch/task)
If you haven't activated the BatchCompute service, activate it as prompted on the BatchCompute Console page.

### Creating task template

1. Click "Task Template" on the left sidebar, select the target region such as "Guangzhou", and click **Create**.

2. Configure the basic information.
  * Name: such as `hello`
  * Description: such as `hello demo`
  * Resource Configuration: default value
  * Number of Resources: such as 1
  * Timeout Period: default value
  * Number of Retries: default value
  * Image: img-m4q71qnf
![](https://main.qcloudimg.com/raw/5eaf007532cdb04dc9f359e24a2f6922.png)

3. Configure the program information.
  * Execution Method: Local
  * Stdout Log: for more information on the format, please see [How to Enter COS and CFS Paths](https://intl.cloud.tencent.com/document/product/599/13996)
  * Stderr Log: same as Stdout log
  * Command Line: echo 'hello, world'
![](https://main.qcloudimg.com/raw/df04fd8aa361eff74796d40bb7d85171.png)

4. Configure the storage mapping and click **Next**.
   ![](https://main.qcloudimg.com/raw/a9f02dff4b5f84a7253a5b940c5f6e2d.png)

5. Preview the task's JSON file and click **Save** after confirming that everything is correct.
  ![](https://main.qcloudimg.com/raw/fe380f3cb4e60cd405f623ab70677461.png)

6. View the task template.
  ![](https://main.qcloudimg.com/raw/56ba751132050eefd71a451cd24aca00.png)

### Submitting job
1. Click "Job" on the left sidebar, select the target region such as "Guangzhou", and click **Create**.

2. Configure the basic information for the job.
  * Job Name: such as `hello`
  * Priority: default value
  * Description: such as `hello job`
  ![](https://main.qcloudimg.com/raw/7aac41e3f597d348daf9aadb2d4f0dd2.png)

3. Select the "hello" task on the left on the "Task Flow" page and drag the task to the canvas on the right.
  ![](https://main.qcloudimg.com/raw/023f92bcda936696fd0434eeac1c0765.png)

4. Enable "Task Details" on the right on the "Task Flow" page, confirm that the configuration is correct, and click "Complete".
![](https://main.qcloudimg.com/raw/b592938fa04583d04943db6f3047e93d.png)

5. Query the result. You can view the running status of the job on the job list page.
  ![](https://main.qcloudimg.com/raw/018544b3a1f84fd3e32c141c880b007f.png)
 - Click a job ID to view the running status of each task instance in "Task Running Status".
 - Click "View Log" to view the standard output and standard error of a task instance.

  ![](https://main.qcloudimg.com/raw/3f0f2dab7b34e29cb92a2498911f03eb.png)

## What's Next?

In this simplest example, the job only contains a single task. It does not use remote storage mapping, but only shows the most basic capabilities. You can continue to test the advanced capabilities of BatchCompute as instructed in the Console User Guide.
- **Various CVM configurations**: BatchCompute provides a variety of CVM configuration options. You can customize your own CVM configuration based on your business scenario.
- **Remote code package execution**: technically, BatchCompute can fully satisfy your business needs by combining **custom image, remote code package, and command line**.
- **Remote storage mapping**: BatchCompute optimizes storage access and simplifies access to remote storage services into operations in the local file system.
