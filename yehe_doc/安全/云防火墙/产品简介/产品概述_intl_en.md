## What is Cloud Firewall?
Tencent Cloud Firewall (CFW) is a SaaS firewall based on the public cloud environment that provides network perimeter protection and addresses security and management needs for unified access control and log audit. In addition to the features of traditional firewalls, CFW supports multi-tenancy and elastic scaling and is an essential network security infrastructure for cloud migration.

## Features
### Cloud Firewall overview

Cloud Firewall offers centralized network access control. You can view the information of Cloud Firewall clearly on the [console overview page](https://console.cloud.tencent.com/cfw), which includes the following modules:
- **Asset protection overview**: Displays the number of assets in the public and private networks, exposed ports, and security events, and offers vulnerability intelligence for reference.
- **Firewall status monitoring**: Displays the peak bandwidth of the edge and NAT firewalls within the past 7 days.
- **Traffic statistics**: Displays the volume of inbound traffic, outbound traffic, and total traffic within the past 24 hours to 6 months.
- **Security policy configuration**: Displays the number of access control rules configured for edge, NAT, and inter-VPC firewalls, their remaining quota, and security policies for intrusion prevention.
- **Log storage statistics**: Displays the total log storage capacity, used storage, and remaining storage.

### Cloud Firewall toggles

- **Edge firewall**: The system automatically identifies the public IP addresses and the associated instances and assets of a cloud tenant, and allows you to manage access control by public IP. Cloud Firewall supports public BGP IP addresses (IPs provided by CMCC, CUCC, or CTCC are not supported). It offers a public IP address list (asset list) for you to view all of the existing inbound or outbound rules of each public IP, and allows you to manage them using the access control module.

- **Inter-VPC firewall**: The system automatically identifies the number of VPCs in the cloud tenant private network along with their connection status and mode, and visualizes them using a VPC topology. A uniform toggle needs to be enabled when you use the inter-VPC firewall for the first time. After the toggle is enabled, a sub-firewall is automatically configured for each pair of connected VPCs. You can manually enable or disable a sub-firewall, and configure access control rules for each pair of VPCs.

- **NAT firewall**: A virtual firewall that works similarly as a NAT gateway. In addition to network address translation capabilities, it also offers security audit features such as access control and logs.

  After you enable and create a NAT Firewall instance, the system automatically identifies the subnets of the VPCs in the selected region. You only need to enable the firewall for your subnets to route your traffic from the subnets to the NAT firewall. You can configure the access control list for the NAT firewall to filter and control traffic.

### Asset management
Asset Management allows you to view and manage the data and information of each asset. It helps you better understand the current asset status, manage your assets, and predict and prevent security events by showing the top 5 core assets and risky assets and the detailed information of all your public network assets, private network assets, and VPCs.


### Alert management
Alert Management allows you to view the alerts when your assets are under attack. After you configure all the necessary security policies in the access control, intrusion defense, and security baseline modules, you are kept informed of the alerts from Cloud Firewall, which is helpful for security operations and maintenance.


### Traffic monitoring
Traffic Monitoring visually displays external access statistics, outgoing request analysis, and inter-VPC activities based on outbound, inbound, and inter-VPC traffic.

### Access control
Access control rules are a collection of security policies, which are defined in the 5-tuple format and are listed in a list. For any data flows that pass through the edge firewall, Cloud Firewall matches them with the 5-tuple information according to rule priorities. If a data flow is matched, the operation specified in the rule is performed on the data flow, which can help tenants control access to public IP addresses. Besides, logging is used for security operations, maintenance and audit. With the traditional 5-tuple configuration model, enterprise security groups can be easily managed and used for protection between subnets of a VPC, VPCs, and direct connections of hybrid clouds.

### Intrusion defense

According to the protection mode, Cloud Firewall automatically identifies the unknown risks beyond access control rules, monitors the north-south traffic of public IP addresses based on intrusion defense rules, and prevents CVM vulnerabilities from being exposed to the Internet.

### Security baseline

By observing the traffic statistics within a specific period of time, Cloud Firewall generates a basic IP address or domain name access list. You can add or delete IP addresses or domain names based on the security scores, associated security events, and network access statistics to form a security baseline.

### Log audit

Cloud Firewall logs and stores rule hit records for the past 7 days. Security O&M specialists can view the matched network traffic and rules for log audit. When failure like a network connection error occurs, you can search the log for a quick fix. You can also view the operation history for the past 30 days to improve the working efficiency of enterprise and network security administrators and reduce management costs.

### Log analysis

Log Analysis allows you to view the details of all the traffic logs stored in Cloud Firewall for the past 6 months based on login account, query logs with search statements, and use reporting and analysis services.

### Address template

Address Template allows you to batch manage IP addresses more easily. You can create a template for IP addresses or domain names, add multiple IP addresses or domain names to it, and then match the template with access control rules.
