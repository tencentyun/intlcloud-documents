[//]: # (chinagitpath:XXXXX)

## A Record
An A record is used to specify the corresponding IP address of a host name (or domain name).

## BGP Network
The BGP (Border Gateway Protocol) network is a network type implementing high-speed interconnection with the Internet AS (autonomous system) based on the border gateway protocol. Tencent Cloud's BGP line covers 30 ISPs to solve the problem of slow and unstable cross-network access and provide users with high-quality network access experience.

## CNAME
CNAME (Canonical Name) is an alias record that implements the resolution of one domain name to another. CNAME can point more than one host name to the same alias so as to realize quick change of IP addresses.

## CC Attack
In a CC (Challenge Collapsar) attack, the attacker maliciously occupies the application-level resources of the target server to consume its processing performance so that it cannot provide services normally. Common attack types include GET/POST Flood based on HTTP/HTTPS, Layer-4 CC, and Connect Flood.

## DDoS Attack
In a DDoS (Distributed Denial of Service) attack, the attacker remotely controls a large number of zombie hosts through the network and uses them to send a great quantity of requests to one or more targets in order to exhaust the system resources of the targeted server(s) so that the server(s) cannot respond to normal service requests.

## Block
When the attack traffic to the target server exceeds the protection bandwidth limit of the purchased anti-DDoS package, Tencent Cloud will block all public network accesses to the server through the service of the ISPs for a period of time.

## Protection Bandwidth
Protection bandwidth refers to the total protection capability of the Anti-DDoS Advance service pack. It includes base protection and elastic protection.
- Base protection: refers to the base protection capability of an Anti-DDoS instance, and is prepaid by month.
- Elastic protection bandwidth: refers to the maximum elastic protection ability of an Anti-DDoS instance, and is postpaid by day.

If the elastic protection is enabled, the elastic protection bandwidth is deemed as the maximum protection bandwidth of an Anti-DDoS instance. When the attack traffic exceeds the maximum protection bandwidth, the attacked IP will be blocked.

## Traffic Cleansing
When the public network traffic to the target server exceeds the set protection threshold, Tencent Cloud Dayu system will automatically cleanse the inbound public network traffic to the server. The Dayu system redirects the traffic from the original network path to the DDoS cleansing device of Dayu system through BGP. The device can identify the traffic to the IP, abandoning the attack traffic and forwarding normal traffic to the target server. Generally, traffic cleansing does not affect normal access, but in special scenarios or when the cleansing policy is configured inappropriately, it may affect normal access.

## Forwarding Rule
The forwarding rule is a scheduling algorithm based on which the load balancer distributes traffic to multiple servers in the backend. It supports weighted polling and source IP hash algorithms. If a forwarding rule is configured,  requests are first sent to the protective IP port and then forwarded to the real server port.

