[//]: # (chinagitpath:XXXXX)

## A Record
An A record is used to specify the corresponding IP address of a hostname (or domain name).

## BGP Network
BGP network is a network type where BGP is used as the routing protocol and high-speed interconnection of Internet AS (autonomous systems) is provided. Tencent cloud BGP line connects to 30 ISPs, which can fix slow/unstable Internet connections and thus improve the user experience.

## CNAME
A CNAME (Canonical Name) is a type of DNS record that can be used to alias one name to another. CNAME can point more than one hostname to the same alias so as to realize the quick change of IP addresses.

## CC Attack
In a CC (Challenge Collapsar) attack, the attacker maliciously sends requests to the target server to occupy the application-level resources and consume the processing performance of the target server, resulting in server failures. Common CC attacks include HTTP/HTTPS-based GET/POST Flood, layer 4 CC, and Connect Flood.

## DDoS Attack
In a DDoS (Distributed Denial of Service) attack, the attacker remotely controls a botnet and uses it to send a great number of requests to one or more targets to exhaust the system resources of the targeted server(s) so that the server(s) cannot respond to normal service requests.

## Block
When the target server receives attack traffic exceeding the protection bandwidth limit of the purchased anti-DDoS service package, Tencent Cloud will temporarily stop all public network accesses to the server via the ISPs.

## Protection Bandwidth
Protection bandwidth refers to the maximum protection capability of your purchased Anti-DDoS service, which includes base protection and elastic protection.
- Base protection: Monthly prepaid Anti-DDoS service plan that provides base protection of an Anti-DDoS Advanced instance.
- Elastic protection bandwidth: Pay-as-you-go daily Anti-DDoS service plan that provides maximum elastic protection capability of an Anti-DDoS Advanced instance.

With elastic protection enabled, your Anti-DDoS Advanced instance will have a protection bandwidth limit equivalent to the peak value of your purchased elastic protection bandwidth. The attacked IP will be automatically blocked as soon as the attack traffic exceeds the elastic protection bandwidth limit.

## Traffic Cleansing
When the incoming public network traffic exceeds the protection threshold of the target server, Tencent Cloud Anti-DDoS Advanced IP will automatically start the traffic cleansing process. Through BGP the traffic will then be redirected to an Anti-DDoS Advance IP, which will clean, remove the attack traffic and then forward the cleaned traffic back to the target server. Generally, traffic cleansing does not affect normal accesses, unless the cleansing policy is wrongly configured.

## Forwarding Rule
A forwarding rule is a load balancing scheduling algorithm that distributes traffic to multiple servers at the back end. It supports weighted polling and source IP hashing, and its configuration enables the redirection of business request traffic to the Anti-DDoS Advanced IP before sending the traffic back to the real server.

