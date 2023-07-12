CFS Turbo is Tencent Cloud's high-performance parallel file system. Compared with traditional general CFS, it supports CCN and VPC networks on the client and server, both of which have their respective pros and cons. This document describes the two network types to help you select a more suitable one for your business. If you use CCN, we recommend you create Turbo file systems based on CCN; otherwise, you can select VPC for easier use, if applicable.

## CCN

#### Overview

Specified IP ranges are assigned to Turbo file systems, and CCN capabilities are leveraged to connect the VPC and storage server network, implementing the interaction between computing instances and storage.

| Pro | Con |
|---------|---------|
| <ul style="margin: 0;"><li>IP range planning is separately stored for more efficient and convenient management of security groups.</li><li>Turbo CFS has its own IP range to reserve sufficient IPs for further scale-outs without limits.</li><li>Turbo CFS can be accessed more easily across VPCs.</li><li>IPs of the existing VPC are not occupied.</li></ul> | CCN is required for network connection. If CCN is not used, a new component needs to be introduced, which is quite complicated. |

#### Best practices

An existing CCN instance or a newly created one is used to assign 9/11/30 Tencent server IP ranges to Turbo CFS, without occupying business IPs.

## VPC

#### Overview

IPs are mapped to the existing VPC on the storage server for mount and access.

| Pro | Con |
|---------|---------|
| <ul style="margin: 0;"><li>It is the easiest to use and is similar to general CFS.</li><li>No new components need to be introduced in this simple solution.</li></ul> | <ul style="margin: 0;"><li>During large scale-outs, subnet IPs may be insufficient.</li><li>VPC IPs will be occupied, and the storage is bound to the VPC, which hinders network isolation.</li></ul> |

