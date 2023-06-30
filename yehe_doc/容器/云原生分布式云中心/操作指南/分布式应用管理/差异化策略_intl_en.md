## Overview

You can distribute K8s resources to multiple clusters and manage them in a unified way through **Distributed Application Management**. When you release applications to multiple clusters, you can use **Localization/Globalization policy** to conduct batch configuration, localization configuration, canary update and rollback. For example:

- Provides a unified tag for all distributed resources. For example, "apps.my.company/deployed-by: my-platform".
- Configures cluster information for the resource instances distributed to a cluster. For example, "apps.my.company/running-in: cluster-01".
- Independently adjusts configurations (such as number of replicas and image name) of an application in each cluster. For example, the declared replicas number of a Deployment application named “my-nginx” is 3 for all target clusters, and you can adjust the number to 3, 5 and 7 for cluster-01, cluster-02 and cluster-03 respectively.
- Before you distribute the application to cluster-01, you can adjust some configurations of the application in the cluster. For example, you can inject a Sidecar container.
- In scenarios such as major promotion campaigns, sudden traffic peak and urgent scaling, you can release modifications to specified clusters to shorten the risky scope. You can also roll back the modifications.
- If you define multiple localization/globalization configurations, you can set weight for them by specifying the priority to avoid conflicts.


## Concepts
### Localization/globalization policy
**Distributed Application Management** provides localization policy and globalization policy to manage configurations among clusters.

#### Globalization policy

It defines cluster-scoped configurations, and is used to manage the global configurations among clusters. For example, you can configure same tags for resources in batch. 

#### Localization policy

It defines namespace-scoped configurations, and is used to manage the configurations specific to a cluster. For example, you can modify the number of Deployment replicas in a cluster, upgrade an image and add a Sidecar image.

### Priority

You can manage and configure resources based on the priority specified by the localization policy and globalization policy. The priority can be defined on a scale from 0 to 1,000. A smaller value indicates a lower priority. The default value is 500.
When you perform localization and globalization rendering, the Clusternet applies the policies in the order of Globalization (low priority) > Globalization (high priority) > Localization (low priority) > Localization (high priority).

### Override policy

It provides two policy types, including ApplyLater (default) and ApplyNow. ApplyLater indicates the localization/globalization policy does not take effect to the resources immediately, but will take effect in the next time when the resources are modified or updated. ApplyNow indicates the policy takes effect immediately to the resources.

### Override type

It describes the change of specific resource configurations. Two formats are available, including **MergePatch** and **JSONPatch**.

- Json Patch [JSON Patch, RFC 6902](https://tools.ietf.org/html/rfc6902).
- Merge Patch [JSON Merge Patch, RFC 7386](https://tools.ietf.org/html/rfc7386).

For more information about the comparison between the two formats, see [JSON Patch and JSON Merge Patch](https://erosb.github.io/post/json-patch-vs-merge-patch/).

## Configuration Instructions



#### Method 1: Using YAML

A localization policy can be configured to all application resources that are distributed through **Distributed Application Management**. You can create, update and delete a localization policy.
You can use YAML to configure a localization policy. Click **Create localization policy** or **Update localization policy** to enter the edit page. See the sample below.

```yaml
apiVersion: apps.clusternet.io/v1alpha1
kind: Localization
metadata:
  labels:
    f07d0bec-fac8-4ed1-b4e5-1e2f00111111: Deployment
  name: bb-overrides
  namespace: clusternet-flh9s
spec:
  priority: 300
  feed:
    apiVersion: apps/v1
    kind: Deployment
    name: bb
    namespace: demo
  overridePolicy: ApplyLater
  overrides:
    - name: scale-replicas
      type: JSONPatch
      value: |-
        [
          {
            "path": "/spec/replicas",
            "value": 1,
            "op": "replace"
          }
        ]
```

The **spec.feed** field describes the application resources that are associated with the localization policy. The **spec.overridePolicy** field specifies the type of override policy (ApplyLater or ApplyNow). The **spec.overrides** field defines the localization configurations to be processed. You can select **MergePatch** or **JSONPatch** for it. Then, enter the value of patch in the **value** field.

In this sample, we use JSONPatch format to perform localization configuration for Deployment bb application resource. The **/spec/replicas** is set to 1, and the priority is set to 300. If a policy with higher priority modifies **/spec/replicas** of the application, the modification made based on the current policy will be overridden.

>? The field **spec.overrides.value** follows the **MergePatch** and **JSONPatch** standard. You can use the corresponding tool to generate the patch content. For example, [JSON Patch Builder Online](https://json-patch-builder-online.github.io/).


#### Method 2: Via the console

We will introduce how to configure a localization policy via the console next time.


## Resources

The **localization/globalization policy** is based on the open-source multi-cluster application governance project [Clusternet](https://github.com/clusternet/clusternet). For more information, please go to the open-source project website.
