## Layer-4 Troubleshooting

Under TCP protocol, CLB uses SYN packets for check. While under UDP protocol, CLB uses `ping` command for check.

When a real server port is marked as "unhealthy" on the page, troubleshoot via the following procedures:

- Check whether the CLB real server is configured with a firewall that affects the service. If yes, disable it. 
- Run the `netstat` command to check whether there is a process listening on the real server port. If no such process is found, restart the service.

## Layer-7 Troubleshooting
For layer-7 (HTTP protocol) services, when a listener has an exception during health check, troubleshoot via the following steps:

- Because Layer-7 health check service of CLB communicates with the real server via the private network, you need to log into the server to check whether the application server port is listened on normally at the private network address. If not, move the listener on the application server port to the private network to ensure normal communication between CLB and the real server.

Suppose that both CLB’s frontend port and CVM’s backend port are 80, and the CVM’s private IP is `1.1.1.10`:

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

For Layer-4 CLB, it is considered normal as long as backend port `telnet` responds. You can use `telnet 1.1.1.10 80` for testing. For Layer-7 CLB, it is considered normal if an HTTP status code such as 200 is returned. Check as follows:

On Windows, you can directly enter the private IP in the browser of a CVM to test whether it is normal. This example uses `http://1.1.1.10`.   
On Linux, you can run the `curl-I` command to check whether the status is `HTTP/1.1 200 OK`. This example uses the `curl -I 1.1.1.10` command.

- Check whether there is a firewall or other security software on the real server, which is likely to block the local IP address of the CLB. This causes the CLB to be unable to communicate with the real server.

Check whether the private network firewall of the server allows port 80 to pass. You can temporarily disable the firewall for the test.

For Windows, run the `firewall.cpl' command to disable the firewall.
For Linux, run the `/etc/init.d/iptables stop` command to disable the firewall.

- Check whether the health check parameters of CLB are configured correctly. We recommend you use the default health check parameter values in [Health Check](https://intl.cloud.tencent.com/document/product/214/6097).
- For the test file specified for health check, we recommend you use a simple page in HTML format, which is only used to check the returned results. Dynamic programming languages such as PHP are not recommended.
- Check whether the CVM has high load that leads to slow response.

