The use limits of API Gateway under a single tenant are as follows:

| Category | Limit |
| ------------------------------ | ----- |
| Services under one tenant | 50 |
| APIs in one service | 200 |
| Custom domain names in one service | 5 |
| Usage plans under one tenant | 200 |
| Key pairs under one tenant | 400 |
| Keys bound to one usage plan | 50 |
| Usage plans bound to one key pair | 10 |
| Maximum QPS allowed in one usage plan | 2,000 |
| APIs bound to one usage plan | 10,000 |
| Maximum QPS supported by one service | 5,000 |
| Uploadable file size in one request | 16 MB |

>
- In a shared API Gateway cluster, the maximum QPS a single service can support is 5,000, and this value cannot be increased.
- If you need a higher QPS, you can activate the performance-optimized cluster service of API Gateway by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).

