
## TKE Kubernetes 1.16.3 revisions
<table><thead>
<tr><th width="13%">Date</th><th width="13%">Version</th><th width="74%">Updates</th></tr>
</thead>
<tbody>
<tr>
	<td>2020-03-11</td>
	<td>v1.16.3-tke.3</td>
	<td><ul class="params"><li>Fixes an issue where CBS intree continues to unmount a non-existing disk, which causes a large number of invalid requests.</li> <li>Adds a local cache for metadata.</li></ul></td>
</tr>
<tr>
	<td>2020-02-14</td>
	<td>v1.16.3-tke.2</td>
	<td><ul class="params"><li>Merges<a href="https://github.com/google/cadvisor/pull/2359" target="_blank"> pr2359</a>, which fixes the issue with missing monitoring records when the system is unable to obtain docker root.</li><li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/86583" target="_blank"> pr86583</a>, which increases the logging level to reduce the amount of logs caused by the lack of support for random-fully in earlier versions of iptables.</li><li>kube-scheduler now supports dynamic logging level configuration.</li><li>Produces a workaround for the missing CBS device path (/dev/disk/by-id/virtio-xxx/...) issue, which prevented some users from accessing cbs.</li><li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/86230" target="_blank"> pr86230</a>, which skips assumed pod updates when scheduling pods.</li></ul></td>
</tr>
<tr>
	<td>2020-01-06</td>
	<td>v1.16.3-tke.1</td>
	<td><ul class="params"><li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/79036" target="_blank"> pr79036</a>, which fixes an issue where cpumanager disables `cpu quota` when it opens if the `QoS` setting of a pod is `Guaranteed`.</li><li> Merges<href="https://github.com/kubernetes/kubernetes/pull/84167" target="_blank"> pr84167</a>, which fixes an issue where an incorrect ETCD prefix causes apiserver health check to fail.</li><li>Reverts <a href="https://github.com/kubernetes/kubernetes/pull/63066" target="_blank"> pr63066</a>, which caused an issue with IPVS and CLB health checks.</li><li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/72914" target="_blank"> pr72914</a>, which fixes an issue where, if you delete a Pod, create a new one and schedule it to the same node, mounting may fail.</li><li>Fixes an issue where creating containers in CentOS results in cgroup leakage.</li><li>Fixes an issue where upgrading lxcfs in Ubuntu 16 causes pods to exit.</li><li>Adds metadata cache and timeout. cloud-provider now supports using node names as hostnames.</li><li>Produces a workaround for the missing cbs device path (/dev/disk/by-id/virtio-xxx/...) issue, which prevented some users from accessing cbs.</li></ul></td>
</tr>
</tbody></table>

## TKE Kubernetes 1.14.3 revisions
<table>
<thead>
<tr><th width="13%">Date</th><th width="13%">Version</th><th width="74%">Updates</th></tr>
</thead>
<tbody>
<tr>
	<td>2020-01-13</td>
	<td>v1.14.3-tke.9</td>
	<td><ul class="params"><li>Merges<a href="https://github.com/google/cadvisor/pull/2359" target="_blank"> pr2359</a>, which fixes the issue with missing monitoring records when the system is unable to obtain docker root.</li> <li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/86583" target="_blank"> pr86583</a>, which increases the logging level to reduce the amount of logs caused by the lack of support for  random-fully in earlier versions of iptables.</li><li>kube-scheduler now supports dynamic logging level configuration.</li><li>Produces a workaround for the missing cbs device path (/dev/disk/by-id/virtio-xxx/...) issue which prevented some users from accessing cbs.</li><li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/86230" target="_blank"> pr86230</a>, which skips assumed pod updates when scheduling pods.</li></ul></td>
</tr>
<tr>
	<td>2019-11-28</td>
	<td>v1.14.3-tke.6</td>
	<td>cloud-provider now supports using node names as hostnames.</td>
</tr>
<tr>
	<td>2019-11-18</td>
	<td>v1.14.3-tke.5</td>
	<td><ul class="params"><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/83435" target="_blank">pr83435</a>, which fixes an issue that allowed DoS attacks that use malicious YAML or JSON to exhaust CPU or memory.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/84167" target="_blank">pr84167</a>, which fixes an issue where an incorrect ETCD prefix causes apiserver health checks to fail.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/75622" target="_blank">pr75622</a>, which fixes an issue where, when there is a high sts (&gt;2000) workload, it taks too long to sync sts changes to pod (about 20s).</li></ul></td>
