Cloud Access Management (CAM) is a web-based service that helps you securely manage access permissions, resources, and usage permissions for your Tencent Cloud account. With CAM, you can create, manage, and terminate users (groups), and control the Tencent Cloud resources that can be used by the specified user through identity and policy management. For more information, please see [User Guide](https://intl.cloud.tencent.com/document/product/598/17848).

ECDN supports resource-level authorization. By specifying the `Action` and `Resource` to create a custom policy, you can directly call APIs to perform operations on resources such as acceleration domain names. This document describes the mappings between console features and `Action`.

## Overview

| Feature Module                                                     | Authorized Action            | Remarks |
| ------------------------------------------------------------ | ---------------------- | -------------------------- |
| My service - Connected domain names                                            | DescribeDomains        | The total number of authorized domain names will be displayed       |
| My service <li>Total number of requests in the current month</li><li>Total traffic in the current month</li><li>Average bandwidth in the current month</li> | DescribeEcdnStatistics | The access data of authorized domain names in the current month will be displayed |
| Today's data                                                     | DescribeEcdnStatistics | Today's access data of authorized domain names will be displayed |
| Request trend in the current month                                               | DescribeEcdnStatistics | The trend curve of requests in the current month will be displayed   |

## Domain Management

| Feature Module         | Authorized Action                                  | Remarks |
| ---------------- | -------------------------------------------- | ------------------------------------------------------------ |
| Domain name list and query   | DescribeDomains                              | Basic configuration items of a domain name can be queried or displayed<br/>To get all detailed configuration items, `DescribeDomainsConfig` should be authorized |
| Adding domain name         | AddEcdnDomain                                | -                                                            |
| Deactivating ECDN     | StopEcdnDomain                               | -                                                            |
| Activating ECDN     | StartEcdnDomain                              | -                                                            |
| Deleting domain name         | DeleteEcdnDomain                             | -                                                            |
| Modifying domain name project | UpdateDomainConfig                           | The domain name project is in the domain name configuration<br/>All configuration items of a domain name can be modified after authorization |
| Domain name configuration management     | UpdateDomainConfig<br/>DescribeDomainsConfig | All configuration items of a domain name can be viewed/modified after authorization                               |

## Statistical Analysis

| Feature Module     | Authorized Action           | Remarks |
| ---------- | ------------------------------------------------------ | ---------------------------------- |
| Usage statistics | DescribeEcdnDomainStatistics<br>DescribeEcdnStatistics | All access data metrics under a domain name can be queried after authorization |
| Status code statistics | DescribeEcdnStatistics                                 | All status code metrics under a domain name can be queried after authorization |

## Cache Purge

| Feature Module     | Authorized Action        |
| ------------ | ------------------ |
| Submitting URLs for purge | PurgeUrlsCache     |
| Submitting directories for purge | PurgePathCache     |
| Querying purge records | DescribePurgeTasks |

## Certificate Management

| Feature Module     | Authorized Action           | Remarks |
| ------------ | --------------------- | ------------------------ |
| Querying certificate list | DescribeDomainsConfig | All configuration items of a domain name can be viewed after authorization |
| Configuring certificate     | UpdateDomainConfig    | All configuration items of a domain name can be modified after authorization |
| Batch configuring certificates | UpdateDomainsHttps    | It is used to configure certificates in batches         |

## Log Service

| Feature Module         | Authorized Action           |
| ---------------- | ---------------------- |
| Querying log download link | DescribeEcdnDomainLogs |
