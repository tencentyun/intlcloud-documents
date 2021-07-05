## TKE kubernetes 1.18.4 revisions

<table><thead>
<tr><th width="13%">Date</th><th width="13%">Version</th><th width="74%">Updates</th></tr>
</thead>
<tbody>
<tr>
    <td>2021-05-14</td>	
    <td>v1.18.4-tke.9</td>	
    <td><ul class="params">
<li>Ported <a href="https://github.com/kubernetes/kubernetes/pull/93370" rel="nofollow">pr93370</a> to support CronJobControllerV2. (kube-controller-manager)</li>
<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/100376" rel="nofollow">pr100376</a> to enable HTTP/2 health check, which prevented the issue that the underlying layer connection is closed but can still be used incorrectly. (kube-apiserver, kube-controller-manager, kube-scheduler, kubelet, kube-proxy, kubectl)</li>
<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/100317" rel="nofollow">pr100317</a>, which fixed the issue where CVE-2021-25735 node updates might bypass the Validating Admission Webhook. (kube-apiserver)</li>
<li>When TKE cluster adds the virtual node, ComputeResource, EKS ClusterIP, and HPA are supported. (kube-controller-manager, kube-scheduler)</li>
</ul></td>
</tr>
<tr>
    <td>2021-04-02</td>	
    <td>v1.18.4-tke.8</td>	
    <td><ul class="params">
<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/97752" rel="nofollow">pr97752</a>, which fixed the issue where NewReplicaSet is displayed as <code>&lt;none&gt;</code> when describing deployment (kubectl).</li>
<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/93808" rel="nofollow">pr93808</a>, which fixed the issue where unnecessary information is returned when <code>kube-scheduler --version</code> is executed (kube-scheduler).</li>
<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/91590" rel="nofollow">pr91590</a>, which fixed the issue of warning that the port has been allocated when using the multiprotocol service of NodePort type (kube-apiserver).</li>
<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/98262" rel="nofollow">pr98262</a>, which allows kube-controller-manager to dynamically adjust the log level (kube-controller-manager).</li>
<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/95154" rel="nofollow">pr95154</a>, which fixed the issue where kube-scheduler snapshot contains the nodes being deleted (kube-scheduler).</li>
<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/95711" rel="nofollow">pr95711</a>, which fixed the issue where kubectl drain command occupies too much CPU (kubectl).</li>
<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/96602" rel="nofollow">pr96602</a>, which fixed the issue where apiserver memory leaks before or after the time gaps (kube-apiserver).</li>
<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/97023" rel="nofollow">pr97023</a>, which deletes the related metadata directory when unmounting an emptyDir type volume (kubelet).</li>
<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/97527" rel="nofollow">pr97527</a>, which fixed the issue where map access operations are not synchronized in cpumanager (kubelet).</li>
<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/100190" rel="nofollow">pr100190</a>, which automatically deletes the volume directory left by orphaned Pod (kubelet).</li>
<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/92614" rel="nofollow">pr92614</a>, when all containers of the Pod whose restart policy is RestartPolicyOnFailure exit successfully, no new sandbox will be created (kubelet).</li>
<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/94833" rel="nofollow">pr94833</a>, which fixed the issue where the image tag does not match in status when Pod image has multiple tags (kubelet).</li>
	        </ul></td>
</tr>
<tr>
    <td>2020-12-28</td>	
    <td>v1.18.4-tke.6 (ARM clusters are supported starting from this version)</li></td>	
    <td><ul class="params">
		<li>Added metrics to QcloudCbs (kube-controller-manager).</li>
	        <li>Fixed the issue where extra space exists in the value of serial when mounting CBS disk (Kubelet).</li>
	        </ul></td>
</tr>
<tr>
    <td>2020-12-21</td>	
    <td>v1.18.4-tke.5</td>	
    <td><ul class="params">
		<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/94712">pr94712</a>, which fixed CVE-2020-8564 - fixed the issue when the file format was incorrect and logLevel >= 4, Docker configuration leaked (kubelet).</li>
		<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/95316">pr95316</a>, which fixed CVE-2020-8565 - fixed the issue where incomplete fix for CVE-2019-11250 resulting in log token leak (logLevel >= 9) (kube-apiserver, kubectl).</li>
		<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/95245">pr95245</a>, which fixed CVE-2020-8566 - fixed the issue where Ceph RBD adminSecrets was exposed in the log when loglevel >= 4 (kube-controller-manager).</li>
		<li>Fixed the issue where restarting kubelet caused Pod readiness check failed (kubelet).</li>
		<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/90825">pr90825</a>, which fixed the issue where the pop operation of the fifo queue in client-go might be stuck due to race condition, which caused the pod to remain in the pending state (kubelet).</li>
		<li>The scheduler supports virtual nodes (kube-scheduler).</li>
		<li>kube-controller-manager supports virtual nodes (kube-controller-manager).</li>
		<li>Set the instance-type label based on the actual model of the node, instead of being fixed as QCLOUD (kubelet).</li>
		<li>Added the CBS to OpenAPI (kube-apiserver).</li>
		<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/91126">pr91126</a>, which fixed the issue where the scheduler cache was inconsistent when Pod had the same name but different UID (kube-scheduler).</li>
		<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/93387">pr93387</a>, which fixed the issue where the daemonset pod could not be scheduled to nodes due to the disorder of node cache information in the scheduler (kube-scheduler).</li>
                <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/89465">pr89465</a>, which fixed the issue where the HPA based on Pod metrics incorrectly calculated the number of instances during rolling updates (kube-controller-manager).</li>
	        </ul></td>
</tr>
<tr>
    <td>2020-10-13</td>	
    <td>v1.18.4-tke.3</td>	
    <td><ul class="params">
		<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/89629">pr89629</a>, which fixed the issue where the container that mounted the subpath would fail to restart after the configmap is changed (kubelet).</li>
	        <li>QcloudCbs supports BulkVolumeVerification (kube-controller-manager).</li>
	        <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/94430">pr94430</a>, which fixed the issue where the client-go reflector could not detect the "Too large resource version" error (kubelet).</li></ul></td>
</tr>
<tr>
    <td>2020-08-12</td>	
    <td>v1.18.4-tke.2</td>	
    <td><ul class="params">
		<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/93403">pr93403</a>, which removed the printed error information of pod condition irrelevant to the kubelet during kubelet update (kubelet).</li></ul></td>
