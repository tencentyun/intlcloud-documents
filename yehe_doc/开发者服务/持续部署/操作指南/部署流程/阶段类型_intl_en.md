This document describes the stage types of deployment pipelines in CODING Continuous Deployment (CODING-CD).

## Prerequisites

You must activate the CODING DevOps service for your Tencent Cloud account before you can use CODING Project Management (CODING-PM). 

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click **Use Now** to go to CODING.
2. On the Workspace homepage, click <img src ="https://main.qcloudimg.com/raw/12230547b45d5eae85ad1c4fa86fba68.png" style ="margin:0" data-nonescope="true"> on the left to go to the CODING-CD Console.

## General Types

When you edit a deployment pipeline, you can select a stage type for each step.

![](https://qcloudimg.tencent-cloud.cn/raw/2a543934edb4c8aaeee500dc0bc5466f.png)

### Prerequisite check

Check such prerequisites as the cluster size or status of a specific stage before executing the next step.

### Custom variables

Add custom variables (i.e. `key/value` pairs), which can be referenced by downstream stages.

![](https://qcloudimg.tencent-cloud.cn/raw/d322e75164483e81aaa9bb50ce224f63.png)

<!--#### Search for images in clusters

Search for images in the deployed clusters. Make sure that images conforming to the search conditions exist in the specified clusters and service groups. Otherwise, exceptions may occur.

Description of configuration options:

- Select Kubernetes for Cloud Service (Provider)

| Field           | Required? | Description                             |
| ------------ | ---- | ------------------------------ |
| Cloud Service          | Yes    | Cloud service type. Kubernetes and Tencent Cloud are supported.   |
| Cloud Account          | Yes    | Cloud account that manages resource objects                     |
| Namespaces   | Yes    | Namespaces where the images belong                      |
| Clusters           | Yes    | Clusters where the images belong                        |
| Service Groups          | Yes    | Specifies matching rules for service groups                  |
| Only select enabled service groups | No    | If this option is checked, disabled service groups will not be matched.               |
| Image Matching Rules       | No    | Regular expressions used to match images. If this field is left empty, all the images in the target service group are matched. |

![](https://help-assets.codehub.cn/enterprise/20200414141651.png)

- Select **Tencent Cloud** for Cloud Service (Provider)

| Field           | Required? | Description                          |
| ------------ | ---- | --------------------------- |
| Cloud Service          | Yes    | Cloud service type. Kubernetes and Tencent Cloud are supported. |
| Cloud Account          | Yes    | Cloud account that manages resource objects                  |
| Regions           | Yes    | Regions where the images belong                        |
| Clusters           | Yes    | Clusters where the images belong                     |
| Service Groups          | Yes    | Specifies matching rules for service groups               |
| Only select enabled service groups | No    | If this option is checked, disabled service groups will not be matched.           |
-->

### Manual confirmation

Wait for manual confirmation before executing the next step. To facilitate manual confirmation, you can add instructions, or offer input options to users for selection. These input options determine the execution behaviors in the downstream stage. For example, the `prerequisite check` can be used to ensure that a stage will be executed only when specific conditions are met.

### Deployment pipeline

Execute other deployment pipelines as sub-pipelines. You can execute the deployment pipeline of this application, as well as the pipelines of other applications that you have access to. You can select whether to wait for the execution results of the sub-pipelines before the stage execution ends. If you select to wait, the final execution status of the sub-pipelines is deemed as the status of this stage. Otherwise, when the execution of the sub-pipelines starts, the status of this stage will be flagged as "successful".

Description of configuration options:

| Field       | Required? | Description                                                              |
| -------- | ---- | --------------------------------------------------------------- |
| Application       | Yes    | Lists all the applications that you have access to                                                   |
| Deployment Pipeline     | Yes    | Lists all the deployment pipelines under the application                                                    |
| Wait for execution result | No    | If you select to wait, the final execution status of the sub-pipelines is deemed as the status of this stage. Otherwise, when the execution of the sub-pipelines starts, the status of this stage will be flagged as "successful". |

![](https://qcloudimg.tencent-cloud.cn/raw/2e0edd7453c3c8fb24265db5de4a1c14.png)

## Wait

Wait for a certain period of time before resuming execution. During the pipeline execution, you can manually reduce the waiting time or directly skip waiting. The waiting time can be an expression.

![](https://qcloudimg.tencent-cloud.cn/raw/a48862432c49725b6351cf4da3cf775f.png)

## Webhook

Calling external system APIs can be a stage in a deployment pipeline.

To call a specified webhook, the target URL and HTTP method can be used together with a custom `header` and the payload in JSON format. By default, if calling a webhook returns `2XX` or `3XX`, the stage execution has succeeded; if it returns `4XX` or `5XX`, the execution has failed. The final status of the webhook's URL and payload will be displayed in the pipeline execution details.

Pipeline expressions can be used in the URL field and payload. When the stage execution is complete, the payload content will be included in the `Webhook` object of the stage context, so that the payload can be referenced in the subsequent pipeline expressions. For example, you can use the following expression to obtain the final status of the webhook execution:
<dx-codeblock>
:::  text
    ${#stage("My Webhook Stage")["context"]["webhook"]["statusCode"]}
:::
</dx-codeblock>

![](https://qcloudimg.tencent-cloud.cn/raw/f092879ffe8299222d0d3f1ee56304bd.png)

## Disable Cluster

If you disable a cluster, the cluster keeps running but cannot process traffic. If needed, you can specify a certain number of service groups to keep them running, and disable the remaining ones.

Description of configuration options:

- Select Kubernetes for Cloud Service (Provider)
<table>
<tr>
<th>Field</th>
<th>Required?</th>
<th>Description</th>
</tr>
<tr>
<td >Cloud Service</td>
<td>Yes</td>
<td>Cloud service type. Kubernetes and Tencent Cloud are supported.</td>
</tr>
<tr>
<td >Cloud Account</td>
<td>Yes</td>
<td>Cloud account that manages resource objects</td>
</tr>
<tr>
<td >Namespaces</td>
<td>Yes</td>
<td>Namespaces where the service groups belong</td>
</tr>
<tr>
<td >Clusters</td>
<td>Yes</td>
<td>Clusters where the service groups belong</td>
</tr>
<tr>
<td >Disable Options</td>
<td>Yes</td>
<td>Specifies the rules for disabling options</td>
</tr>
</table>
- Select Kubernetes for Cloud Service (Provider)
<table>
<tr>
<th>Field</th>
<th>Required?</th>
<th>Description</th>
</tr>
<tr>
<td >Cloud Service</td>
<td>Yes</td>
<td>Cloud service type. Kubernetes and Tencent Cloud are supported.</td>
</tr>
<tr>
<td >Cloud Account</td>
<td>Yes</td>
<td>Cloud account that manages resource objects</td>
</tr>
<tr>
<td >Namespaces</td>
<td>Yes</td>
<td>Namespaces where the service groups belong</td>
</tr>
<tr>
<td >Clusters</td>
<td>Yes</td>
<td>Clusters where the service groups belong</td>
</tr>
<tr>
<td >Disable Options</td>
<td>Yes</td>
<td>Specifies the rules for disabling options</td>
</tr>
<tr>
<td >Health Check</td>
<td>Yes</td>
<td>Only refers to the health check that Tencent Cloud provides when you perform this task</td>
</tr>
</table>


## Cluster Scale-Down

You can select whether to scale down active service groups (i.e. those operating normally). In addition, you can specify a certain number of service groups to maintain their size, and scale down the remaining ones.

- Select Kubernetes for Cloud Service (Provider)
<table>
<tr>
<th>Field</th>
<th>Required?</th>
<th>Description</th>
</tr>
<tr>
<td >Cloud Service</td>
<td>Yes</td>
<td>Cloud service type. Kubernetes and Tencent Cloud are supported.</td>
</tr>
<tr>
<td >Cloud Account</td>
<td>Yes</td>
<td>Cloud account that manages resource objects</td>
</tr>
<tr>
<td >Namespaces</td>
<td>Yes</td>
<td>Namespaces where the service groups belong</td>
</tr>
<tr>
<td >Clusters</td>
<td>Yes</td>
<td>Clusters where the service groups belong</td>
</tr>
<tr>
<td >Scale-Down Options</td>
<td>Yes</td>
<td>Specifies scale-down options</td>
</tr>
</table>
- Select Tencent Cloud for Cloud Service (Provider)
<table>
<tr>
<th>Field</th>
<th>Required?</th>
<th>Description</th>
</tr>
<tr>
<td >Cloud Service</td>
<td>Yes</td>
<td>Cloud service type. Kubernetes and Tencent Cloud are supported.</td>
</tr>
<tr>
<td >Cloud Account</td>
<td>Yes</td>
<td>Cloud account that manages resource objects</td>
</tr>
<tr>
<td >Regions</td>
<td>Yes</td>
<td>Regions where the service groups belong</td>
</tr>
<tr>
<td >Clusters</td>
<td>Yes</td>
<td>Clusters where the service groups belong</td>
</tr>
<tr>
<td >Health Check</td>
<td>Yes</td>
<td>Only refers to the health check that Tencent Cloud provides when you perform this task</td>
</tr>
</table>

[](id:start)
## Enable Service Group

If you enable a service group that has been disabled, it will process request traffic again. The configuration of the load balancer determines the routing rules between old and new service groups. When a service group is enabled, the scaling strategy is also enabled.

Description of configuration options:

- Select Kubernetes for Cloud Service (Provider)
<table>
<tr>
<th>Field</th>
<th>Required?</th>
<th>Description</th>
</tr>
<tr>
<td >Cloud Service</td>
<td>Yes</td>
<td>Cloud service type. Kubernetes and Tencent Cloud are supported.</td>
</tr>
<tr>
<td >Cloud Account</td>
<td>Yes</td>
<td>Cloud account that manages resource objects</td>
</tr>
<tr>
<td >Namespaces</td>
<td>Yes</td>
<td>Namespaces where the service groups belong</td>
</tr>
<tr>
<td >Clusters</td>
<td>Yes</td>
<td>Clusters where the service groups belong</td>
</tr>
<tr>
<td >Target Service Groups</td>
<td>Yes</td>
<td>Specifies matching rules for service groups</td>
</tr>
</table>
- Select Tencent Cloud for Cloud Service (Provider)
<table>
<tr>
<th>Field</th>
<th>Required?</th>
<th>Description</th>
</tr>
<tr>
<td >Cloud Service</td>
<td>Yes</td>
<td>Cloud service type. Kubernetes and Tencent Cloud are supported.</td>
</tr>
<tr>
<td >Cloud Account</td>
<td>Yes</td>
<td>Cloud account that manages resource objects</td>
</tr>
<tr>
<td >Regions</td>
<td>Yes</td>
<td>Regions where the service groups belong</td>
</tr>
<tr>
<td >Clusters</td>
<td>Yes</td>
<td>Clusters where the service groups belong</td>
</tr>
<tr>
<td >Target Service Groups</td>
<td>Yes</td>
<td>Specifies matching rules for service groups</td>
</tr>
<tr>
<td >Health Check</td>
<td>Yes</td>
<td>Only refers to the health check that Tencent Cloud provides when you perform this task</td>
</tr>
</table>


## Disable Service Group

If you disable a service group, the service group keeps running but cannot process traffic. In addition, any scaling operations on the disabled service groups will be disabled. By disabling service groups, you can easily switch traffic between old and new service groups. Before a stage is initiated, you must specify the newest, oldest, or newer service groups to be disabled.

>? For configuration options, refer to [Enable Service Group](#start).

## Destroy Service Group

You can destroy the service groups and relevant resources of a specified cluster. Before a stage is initiated, you must specify the newest, oldest, or newer service groups to be destroyed.

Description of configuration options:

- Select Kubernetes for Cloud Service (Provider)
<table>
<tr>
<th>Field</th>
<th>Required?</th>
<th>Description</th>
</tr>
<tr>
<td >Cloud Service</td>
<td>Yes</td>
<td>Cloud service type. Kubernetes and Tencent Cloud are supported.</td>
</tr>
<tr>
<td >Cloud Account</td>
<td>Yes</td>
<td>Cloud account that manages resource objects</td>
</tr>
<tr>
<td >Namespaces</td>
<td>Yes</td>
<td>Namespaces where the service groups belong</td>
</tr>
<tr>
<td >Clusters</td>
<td>Yes</td>
<td>Clusters where the service groups belong</td>
</tr>
<tr>
<td >Target Service Groups</td>
<td>Yes</td>
<td>Specifies matching rules for service groups</td>
</tr>
</table>
- Select Tencent Cloud for Cloud Service (Provider)
<table>
<tr>
<th>Field</th>
<th>Required?</th>
<th>Description</th>
</tr>
<tr>
<td >Cloud Service</td>
<td>Yes</td>
<td>Cloud service type. Kubernetes and Tencent Cloud are supported.</td>
</tr>
<tr>
<td >Cloud Account</td>
<td>Yes</td>
<td>Cloud account that manages resource objects</td>
</tr>
<tr>
<td >Regions</td>
<td>Yes</td>
<td>Regions where the service groups belong</td>
</tr>
<tr>
<td >Clusters</td>
<td>Yes</td>
<td>Clusters where the service groups belong</td>
</tr>
<tr>
<td >Target Service Groups</td>
<td>Yes</td>
<td>Specifies matching rules for service groups</td>
</tr>
</table>

## Adjust Service Group Size

Adjusts the size of a service group in proportion to its current size or by a specified amount. The supported adjustment strategies are as follows:

- Scale-up: Increases the size of the target service group
- Scale-down: Decreases the size of the target service group
- Scale up to the relatively largest size: Scales up the target service group to match the size of the largest service group in the current cluster
- Adjust to a specific size: Adjusts the size of the target service group to a specific value

## Tencent Cloud Type

## Bake

Bakes cloud server images from the specified software package. Baking refers to the process of creating cloud server images. The CODING-CD Console abstracts the Baker stage by using HashiCorp's Packer, and offers a default Packer template and basic cloud server images to help you get started.

Note that the bake process will be skipped if Spinnaker does not detect any new bake operation. The console generates a unique key for each bake operation according to the parameters of the Bake stage (the base OS, versioned software package, and so on). Any changes to the software package or the parameters will trigger a new bake operation. If you need to change the default behaviors and rebake images every time the deployment pipeline is executed, select `Rebake` in the stage configuration. For more information, see [Packer by HashiCorp](https://www.packer.io/intro).

## Deploy

Deploys the images baked in advance according to the specified deployment strategies. CODING-CD offers partly built-in deployment strategies such as red/black (blue/green) deployment and Highlander deployment. You can also adopt non-invasive deployment methods for the existing service groups, or create custom deployment strategies.

## Roll Back Cluster

Rolls back the instances of one or more regions in a cluster.

Description of configuration options:

| Field   | Required? | Description                   |
| ---- | ---- | -------------------- |
| Cloud Account  | Yes    | Tencent Cloud Account                |
| Regions   | Yes    | Regions where the clusters belong              |
| Clusters   | Yes    | Specifies the clusters to be rolled back            |
| Health Check | Yes    | Only refers to the health check that Tencent Cloud provides when you perform this task |

## Clone Service Group

Clones all the fields of the existing service group to a new service group (by using images, containers, and so on). When you create a new service group, you can overwrite any field of the cloned service group.

## Shrink Cluster

Retains a certain number of the newest or largest service groups, and deletes the remaining ones. You can select whether to delete active service groups (i.e. those operating normally) that do not meet the specified conditions.

## Modify Scaling Process

Pauses or resumes scaling operations.

## Kubernetes Type

## Bake (Manifest)

Bakes the resource list by using such template renderers as Helm.

## Deploy (Manifest)

Includes two major steps:

- Specifies the manifest to be deployed
- Specifies the artifacts to be overwritten in the manifest (such as `Docker image`)

**Configure manifest**

You can specify a manifest in the following two ways:

- Static: Specify it directly in the deployment pipeline
- Dynamic: Use the bound artifact during execution

Either way, select the `Deploy (Manifest)` stage in advance.

**Configure static manifest**

If you know the manifest that corresponds to the resources to be deployed beforehand (even though you do not know the artifact version), you can directly provide the plaintext content of the manifest in the configuration of the `Deploy (Manifest)` stage.

>? When you select the `Text` type, you can directly edit the YAML file content in the text field.

If a JSON-defined deployment pipeline is used, the corresponding content will be as follows:

```json
    {
      "name": "Deploy my manifest",   // human-readable name
      "type": "deployManifest",       // tells orchestration engine what to run
      "account": "nudge",             // account (k8s cluster) to deploy to
      "cloudProvider": "kubernetes",
      "source": "text",
      "manifest": {
                                      // manifest contents go here
      }
    }
```

**Configure dynamic manifest**

If artifacts are not stored in the pipeline repository, or multiple artifacts need to be deployed at a stage, you can configure the manifest by binding artifacts. CODING-CD artifacts allow you to reference any remote deployable resources. The artifacts referenced at the `Deploy (Manifest)` stage must be the text files that contain the manifest definition, which may exist in GitHub repositories or GCS. For more information, see [Deployment Pipeline Settings](https://www.spinnaker.io/setup/install/storage/).

If you have declared `expected artifacts` at the upstream stages, you can reference them at the `Deploy (Manifest)` stage:

>? After you select `Artifact` for the Manifest Source field, you can deploy the artifacts offered by upstream stages. Make sure that your cloud account has permission to download artifacts.

Upstream stages may match multiple artifacts. For example, if you configure the regular expression `.*\yml` to use all `yml` files as artifacts, then all matching `yml` files will be deployed when the `Deploy (Manifest)` stage is executed.

**Overwrite artifacts**

Normally, when you deploy and update Kubernetes resources, most of the changes involve a `flag` in the Docker image or ConfigMap. Therefore, CODING-CD provides excellent adaptability to these resource type changes.

- Docker image
- Kubernetes ConfigMap
- Kubernetes Secret

If these resource objects exist at an upstream stage of a deployment pipeline, CODING-CD will try to automatically inject them into the manifest file being deployed.

For example: The pipeline execution is triggered by the Docker image registry trigger that carries the image `gcr.io/my-project/my-image`, whose digest value is `sha256:c81e41ef5e...`. In the pipeline, you configure a deployment stage with the following manifest content:

```yaml
    # ... rest of manifest
      containers:
      - name: my-container
        image: gcr.io/my-project/my-image
    # rest of manifest ...
```

Because the pipeline is triggered by `changes in the content of the Docker image`, the pipeline orchestration engine will distribute the Docker image artifact along with the manifest at the deployment stage to the `Clouddriver` component for processing. The content of the manifest that is eventually deployed will be as follows:

```yaml
    # ... rest of manifest
      containers:
      - name: my-container
        image: gcr.io/my-project/my-image@:sha256:c81e41ef5e...
    # rest of manifest ...
```

To ensure that proper artifacts are obtained at the deployment stage, you can forcibly bind all the required artifacts to the stage. If the binding fails, the stage will fail to boot. The following configuration indicates that the Docker image `gcr.io/my-project/my-image` must be bound to the manifest. Otherwise, the stage execution will fail:

## Enable (Manifest)

Enables Kubernetes objects.

Description of configuration options:

- Select `Statically Specify Target` for `Selector`
<table>
<tr>
<th>Field</th>
<th>Required?</th>
<th>Description</th>
</tr>
<tr>
<td >Cloud Account</td>
<td>Yes</td>
<td>Cloud account that manages resource objects</td>
</tr>
<tr>
<td >Namespace</td>
<td>Yes</td>
<td>Namespace where the resource objects belong</td>
</tr>
<tr>
<td >Selector</td>
<td>Yes</td>
<td>Statically specifies the target resources to be deleted by name</td>
</tr>
<tr>
<td >Kind</td>
<td>Yes</td>
<td>Resource object type</td>
</tr>
<tr>
<td >Name</td>
<td>Yes</td>
<td>Resource object name (such as ReplicaSet resources <code>nginx-deployment-5dfd77bbf9</code>)</td>
</tr>
</table>
- Select `Dynamically Select Target` for `Selector`
<table>
<tr>
<th>Field</th>
<th>Required?</th>
<th>Description</th>
</tr>
<tr>
<td >Cloud Account</td>
<td>Yes</td>
<td>Cloud account that manages resource objects</td>
</tr>
<tr>
<td >Namespace</td>
<td>Yes</td>
<td>Namespace where the resource objects belong</td>
</tr>
<tr>
<td >Selector</td>
<td>Yes</td>
<td>Statically specifies the target resources to be deleted by name</td>
</tr>
<tr>
<td >Kind</td>
<td>Yes</td>
<td>Resource object type</td>
</tr>
<tr>
<td >Clusters</td>
<td>Yes</td>
<td>Resource object name (such as ReplicaSet resources <code>nginx-deployment-5dfd77bbf9</code>)</td>
</tr>
<tr>
<td >Target</td>
<td>Yes</td>
<td>Selects matching rules for resource objects</td>
</tr>
</table>


## Delete (Manifest)

Deletes the Kubernetes objects that are created through the resource list.

Description of configuration options:

- Select `Statically Specify Target` for `Selector`
<table>
<tr>
<th>Field</th>
<th>Required?</th>
<th>Description</th>
</tr>
<tr>
<td >Cloud Account</td>
<td>Yes</td>
<td>Cloud account that manages resource objects</td>
</tr>
<tr>
<td >Namespace</td>
<td>Yes</td>
<td>Namespace where the resource objects belong</td>
</tr>
<tr>
<td >Selector</td>
<td>Yes</td>
<td>Statically specifies the target resources to be deleted by name</td>
</tr>
<tr>
<td >Kind</td>
<td>Yes</td>
<td>Resource object type</td>
</tr>
<tr>
<td >Name</td>
<td>Yes</td>
<td>Resource object name (such as ReplicaSet resources <code>nginx-deployment-5dfd77bbf9</code>)</td>
</tr>
</table>
- Select `Dynamically Select Target` for `Selector`
<table>
<tr>
<th>Field</th>
<th>Required?</th>
<th>Description</th>
</tr>
<tr>
<td >Cloud Account</td>
<td>Yes</td>
<td>Cloud account that manages resource objects</td>
</tr>
<tr>
<td >Namespace</td>
<td>Yes</td>
<td>Namespace where the resource objects belong</td>
</tr>
<tr>
<td >Selector</td>
<td>Yes</td>
<td>Dynamically selects resource objects by cluster and <code>target</code> field</td>
</tr>
<tr>
<td >Kind</td>
<td>Yes</td>
<td>Resource object type</td>
</tr>
<tr>
<td >Cluster</td>
<td>Yes</td>
<td>Cluster where the resource objects belong</td>
</tr>
<tr>
<td >Target</td>
<td>Yes</td>
<td>Selects matching rules for resource objects</td>
</tr>
</table>
- Select `Match Target by Tag` for `Selector`
<table>
<tr>
<th>Field</th>
<th>Required?</th>
<th>Description</th>
</tr>
<tr>
<td >Cloud Account</td>
<td>Yes</td>
<td>Cloud account that manages resource objects</td>
</tr>
<tr>
<td >Namespace</td>
<td>Yes</td>
<td>Namespace where the resource objects belong</td>
</tr>
<tr>
<td >Selector</td>
<td>Yes</td>
<td>Matches resource objects according to the specified tag rules</td>
</tr>
<tr>
<td >Kind</td>
<td>Yes</td>
<td>Resource object type</td>
</tr>
<tr>
<td >Labels</td>
<td>Yes</td>
<td>Matches all the resource objects of the specified types if no rules are set</td>
</tr>
</table>

Description of setting options:
<table>
<tr>
<th>Field</th>
<th>Required?</th>
<th>Description</th>
</tr>
<tr>
<td >Delete Cascade</td>
<td>No</td>
<td>If this field is checked, all the resource objects managed by this resource object (for example, all the pods managed by a ReplicaSet) will be deleted. If this field is not checked, orphan resources may be generated.</td>
</tr>
<tr>
<td >Grace Period</td>
<td>No</td>
<td>(Optional) Specifies a termination time for the resource object, which will overwrite the time set in the manifest.</td>
</tr>
</table>
