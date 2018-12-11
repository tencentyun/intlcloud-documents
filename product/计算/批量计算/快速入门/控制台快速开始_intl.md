## Quick Start
This document describes how to submit a job in the Batch Console. The steps are as follows.
### Preparations
Prepare the [COS](https://intl.cloud.tencent.com/document/product/436) bucket. If you have not created a bucket yet, see [Creating a Bucket](https://intl.cloud.tencent.com/document/product/436/6232) and create one.

### Log in to the [Console]()
If you have not activated Batch yet, follow on-screen prompts on the Batch Console homepage to activate it.

### Create a task template

1. Click "Task template" in the left navigation bar, select the target region such as "Guangzhou". Click **Create**.

2. Configure basic information.
  * Name: hello
  * Description: hello demo
  * Resource configuration: Default value
  * Number of resources: 1
  * Timeout: Default value
  * Number of retries: Default value
  * Image: img-m4q71qnf
![](https://main.qcloudimg.com/raw/5eaf007532cdb04dc9f359e24a2f6922.png)

3. Configure application information.
  * Execution method: Local
  * Stdout log: For formats, see [Entering COS or CFS Path](https://cloud.tencent.com/document/product/599/13996)
  * Stderr log: Same as Stdout Log
  * Command line: echo 'hello, world'
![](https://main.qcloudimg.com/raw/df04fd8aa361eff74796d40bb7d85171.png)

4. Configure the storage mapping and click **Next** when finished.
   ![](https://main.qcloudimg.com/raw/a9f02dff4b5f84a7253a5b940c5f6e2d.png)

5. Preview the task's JSON file and click **Save** after confirming it is correct.
    ![](https://main.qcloudimg.com/raw/fe380f3cb4e60cd405f623ab70677461.png)

6. View the task template.
    ![](https://main.qcloudimg.com/raw/56ba751132050eefd71a451cd24aca00.png)

### Submit a job
1. Click **Job** in the left navigation bar, select the target region such as "Guangzhou". Click **Create**.

2. Configure basic job information.
  * Job name: hello
  * Priority: Default value
  * Description: hello job
    ![](https://main.qcloudimg.com/raw/7aac41e3f597d348daf9aadb2d4f0dd2.png)

3. Select the "hello" task on the left in "Task flow" and move the task onto the canvas on the right using the mouse.
    ![](https://main.qcloudimg.com/raw/023f92bcda936696fd0434eeac1c0765.png)

4. Turn on "Task details" to the right of "Task flow", confirm the configuration is correct and click "Finish".
![](https://main.qcloudimg.com/raw/b592938fa04583d04943db6f3047e93d.png)

5. Query the result. You can view the running state of the job on the job list page.
    ![](https://main.qcloudimg.com/raw/018544b3a1f84fd3e32c141c880b007f.png)
 - Click the job ID to view the running state of each task instance under "Task running conditions"
 - Click "View log" to view standard outputs and standard errors of task instances.

  ![](https://main.qcloudimg.com/raw/3f0f2dab7b34e29cb92a2498911f03eb.png)

## What Can I Do Next?

This document illustrates a simple single-task job with no remote storage mapping involved to show the most basic capabilities of Batch. You can continue to test the advanced capabilities according to the Console User Guide.
- **Rich CVM configuration items**: Batch provides a wide variety of CVM configuration items, so you can customize the CVM configuration based on the specific business scenario.
- **Running remote code package**: Batch provides a **custom image + remote code package + command line** method for execution that technically meets your different business needs in all aspects.
- **Remote storage mapping**: Batch optimizes storage access and simplifies access to remote storage services into local file system operations.
