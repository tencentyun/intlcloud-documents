## Overview 
TKE serverless clusters free you from managing cluster nodes. However, to reasonably allocate resources and accurately calculate fees, you need to specify resource specifications for Pods when deploying a workload. Tencent Cloud allocates computing resources to the workload and calculates the fees based on the specified specifications.

When you use the Kubernetes API or kubectl to create a workload for a TKE serverless cluster, you can use annotations to specify resource specifications. If no specifications are specified, the TKE serverless cluster will calculate the specifications based on the container parameters set for the workload, such as Request and Limit. For more information, see [Specifying resource specifications](https://intl.cloud.tencent.com/document/product/457/36161).

>!
> - The resource specifications indicate the maximum amount of resources available for containers in a Pod.
> - The following tables list the supported CPU and GPU specifications. Ensure that allocated resources do not exceed the supported specifications.
> - The total amount of resources specified by Request for all the containers in a Pod cannot exceed the maximum pod specification.
> - The amount of resources specified by Limit for any container in a Pod cannot exceed the maximum Pod specification.


## CPU Specifications

The following table lists CPU specifications that TKE serverless clusters provide for Pods in all regions where CPU resources are supported. TKE serverless clusters also provide a set of CPU options. Different CPU sizes correspond to different memory ranges. Select the CPU specification as needed when creating a workload.

#### Intel
| CPU (Cores) | Memory Range (GiB) | Granularity of Memory Range (GiB) |
| -------|-------|------- |
| 0.25 | 0.5, 1, 2 | - |
| 0.5 | 1, 2, 3, 4 | - |
| 1 | 1 - 8 | 1 |
| 2 | 4 - 16 | 1 |
| 4 | 8 - 32 | 1 |
| 8 | 16 - 32 | 1 |
| 12 | 24 - 48 | 1 |
| 16 | 32 - 64 | 1 |

#### Star Lake AMD
The AMD processor provides high performance with high reliability, security, and stability based on the Star Lake servers developed by Tencent Cloud. For more information, see [CVM Standard SA2 Introduction](https://intl.cloud.tencent.com/document/product/213/11518).

| CPU (Cores) | Memory Range (GiB) | Granularity of Memory Range (GiB) |
| -------|-------|------- |
| 1 | 1 - 4 | 1 |
| 2 | 2 - 8 | 1 |
| 4 | 4 - 16 | 1 |
| 8 | 8 - 32 | 1 |
| 16 | 32 - 64 | 1 |

## GPU Specifications

The following table lists the GPU specifications that TKE serverless clusters provide for Pods. Different GPU card models and sizes correspond to different CPU and memory options. Select the GPU specification as needed when creating a workload.
>!If you create, manage, and use GPU workloads using a YAML file, see [Annotation](https://intl.cloud.tencent.com/document/product/457/36162).

| GPU Model                   | GPU/Card | CPU/Core | Memory/GiB |
| :------------------------- | :----- | :----- | :------- |
| NVIDIA Tesla V100 - 1    | 1      | 8      | 40       |
| NVIDIA Tesla V100 - 2    | 2      | 18     | 80       |
| NVIDIA Tesla V100 - 4    | 4      | 36     | 160      |
| NVIDIA Tesla V100 - 8    | 8      | 72     | 320      |
| 1/4 NVIDIA T4 - 1/4      | 1      | 4      | 20       |
| 1/2 NVIDIA T4 - 1/2      | 1      | 10     | 40       |
| NVIDIA T4 - 1            | 1      | 8      | 32       |
| NVIDIA T4 - 1            | 1      | 20     | 80       |
| NVIDIA T4 - 1            | 1      | 32     | 128      |
| NVIDIA T4 - 2            | 2      | 40     | 160      |
| NVIDIA T4 - 4            | 4      | 80     | 320      |
| NVIDIA A10 - PNV4 - 1    | 1      | 28     | 116      |
| NVIDIA A10 - PNV4 - 2    | 2      | 56     | 232      |
| NVIDIA A10 - PNV4 - 4    | 4      | 112    | 466      |
| NVIDIA A10 - PNV4 - 8    | 8      | 224    | 932      |
| NVIDIA A10 - GNV4 - 1    | 1      | 12     | 44       |
| NVIDIA A10 - GNV4v - 1/4 | 1      | 6      | 24       |
| NVIDIA A10 - GNV4v - 1/2 | 1      | 14     | 58       |
| NVIDIA A10 - GNV4v - 1   | 1      | 28     | 116      |





