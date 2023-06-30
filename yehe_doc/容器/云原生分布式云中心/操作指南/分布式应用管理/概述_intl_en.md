## Overview

**Distributed Application Management** is based on the open-source multi-cluster application governance project [Clusternet](https://github.com/clusternet/clusternet). It supports expanding cloud-native applications, services and resources to distributed cloud. You can distribute and deploy all native Kubernetes resources (Deployment, StatefulSet, ConfigMap, Secret and others), custom CRDs and Helm Chart applications through **Distributed Application Management**, and manage and operate them in a unified way.

## Application Governance Model

It is based on Clusternet distributed application management model, and adopts loose coupling design. Users only need to associate distribution policies (Subscription) and localization/globalization policies with applications to implement multi-cluster application distribution and management, without the need to change or rewrite existing K8s resource objects. See the figure below:

![clusternet-apps-concepts](https://main.qcloudimg.com/raw/7eca100f5e1f1b7c76ae7a58332ca006.png)

The objects in green are created and configured by users, including K8s resources, distribution policies (Subscription) and localization/globalization policies. The objects in purple are generated automatically by Clusternet, including Base and Description objects, and they are used for internal transfer and observation.

- Resources: Fully compatible with K8s standard resources, such as Deployment, StatefulSet, DaemonSet, as well as custom CRDs, without the need to learn the definition of CRDs of other complex multi-cluster resources.
- Distribution policy (Subscription): It is used to define and manage the distribution of K8s resources to multiple clusters. A corresponding Base object is created in the namespace dedicated for each K8s resource and cluster.
- Localization/Globalization policy: It defines the localization/globalization configurations for distributing K8s resources to different clusters. For details, see [Localization/Globalization Policy](https://intl.cloud.tencent.com/document/product/1144/45548).
- Base & Description: They are auto-generated objects and are used to observe and track the distribution instances of each application resource. Description is an object obtained after a Base object is rendered through localization/globalization configurations, and it is used to describe the configuration of objects deployed in target sub-clusters.


## More

For more information about **Distributed Application Management**, please see the open-source multi-cluster application governance project [Clusternet](https://github.com/clusternet/clusternet).
