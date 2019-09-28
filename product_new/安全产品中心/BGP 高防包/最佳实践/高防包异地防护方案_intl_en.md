## Background
Due to objective factors, Anti-DDoS Pro provides up to 300 Gpbs of protection bandwidth in Shanghai and a lower bandwidth in Guangzhou and Beijing. In addition, Anti-DDoS Pro is not available in Chengdu, Chongqing, and other regions in China.
If your business origin servers are deployed on Tencent Cloud and you require DDoS protection in regions other than the region where Tencent Cloud origin servers locate, you can refer to this plan.

## Protection Solution
This plan consists of Anti-DDoS Pro, Cloud Load Balancer (CLB), and customer originservers. Deploy a CLB in the regions with Anti-DDoS Pro resources and bind the CLB to the Anti-DDoS Pro instance. Configure the private network forwarding rules for the CLB to ensure that the public network IPs can access business through the CLB.
- In normal status, business IP can be parsed to the public network IPs of the origin server (or directly to CLB public network IPs in other regions). The business traffic accesses the nearby origin server.
- If attacks occur, the business IP is parsed to CLB IPs for DDoS attack traffic cleansing. After cleansing, the CLB forwards the traffic to the origin server via a private direct connect.

The following figure shows the detailed plan.
![](https://main.qcloudimg.com/raw/26603bdc4a5c0ba147ee14b0d3f7b1e7.png)

## Solution Results
- The protection is no longer limited by regions and provides up to 300 Gpbs of Anti-DDoS Pro protection.
- The business traffic is forwarded by Tencent Cloud through direct connection to the private network with high reliability and a short delay time.
- Enjoy all the advantages of the Tencent Cloud BGP network, where all public network IPs belong to the BGP network lowering delay times.

## Suggestions and Notes
- Deploy Anti-DDoS Pro and CLB in advance.
- Establish a business availability monitoring regime to discover and handle swiftly any exceptional access to the origin server when the automatic switching regime is not deployed.
- Conduct regular tests and practice drills to familiarize yourself with solutions and to solve potential problems.