</tr>
<tr>
    <td>2020-08-04</td>	
    <td>v1.18.4-tke.1</td>	
    <td><ul class="params"><li>revert <a href="https://github.com/kubernetes/kubernetes/pull/63066">pr63066 </a>Fixed the LB health check and IPVS issues (kube-proxy).</li>
    <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/93403">pr72914</a>, which fixed the issue where mounting might fail if you deleted a pod, created a new one, and scheduled it to the same node (kube-controller-manager).</li>
    <li>Fixed the issue where creating containers in CentOS resulted in cgroup leakage (kubelet).</li>
    <li>Fixed the issue where upgrading lxcfs in Ubuntu 16 caused pods to exit (kubelet).</li>
    <li>metadata added cache and timeout. cloud-provider now supports using node names as hostnames (kubelet).</li>
    <li>metadata added local cache (kubelet).</li>
    <li>Incorporated CBS and relevant fixing code (kubelet).</li>
    <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/90260">pr90260</a>, which fixed the issue of missing monitoring records for containerd cluster networks (kubelet).</li>
    <li>TKE can perceive the maximum number of qcloudcbs that can be mounted to a single node. In 1.12 and later versions, the value is maxAttachCount-2. In version 1.10, the value is 18 by default (kube-scheduler).</li>
    <li>Fixed the issue where CBS intree continued to unmount a non-existent disk, causing a large number of invalid requests (kubelet).</li>
    <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/2359">pr2359</a>, which fixed the issue with missing monitoring records when the system was unable to obtain docker root (kubelet).</li>
    <li>kube-scheduler now supports dynamic logging level configuration (kube-scheduler).</li>
    <li>Produced a workaround for the missing CBS device path (/dev/disk/by-id/virtio-xxx/...) issue that prevents some users from accessing CBS properly (kubelet).</li>
    <li>TKE can perceive the maximum number of qcloudcbs that can be mounted to a single node. The kubelet side will not patch node (kubelet).</li>
    <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/89296">pr89296</a>, so that the log will not record whether the iptables random-fully parameter is enabled (kube-proxy).</li>
    <li>Fixed the aws issue <a href="https://github.com/kubernetes/kubernetes/pull/92162">pr92162</a>(kubelet).</li>
    <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/91277">pr91277</a>, which prevents the issue of large numbers of TLS handshake error logs generated by kube-apiserver as a result of CLB health checks (kube-apiserver).</li>
    <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/91500">pr91500</a>, which fixed the issue of missing environmental variables of KUBERNETES_SERVICE_HOST (kubelet).</li>
    <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/92537">92537</a>, which fixed the issue where client-go reflector could not recover from the error "Too large resource version" (kube-apiserver, kube-controller-manager, kube-scheduler, kubelet, and kube-proxy).</li>
    <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/92969">pr92969</a>, which fixed the issue where CVE-2020-8559 privilege escalation from an invaded node resulted in invasion into other nodes (kube-apiserver).</li>
    <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/92921">pr92921</a>, which fixed the DOS attack issue where CVE-2020-8557 exhausted the disk space by writing into “/etc/hosts” (kubelet).</li></ul></td>
</tr>
</tbody></table>




## TKE kubernetes 1.16.3 revisions
<table><thead>
<tr><th width="13%">Date</th><th width="13%">Version</th><th width="74%">Updates</th></tr>
</thead>
<tbody>
<tr>
    <td>2021-05-24</td>	
    <td>v1.16.3-tke.17</td>	
    <td><ul class="params">
<li>Ported <a href="https://github.com/kubernetes/kubernetes/pull/93370" rel="nofollow">pr93370</a> to support CronJobControllerV2. (kube-controller-manager)</li>
<li>When the TKE cluster adds the virtual node, the local replicas can be retained. (kube-scheduler)</li>
	        </ul></td>
</tr>	
<tr>
    <td>2021-05-06</td>	
    <td>v1.16.3-tke.16</td>	
    <td><ul class="params">
<li>Updated the launch method of running kube-proxy as an image, and automatically adapted to the iptables running mode of the node to support the operating system that uses the NF_TABLES mode to run iptables by default.</li>
	        </ul></td>
</tr>	
<tr>
    <td>2021-04-14</td>	
    <td>v1.16.3-tke.15</td>	
    <td><ul class="params">
<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/97752" rel="nofollow">pr97752</a>, which fixed the issue where NewReplicaSet is displayed as <code>&lt;none&gt;</code> when describing deployment (kubectl).</li>
<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/92614" rel="nofollow">pr92614</a>, when all containers of the Pod whose restart policy is RestartPolicyOnFailure exit successfully, no new sandbox will be created (kubelet).</li>
<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/91590" rel="nofollow">pr91590</a>, which fixed the issue of warning that the port has been allocated when using the multiprotocol service of NodePort type (kube-apiserver).</li>
<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/98262" rel="nofollow">pr98262</a>, which allows you to use kube-controller-manager to dynamically adjust the log level (kube-controller-manager).</li>
<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/95301" rel="nofollow">pr95301</a>, which automatically deletes the volume directory left by orphaned Pod (kubelet).</li>
	        </ul></td>
</tr>	
<tr>
    <td>2020-12-28</td>	
    <td>v1.16.3-tke.14</td>	
    <td><ul class="params">
		<li>Added metrics to QcloudCbs (kube-controller-manager).</li>
	        <li>Fixed the issue where extra space exists in the value of serial when mounting CBS disk (Kubelet).</li>
	        </ul></td>
</tr>		
<tr>
    <td>2020-12-21</td>	
    <td>v1.16.3-tke.13</td>	
    <td><ul class="params">
		<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/94712">pr94712</a>, which fixed CVE-2020-8564 - fixed the issue when the file format was incorrect and logLevel >= 4, Docker configuration leaked (kubelet).</li>
		<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/95316">pr95316</a>, which fixed CVE-2020-8565 - fixed the issue where incomplete fix for CVE-2019-11250 resulting in log token leak (logLevel >= 9) (kube-apiserver, kubectl).</li>
		<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/95245">pr95245</a>, which fixed CVE-2020-8566 - fixed the issue where Ceph RBD adminSecrets was exposed in the log when loglevel >= 4 (kube-controller-manager).</li>
	        <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/86191">pr86191</a>, which fixed the issue where Pod might be in the wrong state when the node was restarted (kubelet).</li>
                <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/86140">pr86140</a>, which fixed the issue where the Controller Manager did not handle the timeout error correctly, so that the expanded pod could not be created (kube-controller-manager).</li>
	        <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/90825">pr90825</a>, which fixed the issue where the pop operation of the fifo queue in client-go might be stuck due to race condition, which caused the Pod to remain in the pending state (kubelet).</li>
	        <li>The scheduler supports virtual nodes (kube-scheduler).</li>
		<li>kube-controller-manager supports virtual nodes (kube-controller-manager).</li>
		<li>Set the instance-type label based on the actual model of the node, instead of being fixed as QCLOUD (kubelet).</li>
		<li>Added the CBS to OpenAPI (kube-apiserver).</li>
	        <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/81344">pr81344</a>, which fixed the issue where the CPU Manager did not support SourcesReady (kubelet).</li>
		<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/91126">pr91126</a>, which fixed the issue where the scheduler cache was inconsistent when Pod had the same name but different UID (kube-scheduler).</li>
	        <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/89224">pr89224</a>, which fixed the issue where kube-scheduler restarted abnormally because NodeInfo did not check (kube-scheduler).</li>
                <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/89465">pr89465</a>, which fixed the issue where the HPA based on Pod metrics incorrectly calculated the number of instances during rolling updates (kube-controller-manager).</li>
                </ul></td>
