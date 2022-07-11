## Overview

Cloud Native Gateway is an API gateway hosting product incubated by Tencent Cloud that is 100% compatible with the open source Kong gateway. It is currently in beta test.

This document describes how to create a Cloud Native Gateway instance in the console.


## Directions

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1) and click **Cloud Native Gateway** on the left sidebar.
2. Click **Create** to enter the Cloud Native Gateway instance creation page.

| Parameter | Required | Description |
| ------------ | -------- | ------------------------------------------------------------ |
| Region         | Yes       | Select the region of the Cloud Native Gateway instance.                                 |
| Availability Zone       | Yes       | Select the AZ of the Cloud Native Gateway instance in the selected region. Unavailable AZs have insufficient resources. |
| Gateway Name     | Yes       | Enter the name of the Cloud Native Gateway instance.                                   |
| Gateway Type     | Yes       | Currently, only Kong gateway is supported.                                       |
| Gateway Version     | Yes       | Open-source version of the selected gateway type.                               |
| Cluster Node Specifications | Yes       | Select the specification of each node. A Cloud Native Gateway cluster consists of multiple nodes.       |
| Number of Cluster Nodes | Yes       | Select the number of cluster nodes. A Cloud Native Gateway cluster consists of multiple nodes.           |
| Network     | Yes       | Select the VPC where the Cloud Native Gateway instance is deployed.                |
| Subnet     | Yes       | Select the subnet where the Cloud Native Gateway instance is deployed in the selected VPC.  |
| Description         | No       | Enter the description of the current Cloud Native Gateway instance.                               |

<img src="https://main.qcloudimg.com/raw/aaed3e088e55deeb89fd0e4bab552132.png" width="700px">


3. Click **Save** and wait for the instance to be created.

## Notes

- To create a Cloud Native Gateway instance, your account must be granted with the `ApiGateWay_QCSRole` role, and the role must be associated with the `QcloudAccessForApiGateWayRoleInCloudNativeAPIGateway` policy. If your account doesn't have such role and policy, grant them in the pop-up authorization window during creation.
- The log feature of Cloud Native Gateway relies on [CLS](https://intl.cloud.tencent.com/document/product/614). Make sure that you have activated CLS in the [CLS console](https://console.cloud.tencent.com/cls/overview) before creating a Cloud Native Gateway instance.
- Currently, Cloud Native Gateway is in beta and free of charge.
