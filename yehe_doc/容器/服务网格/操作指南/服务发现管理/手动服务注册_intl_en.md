## Overview
With Istio's ServiceEntry, WorkloadGroup, and WorkloadEntry mechanisms, you can add services in clusters that are not provided by TKE, such as traditional VM services and database services, on Tencent Cloud Mesh. However, if you want to manage and observe external services in the mesh in the same way as other automatically discovered K8s services such as applications deployed in VMs, you further need to install sidecars for applications of the external services through the WorkloadGroup and WorkloadEntry mechanisms. Currently, Tencent Cloud Mesh does not support automatic sidecar installation, you need to install sidecars manually. For detailed instructions, see [Virtual Machine Installation](https://istio.io/latest/docs/setup/install/virtual-machine/).

> Concepts
> * ServiceEntry is similar to the concept Service in K8s. After a service is added to a mesh through ServiceEntry, it can be accessed by other automatically discovered services in the mesh based on routing rules.
> * Similar to the concept Deployment in K8s, WorkloadGroup is used to ServiceEntry deployments.
> * Similar to the concept Pod in K8s, WorkloadEntry is used to map a specific entity application.


### Description of Major ServiceEntry Fields

| Name       | Type | Description                                                     |
| --------------- | -------- | ------------------------------------------------------------ |
| spec.hosts      | string   | Host name in the URL of a service. Multiple host names are allowed.        |
| spec.ports      | Port[]   | Port number of the service. Multiple port numbers are allowed.                            |
| spec.resolution | string   | <li>Static: A static endpoint IP address is used as a service instance.<br/><li>DNS: The endpoint IP address of the service is resolved through DNS, which is mostly used for external services. A declared endpoint needs to use the DNS domain name, and the service is resolved to the host domain name if no endpoint is available.<br/><li>NONE: This option is selected when the service does not require IP resolution. |
| spec.location   | string   | Specify whether the service is in the mesh. Some Istio features cannot be used by services outside the mesh. For example, services outside the mesh do not support mTLS. **MESH_EXTERNAL** represents a service outside the mesh, and **MESH_INTERNAL** represents a service in the mesh. |
| spec.endpoints  | String   | Endpoints associated with the service. Multiple endpoints can be entered, but only one endpoint is used at a time.             |

### Description of Major WorkloadGroup Fields

| Name            | Type | Description              |
| ------------------- | -------- | ------------------------------------------------------------ |
| spec.metadata.label        | string   | Label associated with a WorkloadEntry.    |
| spec.template         | string   | Basic information about generation of the WorkloadEntry.              |
| sepc.probe | string   | Parameter settings about health check on the WorkloadEntry.  |

### Description of Major WorkloadEntry Fields

| Name            | Type | Description              |
| ------------------- | -------- | ------------------------------------------------------------ |
| spec.address        | string   | Address of the current endpoint. It is similar to a pod IP address.                |
| spec.labels         | string   | Labels of the current endpoint. They are used to associate with the ServiceEntry.      |
| sepc.serviceAccount | string   | Permission information about a sidecar. This field must be specified when you need to add a sidecar for the endpoint. |

For details about ServiceEntry and WorkloadEntry, see [Service Entry](https://istio.io/latest/docs/reference/config/networking/service-entry/) and [Workload Entry](https://istio.io/latest/docs/reference/config/networking/workload-entry/).



## Manually Registering a Service
Currently, Tencent Cloud Mesh allows you to add a ServiceEntry on the console or by using yaml.

<dx-tabs>
::: YAML Configuration Example
#### ServiceEntry

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: ServiceEntry
metadata:
  name: external-svc-https
spec:
  hosts:
  - api.dropboxapi.com
  - www.googleapis.com
  - api.facebook.com
  location: MESH_EXTERNAL
  ports:
  - number: 443
    name: https
    protocol: TLS
  resolution: DNS
```

### WorkloadGroup

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: WorkloadGroup
metadata:
  name: reviews
  namespace: bookinfo
spec:
  metadata:
    labels:
      app.kubernetes.io/name: reviews
      app.kubernetes.io/version: "1.3.4"
  template:
    ports:
      grpc: 3550
      http: 8080
    serviceAccount: default
  probe:
    initialDelaySeconds: 5
    timeoutSeconds: 3
    periodSeconds: 4
    successThreshold: 3
    failureThreshold: 3
    httpGet:
     path: /foo/bar
     host: 127.0.0.1
     port: 3100
     scheme: HTTPS
     httpHeaders:
     - name: Lit-Header
       value: Im-The-Best

```

#### WorkloadEntry

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: WorkloadEntry
metadata:
  name: details-svc
spec:
  serviceAccount: details-legacy
  address: 2.2.2.2
  labels:
    app: details-legacy
    instance-id: vm1
```

:::
::: Console Configuration Example

1. Log in to the [Tencent Cloud Mesh console](https://console.cloud.tencent.com/tke2/mesh).
2. Click **ID/Name** to pop up the mesh details page.
3. Click **Service** > **Create**, and specify service basic information. This operation can register a non-containerized third-party service with Tencent Cloud Mesh. 
![](https://qcloudimg.tencent-cloud.cn/raw/0681866ebb6dffa798e7700fe86d2283.png)



:::
</dx-tabs>



