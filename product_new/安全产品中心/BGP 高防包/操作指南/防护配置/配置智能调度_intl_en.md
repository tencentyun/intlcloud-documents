## Use Cases
Each account can have multiple Anti-DDoS instances, and each instance has at least one protective line; therefore, there can be multiple protective lines under one account. Once your business is added to an Anti-DDoS instance, a protective line will be configured for it. If multiple protective lines have been configured, you need to choose the optimal business traffic scheduling method, i.e., how to schedule business traffic to the optimal line for protection while ensuring high business access speed and availability.
Anti-DDoS features priority-based CNAME intelligent scheduling, where you can select an Anti-DDoS instance and set the priority of its protective line as needed.
>Anti-DDoS Pro (includes single-IP and multi-IP instances) and Anti-DDoS Advanced instances support setting resolution.

## Priority-based Scheduling
This refers to using the protective line of the highest priority to respond to all DNS requests, i.e., all access traffic will be scheduled to the protective line of the currently highest priority. You can adjust the priority value of protective line, which is 100 by default. The smaller the value, the higher the priority. The specific scheduling rules are as follows:
- If the protective instance configured for your business contains multiple protective lines from different ISPs and of the same priority, response will be made based on the ISP of the specific DNS request. If one of the lines is blocked, access traffic will be scheduled in the order of BGP > China Telecom > China Unicom > China Mobile > ISP outside Mainland China.
- If all the lines of the same priority are blocked, access traffic will be automatically scheduled to the currently available protective line of the second-highest priority.
>If no protective lines of the second-highest priority are available, automatic scheduling cannot be completed, and business access will be interrupted.
- If the protective instance configured for your business contains multiple protective lines from the same ISP and of the same priority, access traffic will be scheduled by way of load balancing, i.e., evenly distributed to such lines.

#### Example
Assume that you have the following Anti-DDoS instances: BGP protective IPs 1.1.1.1 and 1.1.1.2, China Telecom protective IP 2.2.2.2, and China Unicom protective IP 3.3.3.3, of which the priority of 1.1.1.2 is 2 and that of the rest is 1. Normally, all traffic will be scheduled to the protective lines with the current priority of 1. Specifically, traffic from China Unicom will be scheduled to 3.3.3.3, that from China Telecom to 2.2.2.2, and that from other ISPs to 1.1.1.1. If 1.1.1.1 is blocked, access traffic under this IP will be automatically scheduled to 2.2.2.2. If both 1.1.1.1 and 3.3.3.3 are blocked, traffic supposed to be scheduled to them will be distributed to 2.2.2.2, and if 2.2.2.2 is blocked too, traffic will be scheduled to 1.1.1.2.
## Prerequisites
- Before enabling intelligent scheduling, please connect your business to be protected to your Anti-DDoS instance.
>
	- If you need to add the IP of your protected Tencent Cloud product to a purchased Anti-DDoS Pro instance, please see [Getting Started with Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029/31750).
	- If you need to connect your layer-4 or layer-7 application to a purchased Anti-DDoS Advanced instance, please see Anti-DDoS Advanced documents [Connecting Non-website Application](https://intl.cloud.tencent.com/document/product/297/15200).

- Before modifying DNS information, you need to purchase a domain name resolution product.

## Setting Line Priority
Please follow the steps below to set priorities for your protective lines based on your scheduling scheme.
1. Log in to the Anti-DDoS Console, select **Intelligent Scheduling** > **Domain Name List** on the left sidebar, and click **Create Intelligent Scheduling**. Then, a CNAME record will be generated automatically by the system.
![](https://main.qcloudimg.com/raw/6edb8b562afffb86443f3f7496bd3f4d.png)
2. Locate the row of the CNAME record and click **Add Anti-DDoS Instance** to enter the intelligent scheduling editing page.
![](https://main.qcloudimg.com/raw/5a6f03bc13df5ea70eac17e6aa31d259.png)
3. On the intelligent scheduling editing page, the TTL value is 60s by default, which can range from 1s to 3,600s, and the default scheduling method is priority-based.
![](https://main.qcloudimg.com/raw/eeb46c75e8e9391980ed856162e6d0d9.png)
4. Go to the "Add Anti-DDoS Instance" page, select an instance (Single IP, Multi-IP, or Anti-DDoS Advanced instance) for which you want to set line priority, and then click **OK**.
![](https://main.qcloudimg.com/raw/3f1a8366baa1b4ff7acf417f5de682bd.png)
5. After the instance is selected, DNS will be enabled for its protective line by default. At this point, you can set the line priority.
![](https://main.qcloudimg.com/raw/3f0fa5d1f061b39a4ad4f4b646853515.png)

## Modifying DNS
Before using a CNAME record for intelligent scheduling, you are recommended to change the CNAME record of your business domain name DNS to the CNAME record automatically generated by the intelligent scheduling system of Tencent Cloud Anti-DDoS, to which all access traffic will be directed.

