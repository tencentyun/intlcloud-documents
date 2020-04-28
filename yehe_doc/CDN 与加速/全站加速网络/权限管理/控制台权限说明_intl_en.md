CAM web service provided by Tencent Cloud helps you securely manage access to your Tencent Cloud accounts and permissions of managing and using resources under the accounts. Using CAM, you can create, manage, and terminate users (groups), and control the Tencent Cloud resources that can be used by the specified user through identity and policy management. For more information, please see [User Guide](https://intl.cloud.tencent.com/document/product/598/17848).

ECDN supports resource-level authorization. By specifying the `Action` and `Resource` to create a custom policy, you can directly call APIs to perform operations for resources such as acceleration domain names. This document describes the mappings between console features and `Action`.

## Overview

| Feature Module                                                     | Authorized Action            | Precautions                   |
| ------------------------------------------------------------ | ---------------------- | -------------------------- |
| My service - Connecting to domain names                                            | DescribeDomains        | The total number of authorized domain names will be displayed       |
| My service<li>Total number of requests in this month</li><li>Total traffic in this month</li><li>Average bandwidth peak in this month</li> | DescribeEcdnStatistics | The access data of authorized domain names in this month will be displayed |
| Today's data                                                     | DescribeEcdnStatistics | Today's access data of authorized domain names will be displayed |
| Trend in the number of requests in this month                                               | DescribeEcdnStatistics | The curve of the trend in the number of requests in this month will be displayed   |

## Domain Name Management

| Feature Module         | Authorized Action                                  | Precautions                                                     |
| ---------------- | -------------------------------------------- | ------------------------------------------------------------ |
| Domain name list and query   | DescribeDomains                              | Basic configuration items of a domain name can be queried or displayed<br/>To get all detailed configuration items, `DescribeDomainsConfig` should be authorized |
| Adding domain name         | AddEcdnDomain                                | -                                                            |
| Deactivating ECDN     | StopEcdnDomain                               | -                                                            |
| Activating ECDN     | StartEcdnDomain                              | -                                                            |
| Deleting domain name         | DeleteEcdnDomain                             | -                                                            |
| Modifying domain name project | UpdateDomainConfig                           | The domain name project is in the domain name configuration<br/>All configuration items of a domain name can be modified after authorization |
| Domain name configuration management     | UpdateDomainConfig<br/>DescribeDomainsConfig | All configuration items of a domain name can be viewed/modified after authorization                               |

## Statistical Analysis

| Feature Module   | Authorized Action                                            | Precautions                           |
| ---------- | ------------------------------------------------------ | ---------------------------------- |
| Usage statistics | DescribeEcdnDomainStatistics<br>DescribeEcdnStatistics | All access data metrics under a domain name can be queried after authorization   |
| Status code statistics | DescribeEcdnStatistics                                 | All status code metrics under a domain name can be queried after authorization |

## Cache Purge

| Feature Module     | Authorized Action        |
| ------------ | ------------------ |
| Submitting URLs for purge | PurgeUrlsCache     |
| Submitting directories for purge | PurgePathCache     |
| Querying purge records | DescribePurgeTasks |

## Certificate Management

| Feature Module     | Authorized Action           | Precautions                 |
| ------------ | --------------------- | ------------------------ |
| Querying certificate list | DescribeDomainsConfig | All configuration items of a domain name can be viewed after authorization |
| Configuring certificate     | UpdateDomainConfig    | All configuration items of a domain name can be modified after authorization |
| Batch configuring certificates | UpdateDomainsHttps    | It is used to configure certificates in batches         |

## Log Service

| Feature Module         | Authorized Action            |
| ---------------- | ---------------------- |
| Querying log download link | DescribeEcdnDomainLogs |
