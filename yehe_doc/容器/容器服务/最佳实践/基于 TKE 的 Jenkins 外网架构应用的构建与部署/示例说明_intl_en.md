## Introduction

Jenkins helps users set up a continuous integration and continuous delivery environment. The Jenkins Master/Slave pod architecture can solve the pain points of concurrence restriction in batch building for enterprises, implementing continuous integration. This document describes how to use Jenkins in Tencent Cloud TKE to implement rapid and sustainable business delivery and reduce resource and labor costs.

## How It Works
The TKE-based Jenkins public network architecture is used as an example in this document. In this architecture, the Jenkins Master is located outside the TKE cluster and the slave pod is located within the TKE cluster. The diagram of the architecture is shown in the following figure:
![](https://main.qcloudimg.com/raw/e26d2b0778ba27ea2b77cb5f31079ae7.jpg)

- The Jenkins Master and TKE cluster are located in the same VPC network.
- The Jenkins Master is outside the TKE cluster, and the slave pod is in a node of the TKE cluster.
- The user submits code to GitLab, which triggers the Jenkins Master to call the slave pod to build, package, and then publish the image into the TKE image repository. The TKE cluster pulls the image and triggers rolling update for pod deployment.
- Multi-slave-pod building can meet the need of concurrent batch building.

## Operation Environment

This section describes the specific environment in this scenario.

### TKE cluster
| Role | Kubernetes Version | Operating System |
|---------|---------|---------|
| TKE managed cluster | 1.16.3 | CentOS 7.6.0_x64 |

### Jenkins configuration
<table>
<thead>
<tr>
<th style="width:50%">Role</th>
<th>Version</th>
</tr>
</thead>
<tbody><tr>
<td>Jenkins Master</td>
<td>2.190.3</td>
</tr>
<tr>
<td>Jenkins Kubernetes plug-in</td>
<td>1.21.3</td>
</tr>
</tbody></table>

### Nodes
| Role | Private IP | Operating System | CPU | Memory | Bandwidth |
|---------|---------|---------|---------|--------|--------|
| Jenkins Master | 10.0.0.7 | CentOS 7.6 64-bit | 4 cores | 8 GB | 3 Mbps |
| Node | 10.0.0.14 | CentOS 7.6 64-bit | 2 cores | 4 GB | 1 Mbps |


## Notes
- Be sure that a Jenkins Master node is available under the same VPC as the TKE cluster, and that Git is installed for the node.
- Be sure that the GitLab code repository used in the steps already contains a Dockerfile file.
- We recommend that you set the TKE cluster and Jenkins Master security group as being fully open to the private network. For more information, see [TKE Security Group Settings](https://intl.cloud.tencent.com/document/product/457/9084).

## Procedure
Complete the following steps to configure the TKE cluster and Jenkins. Then, use the slave pod to build, package, and publish the image into the TKE image repository. Lastly, use the pulled image for pod deployment in the TKE console.
1. [TKE Cluster and Jenkins Configuration](https://intl.cloud.tencent.com/document/product/457/34867) 
2. [Slave Pod Building Configuration](https://intl.cloud.tencent.com/document/product/457/34868)
3. [Building Test](https://intl.cloud.tencent.com/document/product/457/30637)
