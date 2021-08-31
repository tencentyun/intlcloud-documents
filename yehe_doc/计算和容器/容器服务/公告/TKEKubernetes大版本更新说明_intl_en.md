
## 1.18 changes since 1.16
### Major updates
#### The cloud provider tag feature goes to the GA stage
The following table lists the deprecated tags and new tags:

| Deprecated Tag | New Tag |
|:---------|:---------|
| `beta.kubernetes.io/instance-type` | `node.kubernetes.io/instance-type` |
| `failure-domain.beta.kubernetes.io/region` |`topology.kubernetes.io/region` |
| `failure-domain.beta.kubernetes.io/zone` | `topology.kubernetes.io/zone` |



#### The Volume Snapshot feature goes to the Beta stage
VolumeSnapshotDataSource is enabled by default. For more information, see [Kubernetes 1.17 Feature: Kubernetes Volume Snapshot Moves to Beta](https://kubernetes.io/blog/2019/12/09/kubernetes-1-17-feature-cis-volume-snapshot-beta/).

#### CSI Migration enters the Beta stage
CSI Migration is enabled by default. For more information, see [Kubernetes 1.17 Feature: Kubernetes In-Tree to CSI Volume Migration Moves to Beta](https://kubernetes.io/blog/2019/12/09/kubernetes-1-17-feature-csi-migration-beta/).

#### Kubernetes Topology Manager moves to Beta stage
Topology Manager enters the Beta stage in Kubernetes 1.18 and enables the CPU to implement NUMA alignment with other devices (such as SR-IOV-VF) so that workloads can support low-latency scenarios.
Before Topology Manager was introduced, the CPU and device manager could only make resource allocation decisions independently. As a result, a multi-socket CPU system might fail to allocate resources appropriately, affecting the performance of latency-sensitive applications.

#### Server-side Apply enters the Beta 2 stage
Server-side Apply entered the Beta stage in Kubernetes 1.16. In Kubernetes 1.18, its second beta version (ServerSideApply) was introduced. This version can record and manage changes to all new Kubernetes object fields, ensuring that users are informed of resource statuses.

#### IngressClass resources
`IngressClass` describes an Ingress controller type in a Kubernetes cluster. The `ingressClassName` field is added for `Ingress` resources to set the name of the controller that uses `IngressClass`. This replaced the deprecated `kubernetes.io/ingress.class` annotation.

### Other updates
- Node Local DNSCache enters the GA stage.
- IPv6 enters the Beta stage.
- `kubectl debug` supports the Alpha feature.
- `Windows CSI support` supports the Alpha feature.
- `ImmutableEphemeralVolumes` supports the Alpha feature (which supports non-changeable ConfigMap and Secret and does not refresh the corresponding volume).
- The following features enter the GA stage:
  - `ScheduleDaemonSetPods`
  - `TaintNodesByCondition`
  - `WatchBookmark`
  - `NodeLease`
  - `CSINodeInfo`
  - `VolumeSubpathEnvExpansion`
  - `AttachVolumeLimit`
  - `ResourceQuotaScopeSelectors` 
  - `VolumePVCDataSource`
  - `TaintBasedEvictions`
  - `BlockVolume`, `CSIBlockVolume`
  - `Windows RunAsUserName`
- The following features enter the Beta stage:
  - `EndpointSlices`: disabled by default
  - `CSIMigrationAWS`: disabled by default
  - `StartupProbe`
  - `EvenPodsSpread`

### Deprecations and removals
#### Removed features
The following features, which were enabled by default and could not be configured, were removed:
- `GCERegionalPersistentDisk`
- `EnableAggregatedDiscoveryTimeout`
- `PersistentLocalVolumes`
- `CustomResourceValidation`
- `CustomResourceSubresources`
- `CustomResourceWebhookConversion`
- `CustomResourcePublishOpenAPI`
- `CustomResourceDefaulting`

#### Other removals
The following built-in cluster roles were removed:
 - `system:csi-external-provisioner` 
 - `system:csi-external-attacher`

#### Deprecated features and parameters
- The default service IP CIDR block (`10.0.0.0/24`) was deprecated. You must set the service IP CIDR block by using the `--service-cluster-ip-range` parameter of kube-apiserver, 
- The `rbac.authorization.k8s.io/v1alpha1` and `rbac.authorization.k8s.io/v1beta1` API groups were deprecated, and we plan to remove them in Kubernetes 1.20. Therefore, migrate your resources to `rbac.authorization.k8s.io/v1`.
- The `CSINodeInfo` feature, which has entered the GA stage and was enabled by default, was deprecated.

### Parameters and other changes
#### kube-apiserver
- `--encryption-provider-config`: if `cacheSize: 0` is specified in the configuration file, versions earlier than 1.18 are configured to cache 1,000 Keys automatically, while version 1.18 will report a configuration verification error. You can disable the cache by setting `cacheSize` to a negative value.
- `--feature-gates`: the following features are enabled by default and no longer support CLI-based configuration.
  - `PodPriority`
  - `TaintNodesByCondition`
  - `ResourceQuotaScopeSelectors` 
  - `ScheduleDaemonSetPods` 
- The following resource versions (group versions) are no longer supported:
    - `apps/v1beta1` and `apps/v1beta2`. Use `apps/v1` instead.
    - Under `extensions/v1beta1`:
     -  `daemonsets`, `deployments`, and `replicasets`. Use `apps/v1` instead.
     - `networkpolicies`. Use `networking.k8s.io/v1` instead.
     - `podsecuritypolicies`. Use `policy/v1beta1` instead.

#### kubelet
- `--enable-cadvisor-endpoints`: this parameter is disabled by default. For access to the cAdvisor v1 JSON API, you must enable this parameter.
- The `--redirect-container-streaming` parameter was deprecated and will be removed in later versions. Kubernetes 1.18 supports only the default action (kubelet proxy for streaming requests). If `--redirect-container-streaming=true` is set, it must be removed.
- The `/metrics/resource/v1alpha1` metrics endpoint was deprecated. Use `/metrics/resource` instead.

#### kube-proxy
- The following parameters were deprecated:
    - `--healthz-port` was deprecated. Use `--healthz-bind-address` instead.
    - `--metrics-port` was deprecated. Use `--metrics-bind-address` instead.
- The `EndpointSliceProxying` feature switch (disabled by default) was added to control whether to enable EndpointSlices in kube-proxy. The `EndpointSlice` feature switch does not affect the actions of kube-proxy any more.
- Added the following timeout settings for ipvs connection configuration:
  - `--ipvs-tcp-timeout`
  - `--ipvs-tcpfin-timeout`
  - `--ipvs-udp-timeout`
- The iptables mode added IPv4/IPv6 dual-protocol stack support.

#### kube-scheduler
- Deprecated the `scheduling_duration_seconds` metric:
 - Deprecated `scheduling_algorithm_predicate_evaluation_seconds`. Use `framework_extension_point_duration_seconds[extension_point="Filter"]` instead.
 - Deprecated `scheduling_algorithm_priority_evaluation_seconds`. Use `framework_extension_point_duration_seconds[extension_point="Score"]` instead.
- Deprecated `AlwaysCheckAllPredicates` in the scheduler policy API.

#### -enable-profiling
For the alignment of `kube-apiserver`, `kube-controller-manager`, and `kube-scheduler`, [profiling is enabled by default](https://github.com/kubernetes/kubernetes/pull/88663). To disable profiling, specify `--enable-profiling=false`.

#### kubectl
- Removed the deprecated `--include-uninitialized` parameter.
- `kubectl` and `k8s.io/client-go` no longer use http://localhost:8080 as the default apiserver address.
- `kubectl run` supports pod creation and no longer supports using the deprecated generator to create other types of resources.
- Removed the deprecated `kubectl rolling-update` command. Use the `rollout` command instead.
- `–dry-run` supports three parameter values: `client`, `server`, and `none`.
- `–dry-run=server` supports the following commands: `apply`, `patch`, `create`, `run`, `annotate`, `label`, `set`, `autoscale`, `drain`, `rollout undo`, and `expose`.
- Added the `kubectl alpha debug` command, which can be used for [debugging and troubleshooting on ephemeral containers in pods](https://github.com/kubernetes/kubernetes/pull/88004) (the `EphemeralContainers` feature introduced in version 1.16 needs to be enabled.)

#### hyperkube
The implementation of hyperkube was changed from Go code to a bash script.

### Changelogs
[kubernetes 1.18 changelog](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.18.md#whats-new-major-themes)
[kubernetes 1.17 changelog](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.17.md#whats-new-major-themes)



## 1.16 changes since 1.14
### Major updates
#### Improved cluster stability and availability
Improved and enhanced the production-ready features like BM cluster tool and HA.
The kubeadm support for HA has entered the Beta stage. Users can run the `kubeadm init` and `kubeadm join` commands to deploy HA control planes. Certificate management is more stable and robust. During cluster update, kubeadm can seamlessly update all certificates prior to certificate expiry. For more information, see [pr357](https://github.com/kubernetes/enhancements/issues/357) and [pr970](https://github.com/kubernetes/enhancements/issues/970).

#### Continuous CSI improvement
Storage SIG continues to migrate built-in storage plug-ins to CSI APIs and support features such as built-in storage plug-in resizing and inline storage volumes. It also introduced some Alpha features that are not available in the Kubernetes storage subsystem, such as storage volume cloning.
Storage volume cloning allows users to specify another PVC as "DataSource" when configuring a new storage volume. If the underlying storage system supports this feature and has implemented the "CLONE_VOLUME" feature in its CSI driver, the new storage volume will become a clone of the source storage volume. For more information, see [pr625](https://github.com/kubernetes/enhancements/issues/625).
#### Features
- The following features enter the GA stage:
	- `CRD`
	- `Admission Webhook`
	- `GCERegionalPersistentDisk` 
	- `CustomResourcePublishOpenAPI` 
	- `CustomResourceSubresources`
	- `CustomResourceValidation`
	- `CustomResourceWebhookConversion`
- CSI support for volume resizing enters the Beta stage.

### General updates
- The Kubernetes core code supports the Go module.
- Preparation for cloud-provider code extraction and organization continues. cloud-provider code has been moved to kubernetes/legacy-cloud-providers to facilitate future deletion and external use.
- [Kubectl get and describe commands support expansion](https://github.com/kubernetes/enhancements/issues/515).
- [Nodes support third-party monitoring plug-ins](https://github.com/kubernetes/enhancements/issues/606).
- Launched a new Alpha scheduling framework for developing and managing plug-ins and expanding the features of the scheduler. For more information, see [pr624](https://github.com/kubernetes/enhancements/issues/624).
- The APIs of extensions/v1beta1, apps/v1beta1, and apps/v1beta2 are still deprecated and will be completely removed in version 1.16.
- Adds Topology Manager component to the kubelet to coordinate resource allocation decisions and optimize resource allocation.
- Supports IPv4/IPv6 dual stacks, so that you can assign both IPv4 and IPv6 addresses to pods and services.
- (Alpha feature) Adds the API server network proxy.
- More [expansion options](https://github.com/kubernetes/enhancements/blob/master/keps/sig-cloud-provider/20190422-cloud-controller-manager-migration.md) are provided for cloud controller manager migration.
- Deprecates extensions/v1beta1, apps/v1beta1, and apps/v1beta2 APIs.

#### Known issues
In version 1.15, when the `--log-file` parameter was used, a log might be written to the same file multiple times. For more information, see [pr78734](https://github.com/kubernetes/kubernetes/issues/78734#issuecomment-501372131).

#### Update notes
- **Clusters**
    - The following tags are no longer configured on nodes: `beta.kubernetes.io/metadata-proxy-ready`, `beta.kubernetes.io/metadata-proxy-ready`, and `beta.kubernetes.io/kube-proxy-ds-ready`.
        * `ip-mask-agent` uses `node.kubernetes.io/masq-agent-ds-ready` as the node selector and no longer uses `beta.kubernetes.io/masq-agent-ds-ready`.
        * `kube-proxy` uses `node.kubernetes.io/kube-proxy-ds-ready` as the node selector and no longer uses `beta.kubernetes.io/kube-proxy-ds-ready`. 
        * `metadata-proxy` uses `cloud.google.com/metadata-proxy-ready` as the node selector and no longer uses `beta.kubernetes.io/metadata-proxy-ready`. 
- **API Machinery**
k8s.io/kubernetes and other released components, including k8s.io/client-go and k8s.io/api, now contain the Go module file including the dependent library version information. When using k8s.io/client-go through the Go module, you can refer to [go-modules](http://git.k8s.io/client-go/INSTALL.md#go-modules) and [pr74877](https://github.com/kubernetes/kubernetes/pull/74877).
- **Apps**
 **Remove hyperkube short aliases from source code**, as hyperkube docker image currently create these aliases. For more information, see [pr76953](https://github.com/kubernetes/kubernetes/pull/76953).
- **Lifecycle**
    - Removes the deprecated kubeadm `v1alpha3` configurations.
    - kube-up.sh no longer supports `centos` and `local`.
- **Storage**
    - The CSI volume no longer configures the `Node.Status.Volumes.Attached.DevicePath` field. The external controller of this field needs to be updated.
    - The Alpha CRD was removed.
    - The `StorageObjectInUseProtection` admission [plug-in](https://github.com/kubernetes/kubernetes/pull/74610) is enabled by default. Previously, if this plug-in is not enabled, cluster actions may change.
    - After PodInfoOnMount is enabled for the CSI driver, the new `csi.storage.k8s.io/ephemeral` parameter will be added in the volume context. During NodePublishVolume implementation, this parameter allows the driver to determine, one by one, whether the current volume is ephemeral storage or persistent storage. For more information, see [pr79983](https://github.com/kubernetes/kubernetes/pull/79983).
    - VolumePVCDataSource (the storage volume cloning feature) entered the Beta phase. For more information, see [pr81792](https://github.com/kubernetes/kubernetes/pull/81792).
    - The built-in and CSI volume limits were combined into the predicate scheduler. For more information, see [pr77595](https://github.com/kubernetes/kubernetes/pull/77595). 
- **kube-apiserver**
    - Deprecated the `--enable-logs-handler` parameter. We plan to remove it in v1.19.
    - Deprecated `--basic-auth-file` and the corresponding authentication mode. Both of them will be removed in the future.
    - Deprecated the default service IP CIDR block (10.0.0.0/24), which will be removed in six months or after two future releases. The `--service-cluster-ip-range` parameter is required for configuring the service IP CIDR block.
- **kube-scheduler**
The `v1beta1` Events API is used. Tools that consume scheduler events need to use the v1beta1 Events API.
- **kube-proxy**
    - Removed the `--conntrack-max` parameter (which can be replaced with `--conntrack-min` and `--conntrack-max-per-core`).
    - Removed the `--cleanup-iptables` parameter.
    - Removed `--resource-container`.
- **kubelet**
    - Removed the `--allow-privileged`, `--host-ipc-sources`, `--host-pid-sources`, and `--host-network-sources` parameters (which can be replaced with the admission controller of `PodSecurityPolicy`).
    - Deprecated the cAdvisor JSON API.
    - Removed `--containerized`.
    - The `--node-labels` parameter can no longer be used to configure tags with the forbidden prefixes of `kubernetes.io-` or `k8s.io-`.
- **kubectl**
    - Removed `kubectl scale job`.
    - Removed the `--pod/-p` parameter in the `kubectl exec` command.
    - Removed the `kubectl convert` command.
    - Removed `--include-uninitialized`.
    - `kubectl cp` no longer supports copying symbol links in a container. This feature can be replaced with the following commands:
     - `local to pod`：`tar cf - /tmp/foo | kubectl exec -i -n <some-namespace> <some-pod> -- tar xf - -C /tmp/bar`
     - `pod to local`：`kubectl exec -n <some-namespace> <some-pod> -- tar cf - /tmp/foo | tar xf - -C /tmp/bar`
- **kubeadm**
    - Deprecated the commands `kubeadm upgrade node config` and `kubeadm upgrade node experimental-control-plane` and replaced them with `kubeadm upgrade node`.
    - Deprecated the `--experimental-control-plane` parameter and replaced it with `--control-plane`.
    - Deprecated the `--experimental-upload-certs` parameter and replaced it with `--upload-certs`.
    - Deprecated the `kubeadm config upload` command and replaced it with `kubeadm init phase upload-confi`.
    - CoreDNS uses the ready plug-in to check readiness.
    - Deprecated the `proxy` plug-in and replaced it with `forward`.
    - Removed the `resyncperiod` option from the `kubernetes` plug-in.
    - Deprecated the `upstream` option. If it is specified, it will be ignored.

### Changelogs
[kubernetes 1.16 changelog](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.16.md#whats-new-major-themes)
[kubernetes 1.15 changelog](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.15.md#whats-new-major-themes)



## 1.14 changes since 1.12
### Major updates
* [Container Storage Interface entered the GA phase](https://github.com/kubernetes/kubernetes/pull/71020).
* [CoreDNS replaced kube-dns and became the default DNS server](https://github.com/kubernetes/kubernetes/pull/69883).
* kubeadm is used to simplify cluster management.
* [Support for Windows Nodes entered the stable phase](https://github.com/kubernetes/enhancements/issues/116).
* [Local storage entered the GA phase](https://github.com/kubernetes/enhancements/issues/121#issuecomment-457396290).
* [Pid Limiting entered the Beta phase](http://github.com/kubernetes/kubernetes/pull/73651).
* [Pod Priority and Preemption are supported](https://github.com/kubernetes/enhancements/issues/564).

### General updates
* dry-run entered the Beta phase (dry-run enables users to simulate real API requests without actually changing the cluster status.)
* kubectl diff entered the Beta phase.
* kubectl plug-in registration entered the stable phase.
* The kubelet plug-in mechanism entered the Beta phase.
* CSIPersistentVolume entered the GA phase.
* TaintBasedEviction entered the Beta phase.
* kube-scheduler perception of volume topology entered the stable phase.
* Support for out-of-tree CSI Volume plug-ins entered the stable phase.
* Supports third-party device monitoring plug-ins.
* kube-scheduler subnet feasibility entered the Beta phase.
* Pod Ready supports custom probe conditions.
* Node memory supports HugePage.
* RuntimeClass entered the Beta phase.
* Node OS/Arch labels entered the GA phase.
* node-leases entered the Beta phase.
* kubelet resource metrics endpoint entered the Alpha phase and supports data collection through Prometheus.
* runAsGroup entered the Beta phase.
* kubectl apply server-side entered the Alpha phase, allowing apply operations to run on the server side.
* kubectl supports kustomize.
* Supports the configuration of resolv.conf in pods.
* CSI volumes support resizing.
* CSI supports topology.
* volume mount supports the configuration of sub-path parameters.
* CSI supports bare devices.
* CSI supports local ephemeral volumes.

### Update notes
* **kube-apiserver**
    * `etcd2` is no longer supported. Default: `--storage-backend=etcd3`.
    * Deprecated the `--etcd-quorum-read` parameter.
    * Deprecated the `--storage-versions` parameter.
    * Deprecated the `--repair-malformed-updates` parameter.
* **kube-controller-manager**
Deprecated the `--insecure-experimental-approve-all-kubelet-csrs-for-group` parameter.
* **kubelet**
 * Deprecated the `--google-json-key` parameter.
 * Deprecated the `--experimental-fail-swap-on` parameter.
* <b>kube-scheduler</b>
 `componentconfig/v1alpha1` is no longer supported.
* **kubectl**
The `run-container` command is no longer supported. 
* **taints**
`node.alpha.kubernetes.io/notReady` and `node.alpha.kubernetes.io/unreachable` are no longer supported and have been replaced with `node.kubernetes.io/not-ready` and `node.kubernetes.io/unreachable`, respectively.

### Changelogs
[kubernetes 1.14 changelog](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.14.md#kubernetes-v114-release-notes)
[kubernetes 1.13 changelog](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.13.md#kubernetes-113-release-notes)

## 1.12 changes since 1.10
### Major updates
#### API 
- The CustomResources sub-resources have entered the Beta phase and are enabled by default, allowing users to update the `/status` sub-resources, except for the `.status` field (previously, only .spec and .metadata could be updated.) When the `/status` sub-resources are enabled, `required` and `rescription` can be used for CRD OpenAPI verification schemas. In addition, users can create multiple versions of CustomResourceDefinitions, without the need for automatic switching. The `spec.additionalPrinterColumns` field of CustomResourceDefinitions can be used to allow the output of `kubectl get` to contain additional columns.
- The `dry run` feature is supported. It allows users to view the execution results of some commands without having to submit relevant modifications.

#### Authentication authorization
- RBAC aggregation of ClusterRoles entered the GA phase. The client-go credentials plug-in entered the Beta phase, allowing users to obtain TLS authentication information from external plug-ins.
- Added the following annotations to audit events, so that users can be better informed of the audit decision-making process:
  * The Authorization component can configure `authorization.k8s.io/decision` (the allow or forbid authorization decision) and `authorization.k8s.io/reason` (the reason for this decision).
  * The PodSecurityPolicy admission controller can configure `podsecuritypolicy.admission.k8s.io/admit-policy` and `podsecuritypolicy.admission.k8s.io/validate-policy`, containing the names of the policies allowing pod admission (PodSecurityPolicy can also restrict mount targets of the hostPath type to the read-only mode.)
- The NodeRestriction admission controller can prohibit nodes from modifying the taint information of their corresponding node objects so that users can control and track the taint settings of nodes more easily.

#### CLI
The CLI implemented a new plug-in mechanism and provided a development library that contains common CLI tools to facilitate plug-in development by plug-in developers.

#### Network
- The ipvs mode entered the GA phase.
- CoreDNS entered the GA phase and replaced kube-dns.

#### Nodes
- DynamicKubeletConfig entered the Beta phase.
- cri-tools entered the GA phase.
- PodShareProcessNamespace entered the Beta phase.
- Added the RuntimeClass and CustomCFSQuotaPeriod Alpha features.

#### Scheduler
- Pod Priority and Preemption entered the Beta phase.
- DaemonSet Pod scheduling is no longer managed by the DaemonSet controller but by the default scheduler.
- TaintNodeByCondition entered the Beta phase.
- The local image preferential selection feature is enabled by default. During pod scheduling, nodes that have locally pulled the images required by all or some pods will have a higher priority. This accelerates the launch of pods.

### General updates
- The ClusterRole and StorageObjectInUseProtection features entered the GA phase.
- The external Cloud Provider feature entered the Beta phase.

### Update notes
- **kube-apiserver**
  - The `--storage-version` parameter was removed and replaced by `--storage-versions`. Meanwhile, `--storage-versions` was also deprecated.
  - The default value of `--endpoint-reconciler-type` was changed to `lease`.
  - When `--enable-admission-plugins` is used, it is contained by default. When the `--admission-control` parameter is used, it must be explicitly specified.
- **kubelet**
  - Deprecated the `--rotate-certificates` parameter and replaced it with the .RotateCertificates field in the configuration file.
- **kubectl**
  - Exception `run-pod/v1`, other `kubectl run` generators have been deprecated.
  - Removed the `--interactive` parameter from `kubectl logs`.
  - `--use-openapi-print-columns` was deprecated and replaced with `--server-print`.

### Changelogs
[kubernetes 1.12 changelog](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.12.md#major-themes)
[kubernetes 1.11 changelog](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.11.md#kubernetes-111-release-notes)
