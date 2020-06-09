This document helps you get started with Tencent Cloud Content Delivery Network (CDN).

## 1. Basic CDN Knowledge

- [How does CDN work?](https://intl.cloud.tencent.com/document/product/228/2939)
- [Why Tencent Cloud CDN?](https://intl.cloud.tencent.com/document/product/228/2941)
- [What are the use cases of CDN?](https://intl.cloud.tencent.com/document/product/228/32980)
- [What are the use limits of CDN?](https://intl.cloud.tencent.com/document/product/228/32981)

-----

## 2. CDN Billing Modes

Tencent Cloud CDN has two billing modes: **bill-by-bandwidth** and **bill-by-traffic**. You need to understand the two CDN billing modes so that you can choose the right mode for you. For more information, please see [Billing Instruction](https://intl.cloud.tencent.com/document/product/228/2949).

-----

## 3. Getting Started

#### 3.1. Activate the service and select the billing mode

Before using CDN, you need to sign up for a Tencent Cloud account and activate the CDN service. For more information, please see [Overview](https://intl.cloud.tencent.com/document/product/228/32978).

#### 3.2. Connect a domain name

You need to add an accelerated domain name for your acceleration service. Through an accelerated domain name, CDN caches resources on an origin server into a CDN cache node closest to the client to accelerate resource access. For more information, please see [Adding Domain Names](https://intl.cloud.tencent.com/document/product/228/5734).

#### 3.3. Configure a CNAME record

When the distribution is created, CDN will assign you a corresponding CNAME address, which needs to be configured before taking effect. For detailed directions, please see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).

> You can also follow the best practices below to get started with CDN and accelerate your domain name:
>- [Accelerating Access to CVM with CDN](https://intl.cloud.tencent.com/document/product/228/34035)
>- [Accelerating Access to COS with CDN](https://intl.cloud.tencent.com/document/product/228/34036)

-----

## 4. Console

Below is the overview page of the CDN Console:
![](https://main.qcloudimg.com/raw/95fff730b132974403698b512260f3fb.png)

-----

## 5. Overview of Console Features

<table>
<thead>
<tr>
<th>Desired Operation</th>
<th>Reference Document</th>
</tr>
</thead>
<tbody><tr>
<td>View, activate, or disable a connected acceleration domain name.</td>
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
<td>View mappings between Console features and `Action` values.</td>
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
<td><a href="https://intl.cloud.tencent.com/document/product/228/32918" target="_blank">Real-Time Monitoring</a></td>
</tr>
<tr>
<td>Analyze your user sources, distribution, and usage.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/32923" target="_blank">Data Analysis</a></td>
</tr>
<tr>
<td>Purge resources cached in CDN nodes on a regular basis so that the nodes will pull the latest versions of resources from the origin server and cache them again.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6299" target="_blank">Cache Purge</a></td>
</tr>
<tr>
<td>Load specified resources onto a cache node in advance.</td>
<td>Cache Prefetch</td>
</tr>
<tr>
<td>Download access logs and analyze popular resources and active users as needed.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6316" target="_blank">Log Download</a></td>
</tr>
<tr>
<td>Quickly search for and analyze your log data.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35380" target="_blank">Real-Time Log</a></td>
</tr>
<tr>
<td>View the real-time status overview and the details of the entire network.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6311" target="_blank">Entire Network Status Monitoring</a></td>
</tr>
<tr>
<td>View multi-dimensional reports that show and help you analyze your business status.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6312" target="_blank">Operational Report</a></td>
</tr>
<tr>
<td>View traffic package usage in mainland China on the CDN Console.</td>
<td>Traffic Package Management</td>
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
<td>Monitor and protect your resources from DDoS, CC, and WAF attacks.</td>
<td>Secure Acceleration</td>
</tr>
<tr>
<td>Use CDN to deliver a massive number of images.</td>
<td>Image Optimization</td>
</tr>
</tbody></table>
-----





