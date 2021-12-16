

TMP presets the [master component](#kubernetes-master-.E7.BB.84.E4.BB.B6), [kubelet](#kubelet), [resource use](#kubernetes-.E8.B5.84.E6.BA.90.E4.BD.BF.E7.94.A8), [workload](#kubernetes-.E5.B7.A5.E4.BD.9C.E8.B4.9F.E8.BD.BD), and [node](#kubernetes-.E8.8A.82.E7.82.B9) alert templates for TKE clusters.

## Kubernetes master component

The following metrics are provided for non-managed clusters:


<table>
<thead>
<tr>
<th width="10%">Rule Name</th>
<th width="50%">Rule Expression</th>
<th width="10%">Duration</th>
<th width="30%">Description</th>
</tr>
</thead>
<tbody><tr>
<td>Error with client access to APIServer</td>
<td>(sum(rate(rest_client_requests_total{code=~"5.."}[5m])) by (instance, job, cluster_id) / sum(rate(rest_client_requests_total[5m])) by (instance, job, cluster_id))&gt; 0.01</td>
<td>15m</td>
<td>The error rate of client access to the APIServer is above 1%</td>
</tr>
<tr>
<td>Imminent expiration of the client certificate for APIServer access</td>
<td>apiserver_client_certificate_expiration_seconds_count{job="apiserver"} &gt; 0 and on(job) histogram_quantile(0.01, sum by (cluster_id, job, le) (rate(apiserver_client_certificate_expiration_seconds_bucket{job="apiserver"}[5m]))) &lt; 86400</td>
<td>None</td>
<td>The client certificate for APIServer access will expire in 24 hours</td>
</tr>
<tr>
<td>Recording API error</td>
<td>sum by(cluster_id, name, namespace) (increase(aggregator_unavailable_apiservice_count[5m])) &gt; 2</td>
<td>None</td>
<td>The recording API reported an error in the last 5 minutes</td>
</tr>
<tr>
<td>Low recording API availability</td>
<td>(1 - max by(name, namespace, cluster_id)(avg_over_time(aggregator_unavailable_apiservice[5m]))) * 100 &lt; 90</td>
<td>5m</td>
<td>The availability of the recording API service in the last 5 minutes was below 90%</td>
</tr>
<tr>
<td>APIServer fault</td>
<td>absent(sum(up{job="apiserver"}) by (cluster_id) &gt; 0)</td>
<td>5m</td>
<td>APIServer disappeared from the collection targets</td>
</tr>
<tr>
<td>Scheduler fault</td>
<td>absent(sum(up{job="kube-scheduler"}) by (cluster_id) &gt; 0)</td>
<td>15m</td>
<td>The scheduler disappeared from the collection targets</td>
</tr>
<tr>
<td>Controller manager fault</td>
<td>absent(sum(up{job="kube-controller-manager"}) by (cluster_id) &gt; 0)</td>
<td>15m</td>
<td>The controller manager disappeared from the collection targets</td>
</tr>
</tbody></table>



## Kubelet

<table>
<thead>
<tr>
<th width="10%">Rule Name</th>
<th width="50%">Rule Expression</th>
<th width="10%">Duration</th>
<th width="30%">Description</th>
</tr>
</thead>
<tbody><tr>
<td>Exceptional node status</td>
<td>kube_node_status_condition{job=~".*kube-state-metrics",condition="Ready",status="true"} == 0</td>
<td>15m</td>
<td>The node status is exceptional for over 15 minutes</td>
</tr>
<tr>
<td>Unreachable node</td>
<td>kube_node_spec_taint{job=~".*kube-state-metrics",key="node.kubernetes.io/unreachable",effect="NoSchedule"} == 1</td>
<td>15m</td>
<td>The node is unreachable, and its workload will be scheduled again</td>
</tr>
<tr>
<td>Too many Pods running on node</td>
<td>count by(cluster_id, node) ((kube_pod_status_phase{job=~".*kube-state-metrics",phase="Running"} == 1) * on(instance,pod,namespace,cluster_id) group_left(node) topk by(instance,pod,namespace,cluster_id) (1, kube_pod_info{job=~".*kube-state-metrics"}))/max by(cluster_id, node) (kube_node_status_capacity_pods{job=~".*kube-state-metrics"} != 1) &gt; 0.95</td>
<td>15m</td>
<td>The number of Pods running on the node is close to the upper limit</td>
</tr>
<tr>
<td>Node status fluctuation</td>
<td>sum(changes(kube_node_status_condition{status="true",condition="Ready"}[15m])) by (cluster_id, node) &gt; 2</td>
<td>15m</td>
<td>The node status fluctuates between normal and exceptional</td>
</tr>
<tr>
<td>Imminent expiration of the kubelet client certificate</td>
<td>kubelet_certificate_manager_client_ttl_seconds &lt; 86400</td>
<td>None</td>
<td>The kubelet client certificate will expire in 24 hours</td>
</tr>
<tr>
<td>Imminent expiration of the kubelet server certificate</td>
<td>kubelet_certificate_manager_server_ttl_seconds &lt; 86400</td>
<td>None</td>
<td>The kubelet server certificate will expire in 24 hours</td>
</tr>
<tr>
<td>Kubelet client certificate renewal error</td>
<td>increase(kubelet_certificate_manager_client_expiration_renew_errors[5m]) &gt; 0</td>
<td>15m</td>
<td>An error occurred while renewing the kubelet client certificate</td>
</tr>
<tr>
<td>Kubelet server certificate renewal error</td>
<td>increase(kubelet_server_expiration_renew_errors[5m]) &gt; 0</td>
<td>15m</td>
<td>An error occurred while renewing the kubelet server certificate</td>
</tr>
<tr>
<td>Time-Consuming PLEG</td>
<td>histogram_quantile(0.99, sum(rate(kubelet_pleg_relist_duration_seconds_bucket[5m])) by (cluster_id, instance, le) * on(instance, cluster_id) group_left(node) kubelet_node_name{job="kubelet"}) &gt;= 10</td>
<td>5m</td>
<td>The 99th percentile of PLEG operation duration exceeds 10 seconds</td>
</tr>
<tr>
<td>Time-Consuming Pod start</td>
<td>histogram_quantile(0.99, sum(rate(kubelet_pod_worker_duration_seconds_bucket{job="kubelet"}[5m])) by (cluster_id, instance, le)) * on(cluster_id, instance) group_left(node) kubelet_node_name{job="kubelet"} &gt; 60</td>
<td>15m</td>
<td>The 99th percentile of Pod start duration exceeds 60 seconds</td>
</tr>
<tr>
<td>Kubelet fault</td>
<td>absent(sum(up{job="kubelet"}) by (cluster_id) &gt; 0)</td>
<td>15m</td>
<td>Kubelet disappeared from the collection targets</td>
</tr>
</tbody></table>




## Kubernetes Resource Use

<table>
<thead>
<tr>
<th width="10%">Rule Name</th>
<th width="50%">Rule Expression</th>
<th width="10%">Duration</th>
<th width="30%">Description</th>
</tr>
</thead>
<tbody><tr>
<td>Cluster CPU resource overload</td>
<td>sum by (cluster_id) (max by (cluster_id, namespace, pod, container) (kube_pod_container_resource_requests_cpu_cores{job=~".*kube-state-metrics"}) * on(cluster_id, namespace, pod) group_left() max by (cluster_id, namespace, pod) (kube_pod_status_phase{phase=~"Pending|Running"} == 1))/sum by (cluster_id) (kube_node_status_allocatable_cpu_cores)&gt;(count by (cluster_id) (kube_node_status_allocatable_cpu_cores)-1) / count by (cluster_id) (kube_node_status_allocatable_cpu_cores)</td>
<td>5m</td>
<td>Too many CPU cores are applied for by Pods in the cluster, and no more failed nodes can be tolerated</td>
</tr>
<tr>
<td>Cluster memory resource overload</td>
<td>sum by (cluster_id) (max by (cluster_id, namespace, pod, container) (kube_pod_container_resource_requests_memory_bytes{job=~".*kube-state-metrics"}) * on(cluster_id, namespace, pod) group_left() max by (cluster_id, namespace, pod) (kube_pod_status_phase{phase=~"Pending|Running"} == 1))/sum by (cluster_id) (kube_node_status_allocatable_memory_bytes) &gt; (count by (cluster_id) (kube_node_status_allocatable_memory_bytes)-1) / count by (cluster_id) (kube_node_status_allocatable_memory_bytes)</td>
<td>5m</td>
<td>Too much memory is applied for by Pods in the cluster, and no more failed nodes can be tolerated</td>
</tr>
<tr>
<td>Cluster CPU quota overload</td>
<td>sum by (cluster_id) (kube_resourcequota{job=~".*kube-state-metrics", type="hard", resource="cpu"})/sum by (cluster_id) (kube_node_status_allocatable_cpu_cores) &gt; 1.5</td>
<td>5m</td>
<td>The CPU quota in the cluster exceeds the total number of allocable CPU cores</td>
</tr>
<tr>
<td>Cluster memory quota overload</td>
<td>sum by (cluster_id) (kube_resourcequota{job=~".*kube-state-metrics", type="hard", resource="memory"}) /  sum by (cluster_id) (kube_node_status_allocatable_memory_bytes) &gt; 1.5</td>
<td>5m</td>
<td>The memory quota in the cluster exceeds the total amount of allocable memory</td>
</tr>
<tr>
<td>Imminent runout of quota resources</td>
<td>sum by (cluster_id, namespace, resource) kube_resourcequota{job=~".*kube-state-metrics", type="used"} / sum by (cluster_id, namespace, resource) (kube_resourcequota{job=~".*kube-state-metrics", type="hard"} &gt; 0) &gt;= 0.9</td>
<td>15m</td>
<td>The quota resource utilization exceeds 90%</td>
</tr>
<tr>
<td>High proportion of restricted CPU execution cycles</td>
<td>sum(increase(container_cpu_cfs_throttled_periods_total{container!="", }[5m])) by (cluster_id, container, pod, namespace) /sum(increase(container_cpu_cfs_periods_total{}[5m])) by (cluster_id, container, pod, namespace) &gt; ( 25 / 100 )</td>
<td>15m</td>
<td>The proportion of restricted CPU execution cycles is high</td>
</tr>
<tr>
<td>High Pod CPU utilization</td>
<td>sum(rate(container_cpu_usage_seconds_total{job="kubelet", metrics_path="/metrics/cadvisor", image!="", container!="POD"}[1m])) by (cluster_id, namespace, pod, container) / sum(kube_pod_container_resource_limits_cpu_cores) by (cluster_id, namespace, pod, container) &gt; 0.75</td>
<td>15m</td>
<td>The Pod CPU utilization exceeds 75%</td>
</tr>
<tr>
<td>High Pod memory utilization</td>
<td>sum(rate(container_memory_working_set_bytes{job="kubelet", metrics_path="/metrics/cadvisor", image!="", container!="POD"}[1m])) by (cluster_id, namespace, pod, container) /sum(kube_pod_container_resource_limits_memory_bytes) by (cluster_id, namespace, pod, container) &gt; 0.75</td>
<td>15m</td>
<td>The Pod memory utilization exceeds 75%</td>
</tr>
</tbody></table>



## Kubernetes Workload

<table>
<thead>
<tr>
<th width="10%">Rule Name</th>
<th width="50%">Rule Expression</th>
<th width="10%">Duration</th>
<th width="30%">Description</th>
</tr>
</thead>
<tbody><tr>
<td>Frequent Pod restarts</td>
<td>increase(kube_pod_container_status_restarts_total{job=~".*kube-state-metrics"}[5m]) &gt; 0</td>
<td>15m</td>
<td>The Pod was frequently restarted in the last 5 minutes</td>
</tr>
<tr>
<td>Exceptional Pod status</td>
<td>sum by (namespace, pod, cluster_id) (max by(namespace, pod, cluster_id) (kube_pod_status_phase{job=~".*kube-state-metrics", phase=~"Pending|Unknown"}) * on(namespace, pod, cluster_id) group_left(owner_kind) topk by(namespace, pod) (1, max by(namespace, pod, owner_kind, cluster_id) (kube_pod_owner{owner_kind!="Job"}))) &gt; 0</td>
<td>15m</td>
<td>The Pod is in the `NotReady` status for over 15 minutes</td>
</tr>
<tr>
<td>Exceptional container status</td>
<td>sum by (namespace, pod, container, cluster_id) (kube_pod_container_status_waiting_reason{job=~".*kube-state-metrics"}) &gt; 0</td>
<td>1h</td>
<td>The container is in the `Waiting` status for a long period of time</td>
</tr>
<tr>
<td>Deployment version mismatch</td>
<td>kube_deployment_status_observed_generation{job=~".*kube-state-metrics"} !=kube_deployment_metadata_generation{job=~".*kube-state-metrics"}</td>
<td>15m</td>
<td>The Deployment version is different from the set version, which indicates that the Deployment change hasn't taken effect</td>
</tr>
<tr>
<td>Deployment replica quantity mismatch</td>
<td>(kube_deployment_spec_replicas{job=~".*kube-state-metrics"} != kube_deployment_status_replicas_available{job=~".*kube-state-metrics"}) and (changes(kube_deployment_status_replicas_updated{job=~".*kube-state-metrics"}[5m]) == 0)</td>
<td>15m</td>
<td>The actual number of replicas is different from the set number of replicas</td>
</tr>
<tr>
<td>StatefulSet version mismatch</td>
<td>kube_statefulset_status_observed_generation{job=~".*kube-state-metrics"} != kube_statefulset_metadata_generation{job=~".*kube-state-metrics"}</td>
<td>15m</td>
<td>The StatefulSet version is different from the set version, which indicates that the StatefulSet change hasn't taken effect</td>
</tr>
<tr>
<td>StatefulSet replica quantity mismatch</td>
<td>(kube_statefulset_status_replicas_ready{job=~".*kube-state-metrics"} != kube_statefulset_status_replicas{job=~".*kube-state-metrics"}) and ( changes(kube_statefulset_status_replicas_updated{job=~".*kube-state-metrics"}[5m]) == 0)</td>
<td>15m</td>
<td>The actual number of replicas is different from the set number of replicas</td>
</tr>
<tr>
<td>Ineffective StatefulSet update</td>
<td>(maxwithout(revision)(kube_statefulset_status_current_revision{job=~".*kube-state-metrics"}unlesskube_statefulset_status_update_revision{job=~".*kube-state-metrics"})*(kube_statefulset_replicas{job=~".*kube-state-metrics"}!=kube_statefulset_status_replicas_updated{job=~".*kube-state-metrics"})) and (changes(kube_statefulset_status_replicas_updated{job=~".*kube-state-metrics"}[5m])==0)</td>
<td>15m</td>
<td>The StatefulSet hasn't been updated on some Pods</td>
</tr>
<tr>
<td>Frozen DaemonSet change</td>
<td>((kube_daemonset_status_current_number_scheduled{job=~".*kube-state-metrics"}!=kube_daemonset_status_desired_number_scheduled{job=~".*kube-state-metrics"}) or (kube_daemonset_status_number_misscheduled{job=~".*kube-state-metrics"}!=0) or (kube_daemonset_updated_number_scheduled{job=~".*kube-state-metrics"}!=kube_daemonset_status_desired_number_scheduled{job=~".*kube-state-metrics"}) or (kube_daemonset_status_number_available{job=~".*kube-state-metrics"}!=kube_daemonset_status_desired_number_scheduled{job=~".*kube-state-metrics"})) and (changes(kube_daemonset_updated_number_scheduled{job=~".*kube-state-metrics"}[5m])==0)</td>
<td>15m</td>
<td>The DaemonSet change lasts more than 15 minutes</td>
</tr>
<tr>
<td>DaemonSet not scheduled on some nodes</td>
<td>kube_daemonset_status_desired_number_scheduled{job=~".*kube-state-metrics"} - kube_daemonset_status_current_number_scheduled{job=~".*kube-state-metrics"} &gt; 0</td>
<td>10m</td>
<td>The DaemonSet is not scheduled on some nodes</td>
</tr>
<tr>
<td>Faulty scheduling of DaemonSet on some nodes</td>
<td>kube_daemonset_status_number_misscheduled{job=~".*kube-state-metrics"} &gt; 0</td>
<td>15m</td>
<td>The DaemonSet is incorrectly scheduled to some nodes</td>
</tr>
<tr>
<td>Excessive Job execution</td>
<td>kube_job_spec_completions{job=~".*kube-state-metrics"} - kube_job_status_succeeded{job=~".*kube-state-metrics"}  &gt; 0</td>
<td>12h</td>
<td>The execution duration of the Job exceeds 12 hours</td>
</tr>
<tr>
<td>Job execution failure</td>
<td>kube_job_failed{job=~".*kube-state-metrics"}  &gt; 0</td>
<td>15m</td>
<td>Job execution failed</td>
</tr>
<tr>
<td>Mismatch between replica quantity and HPA</td>
<td>(kube_hpa_status_desired_replicas{job=~".*kube-state-metrics"} != kube_hpa_status_current_replicas{job=~".*kube-state-metrics"}) and changes(kube_hpa_status_current_replicas[15m]) == 0</td>
<td>15m</td>
<td>The actual number of replicas is different from that set in HPA</td>
</tr>
<tr>
<td>Number of replicas reaching maximum value in HPA</td>
<td>kube_hpa_status_current_replicas{job=~".*kube-state-metrics"} == kube_hpa_spec_max_replicas{job=~".*kube-state-metrics"}</td>
<td>15m</td>
<td>The actual number of replicas reaches the maximum value configured in HPA</td>
</tr>
<tr>
<td>Exceptional PersistentVolume status</td>
<td>kube_persistentvolume_status_phase{phase=~"Failed|Pending",job=~".*kube-state-metrics"} &gt; 0</td>
<td>15m</td>
<td>The PersistentVolume is in the `Failed` or `Pending` status</td>
</tr>
</tbody></table>


## Kubernetes Node

<table>
<thead>
<tr>
<th width="10%">Rule Name</th>
<th width="50%">Rule Expression</th>
<th width="10%">Duration</th>
<th width="30%">Description</th>
</tr>
</thead>
<tbody><tr>
<td>Imminent runout of filesystem space</td>
<td>(node_filesystem_avail_bytes{job="node-exporter",fstype!=""}/node_filesystem_size_bytes{job="node-exporter",fstype!=""}*100&lt;15 and predict_linear(node_filesystem_avail_bytes{job="node-exporter",fstype!=""}[6h],4*60*60)&lt;0 and node_filesystem_readonly{job="node-exporter",fstype!=""}==0)</td>
<td>1h</td>
<td>It is estimated that the filesystem space will be used up in 4 hours</td>
</tr>
<tr>
<td>High filesystem space utilization</td>
<td>(node_filesystem_avail_bytes{job="node-exporter",fstype!=""}/node_filesystem_size_bytes{job="node-exporter",fstype!=""}*100&lt;5 and node_filesystem_readonly{job="node-exporter",fstype!=""}==0)</td>
<td>1h</td>
<td>The available filesystem space is below 5%</td>
</tr>
<tr>
<td>Imminent runout of filesystem inodes</td>
<td>(node_filesystem_files_free{job="node-exporter",fstype!=""}/node_filesystem_files{job="node-exporter",fstype!=""}*100&lt;20 and predict_linear(node_filesystem_files_free{job="node-exporter",fstype!=""}[6h],4*60*60)&lt;0 and node_filesystem_readonly{job="node-exporter",fstype!=""}==0)</td>
<td>1h</td>
<td>It is estimated that the filesystem inodes will be used up in 4 hours</td>
</tr>
<tr>
<td>High filesystem inode utilization</td>
<td>(node_filesystem_files_free{job="node-exporter",fstype!=""}/node_filesystem_files{job="node-exporter",fstype!=""}*100&lt;3 and node_filesystem_readonly{job="node-exporter",fstype!=""}==0)</td>
<td>1h</td>
<td>The proportion of available inodes is below 3%</td>
</tr>
<tr>
<td>Unstable network interface status</td>
<td>changes(node_network_up{job="node-exporter",device!~"veth.+"}[2m])</td>
<td>2m</td>
<td>The network interface status is unstable and frequently changes between "up" and "down"</td>
</tr>
<tr>
<td>Network interface data reception error</td>
<td>increase(node_network_receive_errs_total[2m]) &gt; 10</td>
<td>1h</td>
<td>An error occurred while the network interface received data</td>
</tr>
<tr>
<td>Network interface data sending error</td>
<td>increase(node_network_transmit_errs_total[2m]) &gt; 10</td>
<td>1h</td>
<td>An error occurred while the network interface sent data</td>
</tr>
<tr>
<td>Unsynced server clock</td>
<td>min_over_time(node_timex_sync_status[5m]) == 0</td>
<td>10m</td>
<td>The server time has not been synced recently. Please check whether NTP is correctly configured</td>
</tr>
<tr>
<td>Server clock skew</td>
<td>(node_timex_offset_seconds&gt;0.05 and deriv(node_timex_offset_seconds[5m])&gt;=0) or (node_timex_offset_seconds&lt;-0.05 and deriv(node_timex_offset_seconds[5m])&lt;=0)</td>
<td>10m</td>
<td>The server clock skew exceeds 300 seconds. Please check whether NTP is correctly configured</td>
</tr>
</tbody></table>

