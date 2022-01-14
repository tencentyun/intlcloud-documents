## Overview

An instance is a resource in API Gateway that can provide public IP, private IP, public network egress, computing, and storage resources required to process an API. A service must be mounted under an instance before it can run normally.

## Instance Types

- **Shared instance:** shared instance is the default instance type provided by API Gateway. It adopts a pay-as-you-go billing mode, where the underlying machine resources are shared by a group of API Gateway users in the same region. It is suitable for individual users with a small business scale and moderate requirements for performance and stability.

- **Dedicated instance:** dedicated instance has all the capabilities of shared instance and supports two billing modes: monthly subscription and pay-as-you-go. Its underlying resources are exclusive to one user. Compared with shared instance, it can provide higher performance and SLA guarantee and thus is more suitable for use in production environments by large-sized customers.

## Instance Comparison

| Item | Shared Instance | Dedicated Instance |
| ------------------ | -------------------------- | --------------------------------------------- |
| Applicable scenarios | R&D and test environments with a small business scale | Production environments with a large business scale |
| Billing mode | Pay-as-you-go | Monthly subscription and pay-as-you-go |
| Billable items | Number of calls and public traffic outbound traffic | Instances and public traffic outbound traffic |
| SLA | 99.9% | 99.95%–99.99% |
| Public network entry address | Shared by a group of users | Dedicated |
| VPC private network entry address | Shared by a group of users | Dedicated |
| Public network egress address | Shared by a group of users | Dedicated |
| Public network egress bandwidth | Shared by a group of users | Dedicated |
| Request packet size limit | 16 MB | Customizable and up to 10 GB (coming soon) |
| Service and API QPS limit | 500 QPS | 2500–50000 QPS |
| Operating environment | Not in VPC | In VPC with native capability to connect with VPCs and Direct Connect lines |

> !If the actual request volume greatly exceeds the QPS limit, the overall performance of the instance may be affected, and excessive requests may be discarded with a certain probability.

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
- Connection with security services: an API Gateway dedicated instance can be connected with Tencent Cloud security services such as WAF and IAM to enjoy professional security support.

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

## Regions Available for Dedicated Instance

| Region | Value | Support |
| ------------------ | ------------ | -------- |
| South China (Guangzhou) | ap-guangzhou | Yes |
| East China (Shanghai) | ap-shanghai | Yes |
| North China (Beijing) | ap-beijing | Yes |
| Hong Kong/Macao/Taiwan (China Region) (Hong Kong (China)) | ap-hongkong  | Yes     |
