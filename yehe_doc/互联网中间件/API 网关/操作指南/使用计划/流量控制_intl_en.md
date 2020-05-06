You can limit the maximum number of calls under a usage plan by setting the QPS in it and binding a key.

For example, if you create a `secret_id` and `secret_key` pair and a usage plan with 1,000 QPS, bind the `secret_id` and `secret_key` pair to the usage plan, and bind the usage plan to the environment where you need to limit the traffic, such as the release environment, then an API in the release environment can be called by a user with the `secret_id` and `secret_key` pair at a frequency of up to 1,000 QPS.

Currently, up to 2,000 QPS can be set for each usage plan. Because the architecture of API Gateway is designed to be highly available, forwarded requests will be processed by different underlying nodes. If the traffic control value is too small (such as less than 5 QPS), there will be a certain probability that traffic control will be inaccurate, and the actual number of requests allowed to pass will be slightly greater than the set value.
