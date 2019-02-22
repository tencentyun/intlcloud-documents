[//]: # (chinagitpath:XXXXX)

The process of a stress testing is similar to a DDoS attack to a certain extent. To ensure a successful stress testing, it is recommended that you develop an appropriate implementation scheme by referring to this document before conducting a stress testing.

>! The following suggestions are specific for stress testing against DDoS attacks. For other aspects, such as network bandwidth, linkage load or other basic resources, should be taken into account according to the actual situation.
### Adjust protection policies
- Disable CC protection policies, or set the HTTP request threshold for CC protection to a value higher than the maximum value for stress testing.
- Disable DDoS protection policies, or set the cleansing threshold for DDoS protection to a value higher than the maximum value for stress testing.

### Limits of stress testing traffic and request number
- The stress testing traffic should be limited to 1 Gbps, otherwise attack defense may be triggered.
- It is recommended that the HTTP requests in the stress testing be limited to 20,000 QPS (i.e. not more than 20,000 HTTP requests per second), otherwise attack defense may be triggered.
- It is recommended that the number of new connections per second be limited to 50,000, the maximum number of connections to 2,000,000, and the number of inbound packets per second to 200,000, respectively.

>! If raise the limit for stress testing, please contact [Tencent Cloud support team](https://cloud.tencent.com/about/connect)

### Assess possible impacts of stress testing in advance
You can consult [Tencent Cloud support team](https://cloud.tencent.com/about/connect) before conducting the stress testing, to comprehensively assess the possible impacts and the scope of impact, and to establish reasonable risk aversion measures.

