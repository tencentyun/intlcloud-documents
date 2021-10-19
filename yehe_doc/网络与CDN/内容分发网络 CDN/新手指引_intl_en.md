This document helps you get started with Tencent Cloud Content Delivery Network (CDN).

## 1. Basic CDN Knowledge

- [How does CDN work?](https://intl.cloud.tencent.com/document/product/228/2939)
- [Why Tencent Cloud CDN?](https://intl.cloud.tencent.com/document/product/228/2941)
- [CDN use cases](https://intl.cloud.tencent.com/document/product/228/32980)
- [What are the use limits of CDN?](https://intl.cloud.tencent.com/document/product/228/32981)
- [Basic concepts](https://intl.cloud.tencent.com/document/product/228/36183)



## 2. CDN Billing Modes

Tencent Cloud CDN has two billing modes: **bill-by-bandwidth** and **bill-by-traffic**. You need to understand the two CDN billing modes so that you can choose the right mode for you. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/228/2949).






## 3. Getting Started

#### 3.1. Activate the service and select the billing mode

Before using CDN, you need to sign up for a Tencent Cloud account and activate the CDN service. For more information, please see [Configuring CDN from Scratch](https://intl.cloud.tencent.com/document/product/228/32978).

#### 3.2. Connect a domain name

You need to add an acceleration domain name for your acceleration service. Through an acceleration domain name, CDN caches resources from an origin server to a CDN cache node closest to the client to accelerate resource access. For more information, please see [Adding Domain Names](https://intl.cloud.tencent.com/document/product/228/5734).

#### 3.3 Configure CNAME

When the distribution is created, CDN will assign you a corresponding CNAME address, which needs to be configured before taking effect. For detailed directions, please see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).

>? You can also follow the best practices below to get started with CDN and accelerate your domain name:
>- [Accelerating access to CVM with CDN](https://intl.cloud.tencent.com/document/product/228/34035)
>- [Accelerating access to COS with CDN](https://intl.cloud.tencent.com/document/product/228/34036)




## 4. Console

Below is the overview page of the CDN console:
![](https://main.qcloudimg.com/raw/95fff730b132974403698b512260f3fb.png)




## 5. Overview of Console Features

<table>
<thead>
<tr>
<th>Desired Operation</th>
<th>Reference Document</th>
</tr>
</thead>
<tbody><tr>
<td>View, enable, or disable a connected acceleration domain name.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/5736" target="_blank">Domain Name Operations</a></td>
</tr>
<tr>
<td>Filter and view Tencent Cloud resources or manage them by tag, project, etc.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/32913" target="_blank">Domain Name Search</a></td>
</tr>
<tr>
<td>Optimize your CDN acceleration effect. CDN supports various custom configurations.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6288" target="_blank">Configuration Overview</a></td>
</tr>
<tr>
<td>View mappings between console features and `Action` values.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35229" target="_blank">Console Permissions</a></td>
</tr>
<tr>
<td>Grant permissions at the domain name level through custom policy statements.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35228" target="_blank">Policy Creation</a></td>
</tr>
<tr>
<td>Grant different project-level permissions.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35743" target="_blank">Project-Level Permissions</a></td>
</tr>
<tr>
<td>Use real-time monitoring data to analyze the running status.</td>
<td>Real-time Monitoring</a></td>
</tr>
<tr>
<td>Analyze your user sources, distribution, and usage.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/32923" target="_blank">Data Analysis</a></td>
</tr>
<tr>
<td>Purge resources cached on CDN nodes on a regular basis so that the nodes will pull the latest versions of resources from the origin server and cache them again.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6299" target="_blank">Purge Cache</a></td>
</tr>
<tr>
<td>Load specified resources onto a cache node in advance.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/39000" target="_blank">Prefetch Cache</a></td>
</tr>
<tr>
<td>Download access logs and analyze popular resources and active users as needed.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6316" target="_blank">Download Logs</a></td>
</tr>
<tr>
<td>Quickly search for and analyze your log data.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35380" target="_blank">Real-time Logs</a></td>
</tr>
<tr>
<td>View the real-time status overview and the details of the entire network.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6311" target="_blank">Entire Network Status Monitoring</a></td>
</tr>
<tr>
<td>View multi-dimensional reports that show your business status for analysis.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6312" target="_blank">Operational Report</a></td>
</tr>
<tr>
 
 
</tr>
<tr>
<td>Verify whether a specified IP is of a CDN node.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/10747" target="_blank">Verify Tencent IP</a></td>
</tr>
<tr>
<td>Diagnose a URL with an access exception and quickly locate the problem.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6304" target="_blank">Self-Diagnosis Tool</a></td>
</tr>
<tr>
<td>Monitor and protect your resources from DDoS and CC attacks.</td>
<td>Security Content Delivery Network</a></td>
</tr>
<tr>
<td>Use CDN to deliver a massive number of images.</td>
<td>Image Optimization</a></td>
</tr>
</tbody></table>


## 6. FAQs
#### Billing
- [How to query CDN bills?](https://intl.cloud.tencent.com/document/product/228/31479)
 
- [Can CDN be billed by the number of requests?](https://intl.cloud.tencent.com/document/product/228/31479)
- [If the origin server uses COS, will I be charged for traffic generated by origin-pull from CDN to COS?](https://intl.cloud.tencent.com/document/product/228/31479)
- [When CDN is disabled or deactivated, will it generate traffic and incur fees?](https://intl.cloud.tencent.com/document/product/228/31479)
- [How do I change the billing mode of CDN?](https://intl.cloud.tencent.com/document/product/228/31479)
 
- [Is only downstream traffic billable in CDN?](https://intl.cloud.tencent.com/document/product/228/31479)

#### Domain name connection

- [Does CDN support wildcard domain names?](https://intl.cloud.tencent.com/document/product/228/31476)
- [My domain name has already obtained an ICP filing from the MIIT. Why does the system prompt that it does not have an ICP filing when I try to connect it to CDN?](https://intl.cloud.tencent.com/document/product/228/31476)
- [How long does it take to configure CDN?](https://intl.cloud.tencent.com/document/product/228/31476)
- [Can I configure multiple origin server IPs?](https://intl.cloud.tencent.com/document/product/228/31476)
- [How do I tell whether CDN has taken effect?](https://intl.cloud.tencent.com/document/product/228/31476)
- [Why can a domain name be disabled but not deleted?](https://intl.cloud.tencent.com/document/product/228/31476)
- [How do I disable the acceleration service?](https://intl.cloud.tencent.com/document/product/228/31476)
- [How do I delete an acceleration domain name?](https://intl.cloud.tencent.com/document/product/228/31476)
- [Can I configure ports for acceleration domain names or origin servers?](https://intl.cloud.tencent.com/document/product/228/31476)
- [What should I do if files cannot be downloaded from CDN?](https://intl.cloud.tencent.com/document/product/228/31476)



## 7. Feedback and Suggestions
If you have any doubts or suggestions when using Tencent Cloud CDN, you can submit your feedback through the following channels. Dedicated personnel will contact you to solve your problems.
- If you have any questions regarding CDN documentation, such as links, content, or APIs, please click **Send Feedback** at the bottom of the page.
- If you have any questions about CDN, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