</tr>
<tr>
	<td>2019-10-23</td>
	<td>v1.14.3-tke.4</td>
	<td>Merges <a href="https://github.com/kubernetes/kubernetes/pull/79036" target="_blank">pr79036</a>, which fixes an issue where cpumanager disables cpu quota when it opens if the QoS setting of a pod is Guaranteed.</td>
</tr>
<tr>
	<td>2019-09-10</td>
	<td>v1.14.3-tke.3</td>
	<td>Merges <a href="https://github.com/kubernetes/kubernetes/pull/63066" target="_blank">pr63066</a>, which fixes an issue where CLB health checks fail in IPVS mode.</td>
</tr>
<tr>
	<td>2019-09-06</td>
	<td>v1.14.3-tke.2</td>
	<td><ul class="params"><li>Fixes the <a href="https://discuss.kubernetes.io/t/security-release-of-kubernetes-v1-15-3-v1-14-6-v1-13-10-cve-2019-9512-and-cve-2019-9514/7596" target="_blank">cve-2019-9512&amp;cve-2019-9514</a>HTTP/S DDoS security issue.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/72914" target="_blank">pr72914</a>, which fixes an issue where, if you delete a Pod, create a new one and schedule it to the same node, mounting a volume may fail.</li><li>Resolves the issue where creating containers in CentOS resulted in cgroup leakage.</li></ul></td>
</tr>
</tbody></table>

## TKE Kubernetes 1.12.4 revisions

<table>
<thead>
<tr><th width="13%">Date</th><th width="13%">Version</th><th width="74%">Updates</th></tr>
</thead>
<tbody>
<tr>
	<td>2020-01-13</td>
	<td>v1.12.4-tke.16</td>
	<td><li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/2359" target="_blank"> pr2359</a>, which fixes the issue with missing monitoring records when the system is unable to obtain docker root.</li><li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/86583" target="_blank"> pr86583</a>, which increases the logging level to reduce the amount of logs caused by the lack of support for random-fully in earlier versions of iptables.</li><li> kube-scheduler now supports dynamic logging level configuration.</li><li>Produces a workaround for the missing CBS device path (/dev/disk/by-id/virtio-xxx/...) issue which prevented some users from accessing cbs.</li><li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/86230" target="_blank"> pr86230</a>, which skips assumed pod updates when scheduling pods.</li></td>
</tr>
<tr>
	<td>2019-12-23</td>
	<td>v1.12.4-tke.15</td>
	<td>Reverts <a href="https://github.com/kubernetes/kubernetes/pull/79036" target="_blank">pr79036</a>, which fixes an issue where cpumanager disables cpu quota when it opens if the QoS setting of a pod is Guaranteed.</td>
</tr>
<tr>
	<td>2019-12-17</td>
	<td>v1.12.4-tke.14</td>
	<td><ul class="params"> <li>Adds metadata cache and timeout.</li> <li>Fixes an issue where upgrading lxcfs in Ubuntu 16 causes pods to exit.</li><li>Adds the ability to reboot kubelet to avoid pod not ready.</li></ul></td>
</tr>
	<tr>
	<td>2019-11-28</td>
	<td>v1.12.4-tke.13</td>
	<td>cloud-provider now supports using node names as hostnames.</td>
	</tr>
<tr>
	<td>2019-11-18</td>
	<td>v1.12.4-tke.12</td>
	<td>Merges <a href="https://github.com/kubernetes/kubernetes/pull/75622" target="_blank">pr75622</a>, which fixes an issue where, when there is a high sts (&gt;2000) workload, it takes too long to to sync sts changes to pod (about 20s).</td>
</tr>
<tr>
	<td>2019-10-23</td>
	<td>v1.12.4-tke.11</td>
	<td><ul class="params"><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/79036" target="_blank">pr79036</a>, which fixes an issue where cpumanager disables cpu quota when it opens if the QoS setting of a pod is Guaranteed.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/72868" target="_blank">pr72866</a>, which adds a new parameter, <code>--metrics-port</code>, to kube-proxy and addresses the issue where <code>--metrics-bind-address</code> did not recognize port numbers.</li></ul></td>