</tr>	    
<tr>
    <td>2020-10-13</td>	
    <td>v1.16.3-tke.11</td>	
    <td><ul class="params">
	    <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/92971">pr92971</a>, which fixed the issue where CVE-2020-8559 privilege escalation from an invaded node resulted in invasion into other nodes (kube-apiserver).</li>
	    <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/92924">pr92924</a>, which fixed the DOS attack issue where CVE-2020-8557 exhausted the disk space by writing into /etc/hosts (kubelet).</li>
	    <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/93403">pr93403</a>, which removed the printed error information of pod condition irrelevant to the kubelet during kubelet update (kubelet).</li>
	    <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/89629">pr89629</a>, which fixed the issue where the container that mounted the subpath would fail to restart after the configmap is changed (kubelet).</li>
	    <li>QcloudCbs supports BulkVolumeVerification (kube-controller-manager).</li>
	    <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/84998">pr84998</a>, which resolved the issue where the corresponding node lease object might be rebuilt after the node was deleted and caused junk data (kubelet).</li></ul></td>
</tr>
<tr>
    <td>2020-07-28</td>	
    <td>v1.16.3-tke.10</td>	
    <td><ul class="params"><li>Incorporated <a href="https://github.com/kubernetes/kubernetes/pull/91277">pr91277</a>, which prevents the issue of large numbers of TLS handshake error logs generated by kube-apiserver as a result of CLB health checks (kube-apiserver).</li><li>Incorporated <a href="https://github.com/kubernetes/kubernetes/pull/91500">pr91500</a>, which fixed the issue of missing environmental variables of KUBERNETES_SERVICE_HOST (kubelet).</li></ul></td>
</tr>
<tr>
    <td>2020-06-17</td>	
    <td>v1.16.3-tke.9</td>	
    <td>Temporarily fixes the AWS issue<a href="https://github.com/kubernetes/kubernetes/issues/92162">pr92162</a>. AWS Credential Provider is no longer registered to prevent this issue from causing slow node launches.</td>
</tr>
<tr>
    <td>2020-06-11</td>	
    <td>v1.16.3-tke.8</td>	
    <td>Merges <a href="https://github.com/kubernetes/kubernetes/pull/85993">pr85993</a>, which allows you to use CNI results to set kubenet gateway addresses.</td>
</tr>
<tr>
    <td>2020-06-10</td>	
    <td>v1.16.3-tke.7</td>	
    <td><ul class="params"><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/90260">pr90260</a>, which fixes the issue of missing monitoring records for containerd cluster networks.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/89515">pr89515</a>, which fixes the issue where HPA miscalculates the number of pods during rolling updates.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/91252">pr91252</a>, which ignores Pod Condition updates generated by other components to avoid unnecessary scheduling.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/89794">pr89794</a>, which clears kube-controller-manager error logs to avoid CVE-2020-8555 Half-Blind SSRF attacks.</li></ul></td>
</tr>
<tr>
    <td>2020-05-18</td>	
    <td>v1.16.3-tke.6</td>	
    <td>TKE can perceive the maximum number of qcloudcbs that can be mounted to a single node. The max value cannot be dynamically obtained.</td>
</tr>
<tr>
    <td>2020-04-20</td>	
    <td>v1.16.3-tke.5</td>	
    <td>Merges<a href="https://github.com/kubernetes/kubernetes/pull/69047"> pr69047</a>, which fixes the <code>node.Spec.Unschedulable</code> backward compatibility issue. (This fix is overwritten when the in-tree cbs code is incorporated).</td>
</tr>
<tr>
    <td>2020-04-14</td>
    <td>v1.16.3-tke.4</td>
    <td><ul class="params"><li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/87913"> pr87913</a>, which fixes the CVE-2020-8551: Kubelet DoS attack issue.</li><li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/87669"> pr87669</a>, which fixes the CVE-2020-8552: apiserver DoS attack issue.</li><li>TKE can perceive the maximum number of qcloudcbs that can be mounted to a single node. (In 1.12 and later versions, the value is maxAttachCount-2. In version 1.10, the value is 18 by default).</li><li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/87467"> pr87467</a>, which fixes the issue of excessive CPU consumption by kubectl in parsing YAML files when an authorized user sends a malicious YAML file.</li></ul></td>
</tr>
<tr>
	<td>2020-03-11</td>
	<td>v1.16.3-tke.3</td>
	<td><ul class="params"><li>Fixed the issue where CBS intree continued to unmount a non-existent disk, which caused a large number of invalid requests.</li> <li>Added a local metadata cache.</li></ul></td>
</tr>
<tr>
	<td>2020-02-14</td>
	<td>v1.16.3-tke.2</td>
	<td><ul class="params"><li>Merges<a href="https://github.com/google/cadvisor/pull/2359" target="_blank"> pr2359</a>, which fixes the issue of missing monitoring records when the system is unable to obtain docker root.</li><li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/86583" target="_blank"> pr86583</a>, which increases the logging level to reduce the amount of logs caused by the lack of support for random-fully in earlier versions of iptables.</li><li>kube-scheduler now supports dynamic logging level configuration.</li><li>Produces a workaround for the missing CBS device path (/dev/disk/by-id/virtio-xxx/...) issue that prevents some users from accessing CBS properly.</li><li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/86230" target="_blank"> pr86230</a>, which skips assumed pod updates when pods are scheduled.</li></ul></td>
</tr>
<tr>
	<td>2020-01-06</td>
	<td>v1.16.3-tke.1</td>
	<td><ul class="params"><li>Incorporates<a href="https://github.com/kubernetes/kubernetes/pull/79036" target="_blank"> pr79036</a>, which fixes the issue where upon being opened, the CPU Manager disables the CPU quota if the QoS setting of a pod is Guaranteed.</li><li>Incorporates<href="https://github.com/kubernetes/kubernetes/pull/84167" target="_blank"> pr84167</a>, which fixes the issue where an incorrect Etcd key prefix causes an apiserver health check failure.</li><li>Reverts<a href="https://github.com/kubernetes/kubernetes/pull/63066" target="_blank"> pr63066</a>, which fixes the CLB health check and IPVS issues.</li><li>Incorporates<a href="https://github.com/kubernetes/kubernetes/pull/72914" target="_blank"> pr72914</a>, which fixes the issue where mounting may fail if you delete a pod, create a new one, and schedule it to the same node.</li><li>Fixes the issue where creating containers in CentOS results in cgroup leakage.</li><li>Fixes the issue where upgrading lxcfs in Ubuntu 16 causes pods to exit.</li><li>Adds metadata cache and timeout. cloud-provider now supports using node names as hostnames.</li><li>Reverts pr79036, which fixes the issue where upon being opened, the CPU Manager disables the CPU quota if the QoS setting of a pod is Guaranteed.</li><li>Produces a workaround for the missing CBS device path (/dev/disk/by-id/virtio-xxx/...) issue that prevents some users from accessing CBS properly.</li></ul></td>
