## Kubernetes 1.22 Changes Since 1.20
### Major updates
#### PodSecurityPolicy deprecated
PodSecurityPolicy is deprecated in 1.21 and will be removed in 1.25. You can evaluate and migrate it to Pod Security Admission or third-party admission plug-ins.

#### GA of immutable Secret and ConfigMap volumes
After Secret and ConfigMap volumes are set as immutable (`immutable: true`), kubelet no longer watches the changes of these objects and mounts them to the container again to reduce the load of apiserver. This feature enters GA in 1.21.

#### CronJobs GA
CronJobs enters GA (batch/v1) in 1.21, and the new version controller CronJobControllerV2 with higher performance is enabled by default.

#### Beta of IPv4/IPv6 addresses in dual-stack networks
Dual-stack networks allow Pods, services, and nodes to obtain IPv4 and IPv6 addresses. In 1.21, the dual-stack network feature is upgraded from alpha to beta and the feature is enabled by default.

#### Graceful node shutdown
This feature enters beta in 1.21. It allows kubelet to listen for node shutdown events and gracefully terminates Pods on nodes.

#### Persistent volume health monitoring
This alpha feature is introduced in 1.21. It monitors the running status of persistent volumes (PVs) and marks PVs when they become unhealthy so that workloads can be adjusted accordingly to avoid data from being written to or read from unhealthy PVs.

#### Server-side Apply GA
Server-side Apply helps users and controllers manage resources through declarative configuration, such as creating or modifying objects declaratively. Server-side Apply entered GA in 1.22.

