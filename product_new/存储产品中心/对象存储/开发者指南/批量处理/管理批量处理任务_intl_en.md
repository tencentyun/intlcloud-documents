This document describes how to manage batch operation jobs in the COS console.

## Filtering Jobs

You can view the list of the batch operation jobs created in the last 90 days using the [List Jobs](https://intl.cloud.tencent.com/document/product/436/33783) API. The list contains information of each job, such as job ID, description, priority, status, and execution progress. You can filter them by job status in the list to display the ones in the same status or filter them by job description or ID in the console.

## Querying Job Status

If you need more information, you can get all the information of a job using the [DescribeJob](https://intl.cloud.tencent.com/document/product/436/33782) API. This API will return information such as the task configuration of the specified job, object inventory information, and job report.

## Setting Job Priority

You can set priority for your batch operation jobs, and COS will execute them based on priority, i.e., executing jobs of a higher priority first. Priority is expressed as an integer; the greater the value, the higher the priority. You can modify the priority during job execution. If a higher-priority job needs to be added, you can run it first by pausing the lower-priority job.

> Although higher-priority jobs generally take precedence over lower-priority ones, priority is not a criterion for sequential execution. If you want to run batch operation jobs sequentially, please monitor the execution status of each job on your own and start them manually.

## Job Status

Job status changes as the execution proceeds, as shown below:
<img src="https://main.qcloudimg.com/raw/1b2edc84eb8cc664dc006f56c6810e2e.png"  width="95%">


The specific meaning of each job status is as follows:

| Job Status | Description | Next Status |
| ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| New | When a job is created, its status will be "New". | It can change to "Preparing", meaning that COS starts to parse the inventory in the job. |
| Preparing | When COS starts to parse the configured inventory in the batch operation job, the job status will change to "Preparing". | It can change to "Ready" or "Suspended". The former means that COS has finished parsing the job configuration information and is going to perform the specified tasks on the objects in the inventory based on the configuration, while the latter means that COS has finished parsing the job configuration information but is still waiting for your confirmation before it proceeds to perform the specified tasks (this status appears if a batch operation job is configured in the console). |
| Suspended | A batch operation job pending your confirmation is in the "Suspended" status, which appears if the job is created in the console. After your confirmation, COS will start executing the job, and the status will change accordingly and cannot revert to "Suspended". | When you confirm to execute the job, the job status will change to "Ready". |
| Ready | When COS has finished parsing the object inventory and job configuration information in your batch operation job and is going to perform tasks, the job status will change to "Ready". | It can change to "Active", at which point COS starts executing the job. If a higher-priority job is running, COS will keep the job status as "Ready" until the job status of the higher-priority job changes to "Complete". |
| Active | When COS is performing tasks on the objects in the inventory based on the configuration information, the job status will be "Active". You can query job progress in the console or by calling the [DescribeJob](https://intl.cloud.tencent.com/document/product/436/33782) API. | It can change to "Complete", "Failing", "Pausing", or "Canceling" if your job succeeds, fails, or is paused or canceled. |
| Pausing | After COS pauses an ongoing job and before the status changes to "Paused", the job status in between will be "Pausing". | It can be followed by "Paused" when COS has successfully paused the ongoing job. |
| Paused | If a higher-priority job is created, the status of the ongoing job will change to "Paused". | If the higher-priority job is completed, fails, or is pending conformation, the job in "Paused" status can automatically shift to "Active" status. |
| Complete | When the batch operation job has successfully completed the tasks on all the objects in the inventory or fails, the job status will change to "Complete".<br>If job report generation is configured, COS will deliver the report to your specified bucket when the status changes to "Complete". | "Complete" is a final status, i.e., the job will not change to any other status. |
| Canceling | After COS cancels an ongoing job and before the status changes to "Canceled", the job status in between will be "Canceling". | It can be followed by "Canceled" when COS has successfully canceled the ongoing job. |
| Canceled | When a batch operation job is successfully canceled, the job status will change to "Canceled". At this point, you cannot make any modification to the job status. | "Canceled" is a final status. i.e., the job will not change to any other status. |
| Failing | The "Failing" status comes before "Failed". | It can change to the "Failed" status. |
| Failed | After a job fails, the job status will change to "Failed". For more information, see [Tracking Job Failure](https://intl.cloud.tencent.com/document/product/436/32961). | "Failed" is a final status, i.e., the job will not change to any other status. |



## Tracking Job Failure

If a problem arises during job execution, such as trouble in parsing the object inventory, the batch operation job will fail, and COS will return the corresponding error code and cause. You can call the [DescribeJob](https://intl.cloud.tencent.com/document/product/436/33782) API or view the job report to get the cause of failure and other information.

COS sets a task failure threshold for each batch operation job to avoid frequent task failures. If a job involves more than 1,000 tasks, COS will monitor the task failure rate, i.e., proportion of failed tasks to all tasks executed. If the rate exceeds the threshold of 50% at any moment, COS will terminate the job and return the failure message. You can check the cause why this happens (e.g., the object inventory contains large amounts of information on non-existing objects). Then, you can fix the problem accordingly and create a job again.

> COS executes batch operation jobs in an async manner and does not necessarily perform tasks in the same order that the objects are listed in the inventory. Therefore, you cannot determine which object is being operated on according to the order in the object inventory and whether a task is successful or fails. However, you can get the information on successful or failed tasks from the job report.


## Job Report

You can configure whether to output a job report when creating a job. If yes, COS will output a job report when the job succeeds, fails, or is canceled. You can view the information on all successful or failed tasks in the job report.

A job report contains information such as the configuration parameters and execution status of the specified task as well as name and version ID of the objects operated on, task status codes, and error description.