</tr>
</tbody></table>

## TKE kubernetes 1.14.3 revisions
<table>
<thead>
<tr><th width="13%">Date</th><th width="13%">Version</th><th width="74%">Revisions</th></tr>
</thead>
<tbody>
<tr>
    <td>2021-05-06</td>	
    <td>v1.14.3-tke.22</td>	
    <td>Updated the launch method of running kube-proxy as an image, and automatically adapted to the iptables running mode of the node to support the operating system that uses the NF_TABLES mode to run iptables by default.</td>
</tr>	
<tr>
    <td>2021-04-14</td>	
    <td>v1.14.3-tke.21</td>	
    <td><ul class="params">
	<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/97752" rel="nofollow">pr97752</a>, which fixed the issue where NewReplicaSet is displayed as <code>&lt;none&gt;</code> when describing deployment (kubectl).</li>
<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/78999" rel="nofollow">pr78999</a>, which fixed the issue of judging the case of the protocol during graceful close (kube-proxy).</li>
<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/91590" rel="nofollow">pr91590</a>, which fixed the issue of warning that the port has been allocated when using the multiprotocol service of NodePort type (kube-apiserver).</li>
<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/98262" rel="nofollow">pr98262</a>, which allows kube-controller-manager to dynamically adjust the log level (kube-controller-manager).</li>
<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/95301" rel="nofollow">pr95301</a>, which automatically deletes the volume directory left by orphaned Pod (kubelet).</li>
	        </ul></td>
</tr>	
<tr>
    <td>2020-12-28</td>	
    <td>v1.14.3-tke.19</td>	
    <td><ul class="params">
		<li>Added metrics to QcloudCbs (kube-controller-manager).</li>
	        <li>Fixed the issue where extra space exists in the value of serial when mounting CBS disk (Kubelet).</li>
	        </ul></td>
</tr>	
<tr>
    <td>2020-12-21</td>	
    <td>v1.14.3-tke.18</td>	
    <td><ul class="params">
		<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/94712">pr94712</a>, which fixed CVE-2020-8564 - fixed the issue when the file format was incorrect and logLevel >= 4, Docker configuration leaked (kubelet).</li>
		<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/95316">pr95316</a>, which fixed CVE-2020-8565 - fixed the issue where incomplete fix for CVE-2019-11250 resulting in log token leak (logLevel >= 9) (kube-apiserver, kubectl).</li>
		<li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/95245">pr95245</a>, which fixed CVE-2020-8566 - fixed the issue where Ceph RBD adminSecrets was exposed in the log when loglevel >= 4 (kube-controller-manager).</li>
	        <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/86140">pr86140</a>, which fixed the issue where the Controller Manager did not handle the timeout error correctly, so that the expanded Pod could not be created (kube-controller-manager).</li>
	        <li>The scheduler supports virtual nodes (kube-scheduler).</li>
	        <li>kube-controller-manager supports virtual nodes (kube-controller-manager).</li>
		<li>Set the instance-type label based on the actual model of the node, instead of being fixed as QCLOUD (kubelet).</li>
	        <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/79338">pr79338</a>, when both SupportPodPidsLimit and SupportNodePidsLimit are not enabled, the pids cgroup subsystem will not be enabled (kubelet).</li>
	        <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/89224">pr89224</a>, which fixed the issue where kube-scheduler restarted abnormally because NodeInfo is not checked (kube-scheduler).</li>
                <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/89465">pr89465</a>, which fixed the issue where the HPA based on Pod metrics incorrectly calculated the number of instances during rolling updates (kube-controller-manager).</li></ul></td>
</tr>	    
<tr>
    <td>2020-10-13</td>
    <td>v1.14.3-tke.17</td>
    <td><ul class="params">
	    <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/74781">pr74781</a>, which changed the default update strategy of ConfigMap and Secret from Cache to Watch (kubelet).</li>
	    <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/93403">pr93403</a>, which removed the printed error information of pod condition irrelevant to the kubelet during kubelet update (kubelet).</li>
	    <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/89629">pr89629</a>, which fixed the issue where the container that mounted the subpath would fail to restart after the configmap is changed (kubelet).</li>
	    <li>Merged <a href="https://github.com/kubernetes/kubernetes/pull/8094">pr80942</a>, which fixed the issue where rules were not deleted after the service was deleted in ipvs mode (kube-proxy).</li>
            <li>QcloudCbs supports BulkVolumeVerification (kube-controller-manager).</li></ul></td>
</tr>
<tr>
    <td>2020-08-04</td>
    <td>v1.14.3-tke.16</td>
    <td>Merged <a href="https://github.com/kubernetes/kubernetes/pull/78883">pr78883</a>, which fixed the bug where the default value for pod.spec.container.SecurityContext.ProcMount was added by default.</td>
</tr>
<tr>
    <td>2020-07-28</td>	
    <td>v1.14.3-tke.15</td>	
    <td><ul class="params"><li>Incorporated <a href="https://github.com/kubernetes/kubernetes/pull/76518">pr76518</a> and <a href="https://github.com/kubernetes/kubernetes/pull/82514">pr82514</a>, which limits the return size of http and exec probe to prevent occupation of large amounts of node memory (kubelet).</li><li>Incorporated <a href="https://github.com/kubernetes/kubernetes/pull/91277">pr91277</a>, which prevents the issue of large numbers of TLS handshake error logs generated by kube-apiserver as a result of CLB health checks (kube-apiserver).</li><li>Incorporated <a href="https://github.com/kubernetes/kubernetes/pull/91500">pr91500</a>, which fixed the issue of missing environmental variables of KUBERNETES_SERVICE_HOST (kubelet).</li><li>Incorporated <a href="https://github.com/kubernetes/kubernetes/pull/77475">pr77475</a>, which fixed the issue of Cronjob scheduling failure when the number of jobs exceeded 500 (kube-controller-manager).</li></ul></td>
</tr>
<tr>
    <td>2020-06-10</td>	
    <td>v1.14.3-tke.14</td>	
    <td><ul class="params"><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/85027">pr85027</a>, which fixes the issue where HPA miscalculates of the number of pods during rolling updates.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/79708">pr79708</a>, which uses spec.replicas to calculate the current number of replicas of HPA.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/91252">pr91252</a>, which ignores Pod Condition updates generated by other components to avoid unnecessary scheduling.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/89794">pr89794</a>, which clears kube-controller-manager error logs to avoid CVE-2020-8555 Half-Blind SSRF attacks.</li></ul></td>
