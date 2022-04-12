## Overview
HTTPDNS sends DNS requests to the DNS server of Tencent Cloud over the HTTP protocol instead of the local DNS of the ISP over the DNS protocol. This helps avoid domain name hijacking and cross-network access problems caused by local DNS and eliminate DNS exceptions in mobile internet services.

## Purpose
The purpose of HTTPDNS is to address DNS query exceptions and domain hijacking on the mobile internet:
- Status quo of mobile DNS: the local DNS egress of an ISP performs NAT based on the destination IP address of the authoritative DNS or forwards DNS requests to other DNS servers. This prevents the authoritative DNS from correctly identifying the local DNS IP of the ISP and thus gives rise to DNS query errors and cross-network traffic.
- Consequences of domain hijacking: no network access (inability to connect to the server) or access to a phishing website.
- Consequences of cross-domain, cross-region, cross-ISP, or cross-border DNS queries: slow or even no website access.

## How It Works
- The client directly accesses the HTTPDNS APIs to get the optimal IP of the domain. (For disaster recovery reasons, we recommend you retain your ISP's local DNS as a backup.)
- After the business IP is obtained, the client directly sends requests to it over the business protocol; for example, for HTTP requests, the client can specify the `host` field in the headers and then send standard HTTP requests to the IP returned by HTTPDNS.

## Service Quality
HTTPDNS is highly available and responsive.
- BGP Anycast network deployment: HTTPDNS is connected to the BGP Anycast network architecture to establish BGP interconnection with top 17 Chinese ISPs. This ensures that user requests from ISPs can quickly access the HTTPDNS server. More ISPs are being connected to guarantee a faster service response.
- Remote disaster recovery and real-time failover: HTTPDNS has multiple nodes in multiple IDCs across China. If any node fails, it can seamlessly switch to a backup node to ensure high service availability.

## Features
- Proprietary intelligent SDKs (available for iOS and Android) that cover more than 100 million users.
- Support for encryption.
- SLA of up to 99.99%.
- Unlimited queries.
- Support for user access distribution reports.
- Support for EDNS Client Subnet.
- Ticket and telephone support.