</tr>
<tr>
	<td>2019-09-06</td>
	<td>v1.12.4-tke.10</td>
	<td><ul class="params"><li>Fixes the <a href="https://discuss.kubernetes.io/t/security-release-of-kubernetes-v1-15-3-v1-14-6-v1-13-10-cve-2019-9512-and-cve-2019-9514/7596" target="_blank">cve-2019-9512&amp;cve-2019-9514</a> HTTP/S DDoS security issue.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/72914" target="_blank">pr72914</a>, which fixes an issue where, if you delete a Pod, create a new one and schedule it to the same node, mounting may fail.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/71834" target="_blank">pr71834</a>, which fixes an issue with IPVS load balancing where, if sessionAffinity is set to ClientIP, traffic is routed to an invalid real server.</li></ul></td>
</tr>
<tr>
	<td>2019-08-09</td>
	<td>v1.12.4-tke.9</td>
	<td>Fixes an issue where creating containers in CentOS results in cgroup leakage.</td>
</tr>
<tr>
	<td>2019-08-08</td>
	<td>v1.12.4-tke.8</td>
	<td>Merges <a href="https://github.com/kubernetes/kubernetes/pull/72118" target="_blank">pr72118</a>, which fixes an issue where, if a CBS StatefulSet is rescheduled to the same node, it fails to mount.</td>
</tr>
<tr>
	<td>2019-07-17</td>
	<td>v1.12.4-tke.7</td>
	<td>Merges <a href="https://github.com/kubernetes/kubernetes/pull/75037" target="_blank">pr75037</a>, which solves a security issue affecting the cp command in kubectl.</td>
</tr>
<tr>
	<td>2019-07-16</td>
	<td>v1.12.4-tke.6</td>
	<td>Fixes a compatibility issue between the Linux kernel and IPVS load balancing, which caused CLB health checks to fail.</td>
</tr>
<tr>
	<td>2019-07-09</td>
	<td>v1.12.4-tke.5</td>
	<td>Merges <a href="https://github.com/kubernetes/kubernetes/pull/72361" target="_blank">pr72361</a>, which fixes a kube-proxy deadlock issue.</td>
</tr>
<tr>
	<td>2019-06-25</td>
	<td>v1.12.4-tke.4</td>
	<td>Fixes a Linux kernel and IPVS load balancing issue.</td>
</tr>
<tr>
	<td>2019-06-17</td>
	<td>v1.12.4-tke.3</td>
	<td>Merges <a href="https://github.com/kubernetes/kubernetes/pull/71114" target="_blank">pr71114</a>, which fixes an IPVS throughput issue.</td>
</tr>
<tr>
	<td>2019-06-04</td>
	<td>v1.12.4-tke.2</td>
	<td><ul class="params"><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/74755" target="_blank">pr74755</a>, which fixes a hang/timeout issue when running large numbers of pods with unique configmap/secret references.</li> <li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/69047" target="_blank">pr69047</a>, which fixes a backward compatibility issue with  <code>node.Spec.Unschedulable</code>.</li></ul></td>
</tr>
</tbody></table>

## TKE Kubernetes 1.10.5 revisions

<table>
<thead>
<tr><th width="13%">Date</th><th width="13%">Version</th><th width="74%">Updates</th></tr>
</thead>
<tbody><tr>
	<td>2020-01-13</td>
	<td>v1.10.5-tke.14</td>
	<td><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/2359" target="_blank">pr2359</a>, which fixes the issue with missing monitoring records when the system is unable to obtain docker root.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/86583" target="_blank">pr86583</a>, which increases the logging level reduce the amount of logs caused by the lack of support for random-fully in earlier versions of iptables.</li><li>kube-scheduler now supports dynamic logging level configuration.</li><li>Produces a workaround for the missing cbs device path (/dev/disk/by-id/virtio-xxx/...) issue which prevented some users from accessing cbs.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/86230" target="_blank">pr86230</a>, which skips assumed pod updates when scheduling pods.</li></td>
</tr>
<tr>
	<td>2019-12-23</td>
	<td>v1.12.4-tke.15</td>
	<td>Reverted <a href="https://github.com/kubernetes/kubernetes/pull/79036" target="_blank">pr79036</a>, which fixes an issue where cpumanager disables cpu quota when it opens if the QoS setting of a pod is Guaranteed.</td>