</tr>
<tr>
    <td>2020-06-04</td>	
    <td>v1.14.3-tke.13</td>	
    <td><ul class="params"><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/90260">pr90260</a>, which fixes the issue of missing monitoring records for containerd cluster networks.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/79451">pr79451</a>, which fixes the issue where if restartPolicy is set to Never, kubelet does not try to create SandBox again after the first attempt fails.</li></ul></td>
</tr>
<tr>
    <td>2020-05-18</td>	
    <td>v1.14.3-tke.12</td>	
    <td>TKE can perceive the maximum number of qcloudcbs that can be mounted to a single node. The max value cannot be dynamically obtained.</td>
</tr>
<tr>
    <td>2020-04-14</td>
    <td>v1.14.3-tke.11</td>
    <td><ul class="params"><li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/75442"> pr75442</a>, which changes the bandwidth unit from Kb to b.</li><li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/87669"> pr87669</a>, which fixes the CVE-2020-8552: apiserver DoS attack issue.</li> <li>TKE can perceive the maximum number of qcloudcbs that can be mounted to a single node. (In 1.12 and later versions, the value is maxAttachCount-2. In version 1.10, the value is 18 by default).</li></ul></td>
</tr>
<tr>
    <td>2020-04-14</td>
    <td>v1.14.3-tke.10</td>
    <td>Fixes the issue where CBS intree continues to unmount a non-existent disk, which causes a large number of invalid requests.</td>
</tr>
<tr>
	<td>2020-01-13</td>
	<td>v1.14.3-tke.9</td>
	<td><ul class="params"><li>Merges<a href="https://github.com/google/cadvisor/pull/2359" target="_blank"> pr2359</a>, which fixes the issue of missing monitoring records when the system is unable to obtain docker root.</li> <li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/86583" target="_blank"> pr86583</a>, which increases the logging level to reduce the amount of logs caused by the lack of support for random-fully in earlier versions of iptables.</li><li>kube-scheduler now supports dynamic logging level configuration.</li><li>Produces a workaround for the missing CBS device path (/dev/disk/by-id/virtio-xxx/...) issue that prevents some users from accessing CBS properly.</li><li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/86230" target="_blank"> pr86230</a>, which skips assumed pod updates when pods are scheduled.</li></ul></td>
</tr>
<tr>
	<td>2019-12-23</td>
	<td>v1.14.3-tke.8</td>
	<td>Reverts <a href="https://github.com/kubernetes/kubernetes/pull/79036" target="_blank">pr79036</a>, which fixes an issue where upon being opened, the CPU Manager disables the CPU quota if the QoS setting of a pod is Guaranteed.</td>
</tr>
<tr>
	<td>2019-12-17</td>
	<td>v1.14.3-tke.7</td>
	<td><ul class="params"><li>Added metadata cache and timeout.</li> <li>Fixed the issue where upgrading lxcfs in Ubuntu 16 caused pods to exit.</li><li>Avoided the readiness state of “pod not ready” when kubelet was restarted.</li></ul></td>
</tr>
<tr>
	<td>2019-11-28</td>
	<td>v1.14.3-tke.6</td>
	<td>cloud-provider supports using node names as hostnames.</td>
</tr>
<tr>
	<td>2019-11-18</td>
	<td>v1.14.3-tke.5</td>
	<td><ul class="params"><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/83435" target="_blank">pr83435</a>, which fixes an issue that allows DoS attacks that use malicious YAML or JSON files to exhaust kube-apiserver CPU or memory resources, resulting in a loss of service.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/84167" target="_blank">pr84167</a>, which fixes an issue where an incorrect ETCD prefix causes apiserver health checks to fail.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/75622" target="_blank">pr75622</a>, which fixes an issue where, when there is a high sts (&gt;2000) workload in a cluster, it takes too long to sync sts changes to pod (about 20s).</li></ul></td>
</tr>
<tr>
	<td>2019-10-23</td>
	<td>v1.14.3-tke.4</td>
	<td>Merges <a href="https://github.com/kubernetes/kubernetes/pull/79036" target="_blank">pr79036</a>, which fixes an issue where upon being opened, the CPU Manager disables the CPU quota if the QoS setting of a pod is Guaranteed.</td>
</tr>
<tr>
	<td>2019-09-10</td>
	<td>v1.14.3-tke.3</td>
	<td>Incorporated <a href="https://github.com/kubernetes/kubernetes/pull/63066" target="_blank">pr63066</a>, which fixed the issue where CLB health checks failed in IPVS mode.</td>
</tr>
<tr>
	<td>2019-09-06</td>
	<td>v1.14.3-tke.2</td>
	<td><ul class="params"><li>Fixes the <a href="https://discuss.kubernetes.io/t/security-release-of-kubernetes-v1-15-3-v1-14-6-v1-13-10-cve-2019-9512-and-cve-2019-9514/7596" target="_blank">cve-2019-9512&amp;cve-2019-9514</a> HTTP/2 DDoS security issue.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/72914" target="_blank">pr72914</a>, which fixes an issue where deleting a Pod and then creating a new one and scheduling it to the same node could cause mounting a volume to fail.</li><li>Resolves the issue where creating containers in CentOS results in cgroup leakage.</li></ul></td>
</tr>
</tbody></table>

## TKE kubernetes 1.12.4 revisions

<table>
<thead>
<tr><th width="13%">Date</th><th width="13%">Version</th><th width="74%">Revisions</th></tr>
</thead>
<tbody>
<tr>
    <td>2021-05-06</td>	
    <td>v1.12.4-tke.28</td>	
    <td>Updated the launch method of running kube-proxy as an image, and automatically adapted to the iptables running mode of the node to support the operating system that uses the NF_TABLES mode to run iptables by default.</td>
</tr>	
<tr>
    <td>2020-12-28</td>	
    <td>v1.12.4-tke.27</td>	
    <td><ul class="params">
		<li>Added metrics to QcloudCbs (kube-controller-manager).</li>
	        <li>Fixed the issue where extra space exists in the value of serial when mounting CBS disk (Kubelet).</li>
	        </ul></td>
</tr>	
<tr>
    <td>2020-12-15</td>	
    <td>v1.12.4-tke.26</td>	
    <td>QcloudCbs supports BulkVolumeVerification (kube-controller-manager).</td>
</tr>
<tr>
    <td>2020-11-17</td>	
    <td>v1.12.4-tke.25</td>	
    <td>Merged <a href="https://github.com/kubernetes/kubernetes/pull/79495">pr79495</a>, which fixed the issue where the webhook call failed when there were multiple versions of CRD (kube-apiserver).</td>
</tr>
<tr>
    <td>2020-10-13</td>
    <td>v1.12.4-tke.24</td>
    <td>Merged <a href="https://github.com/kubernetes/kubernetes/pull/93403">pr93403</a>, which removed the printed error information of pod condition irrelevant to the kubelet during kubelet update (kubelet).</td>
