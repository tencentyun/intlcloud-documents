### Will I receive alerts for DDoS attacks?
Yes. You will receive an alarm message once DDoS attacks are detected. You can also customize an inbound traffic alarm threshold for notification. For details, see [Configuring Security Event Notification](https://intl.cloud.tencent.com/document/product/1029/36139).

### Why my application suffers DDoS attacks when it is not running on the server?
- A DDoS attack is an attack involving multiple machines attempts to make your application, rather than the IP or domain name of the server, inaccessible for users.
- Your application may be at risk of DDoS attacks if it communicates over the public network.

### Why my application is attacked again after I have Anti-DDoS products deployed?
- Your application may be at risk of DDoS attacks if it communicates over the public network.
- Your application protected by Anti-DDoS products may be still targeted, but it is less likely to cause losses.

### What are the targets when the server is attacked?
DDoS attacks target your IP or application by attacking the server.

### What are the common types of attacks?
- Network layer attacks: It includes UDP reflection attacks, SYN floods, and connection attacks. This type of attacks causes a denial of service by consuming server bandwidth and connection resources.
- Application layer attacks: It includes DNS floods, HTTP floods, and CC attacks. This type of attacks cause a denial of service by exhausting server performance.

### Where can I view attack logs for the attacked server?
On the [Overview](https://console.cloud.tencent.com/ddos/antiddos-native/overview/ddos/bgp-00000160/2402:4e00:1201:6603:0:910c:3c54:e7c9) page, you can view attack logs for the attacked server over the selected time period.

### Where can I view details of the attack source IP?
On the [Overview](https://console.cloud.tencent.com/ddos/antiddos-native/overview/ddos/bgp-00000160/2402:4e00:1201:6603:0:910c:3c54:e7c9) page, select an attack event you want to view, and then click **Attack Details** to check the attack source information, source region, attack traffic and attack packet size.
![](https://main.qcloudimg.com/raw/25cd15030c30e4101b167a22ff93dc56.png)

### What should I do when the lightweight server is under DDoS attacks?
We recommend that you purchase an [Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029/36115) instance to defeat DDoS attacks and guarantee the availability of your server and applications.

### What is the protection bandwidth threshold for the server? What will happen if the threshold reaches?
Users can enjoy free basic protection bandwidth of up to 2 Gbps. Once the threshold is reached, blocking will be triggered, causing potential application interruptions.

### How to identify an attack by the amount of attack traffic?
An attack is identified as long as attack traffic is detected. You can set an alert threshold based on the amount of attack traffic.

### I have added the source IP to a blocklist configured for the Anti-DDoS Pro instance when my application is attacked, but the IP still has access to my application. Is the instance not working?
The access restriction for the IP will not be taken right after it is added to the blocklist. Only when the incoming traffic exceeds the cleansing threshold, the IP will be denied directly from accessing your application.
