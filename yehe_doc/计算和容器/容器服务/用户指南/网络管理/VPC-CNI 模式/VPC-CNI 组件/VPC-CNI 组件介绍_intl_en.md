VPC-CNI component contains three kubernetes cluster components: `tke-eni-agent`, `tke-eni-ipamd` and `tke-eni-ip-scheduler`.


## tke-eni-agent

It is deployed on each node of the cluster in the form of `daemonset`. The responsibilities are described below.
- Copy `tke-route-eni`, `tke-eni-ipamc` and other CNI plugins to the directory of CNI executive file of the node (it is set to `/opt/cni/bin` by default).
- Generate CNI configuration file in CNI configuration directory (it is set to `/etc/cni/net.d/` by default).
- Configure policy-based routing and an ENI for the node.
- It acts as the GRPC Server to be responsible for allocating/releasing Pod IPs.
- Conduct IP garbage collection periodically, and reclaim IPs for which the Pods does not on the node.
- Set expansion resources of ENIs and IPs through [Device Plugins] of kubernetes(https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/device-plugins/).

## tke-eni-ipamd

It is deployed on certain nodes or masters of the cluster in the form of `deployment`. The responsibilities are described below.

- Create and manage CRD resources such as nec, vipc, vip and veni.
- In non-static IP address mode, create/bind/unbind/delete an ENI and allocate/release an ENI IP based on node requirements and status.
- In static IP address mode, create/bind/unbind/delete an ENI and allocate/release an ENI IP based on Pod requirements and status.
- Manage the security groups of ENIs of the node.
- Create/bind/unbind/delete an EIP based on Pod requirements.

## tke-eni-ip-scheduler

It is deployed on certain nodes or masters of the cluster in the form of `deployment` only in static IP address mode to act as an extension plugin for scheduling. The responsibilities are described below.

- If there are multiple subnets, it schedule the Pods with static IP addresses to the nodes of the specified subnet.
- In static IP address mode, it judges whether the IPs in the subnets corresponding to the node to which the Pod is scheduled are sufficient.
