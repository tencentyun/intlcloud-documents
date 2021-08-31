### Will I get an alert on DDoS attacks?
Yes. You will receive an alarm message once DDoS attacks are detected. You can also customize an inbound traffic alarm threshold for notification. For more details, see [Configuring Security Event Notification](https://intl.cloud.tencent.com/document/product/1029/36139).

### Why my business suffers DDoS attacks without my business running on the server?
- A DDoS attack is an attack involving multiple machines attempts to make your business, rather than the IP or domain name of the server, unaccessible for users.
- Your business may be at risk of DDoS attacks if it communicates over the public network.

### Why my business is attacked again after I have Anti-DDoS products deployed?
- Your business may be at risk of DDoS attacks if it communicates over the public network.
- Your business protected by Anti-DDoS products may be still targeted, but it is less likely to cause losses.

### What are the targets when the server is attacked?
DDoS attacks target your IP or business by attacking the server.

### What are the common types of attacks?
- Network layer attacks: includes UDP reflection attacks, SYN floods, and connection attacks. This type of attacks causes a denial of service by consuming server bandwidth and connection resources.
- Application layer attacks: includes DNS floods, HTTP floods, and CC attacks. This type of attacks cause a denial of service by exhausting server performance.

### Where to view attack logs for the attacked server?
On the [Overview](https://console.cloud.tencent.com/ddos/antiddos-native/overview/ddos/bgp-00000160/2402:4e00:1201:6603:0:910c:3c54:e7c9) page, you can view attack logs for the attacked server over the selected time period.

### Where to view details of the attack source IP?
On the [Overview](https://console.cloud.tencent.com/ddos/antiddos-native/overview/ddos/bgp-00000160/2402:4e00:1201:6603:0:910c:3c54:e7c9) page, select an attack event you want to view, and then click **Attack Details** to check the attack source information, source region, attack traffic and attack packet size.
![](https://main.qcloudimg.com/raw/25cd15030c30e4101b167a22ff93dc56.png)

### What to do when the lightweight server is under DDoS attacks?
We recommend getting an [Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029/36115) instance to defeat DDoS attacks and guarantee the availability of your server and business.

### What is the protection bandwidth threshold for the server? What will happen if the threshold reaches?
General users can enjoy free basic protection at a bandwidth of 2 Gbps while 10 Gbps for VIP users. Once the threshold reaches, blocking will be triggered, causing potential business interruptions.

### How to identify an attack by the amount of attack traffic?
An attack is identified as long as attack traffic is detected. You can set an alarm threshold upon the amount of attack traffic.

### I have added the source IP to a blocklist configured for the Anti-DDoS Pro instance when my business is attacked, but the IP still has access to my business. Is the instance not working?
The access restriction for the blocklisted IP will not be taken immediately. Only when the accessing traffic exceeds the cleansing threshold, it will be denied directly from accessing your business.
