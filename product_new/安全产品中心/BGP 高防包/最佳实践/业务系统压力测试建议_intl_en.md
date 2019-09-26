Stress testing is designed for mimicking DDoS attacks. To ensure the quality of the test, you are advised to read this document carefully before conducting a stress test and formulating an implementation plan.

>The following suggestions are based on the influence of anti-DDoS protection on stress testing. Other test-related factors, such as network bandwidth, linkage loads, or other basic resources, are subject to circumstance.
### Adjusting Protection Policies
- Disable CC protection policies, or set the HTTP request threshold for CC protection to a value higher than the maximum value for stress testing.
- Disable anti-DDoS protection policies, or set the cleansing threshold for anti-DDoS protection to a value higher than the maximum value for stress testing.

### Controlling Stress Testing Traffic and Request Number
- The bandwidth of stress testing should be slower than 1 Gbps, otherwise the attack defense may be triggered.
- The number of HTTP requests in the stress testing should be no more than 20,000 requests per second (QPS), otherwise the attack defense may be triggered.
- The number of new connections per second, total connections, and inbound packets per second should be less than 50,000, 2,000,000, and 200,000 respectively.

>If the stress testing requirements exceed the above ranges, please contact [Tencent Cloud Technical Support](https://intl.cloud.tencent.com/support). The after-sales team will offer support during stress testing.

### Assessing Stress Testing in Advance
Contact Tencent cloud architectural engineers or [Tencent Cloud Technical Support](https://intl.cloud.tencent.com/support) before the stress testing to comprehensively assess the possible consequences involved and to formulate risk aversion measures.

