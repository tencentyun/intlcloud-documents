Tencent Cloud BatchCompute enables you to run batch computing workloads on CVM instances. It is a common way for developers, scientists, and engineers to access large amounts of computing resources, which eliminates the need of tedious configuration and management of required infrastructure. Just like traditional batch computing software, it can efficiently configure resources in advance in response to submitted tasks so as to remove capacity constraints, reduce computing costs, and deliver results more quickly.



BatchCompute operations supported by CloudAudit are as shown below:

| Operation Name	| Resource Type | Event Name |
|------------|------------------------------|------------|
| Creating compute environment     | batch        | CreateComputeEnv |
| Creating CPM compute environment   | batch     | CreateCpmComputeEnv |
| Creating task template     | batch      | CreateTaskTemplate |
| Deleting compute environment     | batch        | DeleteComputeEnv |
| Deleting job       | batch               | DeleteJob |
| Deleting task template     | batch     | DeleteTaskTemplates |
| Viewing compute environment information   | batch      | DescribeComputeEnv |
| Viewing information about activities in compute environment | batch | DescribeComputeEnvActivities |
| Viewing compute environment list   | batch     | DescribeComputeEnvs |
| Viewing job information     | batch             | DescribeJob |
| Viewing job list     | batch            | DescribeJobs |
| Viewing job submission information  | batch   | DescribeJobSubmitInfo |
| Viewing task information     | batch            | DescribeTask |
| Getting task log details   | batch        | DescribeTaskLogs |
| Querying task template     | batch   | DescribeTaskTemplates |
| Modifying compute environment     | batch        | ModifyComputeEnv |
| Modifying task template     | batch      | ModifyTaskTemplate |
| Submitting job       | batch               | SubmitJob |
| Terminating job       | batch            | TerminateJob |
| Terminating task instance     | batch   | TerminateTaskInstance |
