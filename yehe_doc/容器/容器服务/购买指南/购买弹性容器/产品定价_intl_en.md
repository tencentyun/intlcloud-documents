Elastic Kubernetes Service (EKS) bills a pod by multiplying the [resource specification](https://intl.cloud.tencent.com/document/product/457/34057) of the pod by the **Unit price of the resource** and **Running time**. The following table shows the unit prices of the CPU and memory resources.

| Billing Item | Price (per second) |  Price (per hour) |
|---------|---------|---------|
| CPU | 0.000004976 USD per core per second |  0.0179 USD per core per hour |
| Memory | 0.000002073 USD per GiB per second |  0.0075 USD per GiB per hour |


#### Star Lake AMD
Based on Tencent Cloud’s self-developed Star Lake servers, EKS provides reliable, secure, and stable high performance. For more information, see [CVM Standard SA2 Introduction](https://intl.cloud.tencent.com/document/product/213/11518#SA2).

| Billing Item | Price (per second) | Price (per hour) |
|---------|---------|---------|
| CPU | 0.00000219 USD per core per second | 0.0079 USD per core per hour |
| Memory | 0.00000127 USD per GiB per second | 0.0046 USD per GiB per hour |


## Running Time
The running time is the time that elapses from when a pod fetches the first container image until the pod stops running. The pod is billed for the resources used during this period, which is measured in seconds.


## Billing Examples
#### Sample 1
Assume that the specification of pods managed by a Deployment is 2 cores and 4 GB memory, and the number of replicas is fixed at 2. If the period from the time when the Deployment is launched to the time when the Deployment is terminated is 5 minutes, the Deployment is billed for the resources used during the running time of 300 seconds (5 minutes × 60 seconds). 

In this case, the running fees of the Deployment = 2 × (2 × 0.000004976 + 4 × 0.000002073) × 300 = 0.019495 USD.


#### Sample 2
Assume that a CronJob needs to launch 10 pods with 4 cores and 8 GB memory each time and terminate the pods 10 minutes later. If the CronJob executes the job twice a day and this task is managed by EKS, the task is billed as follows:

Daily task fees = 2 × 10 × (4 × 0.000004976 + 8 × 0.000002073) × 600 = 0.437856 USD.
