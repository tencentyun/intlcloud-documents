## Overview

An instance is a resource in API Gateway that can provide public IP, private IP, public network egress, computing, and storage resources required to process an API. A service must be mounted under an instance before it can run normally.

## Instance Types

- **Shared instance:** shared instance is the default instance type provided by API Gateway. It adopts a pay-as-you-go billing mode, where the underlying machine resources are shared by a group of API Gateway users in the same region. It is suitable for individual users with a small business scale and moderate requirements for performance and stability.

- **Dedicated instance:** dedicated instance has all the capabilities of shared instance and supports two billing modes: monthly subscription and pay-as-you-go. Its underlying resources are exclusive to one user. Compared with shared instance, it can provide higher performance and SLA guarantee and thus is more suitable for use in production environments by large-sized customers.

## Instance Comparison

<table>
<thead>
<tr>
<th>Item</th>
<th>Shared instance</th>
<th>Dedicated instance</th>
</tr>
</thead>
<tbody><tr>
<td>Scenario</td>
<td>Small-scale services, develop and test environments</td>
<td>Large-scale services, production environments</td>
</tr>
<tr>
<td>Billing mode</td>
<td>Pay-as-you-go</td>
<td>Monthly Subscription, Pay-as-You-Go</td>
</tr>
<tr>
<td>Billable items</td>
<td>Invocations, outbound traffic</td>
<td>Instance fee, outbound traffic</td>
</tr>
<tr>
<td>SLA</td>
<td>99.9%</td>
<td>99.95% - 99.99%</td>
</tr>
<tr>
<td>Public network ingress point</td>
<td>Shared by a group of users</td>
<td>Dedicated</td>
</tr>
<tr>
<td>VPC ingress address</td>
<td>Shared by a group of users</td>
<td>Dedicated</td>
</tr>
<tr>
<td>Public network egress point</td>
<td>Shared by a group of users</td>
<td>Dedicated</td>
</tr>
<tr>
<td>Public network outgoing bandwidth</td>
<td>Shared by a group of users</td>
<td>Dedicated</td>
</tr>
<tr>
<td>Request size</td>
<td>Up to 16 MB</td>
<td>Customized (Up to 10 GB</td>
</tr>
<tr>
<td>Max services/instance</td>
<td>200</td>
<td>100 - 2,000</td>
</tr>
<tr>
<td>Max API QPS/service</td>
<td>500 QPS</td>
<td>2,500 QPS - 50,000 QPS</td>
</tr>
<tr>
<td>Environment</td>
<td>Cannot connect to VPC</td>
<td>Support connecting to VPC and Direct Connect instances</td>
</tr>
<tr>
<td>TLS version control</td>
<td>Not supported</td>
<td>Supported</td>
</tr>
</tbody></table>

> ! Requests may be discarded if the QPS limit is reached. For shared instances, the resource is shared by a group of users. This means if other users in the group have large number of requests, your service performance is affected. To sure the service availability, it’s recommended to use dedicated instances for production environments. 

## Features of Dedicated Instance

#### High performance and low latency

Compared with a shared instance, a dedicated instance has underlying resources that are exclusive to one user, so it has higher performance and lower latency, making it able to support tens of thousands of QPS and easily cope with large traffic.

#### Network interconnection

An API Gateway dedicated instance runs in a VPC and supports forwarding client requests to various services deployed in the VPC or Direct Connect IDC or on the public network. It is deeply integrated with common backend services in the cloud such as CVM, SCF, TKE, TSF, CLB as well as your own services to provide a productized connection method.

#### Fixed and independent egress address

Unlike a shared instance where different users share the same egress IP, an API Gateway dedicated instance provides a fixed and independent egress IP to ensure the long-term stable operations of the business.

#### Security and high availability

The security and high availability of an API Gateway dedicated instance can be reflected in several aspects such as physical isolation, clustering, and exceptional address removal.

- Physical isolation: an API Gateway dedicated instance tenant is completely physically isolated from other dedicated/shared instance tenants in the same region. There is no data interaction between instances. Attacks to other instances will not affect the stability of the current instance.
- Clustering: the underlying resources of an API Gateway dedicated instance generally consist of multiple machines (except the Basic Edition), so that the exception of a single machine does not affect the overall availability of the service.
- Exceptional address removal: an API Gateway dedicated instance dynamically monitors the backend health and automatically removes exceptional backend addresses. In this way, if multiple backend addresses are configured, some exceptional addresses will not affect the gateway service.
- Connection with security services: an API Gateway dedicated instance can be connected with Tencent Cloud security services such as WAF and EIAM to enjoy professional security support.

#### Support for backend load balancing

An API Gateway dedicated instance has the backend load balancing capabilities that can be connected with multiple business nodes running in a VPC. As a result, you can easily use API Gateway to open up the capabilities of TKE and CVM.

## Applicable Scenarios of Dedicated Instance

The core strengths of API Gateway dedicated instance are ultra-high performance, SLA guarantee, and security. Its typical applicable scenarios are as follows:

#### High concurrency

High-Concurrency scenarios such as ecommerce flash sales and ticketing systems are generally triggered at scheduled times, and the traffic may surge instantaneously, yet they require that only part of client requests succeed. In this case, you can use API Gateway dedicated instances in combination with the traffic throttling feature to meet the needs for high concurrency and traffic throttling.

#### Key online businesses

Key online businesses generally have higher requirements for stability and security. API Gateway dedicated instances provide an ultra-high SLA, which can ensure the smooth operations of such businesses.

#### Complex network environment

If your backend businesses are distributed in a variety of complex network environments such as public network, VPC, and IDC Direct Connect, and you need a common traffic egress, API Gateway dedicated instances are your ideal choice, as they support interconnection with diversified complex network environments in the cloud and serve as a unified access layer for such environments. 

## Regions Supporting Dedicated API Gateways

| Region | Value | Support |
| ------------------ | ------------ | -------- |
| South China (Guangzhou) | ap-guangzhou | Yes |
| East China (Shanghai) | ap-shanghai | Yes |
| North China (Beijing) | ap-beijing | Yes |
| Hong Kong/Macao/Taiwan (China) | ap-hongkong  | Yes     |
