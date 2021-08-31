## Background
Anti-DDoS Pro provides up to 300 Gbps of protection bandwidth in Shanghai but a lower bandwidth in Guangzhou and Beijing. In addition, Anti-DDoS Pro is not available in Chengdu, Chongqing, and other regions in Mainland China.
If your business real server is deployed in Tencent Cloud and you need to use the DDoS protection capability in regions other than the region where your real server is located, you may consider the following solution.

## Solution
This solution involves Anti-DDoS Pro, Cloud Load Balancer (CLB), and your real server. First, you will need to deploy a CLB instance in the region where you have Anti-DDoS Pro resources and bind it to your Anti-DDoS Pro instance. Then, configure the private network forwarding rules for CLB to ensure that your business can be accessed through the public IP of the CLB instance.
- Under normal circumstances, business traffic will be resolved to the public IP of the real server or directly to the public IP of the CLB instance in another region for nearby access to the real server.
- If attacks occur, business traffic will be resolved to the CLB IP for the Anti-DDoS Pro instance to cleanse the traffic. After the traffic is cleansed, CLB will forward the traffic back to the real server through private network Direct Connect.

The following figure describes the details of the solution:
![](https://main.qcloudimg.com/raw/26603bdc4a5c0ba147ee14b0d3f7b1e7.png)

## Benefits
- The DDoS protection capability will no longer be limited by regions and can be as high as 300 Gbps.
- The business traffic will be forwarded via private network Direct Connect with high reliability and a low latency.
- You will enjoy all the advantages brought by Tencent Cloud BGP network. All your public IPs will be BGP IPs and the latency will be very low.

## Suggestions and Notes
- Deploy Anti-DDoS Pro and CLB instances in advance.
- Establish a business availability monitoring system so that you can promptly detect and respond to any problem with access to the real server if no automatic switching mechanism is deployed.
- Test regularly, familiarize yourself with the solution details, and solve potential problems promptly.
