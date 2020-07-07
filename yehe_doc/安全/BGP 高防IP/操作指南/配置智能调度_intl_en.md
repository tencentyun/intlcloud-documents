## Use Cases
Each account can have multiple Anti-DDoS instances, and each instance has at least one protective line; therefore, there can be multiple protective lines under one account. Once your business is added to an Anti-DDoS instance, a protective line will be configured for it. If multiple protective lines have been configured, you need to choose the optimal business traffic scheduling method, i.e., how to schedule business traffic to the optimal line for protection while ensuring high business access speed and availability.
Anti-DDoS features priority-based CNAME intelligent scheduling, where you can select an Anti-DDoS instance and set the priority of its protective line as needed.
>DNS configuration is supported for Anti-DDoS Pro instances and Anti-DDoS Advanced instances (including instances for BGP, China Telecom, China Unicom, and China Mobile).

## Priority-based Scheduling
This refers to using the protective line of the highest priority to respond to all DNS requests, i.e., all access traffic will be scheduled to the protective line of the currently highest priority. You can adjust the priority value of a protective line, which is 100 by default. The smaller the value, the higher the priority. The specific scheduling rules are as follows:
- If the Anti-DDoS instance configured for your business contains multiple protective lines from different ISPs and of the same priority, response will be made based on the ISP of the specific DNS request. If one of the lines is blocked, access traffic will be scheduled in the order of BGP > China Telecom > China Unicom > China Mobile > ISPs outside Mainland China (including those in Hong Kong (China) and Taiwan (China)).
- If all the lines of the same priority are blocked, access traffic will be automatically scheduled to the currently available protective line of the second-highest priority.
>If no protective lines of the second-highest priority are available, automatic scheduling cannot be completed, and business access will be interrupted.
- If the Anti-DDoS instance configured for your business contains multiple protective lines from the same ISP and of the same priority, access traffic will be scheduled by way of load balancing, i.e., evenly distributed to such lines.

#### Example
Suppose you have the following Anti-DDoS instances: BGP IPs `1.1.1.1` and `1.1.1.2`, China Telecom IP `2.2.2.2`, and China Unicom IP `3.3.3.3`, of which the priority of `1.1.1.2` is 2 and that of the rest is 1. Normally, all traffic will be scheduled to the protective lines with the current priority of 1. Specifically, traffic from China Unicom will be scheduled to `3.3.3.3`, that from China Telecom to `2.2.2.2`, and that from other ISPs to `1.1.1.1`. If `1.1.1.1` is blocked, access traffic under this IP will be automatically scheduled to `2.2.2.2`. If both `1.1.1.1` and `3.3.3.3` are blocked, traffic supposed to be scheduled to them will be distributed to `2.2.2.2`, and if `2.2.2.2` is blocked too, traffic will be scheduled to `1.1.1.2`.
## Prerequisites
- Before enabling intelligent scheduling, please connect your business to be protected to your Anti-DDoS instance.
>
	- If you need to add the IP of your protected Tencent Cloud service to a purchased Anti-DDoS Pro instance, please see [Getting Started with Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029/36116).
	- If you need to connect your layer-4 or layer-7 application to a purchased Anti-DDoS Advanced instance, please see Anti-DDoS Advanced documents [Port Connection](https://intl.cloud.tencent.com/document/product/297/37221) or [Domain Name Connection](https://intl.cloud.tencent.com/document/product/297/37222).


- To modify the DNS resolution, you need to purchase the domain name resolution product.

## Setting Line Priority
Please follow the steps below to set priorities for your Anti-DDoS instance based on your scheduling scheme:
1. Log in to the [new Anti-DDoS Advanced Console](https://console.cloud.tencent.com/ddos/antiddos-advanced/overview) and click **Intelligent Scheduling** on the left sidebar to enter the list page. Click **Add Scheduling**, and the system will automatically generate a CNAME record.
![](https://main.qcloudimg.com/raw/e36d84cfb9510c775666c62432047097.png)
2. Locate the row of the CNAME record and click **Add Anti-DDoS Instance** to enter the intelligent scheduling editing page.
![](https://main.qcloudimg.com/raw/f066c16b5c5bfc6ecacf599ef5c731b0.png)
3. On the intelligent scheduling editing page, the TTL value is 60s by default, which can range from 1s to 3,600s, and the default scheduling method is priority-based.
![](https://main.qcloudimg.com/raw/1d24ad62706d6b4405a107de09f82e07.png)
4. Click **Add Anti-DDoS Resource IP**, select the target Anti-DDoS Advanced instance and IP, and click **OK**.
![](https://main.qcloudimg.com/raw/058a1f86c8c19014e70f404814d2d565.png)
5. After the instance is selected, domain name resolution will be enabled for its protective line by default. At this point, you can set the line priority.
![](https://main.qcloudimg.com/raw/5974cdf54b4ba7a0542b7f2fc8e73eed.png)
#### Example
Suppose you want to implement the following scheme: the business traffic will be scheduled to a BGP protective line first; if it is blocked due to attacks, the traffic will be automatically scheduled to a China Telecom protective line; if it is also blocked, the traffic will be scheduled to a China Unicom protective line; and after the BGP protective line is unblocked, the traffic will be scheduled to it automatically.
To implement this scheduling scheme, set the priority of the BGP line in the Anti-DDoS instance to 1 and that of the China Telecom line to 2, and keep the priority of the China Unicom line unchanged.
![](https://main.qcloudimg.com/raw/ad5ca28374b0ff9ccb2c81f9dc81d6e9.png)
If you do not want the China Unicom protective line to be in the traffic scheduling scheme, click <img src="https://main.qcloudimg.com/raw/5a5d700ec3e79ad7e0e6f50d4f440b02.png" style = "margin:0;"> to disable domain name resolution for it, and you can enable domain name resolution again and set its priority when necessary. If you want to delete it from the current scheduling scheme, you can locate the row of its corresponding instance and click **Unbind**.

## Modifying DNS Resolution
Before using a CNAME record for intelligent scheduling, you are recommended to change the CNAME record of your business domain name DNS to the CNAME record automatically generated by the intelligent scheduling system of Tencent Cloud Anti-DDoS, to which all access traffic to your business website will be directed.

