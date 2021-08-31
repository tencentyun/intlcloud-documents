A stress test is designed to simulate DDoS attacks. To ensure the quality of the test, you are recommended to read this document carefully before conducting a stress test.

>The following suggestions are mainly about the impact of DDoS protection on stress testing. You may also need to consider other test-related factors, such as network bandwidth, linkage loads, and other basic resources.
### Adjusting Protection Policies
- Disable CC protection policies, or set the HTTP request threshold for CC protection to a value higher than the maximum value of your stress test.
- Disable DDoS protection policies, or set the cleansing threshold for DDoS protection to a value higher than the maximum value of your stress test.

### Limiting Traffic and Number of Requests in Stress Test
- The bandwidth of your stress test should be lower than 1 Gbps; otherwise, attack protection may be triggered.
- The number of HTTP requests in your stress test should be no more than 20,000 requests per second (QPS); otherwise, attack protection may be triggered.
- The number of new connections established per second, the maximum number of connections, and the number of inbound packets per second in your stress test should be less than 50,000, 2,000,000, and 200,000, respectively.

>If the traffic and number of requests in your stress test will exceed the above ranges, please contact [Tencent Cloud Technical Support](https://intl.cloud.tencent.com/support). We will offer support during your stress test.

### Evaluating Impact of Stress Test in Advance
You are recommended to contact Tencent Cloud solution architects or [Tencent Cloud Technical Support](https://intl.cloud.tencent.com/support) before you conduct the stress test to evaluate possible consequences and develop risk aversion measures.
