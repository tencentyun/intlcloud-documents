If an exception is detected during health check, it can be checked from three aspects: layer 4, layer 7, and backend bandwidth.
## Layer-4 Troubleshooting

Under TCP protocol, CLB uses SYN packets for check. Under UDP protocol, CLB uses the `ping` command for check.

When a real server port is marked as "unhealthy" on the page, troubleshoot in the following procedures:

- Check whether the CLB real server is configured with a firewall that affects the service, and if so, disable it. 
- Run the `netstat` command to check whether there is a process listening on the real server port. If no such process is found, restart the service.

## Layer-7 Troubleshooting
For layer-7 (HTTP protocol) services, when a listener has an exception during health check, troubleshoot in the following procedures:

- Because layer-7 health check service of CLB communicates with the backend CVM instance over the private network, you need to log in to the server to check whether the application server port is listened on normally at the private network address. If not, move the listener on the application server port to the private network to ensure normal communication between CLB and the real server.

Suppose that both CLB's frontend port and CVM's backend port are 80, and the CVM's private IP is `1.1.1.10`:

For a server on Windows, use the following command:

```
netstat -ano | findstr :80
```

For a server on Linux, use the following command:

```
netstat -anp | grep :80
```

If you can see the listening on `1.1.1.10:80` or `0.0.0.0:80`, the configuration is normal.

- Make sure the relevant port has been opened on the real server, which must be the same as the backend port configured for the CLB listener.

For layer-4 CLB, it is considered normal as long as backend port `telnet` responds. You can use `telnet 1.1.1.10 80` for testing. For layer-7 CLB, it is considered normal if an HTTP status code such as 200 is returned. Check as follows:

On Windows, you can directly enter the private IP in the browser on a CVM instance to test whether it is normal. This example uses `http://1.1.1.10`.   
On Linux, you can run the `curl -I` command to check whether the status is `HTTP/1.1 200 OK`. This example uses the `curl -I 1.1.1.10` command.

- Check whether the backend CVM has a firewall or other security software, which is likely to block the local IP address of the CLB. This causes CLB to be unable to communicate with the real server.

Check whether the private network firewall of the server allows port 80 to pass. You can temporarily disable the firewall for the test.

For Windows, run the `firewall.cpl' command to disable the firewall.
For Linux, run the `/etc/init.d/iptables stop` command to disable the firewall (for CenOS 7.x, run `systemctl stop firewalld`).

- Check whether the health check parameters of CLB are configured correctly. We recommend you use the default health check parameter values as described in [Health Check](https://intl.cloud.tencent.com/document/product/214/6097).
- For the test file specified for health check, we recommend you use a simple page in HTML format, which is only used to check the returned results. Dynamic programming languages such as PHP are not recommended.
- Check whether the real server has high load that leads to slow response.
- If both TCP fast recycling (tcp_tw_recycle) and timestamp (tcp_timestamps) are enabled, the health check may get exceptional. We recommend you disable `tcp_tw_recycle`. For more information, please see [Cause Analysis](https://intl.cloud.tencent.com/document/product/214/10328).

## Backend Bandwidth Problem
#### Does a backend CVM instance need public network bandwidth? Will the bandwidth affect the CLB service?
 - For bill-by-IP accounts, there is no need to configure public network bandwidth for the backend CVM instance bound to CLB, and the CLB service will not be affected.
 - For non-bill-by-IP accounts, public network bandwidth must be configured for the backend CVM instance bound to CLB; otherwise, the CLB service will be affected.
>?
>- No CLB traffic or bandwidth fees are charged for non-bill-by-IP accounts. The public network traffic fees incurred by the CLB service are charged by the bound backend CVM instance.
>- Due to the impossibility to accurately predict the traffic of internet and web businesses, in order to avoid waste and packet loss, we recommend you select "bill-by-traffic" and set a reasonable peak bandwidth cap for public network bandwidth when purchasing a backend CVM instance. In this way, you don't need to care about the increase/decrease in the total traffic of the CLB egress, as fees will be charged by traffic.
