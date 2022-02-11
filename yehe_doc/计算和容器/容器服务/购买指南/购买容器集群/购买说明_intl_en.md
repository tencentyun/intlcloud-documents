
## Purchase Notes



>? If the service is unavailable due to the failure of you to abide by the following suggestions, the corresponding service downtime shall not be counted towards the service unavailability period. For more information, see [TKE Service Level Agreement](https://intl.cloud.tencent.com/zh/document/product/457/12356?lang=zh&pg=#4.-release-of-liabilities).

Refer to the recommended configuration below and choose the model that best suits your requirements, so as to prevent cluster unavailability caused by heavy load of the control plane.
Assume that you want to deploy 50 nodes in a cluster and need 2,000 Pods. You need to select a model with the maximum number of nodes of 100, but not 50.

Note: the number of Pods includes Pods in all namespaces and in any status, and excludes the Pods related to system components such as cni-agent.

| Max nodes | Max Pods (recommended) | Max ConfigMap (recommended) | Maximum CRDs (recommended) |
| ---------------- | ------------------- | ------------------------- | ------------------- |
| 5                | 150                 | 32                        | 150                 |
| 20               | 600                 | 64                        | 600                 |
| 50               | 1500                | 128                       | 1250                |
| 100              | 3000                | 256                       | 2500                |
| 200              | 6000                | 512                       | 5000                |
| 500              | 15000               | 1024                      | 10000               |
| 1000             | 30000               | 2048                      | 20000               |
| 3000             | 90000               | 4096                      | 50000               |
| 5000             | 150000              | 6144                      | 100000              |

