### A Record
An A record is used to specify the corresponding IP address of a host name (or domain name).

### BGP Network
Border Gateway Protocol (BGP) network is a network type where BGP is used as the routing protocol and high-speed interconnection of Internet autonomous systems (AS) is provided. Tencent cloud BGP line connects to 30 carriers, which can fix slow/unstable Internet connections and thus improve the user experience.

### CNAME
Canonical Name (CNAME) is a type of DNS records that can be used to alias one name to another. CNAME can point more than one hostname to the same alias to realize the quick change of IP addresses.

### CC Attacks
In a Challenge Collapsar (CC) attack, the attacker uses a proxy server to send a large number of deceptive requests to the target server to occupy the application-level resources and consume server's processing power, resulting in server failures. Common CC attacks include HTTP/HTTPS-based GET/POST Flood, Layer-4 CC, and Connect Flood.

### DDoS Attacks
A Distributed Denial of Service (DDoS) attack is a malicious attempt to make service unavailable by overwhelming the target system with a flood of Internet traffic.

### Block
Block means when the target server receives attack traffic exceeding the protection bandwidth limit of the purchased anti-DDoS service pack, Tencent Cloud will temporarily stop all public network accesses to the server through the carriers.

### Protection Bandwidth
Protection bandwidth refers to the maximum protection capability of your purchased Anti-DDoS service, which includes base protection and elastic protection.
- Base protection bandwidth refers to the basic protection capability of the Anti-DDoS Pro instance. The base part uses frozen payment method, which means the cost will be frozen when you successfully purchase it. You will need to pay the cost of the previous month in the following month.
- Elastic protection bandwidth is the Anti-DDoS Pro instance that provides maximum elastic protection capability and is postpaid based on the actual usage on a daily basis.

With elastic protection enabled, the elastic protection bandwidth is the highest possible protection bandwidth of your Anti-DDoS Pro instance. The attacked IP will be automatically blocked when the attack traffic exceeds the elastic protection bandwidth

### Traffic Cleansing
When the public network traffic of the destination server exceeds the limit of protection threshold, Tencent Cloud Anti-DDoS service system will automatically cleanse the public inbound traffic of the server. Traffics are redirected from the original network path to the cleansing device of Anti-DDoS via BGP route protocol. The security system then identifies traffic to this IP through the cleansing device, discards the attack traffic, and forwards normal traffic to the destination server. Generally, cleansing will not affect normal access. It is only in special occasions or when errors occur to the configuration of cleansing policy that the normal access will be affected.

### Forwarding Rule
A forwarding rule is a load balancing scheduling algorithm that distributes traffic to multiple servers at the backend. It supports weighted polling and source IP hashing, and its configuration enables the redirection of business request traffic to the Anti-DDoS Advanced IP before sending the traffic back to the origin server.
