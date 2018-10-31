## Introduction

Cloud Archive Storage (CAS) provides a reliable and low-cost offline storage service on the cloud to enterprises and developers. You can store unstructured data in any size and any form in CAS for disaster recovery and backup. Due to the distributed cloud storage in CAS, you can use the RESTful API to manage your data in any network environment.

CAS mainly provides long-term archive and backup management for large amounts of important unstructured data that is accessed infrequently. A data lock mechanism in CAS can prevent data from being modified and deleted, to ensure data security. You can store huge amounts of data at very low storage fees, greatly reducing your costs.

## Architecture
![Image Description](https://mc.qcloudimg.com/static/img/2af86f003c7d9cb3d610104d0b67b574/RTX20170427-162613%402x.png)

## Performance Metrics

Tencent Cloud CAS has three performance metrics: high QPS, large bandwidth, and data retrieval.

### Requests per second (QPS)

By default, each user has a quota of 800 QPS in each region. For example, if you use CAS in the Beijing and Shanghai regions, you are allocated 800 QPS for each. If you require a higher QPS, submit a ticket or contact us to increase this quota.

### Large bandwidth

To better serve users, Tencent Cloud CAS has a very large bandwidth in each region. You can reuse these public bandwidths. Generally, the CAS bandwidth is larger than each user's bandwidth. If you have special requirements for bandwidth, [submit a ticket](https://console.cloud.tencent.com/workorder/category) and we will provide specific support.

### Data retrieval

Data retrieval has three tiers. For data within 256 MB, Expedited retrieval is applicable. For data larger than 256 MB, Standard or Bulk retrieval is applicable.
Expedited retrieval is normally completed within 1-5 minutes, standard retrieval within 3-5 hours, and bulk retrieval within 5-12 hours.

## Differences with COS
CAS is an offline storage service, while COS is an online service. The differences in usage are as follows:

### 1. File index is not saved

#### Description

COS is composed of file data and the file index (including file meta information). You can access data with specific URI strings, and it is possible for you to obtain all of the URIs in real time.

To reduce costs, instead of the file index, CAS uses the archive ID which records information such as the archive owner and storage address. The ID is not readable to users, but can only be identified and translated by the CAS system.

- Archive ID usage method I

1. When you upload an archive and the system returns the archive ID, you record the archive ID.
2. Initiate a data retrieval job with the archive ID.

- Archive ID usage method II

1. When you upload an archive and the system returns the archive ID, you do not record the archive ID.
2. Initiate a "retrieve the archive inventory" data retrieval job.
3. The job returns a table or a JSON string, and each record includes an archive ID, remarks for the archive, upload time, etc. This process lasts about 3-5 hours.
4. Initiate archive retrieval jobs using the archive IDs.

#### Effects

- Cost savings: As the file index is not saved, CAS is much cheaper than COS.
- You cannot obtain an inventory of all archives in the current vault in real time. You need to initiate a "retrieve the archive inventory" data retrieval job, which takes about 3-5 hours.
- You cannot use URIs to obtain archives directly. You need to record the archive ID to initiate a data retrieval request.
- You cannot obtain the number and total size of the archives in the current vault in real time. Such data is updated once a day.
  [](https://mc.qcloudimg.com/static/img/46ce4d096dabbd260302b1dfeea26b76/f39b95eb-a595-43f8-88b8-809498d9dce1.png)

### 2. Data retrieval takes time

#### Description

The storage clusters in CAS are classified into the "temporary cache cluster" and "persistent cold data cluster". When you upload data, the data first goes to the "temporary cache cluster", and then degrades to the "persistent cold data cluster". When you retrieve data, the data moves from the "persistent cold data cluster" to the "temporary cache cluster", and then it is returned to you.

The data saved in the "persistent cold data cluster" undergoes disk hibernation and the data is scheduled between the "persistent cold data cluster" and the "temporary cache cluster". As such, you need to wait for the disk to wake up and the data to be scheduled before you can retrieve the data.

#### Effects

- Cost savings: As disk hibernation saves power for the data center, CAS is much cheaper than COS.
- You have to initiate a job request. After waiting a while, you then have to initiate a Get Job Output request to get the data in the output that is an external manifestation of the "temporary cache cluster". Data in the output is retained for 24 hours.
- There are three modes for an archive retrieval or an archive import to COS job. The three modes require different amounts of time, and have different pricing. **A shorter return time means a higher priority in the system data scheduling, and a higher price.**