<tr>
    <td>2020-08-04</td>
    <td>v1.12.4-tke.23</td>
    <td>Merged <a href="https://github.com/kubernetes/kubernetes/pull/78881">pr78881</a>, which fixed the bug where the default value for pod.spec.container.SecurityContext.ProcMount was added by default.</td>
</tr>
<tr>
    <td>2020-07-28</td>	
    <td>v1.12.4-tke.22</td>	
    <td><ul class="params"><li>Incorporated <a href="https://github.com/kubernetes/kubernetes/pull/91277">pr91277</a>, which prevents the issue of large numbers of TLS handshake error logs generated by kube-apiserver as a result of CLB health checks (kube-apiserver).</li><li>Incorporated <a href="https://github.com/kubernetes/kubernetes/pull/91500">pr91500</a>, which fixed the issue of missing environmental variables of KUBERNETES_SERVICE_HOST (kubelet).</li></ul></td>
</tr>
<tr>
    <td>2020-06-10</td>	
    <td>v1.12.4-tke.21</td>	
    <td><ul class="params"><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/73915"> pr73915</a>, which prevents the watcher from receiving events before the watch is started.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/91252">pr91252</a>, which ignores Pod Condition updates generated by other components to avoid unnecessary scheduling.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/89794">pr73915</a>, which clears kube-controller-manager error logs to avoid CVE-2020-8555 Half-Blind SSRF attacks.</li></ul></td>
</tr>
<tr>
    <td>2020-06-04</td>
    <td>v1.12.4-tke.20</td>
    <td><ul class="params"><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/90260"> pr90260</a>, which fixes the issue of missing monitoring records for containerd cluster networks.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/79451">pr79451</a>, which fixes the issue where if restartPolicy is set to Never, kubelet does not try to create SandBox again after the first attempt fails.</li></td>
<tr>
    <td>2020-05-18</td>	
    <td>v1.12.4-tke.19</td>	
    <td><ul class="params"><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/77802"> pr77802</a>, which disables graceful termination for UDP traffic.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/68741"> pr68741</a>, which fixes the issue of when the soft link /var/lib/kubelet and subpath are used, the host fails to unmount after pod deletion, resulting in mount target leakage and the pod being stuck in terminating.</li><li>TKE can perceive the maximum number of qcloudcbs that can be mounted to a single node. The max value cannot be dynamically obtained.</li></ul></td>
</tr>
<tr>
    <td>2020-04-14</td>	
    <td>v1.12.4-tke.18</td>
    <td><ul class="params"><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/73401"> pr73401</a>, <a href="https://github.com/kubernetes/kubernetes/pull/73606">pr73606</a>, and <a href="https://github.com/kubernetes/kubernetes/pull/76060">pr76060</a>, which deletes DaemonSet pods allocated to non-existent nodes.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/68619"> pr68619</a>, which fixes the CPU Manager dirty data issue.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/87669"> pr87669</a>, which fixes the CVE-2020-8552: apiserver DoS attack issue.</li><li>TKE can perceive the maximum number of qcloudcbs that can be mounted to a single node. (In 1.12 and later versions, the value is maxAttachCount-2. In version 1.10, the value is 18 by default).</li></ul></td>
    </tr>
<tr>
    <td>2020-02-14</td>	
    <td>v1.12.4-tke.17</td>	
    <td><ul class="params"><li> Upgrades the CBS V2 interface to V3.</li><li>Fixes the issue where CBS intree continues to unmount a non-existent disk, which causes a large number of invalid requests.</li></ul></td>
    </tr>
<tr>
	<td>2020-01-13</td>
	<td>v1.12.4-tke.16</td>
	<td><ul class="params"><li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/2359" target="_blank"> pr2359 </a>, which fixes the issue of missing monitoring records when docker root fails to be obtained.</li> <li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/86583" target="_blank"> pr86583 </a>, which increases the logging level to prevent excessive logs from being generated when iptables does not support random-fully.</li><li>kube-scheduler supports dynamic logging level configuration.</li><li>Produces a workaround for the missing CBS device path (/dev/disk/by-id/virtio-xxx/...) issue that prevents some users from accessing CBS properly.</li><li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/86230" target="_blank"> pr86230</a>, which skips assumed pod updates when pods are scheduled.</li></ul></td>
</tr>
<tr>
	<td>2019-12-23</td>
	<td>v1.12.4-tke.15</td>
	<td>Reverted <a href="https://github.com/kubernetes/kubernetes/pull/79036" target="_blank">pr79036</a>, which fixed the issue where the enabled CPU Manager disabled `cpu quota` if `QoS` of a pod was set to `Guaranteed`.</td>
</tr>
<tr>
	<td>2019-12-17</td>
	<td>v1.12.4-tke.14</td>
	<td><ul class="params"> <li>Added metadata cache and timeout.</li> <li>Fixed the issue where upgrading lxcfs in Ubuntu 16 caused pods to exit.</li><li>Avoided the readiness state of “pod not ready” when kubelet was restarted.</li></ul></td>
</tr>
	<tr>
	<td>2019-11-28</td>
	<td>v1.12.4-tke.13</td>
	<td>cloud-provider supports using node names as hostnames.</td>
	</tr>
<tr>
	<td>2019-11-18</td>
	<td>v1.12.4-tke.12</td>
	<td>Merges <a href="https://github.com/kubernetes/kubernetes/pull/75622" target="_blank">pr75622</a>, which fixes an issue where, when there is a high sts (&gt;2000) workload, it takes too long to sync sts changes to pod (about 20s).</td>
</tr>
<tr>
	<td>2019-10-23</td>
	<td>v1.12.4-tke.11</td>
	<td><ul class="params"><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/79036" target="_blank">pr79036</a>, which fixes an issue where upon being opened, the CPU Manager disables the CPU quota if the QoS setting of a pod is Guaranteed.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/72868" target="_blank">pr72868</a>, which adds a new parameter<code>--metrics-port</code> to kube-proxy and addresses the issue where <code>--metrics-bind-address</code> does not recognize port numbers.</li></ul></td>
</tr>
<tr>
	<td>2019-09-06</td>
	<td>v1.12.4-tke.10</td>
	<td><ul class="params"><li>Fixes the <a href="https://discuss.kubernetes.io/t/security-release-of-kubernetes-v1-15-3-v1-14-6-v1-13-10-cve-2019-9512-and-cve-2019-9514/7596" target="_blank">cve-2019-9512&amp;cve-2019-9514</a> HTTP/2 DDoS security issue.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/72914" target="_blank">pr72914</a>, which fixes an issue where deleting a Pod and then creating a new one and scheduling it to the same node could cause mounting a volume to fail.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/71834" target="_blank">pr71834</a>, which fixes an issue with IPVS load balancing where, if sessionAffinity is set to ClientIP, traffic is routed to an invalid real server.</li></ul></td>
</tr>
<tr>
	<td>2019-08-09</td>
	<td>v1.12.4-tke.9</td>
	<td>Fixed the issue where creating containers in CentOS resulted in cgroup leakage.</td>