#### External credential GA
External credentials enters GA in 1.22, providing better support for interactive login process plug-ins. For more information, see [sample-exec-plugin](https://github.com/ankeesler/sample-exec-plugin).

#### Etcd updated to 3.5.0
Etcd 3.5.0 is used by default in 1.22. Etcd 3.5.0 has improved security, performance, monitoring, and developer experience, fixed multiple bugs, and added important new features such as structured log records and built-in log rotation.

#### MemoryQoS
The alpha MemoryQoS feature is supported starting from 1.22. When it is enabled, the Cgroups v2 API will be used to manage and control memory allocation and isolation, ensuring memory usage for workloads and improving the availability of workloads and nodes in the case of memory resource competition. This feature was proposed by Tencent Cloud and contributed to the Kubernetes community.

#### Cluster's default seccomp configuration
Kubelet introduces the `SeccompDefault` alpha feature in 1.22. According to the `--seccomp-default` parameter and setting, kubelet will use the `RuntimeDefault` seccomp setting instead of `Unconfined`, improving the security of workloads.

### Other updates
- GA features:
	- 1.21: EndpointSlice,Sysctls,PodDisruptionBudget
	- 1.22: CSIServiceAccountToken
- Features graduating to beta:
	- 1.21: TTLAfterFinished
	- 1.22: SuspendJob,PodDeletionCost,NetworkPolicyEndPort
- 1.22: Introduces the new scheduler scoring plug-in `NodeResourcesFit`, which is used to replace three plug-ins: `NodeResourcesLeastAllocated`, `NodeResourcesMostAllocated`, and `RequestedToCapacityRatio`.
- 1.22: When the alpha feature `APIServerTracing` is enabled, apiserver supports distributed tracing and allows users to use the `--service-account-issuer` parameter to set multiple issuers. In addition, apiserver can provide uninterrupted service when issuers are changed.

### Deprecations and removals
#### Removed parameters and features
1. `Service TopologyKeys` is deprecated and replaced with `Topology Aware Hints`.
2. kube-proxy
	- Starting from 1.21, `net.ipv4.conf.all.route_localnet=1` will not be automatically set in IPVS mode. For upgraded nodes, `net.ipv4.conf.all.route_localnet=1` will be retained. But for new nodes, the default system value (usually `0`) is inherited.
	- The `--cleanup-ipvs` parameter is deleted and can be replaced with the `--cleanup` parameter.
3. kube-controller-manager
	- Starting from 1.22, the `--horizontal-pod-autoscaler-use-rest-clients` parameter is removed.
	- The `--port` and `--address` parameters become invalid and will be removed in 1.24.
4. kube-scheduler: The `--hard-pod-affinity-symmetric-weight` and `--scheduler-name` parameters are removed in 1.22, and instead, these information can be configured in the `config` file.
5. Kubelet: The `DynamicKubeletConfig` feature is deprecated and is disabled by default. If the `--dynamic-config-dir` parameter is set when kubelet is started, an alarm will be reported.

#### Removed or deprecated versions
1. Starting from 1.21, CronJob batch/v2alpha1 is removed.
2. Starting from 1.22, the following beta APIs are removed: (Find details in [Kubernetes official documentation](https://kubernetes.io/docs/reference/using-api/deprecation-guide/#v1-22).)
	- rbac.authorization.k8s.io/v1beta1
	- admissionregistration.k8s.io/v1beta1
	- apiextensions.k8s.io/v1beta1
	- apiregistration.k8s.io/v1beta1
	- authentication.k8s.io/v1beta1
	- authorization.k8s.io/v1beta1
	- certificates.k8s.io/v1beta1
	- coordination.k8s.io/v1beta1
	- extensions/v1beta1 and networking.k8s.io/v1beta1 ingress API

### Change logs
- [kubernetes1.22changelog](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.22.md#whats-new-major-themes)
- [kubernetes1.21changelog](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.21.md#whats-new-major-themes)


## Kubernetes 1.20 Changes Since 1.18
### Major updates
#### New version of CronJob controller
Kubernetes 1.20 introduces the new version of the CronJob controller, which uses the informer mechanism to replace polling, optimizing the performance. You can set `--feature-gates="CronJobControllerV2=true"` in `kube-controller -manager` to enable the new version. The new version will be enabled by default on later Kubernetes versions.

#### Dockershim deprecation
Dockershim is being deprecated. Support for Docker is deprecated and will be removed from a future release. Docker-produced images will continue to work in your cluster with all CRI compliant runtimes as Docker images follow the Open Container Initiative (OCI) image specification.
For more information, see [Don't Panic: Kubernetes and Docker](https://kubernetes.io/blog/2020/12/02/dont-panic-kubernetes-and-docker/) and [Dockershim Deprecation FAQ](https://blog.k8s.io/2020/12/02/dockershim-faq/).
#### Structured logs
The log message and Kubernetes object reference structures are standardized to make log parsing, processing, storage, query, and analysis easier. Two methods are added to klog to support structured logs: `InfoS` and `ErrorS`.
The `--logging-format` parameter is added to all components, and its default value is `text` in the previous format. You can set it to `json` to support structured logs, and the following parameters will become invalid: `--add_dir_header`, `--alsologtostderr`, `--log_backtrace_at`, `--log_dir`, `--log_file`, `--log_file_max_size`, `--logtostderr`, `--skip_headers`, `--skip_log_headers`, `--stderrthreshold`, `--vmodule`, and `--log-flush-frequency`.
#### Exec probe timeout handling
A longstanding bug regarding exec probe timeouts that may impact existing Pod definitions has been fixed. Prior to this fix, the `timeoutSeconds` field was not respected for exec probes. Instead, probes would run indefinitely, even past their configured deadline, until a result was returned. With this change, the default value of `1 second` will be applied if a value is not specified and existing Pod definitions may no longer be sufficient if a probe takes longer than one second. A feature gate, called `ExecProbeTimeout`, has been added with this fix that enables you to revert to the previous behavior, but this will be locked and removed in subsequent releases. In order to revert to the previous behavior, you should set this feature gate to `false`.
For more information, see [Configure Liveness, Readiness and Startup Probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#configure-probes).
#### Graduation of volume snapshot operation feature to GA
This feature provides a standard way to trigger volume snapshot operations and allows you to incorporate snapshot operations in a portable manner on any Kubernetes environment and supported storage providers.
Additionally, these Kubernetes snapshot primitives act as basic building blocks that unlock the ability to develop advanced and enterprise-grade storage administration features for Kubernetes, including application or cluster level backup solutions.
Note that snapshot support requires Kubernetes distributors to bundle and deploy the snapshot controller, snapshot CRDs, and validation webhook. A CSI driver supporting the snapshot feature must also be deployed in the cluster.

#### Graduation of kubectl debug to beta
 The `kubectl alpha debug` command graduates to beta, becoming `kubectl debug`. It supports common debugging workflows directly from kubectl, for example:
- Troubleshoot workloads that crash on startup by creating a copy of the Pod with a different container image or command.
- Troubleshoot distroless containers by adding a new container with debugging tools, either in a new copy of the Pod or using an ephemeral container. (Ephemeral containers (`EphemeralContainers`) are an alpha feature that are not enabled by default.)
- Troubleshoot on a node by creating a container running in the host namespaces and with access to the host's file system.
Note that as a new built-in command, `kubectl debug` takes priority over any kubectl plugin named `debug`. You need to rename the affected plugins.
 `kubectl alpha debug` is now deprecated and will be removed in a subsequent release. Update your scripts to use `kubectl debug`. For more information, see [Debug Running Pods](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-running-pod/).
 
#### Graduation of API priority and fairness to beta
Introduced on Kubernetes 1.18, the API priority and fairness feature is now enabled by default on Kubernetes 1.20. This allows `kube-apiserver` to categorize incoming requests by priority.
#### Graduation of PID limits to GA
 `SupportNodePidsLimit` (node-to-Pod PID isolation) and `SupportPodPidsLimit` (ability to limit PIDs per Pod) move to GA.
 
#### Alpha feature: Graceful node shutdown
Users and cluster admins expect that Pods will adhere to the expected Pod lifecycle, including Pod termination. Currently, when a node shuts down, Pods do not follow the expected Pod termination lifecycle and are not terminated gracefully, which may cause issues for some workloads. The `GracefulNodeShutdown` feature is now in alpha on Kubernetes 1.20. It makes the kubelet aware of node system shutdowns, enabling graceful termination of Pods during a system shutdown.

#### Graduation of CSIVolumeFSGroupPolicy to beta
CSIDrivers can use the `fsGroupPolicy` field to control whether ownership and permissions (`ReadWriteOnceWithFSType`, `File`, and `None`) can be modified during mounting.

#### Graduation of ConfigurableFSGroupPolicy to beta
The following can be set in a non-recursive manner: fsgroup -  `PodFSGroupChangePolicy`  =  `OnRootMismatch`.

### Other updates
- The Cloud Controller Manager component is added.
- Features graduating to GA:
  - [RuntimeClass](https://github.com/kubernetes/enhancements/issues/585)
 `node.k8s.io/v1beta1` is deprecated and replaced with `node.k8s.io/v1`. 
  - [Built-in API types defaults](https://github.com/kubernetes/enhancements/issues/1929)
  - [StartupProbe](https://github.com/kubernetes/enhancements/issues/950)
  - [Adding AppProtocol to Services and Endpoints](https://github.com/kubernetes/enhancements/issues/1507)
  - [TokenRequest and TokenRequestProjection](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/#service-account-token-volume-projection)
  - SCTPSupport
  - Containerd support for Windows
  - Ingress
  `networking.k8s.io/v1beta1` is deprecated (it will be removed on Kubernetes 1.22) and replaced by `networking.k8s.io/v1`.
  - seccomp
  seccomp annotations `seccomp.security.alpha.kubernetes.io/pod` and `container.seccomp.security.alpha.kubernetes.io/...` are deprecated (they will be removed on Kubernetes 1.22). You can directly specify the following fields for Pods and container specs:
```
securityContext:
  seccompProfile:
    type: RuntimeDefault|Localhost|Unconfined ## choose one of the three
    localhostProfile: my-profiles/profile-allow.json ## only necessary if type == Localhost
```
  K8S converts annotations and fields automatically, so no additional operations are required.
  - [Kubelet Client TLS Certificate Rotation](https://github.com/kubernetes/enhancements/issues/266)
  - [Limit node access to API](https://github.com/kubernetes/enhancements/issues/279)
  Node authentication mode features are all implemented.
  - [Redesign Event API](https://github.com/kubernetes/enhancements/issues/383)
  To reduce the impact of events on the system performance and add more fields to provide more useful information, Event API is redesigned on Kubernetes 1.19.
  - [CertificateSigningRequest API](https://github.com/kubernetes/enhancements/issues/1513)
  In addition to `certificates.k8s.io/v1beta1`, the `certificates.k8s.io/v1` version is added to `CertificateSigningRequest`. When using `certificates.k8s.io/v1`:
    - You must specify `spec.signerName` and stop using `kubernetes.io/legacy-unknown`.
    - You must specify `spec.usages`, which can contain only known and unique usages.
    - You must specify `status.conditions[*].status`.
    - `status.certificate` must be PEM encoded and can contain only the `CERTIFICATE` block.
- Features graduating to beta:
The following features graduate to beta and are enabled by default:
  - EndpointSliceProxying
  kube-proxy reads information from EndpointSlices instead of Endpoints, which greatly improves the cluster scalability and makes it easier to add new features such as topology-aware routing.
  - KubeSchedulerConfiguration
  - HugePageStorageMediumSize
  - ImmutableEphemeralVolumes
  The Secret and ConfigMap volumes can be marked as immutable. When there are many Secret and ConfigMap volumes, the pressure on apiserver can be greatly mitigated.
  - NodeDisruptionExclusion
  - NonPreemptingPriority
  - ServiceNodeExclusion
  - [RootCAConfigMap](https://github.com/kubernetes/enhancements/blob/master/keps/sig-auth/1205-bound-service-account-tokens/README.md)
  - [kube-scheduler metrics](https://kubernetes.io/docs/concepts/cluster-administration/system-metrics/#kube-scheduler-metrics)
  - ServiceAccountIssuerDiscovery

### Deprecations and removals
#### Deprecated versions

| Deprecated Version | New Version |
|:--|--|
|apiextensions.k8s.io/v1beta1 |apiextensions.k8s.io/v1 |
|apiregistration.k8s.io/v1beta1 |apiregistration.k8s.io/v1 |
|authentication.k8s.io/v1beta1 |authentication.k8s.io/v1 |
|authorization.k8s.io/v1beta1 |authorization.k8s.io/v1 |
|autoscaling/v2beta1 |autoscaling/v2beta2 |
|coordination.k8s.io/v1beta1 |oordination.k8s.io/v1 |
|storage.k8s.io/v1beta1 |storage.k8s.io/v1 |

#### kube-apiserver
1. The `componentstatus` API is deprecated. This API provided status of etcd, kube-scheduler and kube-controller-manager components, but only worked when those components were local to apiserver, and when kube-scheduler and kube-controller-manager exposed unsecured health endpoints.
After this API is deprecated, etcd health is included in the kube-apiserver health check and kube-scheduler/kube-controller-manager health checks can be made directly against those components' health endpoints.
2. apiserver no longer listens on insecure ports.
 The `--address` and `--insecure-bind-address` parameters can be set, but are invalid. The `--port` and `--insecure-port` parameters can be set to only `0`. These parameters will be removed on Kubernetes 1.24.
3. `TokenRequest` and `TokenRequestProjection` graduate to GA. You need to set the following parameters for kube-apiserver:
  - `--service-account-issuer`: Fixed URL of the cluster API server.
  - `--service-account-key-file`: One or multiple public keys for token verification.
  - `--service-account-signing-key-file`: Private key for service account issuing, which can use the same file as the `--service-account-private-key-file` parameter of `kube-controller-manager`.

#### kubelet
1. The following parameters are removed:
	-  `--seccomp-profile-root` 
	- `--cloud-provider` and `--cloud-config`, which are replaced with `config`
	- `--really-crash-for-testing` and `--chaos-chance`
2. The deprecated `metrics/resource/v1alpha1` endpoint is removed and replaced with `metrics/resource`.

#### Other removals
- The `failure-domain.beta.kubernetes.io/zone` and `failure-domain.beta.kubernetes.io/region` labels are deprecated and replaced with `topology.kubernetes.io/zone` and `topology.kubernetes.io/region` respectively. All users of the `failure-domain.beta...` labels should switch to the `topology...` equivalents.
- PodPreset is removed, and you can use webhooks to implement this feature.
- The `basic auth` authentication method is no longer supported.
- Direct CBS inline mounting to workloads is no longer supported.
>? When you upgrade from Kubernetes 1.18 to 1.20, successful mounting of [CSI ephemeral (inline) volumes](https://kubernetes.io/zh/docs/concepts/storage/ephemeral-volumes/#csi-ephemeral-volumes) cannot be guaranteed. If your application uses a CSI ephemeral volume, we recommend you convert it to a persistent volume before upgrade.
>

### Change logs
[Kubernetes 1.20 changelog](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.20.md#whats-new-major-themes)
[Kubernetes 1.19 changelog](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.19.md#whats-new-major-themes)



## Kubernetes 1.18 Changes Since 1.16
### Major updates
#### Graduation of Cloud Provider labels to GA
Deprecated and new labels are as listed below:

| Deprecated Label | New Label | 
|:---------|:---------|
| `beta.kubernetes.io/instance-type` | `node.kubernetes.io/instance-type` |
| `failure-domain.beta.kubernetes.io/region` |`topology.kubernetes.io/region` |
| `failure-domain.beta.kubernetes.io/zone` | `topology.kubernetes.io/zone` |




#### Graduation of volume snapshot to beta
`VolumeSnapshotDataSource` is enabled by default. For more information, see [Kubernetes 1.17 Feature: Kubernetes Volume Snapshot Moves to Beta](https://kubernetes.io/blog/2019/12/09/kubernetes-1-17-feature-cis-volume-snapshot-beta/).

#### Graduation of CSI Migration to beta
CSI Migration is enabled by default. For more information, see [Kubernetes 1.17 Feature: Kubernetes In-Tree to CSI Volume Migration Moves to Beta](https://kubernetes.io/blog/2019/12/09/kubernetes-1-17-feature-csi-migration-beta/).

#### Graduation of Kubernetes Topology Manager to beta
The Topology Manager feature moves to beta on Kubernetes 1.18. This feature enables NUMA alignment of CPU and devices (such as SR-IOV VFs) that will allow your workload to run in an environment optimized for low latency.
Prior to the introduction of the Topology Manager, the CPU and Device Manager would make resource allocation decisions independent of each other. This could result in undesirable allocations on multi-socket CPU systems, causing degraded performance on latency critical applications.

#### Graduation of Server-Side Apply to beta 2
Server-Side Apply was promoted to beta on Kubernetes 1.16, but is now introducing a second beta (Server-Side Apply) on Kubernetes 1.18. This new version will track and manage changes to fields of all new Kubernetes objects, allowing you to know what changed your resources and when.

#### IngressClass resource
The `IngressClass` resource is used to describe a type of Ingress within a Kubernetes cluster. `Ingresses` can specify the class they are associated with by using a new `ingressClassName` field on Ingresses. This new resource and field replace the deprecated `kubernetes.io/ingress.class` annotation.

### Other updates
- Graduation of NodeLocal DNSCache to GA.
- Graduation of IPv6 to beta.
- `kubectl debug`: Alpha feature.
- `Windows CSI support`: Alpha feature.
- `ImmutableEphemeralVolumes`: Alpha feature (it supports immutable ConfigMaps and Secrets without refreshing the corresponding volumes).
- The following features graduate to GA:
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
  - `BlockVolume` and `CSIBlockVolume`
  - `Windows RunAsUserName`
- Features graduating to beta:
  - `EndpointSlices`: Disabled by default
  - `CSIMigrationAWS`: Disabled by default
  - `StartupProbe`
  - `EvenPodsSpread`

### Deprecations and removals
#### Removed features
The following features, which are enabled by default and cannot be configured, are removed.
- `GCERegionalPersistentDisk`
- `EnableAggregatedDiscoveryTimeout`
- `PersistentLocalVolumes`
- `CustomResourceValidation`
- `CustomResourceSubresources`
- `CustomResourceWebhookConversion`
- `CustomResourcePublishOpenAPI`
- `CustomResourceDefaulting`

#### Other removals
The following built-in cluster roles are removed:
 - `system:csi-external-provisioner` 
 - `system:csi-external-attacher`

#### Deprecated feature switches and parameters
- The default service IP CIDR block (`10.0.0.0/24`) is deprecated. It must be set through the `--service-cluster-ip-range` parameter on kube-apiserver.
- The `rbac.authorization.k8s.io/v1alpha1` and `rbac.authorization.k8s.io/v1beta1` API groups are deprecated and will be removed on Kubernetes 1.20. Therefore, migrate your resources to `rbac.authorization.k8s.io/v1`.
- The `CSINodeInfo` feature gate is deprecated. This feature has graduated to GA and is enabled by default.

### Parameter and other changes
#### kube-apiserver
- `--encryption-provider-config`: If `cacheSize: 0` is specified in the configuration file, versions earlier than 1.18 are automatically configured to cache 1,000 keys, while version 1.18 will report a configuration verification error. You can disable the cache by setting `cacheSize` to a negative value.
- `--feature-gates`: The following features are enabled by default and can no longer be configured through the command line.
  - `PodPriority`
  - `TaintNodesByCondition`
  - `ResourceQuotaScopeSelectors` 
  - `ScheduleDaemonSetPods` 
- The following resource versions (group versions) are no longer supported:
    - `apps/v1beta1` and `apps/v1beta2`, which are replaced with `apps/v1`.
    - Under `extensions/v1beta1`:
     - `daemonsets`, `deployments` and `replicasets`, which are replaced with `apps/v1`.
     - `networkpolicies`, which is replaced with `networking.k8s.io/v1`.
     - `podsecuritypolicies`, which is replaced with `policy/v1beta1`.

#### kubelet
- `--enable-cadvisor-endpoints`: This parameter is disabled by default. To access the `cAdvisor v1 JSON` API, you must enable it.
- The `--redirect-container-streaming` parameter is deprecated and will be removed on later versions. Kubernetes 1.18 supports only the default behavior (kubelet proxy for streaming requests). If `--redirect-container-streaming=true` is set, it must be removed.
- The `/metrics/resource/v1alpha1` endpoint is deprecated and replaced with `/metrics/resource`.

#### kube-proxy
- The following parameters are deprecated:
    - `--healthz-port` is deprecated and replaced with `--healthz-bind-address`.
    - `--metrics-port` is deprecated and replaced with `--metrics-bind-address`.
- The `EndpointSliceProxying` feature gate (disabled by default) is added to control whether to enable EndpointSlices in kube-proxy. The `EndpointSlice` feature gate no longer affects the behaviors of kube-proxy.
- The following timeout settings for IPVS connection configuration are added:
  - `--ipvs-tcp-timeout`
  - `--ipvs-tcpfin-timeout`
  - `--ipvs-udp-timeout`
- The iptables mode supports the IPv4/IPv6 dual-protocol stack.

#### kube-scheduler
- The `scheduling_duration_seconds` metric is deprecated.
 - `scheduling_algorithm_predicate_evaluation_seconds` is deprecated and replaced with `framework_extension_point_duration_seconds[extension_point="Filter"]`.
 - `scheduling_algorithm_priority_evaluation_seconds` is deprecated and replaced with `framework_extension_point_duration_seconds[extension_point="Score"]`.
- `AlwaysCheckAllPredicates` is deprecated in the scheduler policy API.

#### -enable-profiling parameter
To align `kube-apiserver`, `kube-controller-manager` and `kube-scheduler`, [profiling is enabled by default](https://github.com/kubernetes/kubernetes/pull/88663). To disable profiling, specify the `--enable-profiling=false` parameter.

#### kubectl
- The deprecated `--include-uninitialized` parameter is removed.
- `kubectl` and `k8s.io/client-go` no longer use `http://localhost:8080` as the default apiserver address.
- `kubectl run` supports Pod creation and no longer supports using the deprecated generator to create other types of resources.
- The deprecated `kubectl rolling-update` command is removed and replaced with the `rollout` command.
- `–dry-run` supports three parameter values: `client`, `server`, and `none`.
- `–dry-run=server` supports the following commands: `apply`, `patch`, `create`, `run`, `annotate`, `label`, `set`, `autoscale`, `drain`, `rollout undo`, and `expose`.
- The `kubectl alpha debug` command is added, which can be used for [debugging and troubleshooting on ephemeral containers in Pods](https://github.com/kubernetes/kubernetes/pull/88004) (the `EphemeralContainers` feature introduced on version 1.16 needs to be enabled).

#### hyperkube
The implementation of hyperkube is changed from Go code to a bash script.

### Change logs
[Kubernetes 1.18 changelog](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.18.md#whats-new-major-themes)
[Kubernetes 1.17 changelog](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.17.md#whats-new-major-themes)



## Kubernetes 1.16 Changes Since 1.14
### Major updates
#### Improved cluster stability and availability
Production-ready features like bare metal cluster tool and high availability (HA) are improved and enhanced.
kubeadm support for HA capability moves to beta, allowing you to use the `kubeadm init` and `kubeadm join` commands to configure and deploy an HA control plane. Certificate management has become more robust, with kubeadm now seamlessly rotating all your certificates (on upgrades) before they expire. For more information, see [Ability to create dynamic HA clusters with kubeadm](https://github.com/kubernetes/enhancements/issues/357) and [kubeadm: graduate the kubeadm configuration](https://github.com/kubernetes/enhancements/issues/970).

#### Continuous CSI improvement
SIG Storage continues work to enable migration of in-tree volume plugins to Container Storage Interface (CSI). It works on bringing CSI to feature parity with in-tree functionality, including resizing and inline volumes. It introduces new alpha functionality in CSI that doesn't exist in the Kubernetes Storage subsystem yet, like volume cloning.
Volume cloning enables you to specify another PVC as a `DataSource` when configuring a new volume. If the underlying storage system supports this functionality and implements the `CLONE_VOLUME` capability in its CSI driver, then the new volume becomes a clone of the source volume. For more information, see [In-tree storage plugin to CSI Driver Migration](https://github.com/kubernetes/enhancements/issues/625).
#### Features
- Features graduating to GA:
	- `CRD`
	- `Admission Webhook`
	- `GCERegionalPersistentDisk` 
	- `CustomResourcePublishOpenAPI` 
	- `CustomResourceSubresources`
	- `CustomResourceValidation`
	- `CustomResourceWebhookConversion`
- CSI support for volume resizing graduates to beta.

### General updates
- Go modules are supported by the Kubernetes core.
- Preparation on cloud provider extraction and code organization is continued. The cloud provider code has been moved to `kubernetes/legacy-cloud-providers` for easier removal later and external usage.
- [kubectl get and describe should work well with extensions](https://github.com/kubernetes/enhancements/issues/515)
- [Support 3rd party device monitoring plugins](https://github.com/kubernetes/enhancements/issues/606).
- A new scheduling framework for developing and managing plugins and extending the scheduler features is in alpha. For more information, see [Scheduling Framework](https://github.com/kubernetes/enhancements/issues/624).
- `extensions/v1beta1`, `apps/v1beta1` and `apps/v1beta2` APIs continue to be depreciated. These extensions will be retired on Kubernetes 1.16.
- The Topology Manager component is added to Kubelet. It aims to coordinate resource allocation decisions to optimize resource allocation.
- IPv4/IPv6 dual stack is supported to assign both IPv4 and IPv6 addresses to Pods and Services.
- The API server network proxy is in alpha.
- More extension options are provided for cloud controller manager migration.
- `extensions/v1beta1`, `apps/v1beta1` and `apps/v1beta2` APIs are deprecated.

#### Known issues
Using the `--log-file` parameter is known to be problematic on Kubernetes 1.15. This presents as things being logged multiple times to the same file. For more information, see [[Failing Test] timeouts in ci-kubernetes-e2e-gce-scale-performance](https://github.com/kubernetes/kubernetes/issues/78734#issuecomment-501372131).

#### Update notes
- **Cluster**
    - The following labels can no longer be added to new nodes: `beta.kubernetes.io/metadata-proxy-ready`, `beta.kubernetes.io/metadata-proxy-ready` and `beta.kubernetes.io/kube-proxy-ds-ready`.
        * `ip-mask-agent` uses `node.kubernetes.io/masq-agent-ds-ready` as the node selector and no longer uses `beta.kubernetes.io/masq-agent-ds-ready`.
        * `kube-proxy` uses `node.kubernetes.io/kube-proxy-ds-ready` as the node selector and no longer uses `beta.kubernetes.io/kube-proxy-ds-ready`.  
        * `metadata-proxy` uses `cloud.google.com/metadata-proxy-ready` as the node selector and no longer uses `beta.kubernetes.io/metadata-proxy-ready`.  
- **API Machinery**
`k8s.io/kubernetes` and other published components (such as `k8s.io/client-go` and `k8s.io/api`) now contain Go module files, including version information of the dependent library. For more information on consuming `k8s.io/client-go` using Go modules, see [Installing client-go](http://git.k8s.io/client-go/INSTALL.md#go-modules) and [add go module support, manage vendor directory using go mod vendor](https://github.com/kubernetes/kubernetes/pull/74877).
- **Apps**
 **Hyperkube short aliases have been removed from source code**, because hyperkube docker image currently creates these aliases. For more information, see [fix Remove hyperkube short aliases](https://github.com/kubernetes/kubernetes/pull/76953).
- **Lifecycle**
    - Support for deprecated kubeadm `v1alpha3` configuration is totally removed.
    - `kube-up.sh` no longer supports `centos` and `local` providers.
- **Storage**
    - The `Node.Status.Volumes.Attached.DevicePath` field is no longer set for CSI volumes. You must update any external controllers that depend on this field.
    - CSI alpha CRDs are removed.
    - The `StorageObjectInUseProtection` admission [plugin](https://github.com/kubernetes/kubernetes/pull/74610) is enabled by default. If you previously had not enabled it, your cluster behavior may change.
    - When `PodInfoOnMount` is enabled for a CSI driver, the new `csi.storage.k8s.io/ephemeral` parameter in the volume context allows a driver's `NodePublishVolume` implementation to determine on a case-by-case basis whether the volume is ephemeral or a normal persistent volume. For more information, see [persistent and ephemeral csi volumes](https://github.com/kubernetes/kubernetes/pull/79983).
    - The `VolumePVCDataSource` (storage volume cloning feature) is promoted to beta. For more information, see [Promote VolumePVCDataSource to beta for 1.16](https://github.com/kubernetes/kubernetes/pull/81792).
    - Limits for in-tree and CSI volumes are integrated into one scheduler predicate. For more information, see [Volume Scheduling Limits](https://github.com/kubernetes/kubernetes/pull/77595).  
- **kube-apiserver**
    - The `--enable-logs-handler` parameter is deprecated and will be removed on Kubernetes 1.19.
    - The `--basic-auth-file` flag and authentication mode are deprecated and will be removed from a future release.
    - The default service IP CIDR block (`10.0.0.0/24`) is deprecated and will be removed in six months/two releases. The `--service-cluster-ip-range` parameter is required to configure the service IP range.
- **kube-scheduler**
The `v1beta1` Event API is used. Any tool targeting scheduler events needs to use it.
- **kube-proxy**
    - The `--conntrack-max` parameter is removed and replaced with `--conntrack-min` and `--conntrack-max-per-core`.
    - The `--cleanup-iptables` parameter is removed.
    - `--resource-container` is removed.
- **kubelet**
    - The `--allow-privileged`, `--host-ipc-sources`, `--host-pid-sources` and `--host-network-sources` parameters are removed and replaced with the admission controller of `PodSecurityPolicy`.
    - The cAdvisor JSON API is deprecated.
    - `--containerized` is removed.
    - The `--node-labels` parameter can no longer be used to configure forbidden labels prefixed with `kubernetes.io-` or `k8s.io-`.
- **kubectl**
    - `kubectl scale job` is removed.
    - The `--pod/-p` parameter of the `kubectl exec` command is removed.
    - The `kubectl convert` command is removed.
    - `--include-uninitialized` is removed.
    - `kubectl cp` no longer supports copying symbolic links from containers. You can use the following commands instead:
     - `local to pod`: `tar cf - /tmp/foo | kubectl exec -i -n <some-namespace> <some-pod> -- tar xf - -C /tmp/bar`
     - `pod to local`: `kubectl exec -n <some-namespace> <some-pod> -- tar cf - /tmp/foo | tar xf - -C /tmp/bar`
- **kubeadm**
    - The `kubeadm upgrade node config` and `kubeadm upgrade node experimental-control-plane` commands are deprecated and replaced with `kubeadm upgrade node`.
    - The `--experimental-control-plane` parameter is deprecated and replaced with `--control-plane`.
    - The `--experimental-upload-certs` parameter is deprecated and replaced with `--upload-certs`.
    - The `kubeadm config upload` command is deprecated and replaced with `kubeadm init phase upload-confi`.
    - CoreDNS checks readiness via the `ready` plugin.
    - The `proxy` plugin is deprecated and replaced with the `forward` plugin.
    - The `resyncperiod` option is removed from the `kubernetes` plugin.
    - The `upstream` option is deprecated. If it is specified, it will be ignored.

### Change logs
[Kubernetes 1.16 changelog](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.16.md#whats-new-major-themes)
[Kubernetes 1.15 changelog](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.15.md#whats-new-major-themes)



## 1.14 Changes Since 1.12
### Major updates
* [Bump CSI Spec to 1.0.0 and gRPC to 1.13.0](https://github.com/kubernetes/kubernetes/pull/71020).
* [Make CoreDNS default in kubeup and update CoreDNS version/manifest in kubeup and kubeadm](https://github.com/kubernetes/kubernetes/pull/69883).
* kubeadm is used to simplify cluster management.
* [Support Windows Server Containers for K8S](https://github.com/kubernetes/enhancements/issues/116).
* [Durable (non-shared) local storage management](https://github.com/kubernetes/enhancements/issues/121#issuecomment-457396290).
* [Support total process ID limiting for nodes](http://github.com/kubernetes/kubernetes/pull/73651).
* [Add pod priority and preemption](https://github.com/kubernetes/enhancements/issues/564).

### General updates
* `dry-run` graduates to beta (`dry-run` enables you to simulate real API requests without actually changing the cluster status).
* `kubectl diff` graduates to beta.
* kubectl plugin registration becomes stable.
* kubelet plugin mechanism graduates to beta.
* `CSIPersistentVolume` graduates to GA.
* `TaintBasedEviction` graduates to beta.
* kube-scheduler perception of volume topology becomes stable.
* Support for out-of-tree CSI volume plugins becomes stable.
* Third-party device monitoring plugins are supported.
* kube-scheduler subnet feasibility graduates to beta.
* Pod Ready supports customizing probe conditions.
* Node memory supports HugePage.
* `RuntimeClass` graduates to beta.
* Node OS/Arch labels graduate to GA.
* Node leases graduate to beta.
* The kubelet resource metrics endpoint graduates to alpha and supports data collection through Prometheus.
* `runAsGroup` graduates to beta.
* `kubectl apply server-side` graduates to alpha, allowing you to perform apply operations on the server side.
* kubectl supports kustomize.
* `resolv.conf` can be configured in Pods.
* CSI volumes can be resized.
* CSI supports topology.
* Volume mounting supports configuration of sub-path parameters.
* CSI supports raw block devices.
* CSI supports local ephemeral volumes.

### Update notes
* **kube-apiserver**
    * `etcd2` is no longer supported. `--storage-backend=etcd3` is used by default.
    * The `--etcd-quorum-read` parameter is deprecated.
    * The `--storage-versions` parameter is deprecated.
    * The `--repair-malformed-updates` parameter is deprecated.
* **kube-controller-manager**
The `--insecure-experimental-approve-all-kubelet-csrs-for-group` parameter is deprecated.
* **kubelet**
 * The `--google-json-key` parameter is deprecated.
 * The `--experimental-fail-swap-on` parameter is deprecated.
* <b> kube-scheduler</b>
 `componentconfig/v1alpha1` is no longer supported.
* **kubectl**
The `run-container` command is no longer supported.  
* **taints**
`node.alpha.kubernetes.io/notReady` and `node.alpha.kubernetes.io/unreachable` are no longer supported and are replaced with `node.kubernetes.io/not-ready` and `node.kubernetes.io/unreachable` respectively.

### Change logs
[Kubernetes 1.14 changelog](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.14.md#kubernetes-v114-release-notes)
[Kubernetes 1.13 changelog](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.13.md#kubernetes-113-release-notes)

## 1.12 Changes Since 1.10
### Major updates
#### API 
- Subresources for `CustomResources` are now beta and enabled by default. With this, updates to the `/status` subresource will disallow updates to all fields other than `.status` (not just `.spec` and `.metadata` as before). Also, `required` and `description` can be used at the root of the CRD OpenAPI validation schema when the `/status` subresource is enabled. In addition, you can now create multiple versions of CustomResourceDefinitions, but without any kind of automatic conversion, and CustomResourceDefinitions now allow specification of additional columns for `kubectl get` output via the `spec.additionalPrinterColumns` field.
- The `dry run` feature is supported. It allows you to view the execution results of some commands without having to submit relevant modifications.

#### Authentication and authorization
- RBAC aggregation of ClusterRoles graduates to GA. The `client-go credentials` plugin graduates to beta, allowing you to get TLS authentication information from external plugins.
- The following annotations are added to audit events, so that you can be better informed of the audit decision-making process:
  * The Authorization component sets `authorization.k8s.io/decision` (the `allow` or `forbid` authorization decision) and `authorization.k8s.io/reason` (the reason for this decision).
  * The PodSecurityPolicy admission controller sets `podsecuritypolicy.admission.k8s.io/admit-policy` and `podsecuritypolicy.admission.k8s.io/validate-policy` annotations containing the name of the policy that allows a Pod to be admitted. (`PodSecurityPolicy` also gains the ability to limit `hostPath` volume mounts to be read-only.)
- The NodeRestriction admission controller prevents nodes from modifying taints on their node objects, making it easier to keep track of which nodes should be in use.

#### CLI
CLI implements a new plugin mechanism, providing a library with common CLI tooling for plugin authors and further refactorings of the code.

#### Internet
- The IPVS mode graduates to GA.
- CoreDNS graduates to GA to replace `kube-dns`.

#### Node
- `DynamicKubeletConfig` graduates to beta.
- `cri-tools` graduates to GA.
- `PodShareProcessNamespace` graduates to beta.
- Alpha features `RuntimeClass` and `CustomCFSQuotaPeriod` are added.

#### Scheduler
- Pod priority and preemption graduate to beta.
- DaemonSet Pod scheduling is no longer managed by the DaemonSet controller, but by the default scheduler.
- `TaintNodeByCondition` graduates to beta.
- The Use Local Image First feature is enabled by default. During Pod scheduling, nodes that have locally pulled the images required by all or some Pods will have a higher priority. This accelerates the launch of Pods.

### General updates
- Features graduating to GA: `ClusterRole` and `StorageObjectInUseProtection`.
- Features graduating to beta: External cloud provider.

### Update notes
- **kube-apiserver**
  - The `--storage-version` parameter is removed and replaced with `--storage-versions`. The `--storage-versions` parameter is also deprecated.
  - The default value of `--endpoint-reconciler-type` is changed to `lease`.
  - When `--enable-admission-plugins` is used, it is contained by default. When the `--admission-control` parameter is used, it must be explicitly specified.
- **kubelet**
  - The `--rotate-certificates` parameter is deprecated and replaced with the `.RotateCertificates` field in the configuration file.
- **kubectl**
  - All `kubectl run` generators except `run-pod/v1` are deprecated.
  - The `--interactive` parameter is removed from `kubectl logs`.
  - `--use-openapi-print-columns` is deprecated and replaced with `--server-print`.

### Change logs
[Kubernetes 1.12 changelog](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.12.md#major-themes)
[Kubernetes 1.11 changelog](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.11.md#kubernetes-111-release-notes)
