

## A

### AI engine

[Artificial Intelligence (AI) engine](https://intl.cloud.tencent.com/document/product/627/35645) refers to a technology used in WAF to detect web attacks based on machine learning. With its self-learning, self-evolvement, and adaptation capabilities, it can maximize the detection rate and capture rate for known and unknown threats, minimize false positives, and flexibly adapt to ever-changing web applications.

## C

### CC protection

[Challenge Collapsar (CC) protection](https://intl.cloud.tencent.com/document/product/627/11709) refers to a protection service against CC attacks where attackers use certain tools to simulate multiple users in order to continuously send connection requests to your website and make your business unavailable. You can add CC protection rules to defend against CC attacks for webpage requests.

## D

### Proxy server

Proxy server is a core server security feature which is applicable to the session layer in the Open Systems Interconnection (OSI) model. It can improve the access speed, hide real website IPs, and enhance website security.

### Territorial prohibition

[Territorial prohibition](https://intl.cloud.tencent.com/document/product/627/14704) refers to a mechanism that determines the region of an attacking IP and blocks access requests from all IPs in the specific region in order to quickly block attacks.

### DNS hijacking protection

## F

### Tampering proofing

[Tamper proofing](https://intl.cloud.tencent.com/document/product/627/11710) refers to a mechanism where core webpages can be cached to the cloud and those in the cache can be published instead to realize the effect of webpage substitution. When the core webpages receive requests, content stored in cloud will be returned.

### Anti-Leakage

[Anti-leakage](https://intl.cloud.tencent.com/document/product/627/14582) refers to a mechanism where the responding webpages are checked for sensitive information such as ID and phone numbers and any sensitive information detected will be observed or replaced with asterisks (*) according to the preset match behaviors, which helps avoid leakage of sensitive information.

## H

### Intermediate IP address

After you add a domain name, WAF will automatically allocate multiple intermediate IP addresses to it accordingly, which can be used as the egress IPs of WAF to forward filtered normal traffic to your real server.

## S

### SSL certificate

SSL certificate is a security protocol designed to ensure security and data integrity for internet communications. Based on the SSL protocol, an SSL certificate can be installed on the server to achieve encrypted data transfer.

## V

### VIP address

After you add a domain name, WAF will automatically allocate a VIP address to it accordingly, which will act as the ingress address of WAF when the real server receives access requests. The access traffic will be forwarded to the VIP after DNS resolution and then to WAF.

## W

### WAF

For more information, please see [WAF](https://intl.cloud.tencent.com/document/product/627/35644#1297).

### WAF

Web Application Firewall (WAF) is a one-stop AI-based risk prevention solution for web business operations. It can identify malicious traffic with the aid of AI and rule engines to protect websites and further improve the website security and reliability. By leveraging bot behavior analysis, it can defend against malicious access requests and safeguard core website businesses and data.

## Y

### Domain name resolution

Servers on the internet communicate with each other through IP addresses. However, most people are used to remembering a domain name that can be mapped to multiple IP addresses. The conversion between a domain name and an IP address is called domain name resolution.
The following are common domain name resolution types:

- A record resolution: it specifies the IPv4 address of the domain name.
  - Record type: "A" should be selected.
  - Record value: the server IP address provided by Tencent Cloud should be entered.
  - MX priority: it does not need to be set.
  - TTL: it is set to 600 by default.
- CNAME record resolution: it is used to point a domain name to another one which will be used to provide the IP address.
  - Record type: "CNAME" should be selected.
  - Record value: the CNAME record generated after the protected domain name is added to WAF should be selected.
  - MX priority: it does not need to be set.
  - TTL: it is set to 600 by default.