</tr>
<tr>
	<td>2019-08-08</td>
	<td>v1.12.4-tke.8</td>
	<td>Incorporated <a href="https://github.com/kubernetes/kubernetes/pull/72118" target="_blank">pr72118</a>, which fixed the issue where mounting failed if a CBS StatefulSet was rescheduled to the same node.</td>
</tr>
<tr>
	<td>2019-07-17</td>
	<td>v1.12.4-tke.7</td>
	<td>Incorporated <a href="https://github.com/kubernetes/kubernetes/pull/75037" target="_blank">pr75037</a>, which resolved the security risks of the cp command in kubectl.</td>
</tr>
<tr>
	<td>2019-07-16</td>
	<td>v1.12.4-tke.6</td>
	<td>Fixed the compatibility issue between the TLinux kernel and IPVS and fixed CLB health check failures in IPVS mode.</td>
</tr>
<tr>
	<td>2019-07-09</td>
	<td>v1.12.4-tke.5</td>
	<td>Incorporated <a href="https://github.com/kubernetes/kubernetes/pull/72361" target="_blank">pr72361</a>, which fixed the kube-proxy deadlock issue.</td>
</tr>
<tr>
	<td>2019-06-25</td>
	<td>v1.12.4-tke.4</td>
	<td>Fixes the compatibility issue between the TLinux kernel and IPVS.</td>
</tr>
<tr>
	<td>2019-06-17</td>
	<td>v1.12.4-tke.3</td>
	<td>Incorporated <a href="https://github.com/kubernetes/kubernetes/pull/71114" target="_blank">pr71114</a>, which fixed the IPVS throughput issue.</td>
</tr>
<tr>
	<td>2019-06-04</td>
	<td>v1.12.4-tke.2</td>
	<td><ul class="params"><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/74755" target="_blank">pr74755</a>, which fixes a hang/timeout issue when running large numbers of pods with unique configmap/secret references.</li> <li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/69047" target="_blank">pr69047</a>, which fixes a backward compatibility issue with <code>node.Spec.Unschedulable</code>.</li></ul></td>
</tr>
</tbody></table>

## TKE kubernetes 1.10.5 revisions

<table>
<thead>
<tr><th width="13%">Date</th><th width="13%">Version</th><th width="74%">Revisions</th></tr>
</thead>
<tbody>
<tr>
    <td>2021-05-06</td>	
    <td>v1.10.5-tke.20</td>	 
    <td>Updated the launch method of running kube-proxy as an image, and automatically adapted to the iptables running mode of the node to support the operating system that uses the NF_TABLES mode to run iptables by default.</td>
<tr>
<tr>
    <td>2020-06-10</td>	
    <td>v1.10.5-tke.19</td>	 
    <td><ul class="params"><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/90260">pr90260</a>, which fixes the issue of missing monitoring records for containerd cluster networks.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/91252">pr91252</a>, which ignores Pod Condition updates generated by other components to avoid unnecessary scheduling.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/89794">pr89794</a>, which clears kube-controller-manager error logs to avoid CVE-2020-8555 Half-Blind SSRF attacks.</li></td>
<tr>
    <td>2020-05-18</td>	
    <td>v1.12.4-tke.19</td>	 
    <td>Merges<a href="https://github.com/kubernetes/kubernetes/pull/61549"> pr61549</a>, which adds volumeSpec data for mountedPods cache and fixes the issue of deletion failure when multiple pods use the same volume.</td>
<tr>
    <td>2020-04-29</td>
	<td>v1.10.5-tke.17</td>
    <td>Merges<a href="https://github.com/kubernetes/kubernetes/pull/75622" target="_blank">pr75622</a>, which fixes the issue where, when a large number (>2000) of sts workloads exist in a cluster, it takes too long (about 20s) to synchronize sts changes to a pod.</td>
    </tr>
<tr>
    <td>2020-04-14</td>
    <td>v1.10.5-tke.16</td>
    <td><ul class="params"><li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/68619"> pr68619</a>, which fixes the CPU Manager dirty data issue.</li><li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/87669"> pr87669</a>, which fixes the CVE-2020-8552: apiserver DoS attack issue. </li><li>TKE can perceive the maximum number of qcloudcbs that can be mounted to a single node. (In 1.12 and later versions, the value is maxAttachCount-2. In version 1.10, the value is 18 by default).</li></ul></td>
    </tr>
<tr>
    <td>2020-02-14</td>	
    <td>v1.10.5-tke.15</td>
    <td><ul class="params"><li> Upgrades the CBS V2 interface to V3.</li><li>Fixes the issue where CBS intree continues to unmount a non-existent disk, which causes a large number of invalid requests.</li></ul></td>
    </tr>
<tr>
<tr>
	<td>2020-01-13</td>
	<td>v1.10.5-tke.14</td>
	<td><ul class="params"><li>Merges<a href="https://github.com/google/cadvisor/pull/2359" target="_blank"> pr2359</a>, which fixes the issue of missing monitoring records when docker root fails to be obtained.</li> <li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/86583" target="_blank"> pr86583</a>, which increases the logging level to prevent excessive logs from being generated when iptables does not support random-fully.</li><li>kube-scheduler supports dynamic logging level configuration.</li><li>Produces a workaround for the missing CBS device path (/dev/disk/by-id/virtio-xxx/...) issue that prevents some users from accessing CBS properly.</li><li>Merges<a href="https://github.com/kubernetes/kubernetes/pull/86230" target="_blank"> pr86230</a>, which skips assumed pod updates when pods are scheduled.</li></ul></td>
</tr>
<tr>
	<td>2019-12-23</td>
	<td>v1.10.5-tke.13</td>
	<td>Reverted <a href="https://github.com/kubernetes/kubernetes/pull/79036" target="_blank">pr79036</a>, which fixes an issue where cpumanager disables cpu quota when it opens if the QoS setting of a pod is Guaranteed.</td>
</tr>
<tr>
	<td>2019-12-13</td>
	<td>v1.10.5-tke.12</td>
	<td><ul class="params"><li>kubelet does not delete nodes when checking externalID.</li> <li>Added metadata cache and timeout.</li><li>Fixed the issue where upgrading lxcfs in Ubuntu 16 caused pods to exit.</li><li>Avoided the readiness state of “pod not ready” when kubelet was restarted.</li></ul></td>
</tr>
<tr>
	<td>2019-11-18</td>
	<td>v1.10.5-tke.11</td>
	<td>Removes the kube-controller-manager probe that sends heartbeats to kubelet.</td>
</tr>
<tr>
	<td>2019-10-23</td>
	<td>v1.10.5-tke.10</td>
	<td><ul class="params"><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/79036" target="_blank">pr79036</a>, which fixes an issue where upon being opened, the CPU Manager disables the CPU quota if the QoS setting of a pod is Guaranteed.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/72868" target="_blank">pr72868</a>, which adds a new parameter<code>--metrics-port</code> to kube-proxy and addresses the issue where <code>--metrics-bind-address</code> does not recognize port numbers.</li></ul></td>
