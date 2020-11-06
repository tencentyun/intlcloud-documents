Tencent Cloud CLB can check the availability of real servers through health check. If a health check exception occurs, you can troubleshoot as follows:

>?
>- If an exception is detected during health check, CLB will no longer forward traffic to the exceptional real server.
>- If exceptions are detected on all real servers during health check, requests will be forwarded to all real servers.
>- For more information on how health check works, please see [Health Check](https://intl.cloud.tencent.com/document/product/214/6097).

## Checking Real Server's Public Network Bandwidth
- For a traditional account, as the bandwidth attribute of the account is in CVM rather than CLB, public network bandwidth must be configured for the backend CVM instance bound to CLB; otherwise, a health check exception will occur.
- For a standard account, there is no need to configure public network bandwidth for the backend CVM instance bound to CLB, and the CLB service will not be affected.
>?
>- You can determine the account type as instructed in [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246#.E8.83.8C.E6.99.AF.E4.BF.A1.E6.81.AF).
>- No CLB traffic or bandwidth fees are charged for traditional accounts. The public network traffic fees incurred by the CLB service are charged by the bound backend CVM instance.
>- You can purchase public network bandwidth for the CVM instance without assigning a public IP.

## Checking Security Group Configuration
Check whether the "Allow Traffic by Default in Security Group" feature is enabled on the CLB instance, and if not, you need to open the source IP in the security group of the CVM instance. If you want the CLB service to allow access from any IP, configure the source IP as 0.0.0.0/0 in the inbound rule of the security group. For more information, please see [Configuring CLB Security Group](https://intl.cloud.tencent.com/document/product/214/14733).

## Checking Layer-4 Listener

>?
>- Under TCP protocol, CLB uses SYN packets for check.
>- Under UDP protocol, CLB uses the `ping` command for check.

When the health status of a CLB real server port is exceptional as displayed on the page, troubleshoot in the following steps:

- Check whether the CLB real server is configured with security groups that affect the service. Real servers can control the access through security groups to ensure normal running of services. For more information, please see [CVM Security Group Configuration Description](https://intl.cloud.tencent.com/document/product/214/6157).
- Run the `netstat` command to check whether there is a process listening on the real server port. If no such process is found, restart the service.

## Checking Layer-7 Protocol

For layer-7 (HTTP protocol) services, when a listener has an exception during health check, troubleshoot in the following procedures:
- Because layer-7 health check service of CLB communicates with the backend CVM instance over the private network, you need to log in to the server to check whether the application server port is listened on normally at the private network address, and if not, move the listener on the application server port to the private network to ensure normal communication between CLB and the backend CVM instance.
Suppose that both CLB's frontend port and CVM's backend port are 80, and the CVM's private IP is `1.1.1.10`:
 -  For a server on Windows, use the following command:
```
netstat -ano | findstr :80
```
 -  For a server on Linux, use the following command:
```
netstat -anp | grep :80
```
If you can see the listening on `1.1.1.10:80` or `0.0.0.0:80`, the configuration is normal.

- Make sure that the backend port configured in the CLB listener has been enabled on the real server.
 - For layer-4 CLB, it is considered normal as long as `telnet` to the backend port responds. You can use `telnet 1.1.1.10 80` for testing.
 - For layer-7 CLB, it is considered normal if an HTTP status code such as 200 is returned. Check as follows:
   -  On Windows, you can directly enter the private IP in the browser on a CVM instance to test whether it is normal. This example uses `http://1.1.1.10`.   
   - On Linux, you can run the `curl -I` command to check whether the status is `HTTP/1.1 200 OK`. This example uses the `curl -I 1.1.1.10` command.

- Check whether the backend CVM has a firewall or other security software, which is likely to block the local IP address of the CLB. This causes CLB to be unable to communicate with the real server.
Check whether the private network firewall of the server allows port 80 to pass. You can temporarily disable the firewall for the test.
 - For Windows, run the `firewall.cpl' command to disable the firewall.
 - For Linux, run the `/etc/init.d/iptables stop` command to disable the firewall (for CentOS 7.x, run `systemctl stop firewalld`).

- Check whether the health check parameters of CLB are configured correctly. We recommend you use the default health check parameter values as described in [Health Check](https://intl.cloud.tencent.com/document/product/214/6097).
- For the test file specified for health check, we recommend you use a simple page in HTML format, which is only used to check the returned results. Dynamic programming languages such as PHP are not recommended.
- Check whether the backend CVM instance has high load that leads to slow response.
- Check the HTTP request method.
 - If HEAD is used, the real server must support HEAD.
 - If GET is used, the real server must support GET.
- If both TCP fast recycling (tcp_tw_recycle) and timestamp (tcp_timestamps) are enabled, the health check may get exceptional. We recommend you disable `tcp_tw_recycle`. For more information, please see [Cause Analysis](https://intl.cloud.tencent.com/document/product/214/10328).

## High Health Check Frequency

A health check packet is sent every 5 seconds as configured in the console, but the real server finds that one or multiple health check requests are received within 1 second. This issue mainly relates to the implementation mechanism of CLB real server health check.
Suppose that 1 million requests from clients are distributed to four CLB real servers before being sent to the CVM instance. Each CLB real server conducts health check separately. If the CLB instances are configured to send a health check request every 5 seconds, each CLB real server will send a health check request every 5 seconds. The backend CVM instance therefore may receive 4 health check requests in 5 seconds. 

The advantages of this scheme are high efficiency, accurate check, and avoidance of mistaken removal. For example, if one of eight physical servers in the CLB instance cluster fails, the other seven servers can still forward traffic normally.

If your business is sensitive to the load, highly frequent health check may affect the normal business access. In this case, you can increase the check interval to reduce the impact (for example, conduct health check once every 15 seconds).