</tr>
<tr>
	<td>2019-12-17</td>
	<td>v1.12.4-tke.14</td>
	<td><ul class="params"> <li>Adds metadata cache and timeout.</li> <li>Fixes an issue where upgrading lxcfs in Ubuntu 16 causes pods to exit.</li><li>Adds the ability to reboot kubelet to avoid pod not ready.</li></ul></td>
</tr>
<tr>
	<td>2019-12-23</td>
	<td>v1.10.5-tke.13</td>
	<td>Reverted <a href="https://github.com/kubernetes/kubernetes/pull/79036" target="_blank">pr79036</a>, which fixes an issue where cpumanager disables cpu quota when it opens if the QoS setting of a pod is Guaranteed.</td>
</tr>
<tr>
	<td>2019-12-13</td>
	<td>v1.10.5-tke.12</td>
	<td><ul class="params"><li>kubelet does not delete nodes when checking externalID.</li> <li>Adds metadata cache and timeout.</li><li>Fixes an issue where upgrading lxcfs in Ubuntu 16 causes pods to exit.</li><li>Adds the ability to reboot kubelet to avoid pod not ready.</li></ul></td>
</tr>
<tr>
	<td>2019-11-18</td>
	<td>v1.10.5-tke.11</td>
	<td>Removes the kube-controller-manager probe that sends heartbeats to kubelet.</td>
</tr>
<tr>
	<td>2019-10-23</td>
	<td>v1.10.5-tke.10</td>
	<td><ul class="params"><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/79036" target="_blank">pr79036</a>, which fixes an issue where cpumanager disables cpu quota when it opens if the QoS setting of a pod is Guaranteed.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/72868" target="_blank">pr72866</a>, which adds a new parameter, <code>--metrics-port</code>, to kube-proxy to address the issue where <code>--metrics-bind-address</code> did not recognize port numbers.</li></ul></td>
</tr>
<tr>
	<td>2019-09-06</td>
	<td>v1.10.5-tke.9</td>
	<td><ul class="params"><li>Fixes the <a href="https://discuss.kubernetes.io/t/security-release-of-kubernetes-v1-15-3-v1-14-6-v1-13-10-cve-2019-9512-and-cve-2019-9514/7596" target="_blank">cve-2019-9512&amp;cve-2019-9514</a>  HTTP/S DDoS security issue.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/72914" target="_blank">pr72914</a>, which fixes an issue where, if you delete a Pod, create a new one and schedule it to the same node, mounting may fail.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/67430" target="_blank">67430</a>, to rollback the state if updateContainerCPUSet fails.</li></ul></td>
</tr>
<tr>
	<td>2019-08-08</td>
	<td>v1.10.5-tke.8</td>
	<td>Merges <a href="https://github.com/kubernetes/kubernetes/pull/72118" target="_blank">pr72118</a>, which fixes an issue where, if kubelet mounts a device immediately after unmounting it, an error occurs with the message `resource name may not be empty` is displayed.</td>
</tr>
<tr>
	<td>2019-07-17</td>
	<td>v1.10.5-tke.7</td>
	<td>Merges <a href="https://github.com/kubernetes/kubernetes/pull/75037" target="_blank">pr75037</a>, which fixes a security issue affecting the cp command in kubectl.</td>
</tr>
<tr>
	<td>2019-06-25</td>
	<td>v1.10.5-tke.6</td>
	<td>Fixes a Linux kernel and IPVS load balancing issue.</td>
</tr>
<tr>
	<td>2019-06-17</td>
	<td>v1.10.5-tke.5</td>
	<td>Merges <a href="https://github.com/kubernetes/kubernetes/pull/71114" target="_blank">pr71114</a>, which fixes an issue with IPVS throughput.</td>
</tr>
<tr>
	<td>2019-03-19</td>
	<td>v1.10.5-tke.4</td>
	<td>Merges <a href="https://github.com/kubernetes/kubernetes/pull/65092" target="_blank">pr65092</a>, which fixes an issue where apiserver panics when handling specific requests.</td>
</tr>
<tr>
	<td>2019-02-19</td>
	<td>v1.10.5-tke.3</td>
	<td>Merges <a href="https://github.com/kubernetes/kubernetes/pull/67288" target="_blank">pr67288</a>, which fixes an issue where apiserver does not close the other side of the connection immediately when proxying.</td>