</tr>
<tr>
	<td>2019-09-06</td>
	<td>v1.10.5-tke.9</td>
	<td><ul class="params"><li>Fixes the <a href="https://discuss.kubernetes.io/t/security-release-of-kubernetes-v1-15-3-v1-14-6-v1-13-10-cve-2019-9512-and-cve-2019-9514/7596" target="_blank">cve-2019-9512&amp;cve-2019-9514</a> HTTP/2 DDoS security issue.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/72914" target="_blank">pr72914</a>, which fixes an issue where deleting a Pod and then creating a new one and scheduling it to the same node could cause mounting a volume to fail.</li><li>Merges <a href="https://github.com/kubernetes/kubernetes/pull/67430" target="_blank">67430</a> to rollback the state if updateContainerCPUSet fails.</li></ul></td>
</tr>
<tr>
	<td>2019-08-08</td>
	<td>v1.10.5-tke.8</td>
	<td>Merges <a href="https://github.com/kubernetes/kubernetes/pull/72118" target="_blank">pr72118</a>, which fixes an issue where, if kubelet mounts a device immediately after unmounting it, an error occurs with the message `resource name may not be empty`.</td>
</tr>
<tr>
	<td>2019-07-17</td>
	<td>v1.10.5-tke.7</td>
	<td>Merges <a href="https://github.com/kubernetes/kubernetes/pull/75037" target="_blank">pr75037</a>, which fixes a security issue affecting the cp command in kubectl.</td>
</tr>
<tr>
	<td>2019-06-25</td>
	<td>v1.10.5-tke.6</td>
	<td>Fixed a Linux kernel and IPVS load balancing issue.</td>
</tr>
<tr>
	<td>2019-06-17</td>
	<td>v1.10.5-tke.5</td>
	<td>Merges <a href="https://github.com/kubernetes/kubernetes/pull/71114" target="_blank">pr71114</a>, which fixes an issue with IPVS throughput.</td>
</tr>
<tr>
	<td>2019-03-19</td>
	<td>v1.10.5-tke.4</td>
	<td>Incorporated <a href="https://github.com/kubernetes/kubernetes/pull/65092" target="_blank">pr65092</a>, which fixed the issue where apiserver would panic when handling specific requests.</td>
</tr>
<tr>
	<td>2019-02-19</td>
	<td>v1.10.5-tke.3</td>
	<td>Incorporated <a href="https://github.com/kubernetes/kubernetes/pull/67288" target="_blank">pr67288</a>, which fixed the issue where apiserver did not close the other side of the connection immediately when proxying.</td>
</tr>
<tr>
	<td>2018-09-28</td>
	<td>v1.10.5-tke.2</td>
	<td>Moves the CLB creation logic from controller-manager to an independent service controller.</td>
</tr>
<tr>
	<td>2018-09-27</td>
	<td>v1.10.5-tke.1</td>
	<td>Backports <a href="https://github.com/kubernetes/kubernetes/pull/63321" target="_blank">pr63321</a>, which fixes an issue where termination takes too long when there are multiple service containers in a pod.</td>
</tr>
<tr>
<td>2018-09-21</td>
<td>v1.10.5-qcloud-rev1</td>
<td>If a kubelet status update times out, controller-manager probes the kubelet port.</td>
</tr>
</tbody></table>                                                

## TKE kubernetes 1.8.13 revisions

<table>
<thead>
<tr><th width="13%">Date</th><th width="13%">Version</th><th width="74%">Revisions</th></tr>
</thead>
<tbody><tr>
	<td>2020-01-13</td>
	<td>v1.8.13-tke.7</td>
	<td><ul class="params"><li>Merges<a href="https://github.com/google/cadvisor/pull/2359" target="_blank"> pr2359</a>, which fixes the issue of missing monitoring records when the system is unable to obtain docker root.</li><li>Produces a workaround for the missing CBS device path (/dev/disk/by-id/virtio-xxx/...) issue that prevents some users from accessing CBS properly.</li></ul></td>
</tr>
<tr>
	<td>2019-12-13</td>
	<td>v1.8.13-tke.6</td>
	<td><ul class="params"> <li>kubelet does not delete nodes when checking externalID.</li> <li>Adds metadata cache and timeout.</li><li>Fixes an issue where upgrading lxcfs in Ubuntu 16 causes pods to exit.</li><li>Adds the ability to reboot kubelet to avoid pod not ready.</li></ul></td>
</tr>
<tr>
	<td>2019-11-18</td>
	<td>v1.8.13-tke.5</td>
	<td><ul class="params"><li>Removes the kube-controller-manager probe that sends heartbeats to kubelet.</li><li>Adds metrics to CBS PVC.</li></ul></td>
</tr>
<tr>
	<td>2018-09-28</td>
	<td>v1.8.13-tke.2</td>
	<td>Moved load balancing logic from controller-manager to independent service controllers.</td>
</tr>
<tr>
	<td>2018-09-27</td>
	<td>v1.8.13-tke.1</td>
	<td><ul class="params"><li>Disables kmem statistics to prevent cgroup numbers from leaking.</li><li>Reduces resourcequota conflicts caused by creating pods.</li></ul></td>
</tr>
<tr>
	<td>2018-09-21</td>
	<td>v1.8.13-qcloud-rev1</td>
	<td>If a kubelet state update times out, controller-manager probes kubelet port.</td>
</tr>
</tbody></table>


## TKE kubernetes 1.7.8 revisions

<table>
<thead>
<tr><th width="13%">Date</th><th width="13%">Version</th><th width="74%">Revisions</th></tr>
</thead>
<tbody>
<tr>
	<td>2019-12-17</td>
	<td>v1.7.8-tke.4</td>
	<td><ul class="params"><li>kubelet does not delete nodes when checking externalID.</li> <li>Added metadata cache and timeout.</li><li>Fixed the issue where upgrading lxcfs in Ubuntu 16 caused pods to exit.</li><li>Avoided the readiness state of “pod not ready” when kubelet was restarted.</li></ul></td>
</tr>
<tr>
	<td>2018-09-28</td>
	<td>v1.7.8-tke.2</td>
	<td>Fixes a conflict between controller-manager and an external service controller.</td>
</tr>
<tr>
	<td>2018-09-27</td>
	<td>v1.7.8-tke.1</td>
	<td>Moves load balancing logic from controller-manager to an independent service controllers.</td>
</tr>
	<tr>
	<td>2018-09-21</td>
	<td>v1.7.8-qcloud-rev1</td>
	<td>If a kubelet status update times out, controller-manager probes the kubelet port.</td>
	</tr>
</tbody></table>

<style>
.params{
	margin-bottom:0px!important;
}
</style>
