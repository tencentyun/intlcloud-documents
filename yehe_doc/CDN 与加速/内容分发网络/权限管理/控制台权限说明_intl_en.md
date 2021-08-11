
When you have specified both `Action` and `Resource` to create a custom policy, you can call APIs to perform operations for desired resources. This document describes the mappings between console features and `Action`.

>!
> - Tencent Cloud CDN can authorize resources by domain name. Authorization does not distinguish between service regions in and outside the Chinese mainland under the same domain name.
> - When you migrate ECDN services to the CDN console, the ECDN API permission policies will be automatically mapped to corresponding CDN API permission policies. However for resource-level permission policies, you need to set them again in CDN after the migration.

## Service Overview

Service overview can categorized as follows based on the displayed content:

| Feature     | Authorized Action                             | Notes                                            |
| ------------ | --------------------------------------- | ---------------------------------------------------- |
| Service usage | DescribeCdnData<br/>DescribeBillingData | If not all domain names are authorized, each domain name’s usage will have to be queried separately |
| Domain name statistics | DescribeDomains                         | The total number of authorized domain names will be returned                                 |
| Billing status     | DescribePayType                         | The permission to change the billing mode cannot be granted to sub-accounts currently                        |
| Traffic package statistics | DescribeTrafficPackages                 | Traffic package status is account-level data, and any associated resources can be queried       |

## Domain Name Management

| Feature         | Authorized Action                                  | Notes                                                     |
| ---------------- | -------------------------------------------- | ------------------------------------------------------------ |
| Domain name list and query   | DescribeDomains                              | Basic configuration items of a domain name can be queried, displayed, and downloaded<br/>To get all detailed configuration items, `DescribeDomainsConfig` should be authorized |
| Adding domain name         | DescribeDomains                              | Domain names can be added in any acceleration service region                                  |
| Disabling domain name         | StopCdnDomain                                | -                                                            |
| Enabling domain name         | StartCdnDomain                               | -                                                            |
| Deleting domain name         | DeleteCdnDomain                              | -                                                            |
| Modifying domain name project | UpdateDomainConfig                           | The domain name project is in the domain name configuration<br/>All configuration items of a domain name can be modified after authorization |
| Domain name configuration management     | UpdateDomainConfig<br/>DescribeDomainsConfig | All configuration items of a domain name can be viewed/modified after authorization                               |

## Certificate Management

| Feature         | Authorized Action                                  | Notes                                                     |
| ------------ | --------------------- | ------------------------ |
| Querying certificate list | DescribeDomainsConfig | All configuration items of a domain name can be viewed after authorization |
| Configuring certificate     | UpdateDomainConfig    | All configuration items of a domain name can be modified after authorization |
| Batch configuring certificates | UpdateDomainsHttps    | This is used to configure certificates in batches         |

## Statistical Analysis

| Feature                                                     | Authorized Action        | Notes                         |
| ------------------------------------------------------------ | ------------------ | -------------------------------- |
| Querying detailed access data                                              | DescribeCdnData    | All access data metrics under a domain name can be queried after authorization |
| Querying detailed origin-pull data                                              | DescribeOriginData | All origin-pull data metrics under a domain name can be queried after authorization |
| Querying top traffic/requests<br/>Querying top domain names<br/>Querying rankings of domain name status codes<br/>Querying usage rankings by province in the Chinese mainland<br/>Querying usage rankings by ISP in the Chinese mainland<br/>Querying usage rankings outside the Chinese mainland | ListTopData        | Rankings of different data metrics and dimensions can be queried after authorization  |
| Querying number of unique IPs                                               | DescribeIpVisit    | -                                |

## Purge and Prefetch

| Feature     | Authorized Action        |
| ------------ | ------------------ |
| Submitting URLs for purge | PurgeUrlsCache     |
| Submitting directories for purge | PurgePathCache     |
| Querying purge records | DescribePurgeTasks |
| Submitting prefetch tasks | PushUrlsCache      |
| Querying prefetch records | DescribePurgeTasks |

## Log Service

| Feature       | Authorized Action           |
| ---------------- | --------------------- |
| Querying log download link | DescribeCdnDomainLogs |

## Network Status Overview

The entire network status monitoring page in the console can be viewed by all sub-accounts with no authorization required.

## Operational Report

| Features                                                     | Authorized Action        | Notes                         |
| ------------------------------------------------------------ | ------------------ | -------------------------------- |
| Querying detailed access data                                              | DescribeCdnData    | All access data metrics under a domain name can be queried after authorization |
| Querying detailed origin-pull data                                              | DescribeOriginData | All origin-pull data metrics under a domain name can be queried after authorization |
| Querying top traffic/requests<br/>Querying top domain names<br/>Querying rankings of domain name status codes<br/>Querying usage rankings by province in the Chinese mainland<br/>Querying usage rankings by ISP in the Chinese mainland<br/>Querying usage rankings outside the Chinese mainland | ListTopData        | Rankings of different data metrics and dimensions can be queried after authorization  |
| Querying number of unique IPs                                               | DescribeIpVisit    | -                                |

## Traffic Package Management

| Feature       | Authorized Action             | Notes                                           |
| -------------- | ----------------------- | -------------------------------------------------- |
| Querying traffic package list | DescribeTrafficPackages | The content returned by the API is irrelevant to the `Resource`. The list can be queried with any authorized resource |

> !Currently, the traffic package renewal and renewal cancellation logics cannot be authorized.

## IP Ownership Query

| Feature                     | Authorized Action   | Notes                                           |
| ---------------------------- | ------------- | -------------------------------------------------- |
| Querying whether IP belongs to Tencent Cloud CDN | DescribeCdnIp | The content returned by the API is irrelevant to the `Resource`. The list can be queried with any authorized resource |

## Self-Diagnosis Tool

Currently, the self-diagnosis tool cannot be authorized for sub-accounts.
