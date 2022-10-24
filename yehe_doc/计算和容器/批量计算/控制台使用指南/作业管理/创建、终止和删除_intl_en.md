## Overview
This document describes how to create, terminate and delete a job in the BatchCompute console. For more information about jobs, see the “Job” section in [Glossary](https://intl.cloud.tencent.com/document/product/599/10396).


## Directions
### Creating a Job
1. Log in to the [BatchCompute console](https://console.cloud.tencent.com/batch/job). 
2. Select **Job** in the left sidebar, and choose a region from the top.
3. Click **Create**.
4. On the **Create job** page, configure basic information of the job.
![](https://qcloudimg.tencent-cloud.cn/raw/aef77141251c4b605449439ea215859d.png)
5. In the **Task flow** section, select tasks under **Task template** and place them onto the right section. Drag and drop them to establish connections.
 ![](https://main.qcloudimg.com/raw/1436b756d73f6fffa68eff65741922ee.png)
6. Toggle on **Task information** on the right, and confirm the task configurations.
![](https://qcloudimg.tencent-cloud.cn/raw/a96a06571e4849b8e655cd4d672f1de2.png)
 + Each task is generated based on the task template.
 + You can select a task to edit the configurations. The task template is not affected by the editing.
7. Click **Done** to complete the process.   
	
### Terminating a Job
You can terminate a job under certain conditions. For more information, see [TerminateTaskInstance](https://intl.cloud.tencent.com/document/product/599/30489). See directions below:
1. Log in to the BatchCompute console, and select **[Job](https://console.cloud.tencent.com/batch/job)** in the left sidebar.
2. Click **Terminate** on the right of the target job.
![](https://qcloudimg.tencent-cloud.cn/raw/71601c4651392824992868b8be1c0fd9.png)
3. In the pop-up window, click **OK**.

### Deleting a Job
You can delete a job when it is in **Successful** or **Failed to run** status. See directions below:
1. Log in to the BatchCompute console, and select **[Job](https://console.cloud.tencent.com/batch/job)** in the left sidebar.
2. Click **Delete** on the right of the target job.
![](https://qcloudimg.tencent-cloud.cn/raw/844978fd665933043d1acce1c7a9f961.png)
3. In the pop-up window, click **OK**.



