Based on customer experiences in stress testing, this document summarizes common performance issues in stress testing, and provides troubleshooting solutions as well as suggestions.

## Stress testing FAQs

### The public network access is not enabled on real server
If public network access is not enabled when you purchase CVM, forwarding may fail when a public network CLB is mounted to the CVM instance.
### The bandwidth of a real server is insufficient
If the real server has a low bandwidth, it cannot return packets to the CLB when the threshold is exceeded. CLB will return a 504 or 502 error to the client.
### The client ports are insufficient 
If the number of clients is too small or the range of client ports is too narrow, client ports become insufficient and connections will fail to be established. In addition, if the `keep_alive` value is greater than 0 when a persistent connection is established, the connection will permanently use the port, which reduces the number of available client ports.
### Applications relied on by real servers have performance issues
After a request reaches a real server through CLB, the load on the real server is normal. However, because applications on real servers also rely on other applications such as database, performance issues in the database may also affect the stress testing performance.
### A real server is unhealthy
The health status of real servers may be ignored in stress testing. If the real server has a health check failure or unstable health check status (sometimes good and sometimes bad with rapid changes), stress testing may have poor performance.
### Session persistence enabled for CLB results in uneven traffic distribution among real servers
After session persistence is enabled for CLB, requests may be distributed to fixed real servers. The traffic distribution becomes uneven, affecting the performance of stress testing. We recommend you disable session persistence during stress testing.

## Suggestions for stress testing
>!The following configurations are only used for CLB stress testing. You do not need to have them in your production environment.

- We recommend you use non-persistent connection when stress testing the forwarding capability of CLB.
Except for verification on session persistence features, stress testing is generally designed to verify the forwarding capability of CLB. Therefore, non-persistent connection can be used to test the processing capability of CLB and real servers.
- We recommend you use persistent connection to stress testing the throughput of CLB, such as the upper limit of bandwidth and persistent connection services.
We recommend you adjust the timeout period of the stress testing tool to a small value. Otherwise, the average response time will increase when the timeout period increases, causing you to be unable to quickly judge whether the stress level is reached.
- We recommend you use a static website provided by the real server for stress testing to avoid loss caused by application logic, such as I/O and DB.
- Disable session persistence for listeners. Otherwise, the stress will be concentrated on certain real servers. If the pressure performance is not satisfactory, you can determine whether the traffic is evenly distributed by checking the monitoring data of real servers under CLB.
- Disable health check for listeners to reduce access requests to real servers generated during health check.
- Use multiple clients (> 5) for stress testing. Dispersed source IPs can better simulate actual online conditions.
