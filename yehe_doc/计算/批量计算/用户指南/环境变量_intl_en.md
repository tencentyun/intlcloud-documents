## Summary

BatchCompute provides the instances of a task with the task-related environment variable information to allow user program to execute different computing tasks based on the environment variables.

## Details

| Variable | Name | Description |
|---------|---------|---------|
| BATCH_JOB_ID | Job ID | ID of the job to which an instance belongs. It is included in the returned result after the job is submitted, such as job-n4ohivif |
| BATCH_TASK_NAME | Task name | Name of the task to which an instance belongs. It is specified when the job is submitted, such as `"TaskName": "Task1"` |
| BATCH_TASK_INSTANCE_NUM | Total number of instances of a task | The total number of instances requested to run concurrently in the task to which the instances belong, such as `"TaskInstanceNum": 5` |
| BATCH_TASK_INSTANCE_INDEX | Task instance index | The index of an instance in the task to which the instance belongs; for example, if five instances are specified to run concurrently in a task, then the indices of these instances are 0, 1, 2, 3, 4 |


