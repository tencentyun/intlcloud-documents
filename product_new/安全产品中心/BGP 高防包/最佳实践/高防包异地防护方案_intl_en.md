## Background
Anti-DDoS Pro provides up to 300 Gpbs of protection bandwidth in Shanghai but a lower bandwidth in Guangzhou and Beijing. In addition, Anti-DDoS Pro is not available in Chengdu, Chongqing, and other regions in China.
If your business origin server is deployed in Tencent Cloud and you need to use the DDoS protection capability of regions other than the region where your origin server is located, you may consider the following solution.

## Solution
This solution involves Anti-DDoS Pro, Cloud Load Balancer (CLB), and your origin server. Firstly, you will need to deploy a CLB instance in a region where you have Anti-DDoS Pro resources and bind the CLB to the Anti-DDoS Pro instance. Next, configure the private network forwarding rules for the CLB to ensure that your business can be accessed through the public IP of the CLB.
- Normally, business traffic will be resolved to the public IP of the origin server or directly to the public IP of the CLB in another region. The business traffic will access the nearest origin server.
- If attacks occur, business traffic will be resolved to the CLB IP for the Anti-DDoS Pro instance to cleanse the traffic. After the traffic is cleansed, the CLB will forward the traffic back to the origin server via private network Direct Connect.

The following figure describes the details of the solution:
![](https://main.qcloudimg.com/raw/26603bdc4a5c0ba147ee14b0d3f7b1e7.png)

## Benefits
- The DDoS protection capability will no longer be limited by regions and can be as high as 300 Gpbs.
- The business traffic will be forwarded via private network Direct Connect with high reliability and a low latency.
- You will enjoy all the advantages brought by Tencent Cloud BGP network. All your public IPs will be BGP IPs and the latency will be very low.

## Tips
- Deploy Anti-DDoS Pro and CLB in advance.
- Establish a business availability monitoring system so that you can promptly notice and respond to any problem with access to the origin server when the automatic switching mechanism is not deployed.
- Test regularly, familiarize yourself with the solution details, and solve potential problems.
