
## Job
A job is the smallest unit in which a user submits a batch processing work and consists of a single or multiple tasks with dependencies. Dependencies among multiple batch tasks can be set through the very easy-to-use DAG syntax to combine multiple tasks into one single job, and then the tasks can be executed in sequence till all of them are completed, that is, the job is completed. Dependencies among tasks can only be specified when the job is submitted and cannot be modified after the submission is completed.
![Job example](https://main.qcloudimg.com/raw/9daacc1499e69b9c1f800e43bbe249d5.png)
## Task
A task is a basic component of a job and contains the information about the application actually executed on a CVM instance. Batch's scheduling system automatically creates CVM instances, installs images and executes applications based on the configuration submitted by the user. The task cannot be submitted directly. Instead, it must be placed in a job before it can be submitted for execution. One or more jobs can be placed in a job.

The core configurable properties of the task are as follows:
* ``CVM instance configuration``: The task is executed on CVM. You need to configure the type and specs of the CVM instance according to the characteristics of your computing task, such as selecting a compute instance (C2) or a high IO instance (IO2), memory and disk size and the VPC network where the instance resides
* ``Execution environment``: It contains image and command configuration. The image is usually a custom image containing your applications and the environment they depends on, and the command specifies how to launch these applications for computation.
* ``Remote storage mapping``: A remote storage address can be mapped to a local file system address. Currently, this supports COS. For details, see the separate definitions below.
* ``Standard output``: You can configure the mapping address (COS) of the standard output. The information output to stdout and stderr from the application will be uploaded to the corresponding address after the task is completed, so that the computing process can be backtracked after the task is completed.

## Task Instance
A task instance is the smallest unit of scheduling and execution in Batch. One task contains one or more task instances. Each task instance runs on a CVM instance and performs the corresponding computing task. You can set the number of instances that need to be executed concurrently in the task configuration. Batch will schedule the specified number of instances with the same configuration when the task is started. You can distinguish these instances by environment variables in the executor.

A typical application scenario of multiple instances is that the input data can be split and then processed concurrently, so that the advantages of elastic cloud resources can be fully taken of to compute concurrently and improve work efficiency.
## Image
An image is configured in a task and used when creating an instance. It must be a standard or custom CVM image. You need to prepare the compute environment and application in advance and make a custom image containing them. You can view your custom images in the [Image Console >>>](https://console.cloud.tencent.com/cvm/image?rid=1&imageType=1). For more information on how to make a custom image, see [Create Custom Images >>>](https://cloud.tencent.com/document/product/213/4942).
## Compute Environment
A compute environment (ComputeEnv) is a compute cluster consisting of one or more CVM instances and can be scaled up or down based on business needs. If the task configuration specifies the compute environment, the task instance will be scheduled to the nodes in the specified compute environment for execution; if no compute environment is specified, Batch will create a CVM instance for executing the task instance and terminate the CVM instance after the task instance is completed by default.
## Task Template
You can make a task template for common tasks based on which to customize different tasks and thus achieve quick submission of jobs.
## Remote Storage Mapping
Storage mapping maps the remote storage address (COS or CFS) to the CVM's local file system, so that the remote storage can be read and written in the same way as the local file system.
