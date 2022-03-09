This document describes the cloud accounts in CODING Continuous Deployment (CODING-CD).

## Prerequisites

You must activate the CODING DevOps service for your Tencent Cloud account before you can use CODING Project Management (CODING-PM). 

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Go to the CODING Workspace homepage, click **Feature Settings** > **Continuous Deployment** on the left to open the Cloud Account Management page.

## Function Overview

A cloud account is a credential for accessing cloud resources. Only after a cloud account is configured can CODING-CD implement the management of infrastructure and the deployment of cloud resources. Currently, the following cloud account types are supported:

- Tencent Cloud TKE: It is displayed only when you register and log in via the Tencent Cloud Developer Platform.
- Kubernetes: Two commonly used credentials are supported, i.e. [Kubeconfig](https://kubernetes.io/zh/docs/concepts/configuration/organize-cluster-access-kubeconfig/) and the Service Account.
- Tencent Cloud Account: Tencent Cloud API key.

In the CODING Workspace homepage, click **Feature Settings** > **Continuous Deployment** > **Cloud Account** to manage your cloud account.

## Tencent Cloud TKE

1. Select "Tencent Cloud TKE" for the cloud account type, and then bind the cloud account to the corresponding cluster according to the directions. If there is no cluster under the cloud account, go to [Tencent Cloud TKE](https://intl.cloud.tencent.com/zh/products/tke) to create a cluster.
![](https://qcloudimg.tencent-cloud.cn/raw/223443d999183852b7cdb81a3195e1c1.png)
2. Select the cluster to be deployed. Once you click **OK**, the cluster under the cloud account will be automatically verified and bound to the account.

## Kubernetes

A Kubernetes cloud account supports two commonly used credentials, i.e. Kubeconfig and the Service Account. Taking Kubeconfig as an example:

Log in to the Cloud Computing Web Console, copy Kubeconfig, and then add the CODING IP range to the extranet access control list (allowlist) of the cluster.

<dx-alert infotype="explain" title="CODING Continuous Deployment：">
 212.64.105.0/24, 212.129.144.0/24
</dx-alert>

![](https://qcloudimg.tencent-cloud.cn/raw/35d2425672d277926d710d4d09d16ff4.png)

Paste Kubeconfig into the CODING console, and then select the "Cluster Context" to add the cloud account.

![](https://qcloudimg.tencent-cloud.cn/raw/41ebe47aed03ddfba65afd80a47ff79f.png)

## Tencent Cloud Account

1. Select "Tencent Cloud" for the cloud account type, enter a cloud account name, and then select a region. Multiple selection is supported. You will be able to manage the Tencent Cloud resources of the selected regions in CODING-CD.
![](https://qcloudimg.tencent-cloud.cn/raw/0f0b1bc6765261251a8e7a78eb3b9a9e.png)
2. Log in to the [Access Management Console](https://console.cloud.tencent.com/cam/capi) to copy the key information.
![](https://qcloudimg.tencent-cloud.cn/raw/50297a54262a313ad31840f33e09e226.png)
3. Paste the SecretID and SecretKey you copied into the corresponding text fields, and then click **OK** to add the cloud account.

