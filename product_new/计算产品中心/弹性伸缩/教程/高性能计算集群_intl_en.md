## Use Case
With cloud computing, high performance computing (HPC) can use applications with higher bandwidth and higher computing capacity to address complex scientific, engineering and business issues.
However, the problems solved by HPC are usually based on projects, and have huge demand for the high scalability of the cloud platform. The compute node can be configured in a launch configuration (template) for the scaling group. By increasing the desired capacity, multiple compute nodes can be generated with one click for any calculation tasks. After saving the calculation results, you can delete the compute nodes for the task by modifying the desired capacity.

![Alt text](https://main.qcloudimg.com/raw/06b9146add277329c32f68606d9a3a51.png)

## Usage
Create a launch configuration for the nodes in the cluster, and place the computing cluster into the scaling group.

There are two ways to use the original data for high performance computing:

- Save the data to a snapshot, so that the data disks of the scaled-out CVMs are created based on the snapshot.

- Save the data to a data server, so that all the compute nodes in the cluster can be read in the data server.


## Benefits of AS
- AS can greatly reduce the workload of manual preparation of environments.

- There is no need to reserve long-term resources for temporary tasks.

## Applicable industries

- Weather forecasting

- Gene sequencing

- Animation rendering, film and TV rendering

- Other industries that require high performance computing
