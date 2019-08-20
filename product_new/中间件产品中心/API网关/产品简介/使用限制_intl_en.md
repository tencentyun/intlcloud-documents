The use limits of API Gateway for a single tenant are as below:

| Category                         | Limits  |
| ------------------------------ | ----- |
| Number of services per single tenant              | 50  |
| Number of APIs per service              | 200 |
| Number of custom domain names per service    | 5  |
| Number of usage plans per single tenant            | 200  |
| Number of key pairs per single tenant              | 400   |
| Number of keys that can be bound per usage plan       | 50    |
| Number of usage plans that can be bound per single key pair | 10    |
| Maximum QPS that can be configured per usage plan    | 2000  |
| Number of APIs that can be bound to usage plan        | 10000个 |
| Maximum QPS supported per service  | 5000  |


>- In the shared cluster of API Gateway, a single service can support up to 5000 QPS, and this limit cannot be increased.
>- If you have higher QPS requirements, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to activate the optimized cluster service of API Gateway.

