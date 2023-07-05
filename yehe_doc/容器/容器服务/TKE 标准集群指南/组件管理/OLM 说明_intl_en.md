
## Overview

### Add-on description

Operator Lifecycle Manager (OLM) is part of the Operator Framework, which helps users install, update, and manage the lifecycle of Operators. Meanwhile, OLM itself is installed and deployed in the form of Operators, so the way it works is to manage Operators with Operators. The declarative automatic management capabilities provided for Operators are fully in line with the design concept of Kubernetes interaction.

## How It Works

OLM is composed of two Operators: the OLM Operator and the Catalog Operator. Each of these Operators is responsible for managing the custom resource definitions (CRDs) that are the basis for the OLM framework:

| Resource | Short Name | Owner | Description |
| --------------------- | ------ | ------------- | ------------------------------------------------------------ |
| ClusterServiceVersion | csv | OLM | Application metadata: application name, version, icon, required resources, installation, and so on. |
| InstallPlan | ip | Catalog | Calculated list of resources to be created to automatically install or upgrade a CSV. |
| CatalogSource | catsrc | Catalog | A repository of CSVs, CRDs, and packages that define an application. |
| Subscription | sub | Catalog | Used to keep CSVs up to date by tracking a channel in a package. |
| OperatorGroup | og | OLM | Configures multi-tenancy during the Operators installation. An Operator group selects target namespaces in which to specify the required resource configurations such as RBAC for Operators creation. |

- The OLM Operator is responsible for deploying the Deployment, Serviceaccount, and RBAC-related roles and role bindings required for the Operator installation. The Catalog Operator is responsible for creating CRDs, CSVs, and the required resources.
- The OLM Operator works based on the ClusterServiceVersion. Once the dependent resources declared in the CSV are registered in the target cluster, the OLM Operator is responsible for installing the application instances corresponding to those resources.
- The Catalog Operator is responsible for resolving the dependent resources declared in the CSV and updating the version of the CSV by listening to the version of the channels for the installation package in the Catalog.


### Kubernetes objects deployed in a cluster

| Kubernetes Object | Type | Required Resource | Namespace |
| ----------------------------------------------- | ------------------------ | ----------------------------------------- | -------------------------- |
| catalogsources.operators.coreos.com | CustomResourceDefinition | - | - |
| clusterserviceversions.operators.coreos.com | CustomResourceDefinition | - | - |
| installplans.operators.coreos.com | CustomResourceDefinition | - | - |
| operatorgroups.operators.coreos.com | CustomResourceDefinition | - | - |
| operators.operators.coreos.com | CustomResourceDefinition | - | - |
| subscriptions.operators.coreos.com | CustomResourceDefinition | - | - |
| olm-operator | Deployment | cpu request: 10m<br>memory request: 160Mi | operator-lifecycle-manager |
| catalog-operator | Deployment | cpu request: 10m<br>memory request: 80Mi | operator-lifecycle-manager |
| system:controller:operator-lifecycle-manager | ClusterRole | - | - |
| aggregate-olm-view | ClusterRole | - | - |
| aggregate-olm-edit | ClusterRole | - | - |
| olm-operator-binding-operator-lifecycle-manager | ClusterRoleBinding | - | - |
| olm-operator | ServiceAccount | - | operator-lifecycle-manager |
| operators | Namespace | - | - |
| operator-lifecycle-manager | Namespace | - | - |
| packageserver | ClusterServiceVersion | - | operator-lifecycle-manager |
| olm-operators | OperatorGroup | - | operator-lifecycle-manager |
| global-operators | OperatorGroup | - | operators |

## Use Cases

OLM helps users install, update, and manage the lifecycle of all Operators.

## Risk Control

To prevent user’s business from being affected, after the OLM add-on is uninstalled, the Operator deployed through OLM and the related CRDs will not be cleaned up. These CRDs can be removed manually.

## Limits

>?If you create a cluster of version 1.12.4 or later. You can use the cluster directly without any parameter changes.


- This add-on is supported only by Kubernetes 1.12 or later versions.
- The launch parameters of kube-apiserver must be set as follows: `--feature-gates=CustomResourceSubresources=true`.



## Directions


1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On the “**Cluster Management** page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on Management** to go to the **Add-on List** page.
4. On the "Add-on List" page, click **Create**, On the "Create Add-on" page that appears, select **OLM**.
5. Click **Done**.
