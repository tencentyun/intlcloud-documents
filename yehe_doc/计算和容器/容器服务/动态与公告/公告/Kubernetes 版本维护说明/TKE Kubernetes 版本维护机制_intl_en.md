

Tencent Kubernetes Engine (TKE) provides container-centric solutions based on native Kubernetes. Since the Kubernetes versions are upgraded continuously, TKE releases the maintained Kubernetes versions on a regular basis. This document describes the Kubernetes version maintenance mechanism.

### Version Maintenance
Starting from September 24, 2018 (UTC +8), TKE only releases Kubernetes major versions with even numbers. The version maintenance mechanism is as follows:

- Cluster creation
TKE supports creating Kubernetes clusters of the latest three versions (for example, v1.16, v1.18 and v1.20). You are unable to create a Kubernetes cluster of an earlier version when a later Kubernetes version is released and upgrading is available. For example, when Kubernetes v1.22 is released and upgrading from v1.20 to v1.22 is available, you are unable to create Kubernetes clusters of v1.16. However, when Kubernetes v1.22 is released and upgrading is unavailable, you are still able to create Kubernetes clusters of v1.16.

- Upgrading and Ops
Upgrading is available for Kubernetes v1.10 and later major versions. However, TKE focuses on the upgrading and Ops of the latest three Kubernetes major versions. For example, currently the latest version is v1.20, so TKE focuses on guaranteeing the upgrade of v1.18, v1.16 and v1.14, and provides troubleshooting, failure recovery, bugfix and other support for them. Clusters of earlier versions are at a risk of unstable operation and upgrade failures. Please upgrade your Kubernetes clusters in time. For details, see [Upgrading a Cluster](https://intl.cloud.tencent.com/document/product/457/30640).

- Technical support
TKE provides technical support for the latest three Kubernetes major versions. For example, answering questions, online guidance and troubleshooting. For Kubernetes clusters of earlier versions, TKE does not guarantee the quality and effectiveness of the technical support.
