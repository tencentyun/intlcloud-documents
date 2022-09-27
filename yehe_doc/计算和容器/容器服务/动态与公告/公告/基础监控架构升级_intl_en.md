

### Background

TKE will be upgraded to provide more stable basic monitoring services and improve the availability of monitoring data, alarming, and HPA scaling. The upgrade falls into three phases, that is, deploying the new version of the monitoring service add-on, switching the add-on version, and deactivating the earlier version, without affecting the services.

### Operation Details

#### Phase 1. Deploying the monitoring service add-on
The `tke-monitor-agent` monitoring data collection add-on will be installed under the `kube-system` namespace of your cluster. The agent will use less than 70 MB memory and 0.01 CPU cores on each node. For add-on details, see [Description of tke-monitor-agent](https://intl.cloud.tencent.com/document/product/457/46740).

#### Phase 2. Switching the add-on version
This phase will be performed one week after the new version of the add-on is deployed to ensure the data source stability.

>?
- If a Kubernetes cluster on v1.8 or later is used, a Service and Endpoint named `metrics-service` will be created under the `kube-system` namespace and point to the `metrics-server` maintained on the container side.
- The `hpa-metrics-service` in the cluster will point to the new data source. If `apiservice v1beta1.metrics.k8s.io` uses the default `kube-system/hpa-metrics-service` data source provided by the container, and the Kubernetes cluster is on v1.8 or later, it will switch to the more stable data source `kube-system/metrics-service`.
- `apiservice v1alpha1.monitor.tencent.io` will be added to support TKE virtual nodes in reporting monitoring data and querying the monitoring data of Pods on each node.



#### Phase 3. Deactivating the earlier version of the monitoring add-on
This phase will be performed one week after the add-on version is switched.
