## Overview

In TEM, an environment is a collection of computing, network, storage, and other resources. TEM provides the multi-environment management feature. In this way, you can create multiple environments for development, testing, prerelease, and production according to your business needs, deploy applications separately, and thus implement environment isolation. Applications in different environments are isolated from each other. Applications in the same environment can access each other through the K8s service mechanism or registries such as ZooKeeper and Eureka.

This document describes how to create an environment in the TEM console.

## Directions

1. Log in to the [TEM console](https://console.cloud.tencent.com/tem).
2. On the **Environment** page, select a deployment region and click **Create**.
3. Configure the environment information.
   ![](https://main.qcloudimg.com/raw/903559e9f19dd970791682461c7e1d63.png)
   - Name: enter up to 40 characters.
   - VPC: select an existing VPC. If your existing VPCs are not suitable or you haven't created a VPC yet, you can click [Create VPC](https://console.cloud.tencent.com/vpc/vpc?rid=4) to create one (note that the selected region must be the same as that of the environment), return to and refresh this page, and select it.
   - Subnet: select an existing subnet. We recommend you choose multi-AZ deployment to improve the disaster recovery capabilities. If your existing subnets are not suitable or you haven't created a subnet yet, you can click [Create Subnet](https://console.cloud.tencent.com/vpc/subnet?rid=4&unVpcId=) to create one, return to and refresh this page, and select it.
   - CoreDNS is automatically deployed to support service discovery in the environment. Specifically, two replica nodes of `Deployment:coredns` are automatically deployed in the Kubernetes cluster namespace `kube-ststem`. This service is free of charge, and we recommend you not modify it.
4. Click **OK** and the environment will enter the initialization state. Wait a few minutes, and the environment will be created.



