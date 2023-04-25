### Will I receive alerts for DDoS attacks?
Yes. You will get alert notifications when the inbound traffic exceeds a specified threshold. To learn how to set thresholds, see [Configuring Alerts](https://intl.cloud.tencent.com/document/product/297/37231).

### Why my business suffers DDoS attacks without my business running on the server?
- A DDoS attack is an attack involving multiple machines attempts to make your business, rather than the IP or domain name of the server, inaccessible for users.
- Your business may be at risk of DDoS attacks if it communicates over the public network.

### Why my business is attacked again after I have Anti-DDoS Advanced products deployed?
- Your business may be at risk of DDoS attacks if it communicates over the public network.
- Your business protected by Anti-DDoS Advanced products may still be targeted, but it is less likely to cause losses.

### What are the targets when the server is attacked?
DDoS attacks target your IP or business by attacking the server.

### What are the common types of attacks?
- Network layer attacks: includes UDP reflection attacks, SYN floods, and connection attacks. This type of attacks causes a denial of service by consuming server bandwidth and connection resources.
- Application layer attacks: includes DNS floods, HTTP floods, and CC attacks. This type of attacks cause a denial of service by exhausting server performance.

### What types of attack statistics are provided by Anti-DDoS Advanced?

Anti-DDoS Advanced provides the following types of attack statistics:

- **Total attack traffic**: presents how the attack traffic on the protected IP distributes over different protocols within the selected time period.
- **Attack packets**: presents how the attack packets to the protected IP distribute over different protocols within the selected time period.
- **Total attacks**: presents how the attacks on the protected IP distribute over different attack types within the selected time period.

### Where to view attack logs for the attacked server?
In the "Recent Events" section of the [Overview page](https://console.cloud.tencent.com/ddos/dashboard/advanced), you can view the recent attack events and logs.

### Where to view details of the attack source IP?
In the "Recent Events" section of the [Overview](https://console.cloud.tencent.com/ddos/dashboard/advanced) page, select an attack event you want to view, and then click **View details** to check the attack source information, source region, attack traffic and attack packet size.
![](https://qcloudimg.tencent-cloud.cn/raw/c969588e5aab0e2a213737de4179bf1d.png)

### What to do when the lightweight server is under DDoS attacks?
We recommend getting an [Anti-DDoS Advanced](https://intl.cloud.tencent.com/document/product/297/37241) instance to defeat DDoS attacks and guarantee the availability of your server and business.

### What is the protection bandwidth threshold for the server? What will happen if the threshold reaches?
Each public IP of all Tencent Cloud users in the Chinese mainland can enjoy free basic protection, with a maximum bandwidth of 2 Gbps for general users and 10 Gbps for VIP users. Users outside the Chinese mainland can enjoy up to 2 Gbps bandwidth. Blocking will be triggered after the threshold reaches, causing potential business interruptions.

### How to identify an attack by the amount of attack traffic?
An attack is identified as long as attack traffic is detected. You can set an alert threshold based on the amount of attack traffic.

### A source IP is added to the Anti-DDoS Pro instance’s blocklist, but it still has access to my business. Is the instance not working?
The access restriction for the IP will not be taken right after it is added to the blocklist. Only when the incoming traffic exceeds the cleansing threshold, the IP will be denied directly from accessing your business.

