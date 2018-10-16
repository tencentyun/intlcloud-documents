## Summary

Batch provides task-related environment variables in the instances used by the tasks, which makes it easier for the user's application to execute different computing tasks according to the environment variables.

## Details

| Variable | Name | Meaning |
|---------|---------|---------|
| BATCH_JOB_ID | Job ID | ID of the job to which the instance belongs; contained in the return structure after the job is submitted; example: job-n4ohivif |
| BATCH_TASK_NAME | Task name | Name of the task to which the instance belongs; specified when submitting the job; example: `"TaskName": "Task1"` |
| BATCH_TASK_INSTANCE_NUM | Total number of task instances | Total number of concurrent instances of the task to which the instances belong; example: `"TaskInstanceNum": 5` |
| BATCH_TASK_INSTANCE_INDEX | Task instance sequence number | The sequence number of the instance in the task; for example, if the task specifies 5 concurrent instances, then the sequence numbers of these 5 instances are 0, 1, 2, 3 and 4 respectively |


