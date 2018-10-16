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
![](https://mc.qcloudimg.com/static/img/d12041618aeba32ecd52f61d84656e40/image.jpg)

3. Configure application information.
  * Execution method: Local
  * Stdout log: For formats, see [Entering COS or CFS Path](https://cloud.tencent.com/document/product/599/13996)
  * Stderr log: Same as Stdout Log
  * Command line: echo 'hello, world'
![](https://mc.qcloudimg.com/static/img/374f5532c7ee7af1211e91b2ff20ddd3/image.jpg)

4. Configure the storage mapping and click **Next** when finished.
   ![](https://mc.qcloudimg.com/static/img/4fa9b5f5516a4ca3e0c04dd6e85481c7/image.jpg)

5. Preview the task's JSON file and click **Save** after confirming it is correct.
  ![](https://mc.qcloudimg.com/static/img/7a462bf1530b0d867473fc95e316943e/image.jpg)

6. View the task template.
  ![](https://mc.qcloudimg.com/static/img/2138233d9271bc270abe0a2ba7deebdc/image.jpg)

### Submit a job
1. Click **Job** in the left navigation bar, select the target region such as "Guangzhou". Click **Create**.

2. Configure basic job information.
  * Job name: hello
  * Priority: Default value
  * Description: hello job
  ![](https://mc.qcloudimg.com/static/img/adfad5bef466330a4f5583a84531f4af/image.jpg)

3. Select the "hello" task on the left in "Task flow" and move the task onto the canvas on the right using the mouse.
  ![](https://mc.qcloudimg.com/static/img/f853b543e328755b0f15b6f62e5b2b8e/image.jpg)

4. Turn on "Task details" to the right of "Task flow", confirm the configuration is correct and click "Finish".
![](https://mc.qcloudimg.com/static/img/7e8faba3818f7ff2ada687ed7602be2e/image.jpg)

5. Query the result. You can view the running state of the job on the job list page.
  ![](https://mc.qcloudimg.com/static/img/6513237516f727b80f3a095ed18f5b77/image.jpg)
 - Click the job ID to view the running state of each task instance under "Task running conditions"
 - Click "View log" to view standard outputs and standard errors of task instances.

  ![](https://mc.qcloudimg.com/static/img/3e743ad83c975d57b7ad9f56d78b8933/image.jpg)

## What Can I Do Next?

This document illustrates a simple single-task job with no remote storage mapping involved to show the most basic capabilities of Batch. You can continue to test the advanced capabilities according to the Console User Guide.
- **Rich CVM configuration items**: Batch provides a wide variety of CVM configuration items, so you can customize the CVM configuration based on the specific business scenario.
- **Running remote code package**: Batch provides a **custom image + remote code package + command line** method for execution that technically meets your different business needs in all aspects.
- **Remote storage mapping**: Batch optimizes storage access and simplifies access to remote storage services into local file system operations.
