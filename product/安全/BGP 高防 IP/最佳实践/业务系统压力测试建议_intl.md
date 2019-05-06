

Stress testing is designed for mimicking DDoS attacks. To ensure the quality of the test, we strongly recommend you to read this document carefully before conducting a stress testing and formulating an implementation plan.

>! The following suggestions are specific for stress testing against DDoS attacks. You should also consider other factors such as network bandwidth, linkage load, and other infrastructure resources, and adjust your plan based on your actual situation.

### Adjust protection policies
- Disable CC protection policies, or set the HTTP request threshold for CC protection to a value higher than the maximum value for stress testing.
- Disable DDoS protection policies, or set the cleansing threshold for DDoS protection to a value higher than the maximum value for stress testing.

### Control stress testing traffic and request number
- The bandwidth of stress testing should be slower than 1 Gbps. Otherwise,  attack defense can be triggered.
- We recommend that the number of HTTP requests in the stress testing is no more than 20,000 QPS (requests per second). Otherwise,  attack defense may be triggered.
- We recommend that the number of new connections per second, the maximum number of connections, and the number of inbound packets per second is less than 50,000, 2,000,000, and 200,000 respectively.

>! If you need to raise the stress testing limits, please contact [Tencent Cloud support team](https://cloud.tencent.com/about/connect)

### Assess possible stress testing results
You can consult [Tencent Cloud support team](https://cloud.tencent.com/about/connect) for the stress testing. We will help you evaluate the possible testing results to avoid risks.

