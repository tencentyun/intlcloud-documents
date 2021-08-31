### Is BatchCompute a paid service?
The BatchCompute service itself is completely free of charge. The CVM instances created for job execution are charged in the corresponding CVM billing mode. For more information, please see [Billing Mode >>](https://intl.cloud.tencent.com/document/product/599/10447)

### What is the relationship between a job and a task?

A job is a carrier for submission of the computing work in BatchCompute and consists of one or more tasks. If there are multiple tasks, there will be a sequence of execution between them. The configuration of a job mainly contains the configurations and execution sequence of the tasks inside it.

### What is the relationship between a task and an instance?

The most important purpose of a task is to describe the CVM instance configuration, image environment, and execution command used to start your application. In addition, the task can configure standard output redirection, remote storage mapping, and other auxiliary functions.

An instance is a CVM instance created according to the task and actually executes the application. The task can specify the number of instances that need to be started concurrently. All the instances are created and execute the application based on the task configuration. You can use the numbers in environment variables to distinguish among the instances.

### Is remote storage mapping mandatory for data inputting and outputting? Is there any other way to read and write data?

Remote storage mapping is a configuration item provided by BatchCompute, which is to reduce the development difficulty in terms of storage. You don't necessarily have to use it. You can have the application access the data on various storage services such as CBS, CFS, and COS.

### What types of instances can I purchase in BatchCompute?

All types of instances can be purchased, except FPGA, GPU, and network enhanced instances as well as some instance types in beta test. For the list of instance types supported in each AZ, please see [Instance Specification](https://intl.cloud.tencent.com/document/product/213/11518).