</tr>
<tr>
	<td>2018-09-28</td>
	<td>v1.10.5-tke.2</td>
	<td>Moves load balancing logic from controller-manager to an independent service controllers.</td>
</tr>
<tr>
	<td>2018-09-27</td>
	<td>v1.10.5-tke.1</td>
	<td>Backported <a href="https://github.com/kubernetes/kubernetes/pull/63321" target="_blank">pr63321</a>, which fixes an issue where it took too long to terminate service containers when there were more than one in a pod.</td>
</tr>
<tr>
<td>2018-09-21</td>
<td>v1.10.5-qcloud-rev1</td>
<td>If a kubelet state update times out, controller-manager probes kubelet port.</td>
</tr>
</tbody></table>                                                

## TKE Kubernetes 1.8.13 revisions

<table>
<thead>
<tr><th width="13%">Date</th><th width="13%">Version</th><th width="74%">Updates</th></tr>
</thead>
<tbody>
<tr>
	<td>2020-01-13</td>
	<td>v1.8.13-tke.7</td>
	<td><ul class="params"><li>Merges<a href="https://github.com/google/cadvisor/pull/2359" target="_blank"> pr2359</a>, which fixes the issue with missing monitoring records when the system is unable to obtain docker root.</li><li>Produces a workaround for the missing cbs device path (/dev/disk/by-id/virtio-xxx/...) issue which prevented some users from accessing cbs.</li></ul></td>
</tr>
<tr>
	<td>2019-12-13</td>
	<td>v1.8.13-tke.6</td>
	<td><ul class="params"> <li>kubelet does not delete nodes when checking externalID.</li> <li>Adds metadata cache and timeout.</li><li>Fixes an issue where upgrading lxcfs in Ubuntu 16 causes pods to exit.</li><li>Adds the ability to reboot kubelet to avoid pod not ready.</li></ul></td>
</tr>
<tr>
	<td>2019-11-18</td>
	<td>v1.8.13-tke.5</td>
	<td><ul class="params"><li>Removes the kube-controller-manager probe that sends heartbeats to kubelet.</li><li>Adds metric to CBS PVC.</li></ul></td>
</tr>
<tr>
	<td>2018-09-28</td>
	<td>v1.8.13-tke.2</td>
	<td>Moves load balancing logic from controller-manager to an independent service controllers.</td>
</tr>
<tr>
	<td>2018-09-27</td>
	<td>v1.8.13-tke.1</td>
	<td><ul class="params"><li>Disabled kmem statistics to prevent cgroup numbers from leaking.</li><li>Reduced resourcequota conflicts caused by creating pods.</li></ul></td>
</tr>
<tr>
	<td>2018-09-21</td>
	<td>v1.8.13-qcloud-rev1</td>
	<td>If a kubelet state update times out, controller-manager probes kubelet port.</td>
</tr>
</tbody></table>

## TKE Kubernetes 1.7.8 revisions

<table>
<thead>
<tr><th width="13%">Date</th><th width="13%">Version</th><th width="74%">Updates</th></tr>
</thead>
<tbody>
<tr>
	<td>2019-12-17</td>
	<td>v1.7.8-tke.4</td>
	<td><ul class="params"> <li>kubelet does not delete nodes when checking externalID.</li> <li>Adds new metadata for cache and timeout.</li><li>Fixes an issue where upgrading lxcfs in Ubuntu 16 causes pods to exit.</li><li>Adds the ability to reboot kubelet to avoid pod not ready.</li></ul></td>
</tr>
<tr>
	<td>2018-09-28</td>
	<td>v1.7.8-tke.2</td>
	<td>Fixes a conflict between controller-manager and external service controller.</td>
</tr>
<tr>
	<td>2018-09-27</td>
	<td>v1.7.8-tke.1</td>
	<td>Moves load balancing logic from controller-manager to an independent service controllers.</td>
</tr>
	<tr>
	<td>2018-09-21</td>
	<td>v1.7.8-qcloud-rev1</td>
	<td>If a kubelet state update times out, controller-manager probes kubelet port.</td>
	</tr>
</tbody></table>

<style>
.params{
	margin-bottom:0px!important;
}
</style>
