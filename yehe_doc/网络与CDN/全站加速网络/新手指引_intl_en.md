This document helps you get started with Tencent Cloud Enterprise Content Delivery Network (ECDN).

## 1. Basic ECDN Knowledge

- [Product Overview](https://intl.cloud.tencent.com/document/product/570/8645)
- [Why Tencent Cloud ECDN?](https://intl.cloud.tencent.com/document/product/570/10358)
- [Use Cases](https://intl.cloud.tencent.com/document/product/570/38536)
- [Basic Concepts](https://intl.cloud.tencent.com/document/product/570/38537)



## 2. ECDN Billing Modes

Tencent Cloud ECDN billing modes consist of **bill-by-number of requests** and **bill-by-traffic exceeding the free tier limit**, that is, the total cost consists of the fees respectively incurred by **the number of requests** and **the traffic exceeding the free tier limit**. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/570/37505).



## 3. Getting Started

#### 3.1 Activate the service and select the billing mode

Before using ECDN, you need to sign up for a Tencent Cloud account and activate the ECDN service. For more information, please see [Configuring ECDN](https://intl.cloud.tencent.com/document/product/570/38299).

#### 3.2 Connect a domain name

To activate the acceleration service for your business, you need to connect an acceleration domain name. ECDN caches static content on edge servers to enable nearby resource access for users and quickly pulls origin servers to get dynamic content through intelligent routing optimization, protocol optimization, and other dynamic acceleration technologies, realizing resource access acceleration. For more information, please see [Domain Name Connection](https://intl.cloud.tencent.com/document/product/570/10361).

#### 3.3 Configure CNAME

When the domain name connection is completed, ECDN will assign a corresponding CNAME address to you, which needs to be configured before the acceleration service taking effect. For detailed directions, please see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/570/11134).





## 4. Overview of Console Features

<table>
<thead>
<tr>
<th>Desired Operation</th>
<th>Reference Document</th>
</tr>
</thead>
<tbody><tr>
<td>Deleting the connected acceleration domain name; enabling/disabling its acceleration service; modifying its project.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/570/10362" target="_blank">Domain Name Operations</a></td>
</tr>
<tr>
<td>Optimizing your ECDN acceleration effect. ECDN supports various custom configurations.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/570/11136" target="_blank">Configuration Overview</a></td>
</tr>
<tr>
<td>Learning about the advanced origin-pull policies supported by ECDN.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/570/35821" target="_blank">Advanced Origin-Pull Policies</a></td>
</tr>
<tr>
<td>Viewing mapping between the console features and `Action` values.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/570/35819" target="_blank">Console Permission Description</a></td>
</tr>
<tr>
<td>Granting permissions at a domain name level via custom policy statements.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/570/35820" target="_blank">Creating Policies</a></td>
</tr>
<tr>
<td>Viewing metrics such as the number of requests, access traffic, and response time.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/570/10368" target="_blank">Statistics of Access</a></td>
</tr>
<tr>
<td>Querying monitoring data of status codes.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/570/35827" target="_blank">Status Code Statistics</a></td>
</tr>
<tr>
<td>Regularly purging resources cached on nodes and caching the latest resources by pulling origin servers.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/570/35817" target="_blank">Cache Purge</a></td>
</tr>
<tr>
<tr>
<td>Configuring HTTPS certificates for domain names connected to ECDN.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/570/10366" target="_blank">Certificate Management</a></td>
</tr>
<tr>
<td>Analyzing the detailed access logs of your connected domain names.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/570/15258" target="_blank">Log Management</a></td>
</tr>
</tbody></table>



## 5. FAQs

#### Billing
- [How is the traffic exceeding the ECDN free tier limit billed?](https://intl.cloud.tencent.com/document/product/570/35823)
- [What will happen to my ECDN service if my account becomes overdue?](https://intl.cloud.tencent.com/document/product/570/35823)
- [Will fees be incurred after the domain name service is disabled (the domain name is deactivated)?](https://intl.cloud.tencent.com/document/product/570/35823)

#### Access service
- [How do I get the cache node IP accessed by a client?](https://intl.cloud.tencent.com/document/product/570/35824)
- [Why is the obtained client IP address different from the user's real IP address?](https://intl.cloud.tencent.com/document/product/570/35824)
- [What should I do if an exceptional status code is returned for access with ECDN?](https://intl.cloud.tencent.com/document/product/570/35824)
- [How do I quickly locate a domain name access exception?](https://intl.cloud.tencent.com/document/product/570/35824)

#### Domain name connection
- [Should I obtain an ICP filing for services in Mainland China for a domain name connected to ECDN?](https://intl.cloud.tencent.com/document/product/570/35825)
- [Does ECDN support connecting wildcard domain names?](https://intl.cloud.tencent.com/document/product/570/35825)
- [What are the differences between an acceleration port (access port) and an origin-pull port?](https://intl.cloud.tencent.com/document/product/570/35825)
- [What should I do if domain name connection failed in the console?](https://intl.cloud.tencent.com/document/product/570/35825)

#### Features and concepts
- [Does ECDN support HTTPS?](https://intl.cloud.tencent.com/document/product/570/35826)
- [Does ECDN support WebSocket?](https://intl.cloud.tencent.com/document/product/570/35826)
- [Does ECDN support acceleration outside Mainland China?](https://intl.cloud.tencent.com/document/product/570/35826)
- [Does ECDN support upload acceleration?](https://intl.cloud.tencent.com/document/product/570/35826)


## 6. Feedback and Suggestion

If you have any doubts or suggestions when using Tencent Cloud ECDN, you can submit your feedback through the following channels. Dedicated personnel will contact you to solve your problems.

- If you find any problems in product documentation such as links, content, or API errors, you can click **Send Feedback** at the bottom of the document to submit the documentation issues.
- If you encounter product-related problems, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
