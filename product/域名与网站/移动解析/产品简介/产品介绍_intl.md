### What is HttpDNS?
Unlike traditional methods where domain name resolution requests are sent to the ISP's local DNS server based on the DNS protocol, with HttpDNS, requests are sent to Tencent Cloud's DNS server based on the HTTP protocol, helping prevent domain name hijacking and cross-network access issues caused by the local DNS server and eliminating the headache of abnormal domain name resolution for mobile Internet services.
Leveraging the basic capabilities provided by DNSPod and Tencent Cloud's technical expertise accumulated over the years, HttpDNS serves over 400 million end users, making it very trustworthy.

### What problems can HttpDNS solve?
HttpDNS aims to solve the problems of DNS resolution exceptions and domain name hijacking in the mobile Internet:
- The status quo of mobile DNS: An ISP's Local DNS egress performs NAT based on an authoritative DNS destination IP address or forwards the resolving request to other DNS servers, making it impossible for the authoritative DNS to correctly identify the ISP's Local DNS IP and thus causing domain name resolution errors and cross-network traffic.
- Consequences of domain name hijacking: The website is inaccessible (connection to the server fails) or the end user is redirected to a phishing website.
- Consequences of cross-domain, cross-province, cross-ISP or cross-border resolution: Access to the website is slow or fails.

### How does HttpDNS work?
- The client directly accesses the HttpDNS API to obtain an optimal IP of the domain name. (For disaster recovery considerations, it is recommended to retain the way to resolve the domain name using the ISP's Local DNS as an alternative.)
- After the client obtains the business' IP, it sends a business protocol request directly to this IP. Take an HTTP request as an example: by specifying the host field in the header, it is sufficient to send a standard HTTP request to the IP returned by HttpDNS.

### How is the HttpDNS service quality?
HttpDNS features high availability and fast response.
- Deployment on BGP Anycast network: HttpDNS has accessed the BGP Anycast network architecture and established BGP interconnections with top 17 Chinese ISPs to ensure that end users of various ISPs can quickly connect to HttpDNS servers. More ISPs will be supported soon, ensuring a fast response of the service.
- Remote disaster recovery and real-time switching: HttpDNS has deployed multiple nodes in many IDCs in North China, East China and South China. In case that a node fails, the service can be seamlessly switched to a backup node, ensuring high service availability.

### Features of HttpDNS Enterprise Edition
- Proprietary Zhiying Analysis SDK (for iOS and Android) that serves over 100 million end users
- Support for encryption
- Up to 99.99% SLA
- Unlimited queries
- Support for user access distribution report
- Support for edns-client-subnet
- Customer service via tickets and telephone
