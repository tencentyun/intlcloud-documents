## Job
A job is the smallest unit in which a user submits a batch processing work and consists of one or multiple tasks with dependencies. Dependencies among multiple batch processing tasks can be set through the very easy-to-use DAG syntax to combine such tasks into one single job, and then the tasks can be executed in sequence till all of them are completed, that is, the job is completed. Dependencies among tasks can be specified only when the job is submitted and cannot be modified after the submission.
![](https://main.qcloudimg.com/raw/b1ddc38f5a3eb6396599db1418100b1e.png)
## Task
A task is a basic component of a job and contains the information about the application actually executed on a CVM instance. BatchCompute's scheduling system automatically creates CVM instances and executes applications based on the configuration submitted by the user. The task cannot be submitted directly. Instead, it must be placed in a job for submission and execution. One or more jobs can be placed in one job.

The core configurable attributes of a task are as follows:
* ``CVM instance configuration``: the task is executed on CVM. You need to configure the type and specification of the CVM instance according to the characteristics of your computing task, such as selecting a compute instance (C2) or a high IO instance (IO2), memory and disk size, and the VPC where the instance resides.
* ``Execution environment``: it contains the image and command configuration. The image is usually a custom image containing your applications and the environment they depends on, and the command specifies how to launch these applications for computation.
* ``Remote storage mapping``: a remote storage address can be mapped to a local file system address. Currently, this feature supports COS. For more information, please see the separate definitions below.
* ``Standard output``: you can configure the mapping address (COS) of the standard output. The information output to `stdout` and `stderr` from the application will be uploaded to the corresponding address after the task is completed, so that the computing process can be traced back after the task is completed.

## Task Template
You can make a task template for common tasks based on which to customize different tasks and thus submit jobs more quickly.

## Remote Storage Mapping
Storage mapping maps the remote storage address (COS or CFS) to the CVM instance's local file system, so that the remote storage can be read and written in the same way just like a local file system.

## Task Instance
Task instance is the smallest unit of scheduling and execution in BatchCompute. One task contains one or more task instances, each of which runs on a CVM instance for executing the corresponding computation task. You can set the number of instances that need to be executed concurrently in the task configuration. BatchCompute will schedule the specified number of instances with the same configuration when the task is started. You can distinguish among these instances by environment variables in the executor.

A typical application scenario of multiple instances is that the input data can be split and then processed concurrently, so that the advantages of elastic cloud resources can be fully leveraged to compute concurrently and improve work efficiency.

## Image
An image is configured in a task and used for instance creation. It must be a standard or custom CVM image. You need to prepare the compute environment and application and make a custom image containing them. You can view your custom images in the [Image Console >>>](https://console.cloud.tencent.com/cvm/image?rid=1&imageType=1). For more information on how to make a custom image, please see [Creating Custom Image >>>](https://intl.cloud.tencent.com/document/product/213/4942) .
## Compute Environment
A compute environment (ComputeEnv) is a compute cluster consisting of one or more CVM instances and can be scaled up or down based on business needs. If the task configuration specifies the compute environment, the task instance will be scheduled to the nodes in the specified compute environment for execution; otherwise, BatchCompute will create a CVM instance for executing the task instance and terminate the CVM instance after the task instance is completed by default.


