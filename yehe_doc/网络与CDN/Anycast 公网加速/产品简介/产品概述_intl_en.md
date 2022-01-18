## What is Tencent Cloud Anycast Internet Acceleration?

Tencent Cloud Anycast Internet Acceleration (AIA) is a dynamic acceleration network with global coverage that can greatly improve the Internet access experience of your business. Unlike other application-layer acceleration services, AIA can optimize IP transfer quality, enable access from the nearest entry node and reduce network transfer jitter and packet loss, thereby improving the service quality of in-cloud applications, expanding the service scope and simplifying backend deployment.

## Why Tencent Cloud AIA?

### Low latency

AIA uses the Anycast method to simultaneously publish an IP to multiple regions. The request packet will reach the optimal IP publishing region according to the transfer protocol. The packet will prioritize entering Tencent Cloud before reaching the server through Tencent Cloud's private network lines, avoiding Internet congestion and reducing latency.

### High reliability

Internet transfers can be unreliable. For example, if a line interruption of the ISP leads to an inability to access the Internet, users will have no choice but to wait for recovery to complete the transfers. With the help of AIA, multiple paths and entries are made possible by Tencent Cloud's private networks, the ISP's backbone networks and Tencent Cloud's POPs, preventing connection failures caused by single-region or single-line network outages and enhancing network stability.

### Reduced Jitter

Unstable performance of the Internet link can lead to an unstable service experience such as network jitter caused by cross-ISP or cross-border connection issues. In contrast, Tencent Cloud private network lines offer stable performance. AIA allows the request to access the nearest Tencent Cloud node and be transferred through Tencent Cloud's private network lines across regions, perfectly resolving Internet jitter issues.

### Simplified deployment

Implementing services that are accessed by end users in many different regions can be cumbersome because servers have to be deployed in each region, DNS has to be properly configured to enable load balancing and IPs vary in different regions. AIA eliminates the need to configure IPs for each region, avoiding geographic dispersion at the IP level. In addition, only one set of logics need to be maintained on the backend, as requests from different regions are accelerated to reach the backend servers through the private network.

### Global Load Balancing

AIA uses the Anycast addressing method to simultaneously publish the IP to multiple regions. The request packet will reach the optimal IP publishing region (usually the nearest region) according to the transfer protocol, which achieves global load balancing. Additionally, in the case of a traffic-based attack, the cross-region publishing of IPs helps distribute the attacking traffic.

### Ease of use

AIA is compatible with common IP operations, allowing you to purchase just one accelerating elastic public IP and simplifying usage. It supports self-service Internet bandwidth limiting, making it easy to configure upper limits for bandwidth based on cost or server processing speed. In addition, it supports traffic monitoring for backtracking and analysis as well as binding and unbinding for easier backend resource changes.
