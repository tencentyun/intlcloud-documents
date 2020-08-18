## What is Tencent Cloud Anycast Internet Acceleration?

Anycast Internet Acceleration (AIA) is a cross-region dynamic acceleration network that significantly enhances your businesses' access to public network. Different from other acceleration services at the application layer, AIA is capable of achieving IP transfer optimization and multi-entry nearby access, while reducing issues such as network jitter and packet loss, which can ultimately increase the service quality of your in-cloud applications, expand their service scope, and streamline backend deployment.

## Why Tencent Cloud AIA?

### Low latency

AIA publishes an IP to multiple regions simultaneously by means of Anycast. According to the transfer protocol, a request package will arrive at the optimal IP publishing region to gain privileged access to Tencent Cloud and then get to the CVM instance through Tencent Cloud private network, avoiding public network congestion and reducing latency.

### High reliability

Internet transmission is unreliable, and for the inaccessibility to the network caused by ISP's line interruption, users can only wait for its restoration. For Tencent Cloud backbone network, ISP's backbone network and Tencent Cloud POP point, AIA can achieve network access through multiple paths and multiple entries, block single-region and single-line failures, and improve the network stability.

### Reducing Jitter

The performance of Internet link is unstable, and network jitter can be caused by north-south or cross-border issue, for example, thereby affecting the service experience. After connecting the request to Tencent Cloud from nearby, AIA can implement cross-region transmission through the private network-based Direct Connect of Tencent Cloud, to solve the problem of Internet jitter and ensure the stability of transmission.

### Simplified deployment

For services with customers located in multiple regions that need to be connected to nearby, you must deploy servers and configure the DNS to implement load balance in these regions. Deployment can be quite complex because different regions have different IPs. After AIA is used, the region attributes are converged at the IP level. It is not required to configure the IP for each region, and only one set of logic needs to be maintained at the backend. The requests from different regions are directly accelerated to the backend servers with the Direct Connect.

### Global Load Balancing

An IP can be published to multiple regions simultaneously with Anycast, and a request packet will arrive at the optimal IP publishing region (usually the nearest one) according to the transfer protocol, thereby achieving global load balancing. When a traffic attack occurs, as the IP has been published to multiple regions, the attacking traffic will be distributed.

### Ease of use

AIA can be made compatible with common IP operations just by purchasing an accelerated EIP. It is simple to use and supports customizing the limit on public network bandwidth, which makes it easier for you to configure an appropriate bandwidth limit depending on costs or server processing speed. Plus, it features traffic monitoring for convenient issue traceability and analysis, and supports binding and unbinding operations to help you make changes to backend resources conveniently.

