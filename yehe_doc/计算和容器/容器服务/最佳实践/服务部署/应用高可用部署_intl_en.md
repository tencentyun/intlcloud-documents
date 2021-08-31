High availability (HA) refers to the ability of an application system to maintain uninterrupted operation, which is usually achieved by improving the fault tolerance of the system. In general, the application fault tolerance can be improved by configuring `replicas` to create multiple replicas of the application, but this does not necessarily mean that the application will have high availability.
This document describes four best practices for deploying applications with high availability. You can choose from them based on your situation.

- [Using anti-affinity to prevent single-point failures](#PodAntiAffinity)
- [Using a placement group to achieve disaster recovery from the physical layer](#PlacementSet)
- [Using PodDisruptionBudget to avoid service unavailability caused by node draining](#PodDisruptionBudget)
- [Using preStopHook and readinessProbe to ensure smooth and uninterrupted service update](#update)

<span ID="PodAntiAffinity"></span>
## Using Anti-affinity to Prevent Single-Point Failures
Kubernetes assumes that nodes are unreliable, so the more nodes there are, the higher the probability of nodes being unavailable due to software or hardware failures will be. Therefore, we usually have to deploy multiple replicas of applications and adjust the `replicas` value based on the actual situation. If its value is 1, there must be risks of single-point failures. Even if its value is greater than 1 but all replicas are scheduled to the same node, the single-point failure risks will still be there.

To prevent single-point failures, we need to have an appropriate number of replicas, and we also need to make sure different replicas are scheduled to different nodes. We can do so with anti-affinity. See the example below:
```
affinity:
 podAntiAffinity:
   requiredDuringSchedulingIgnoredDuringExecution:
   - weight: 100
     labelSelector:
       matchExpressions:
       - key: k8s-app
         operator: In
         values:
         - kube-dns
     topologyKey: kubernetes.io/hostname
```
The relevant configurations in this example are shown below:
 - **requiredDuringSchedulingIgnoredDuringExecution**
This sets anti-affinity as a required condition that must be met when pods are scheduled. If no node meets the condition, pods will not be scheduled to any node (pending).
If you do not want to set anti-affinity as a required condition, you can use `preferredDuringSchedulingIgnoredDuringExecution` to instruct the scheduler to always try to meet the anti-affinity condition. If no node meets the condition, pods can still be scheduled to certain nodes.
- **labelSelector.matchExpressions**
This marks the keys and values of the labels in the service’s corresponding pod.
- **topologyKey**
This example uses `kubernetes.io/hostname` to indicate that pods are prevented from being scheduled to the same node. 
If you have higher requirements, such as preventing pods from being scheduled to nodes in the same availability zone to achieve remote multi-site active-active disaster tolerance, you can use `failure-domain.beta.kubernetes.io/zone`. Generally, all the nodes in the same cluster are in one region. If there are cross-region nodes, there will be considerable latency even if direct connect is used. If pods have to be scheduled to nodes in the same region, you can use `failure-domain.beta.kubernetes.io/region`.
 <span id="PlacementSet"></span>
## Using a Placement Group to Achieve Disaster Recovery from the Physical Layer
When the underlying hardware or software of a CVM is faulty, multiple nodes may have exceptions at the same time. Even if anti-affinity is used to distribute pods to different nodes, business exceptions may still be unavoidable. You can use a [placement group](https://intl.cloud.tencent.com/document/product/213/15486) to distribute nodes from a physical layer, such as the CPM, exchange, or rack layer, to prevent underlying hardware or software faults from causing multiple node exceptions. The steps are as follows:
1. Log in to the [Placement Group Console](https://console.cloud.tencent.com/cvm/ps) to create a placement group and select a layer (CPM layer, exchange layer, or rack layer) as the node distribution policy. For more information, see [Spread Placement Group](https://intl.cloud.tencent.com/document/product/213/17020).
>! The placement group and the TKE self-deployed cluster need to be in the same region.
>
2. Add a batch of nodes, check **Add Instance to Spread Placement Group** in **Advanced Configuration**, and select the created placement group. For more information, see [Adding Nodes](https://intl.cloud.tencent.com/document/product/457/30652). See the figure below:
<img style="width:80%" src="https://main.qcloudimg.com/raw/294da8f8cbc472dd479880d5af553a5e.png">
3. On the "Node List" page, edit the same label for this batch of nodes to mark them. These nodes are simultaneously added to the placement group as a single batch. See the figure below:
>!The placement group policy takes effect only for nodes of the same batch. Therefore, you need to add a label for each batch of nodes and specify different values to mark different batches.
>
<img style="width:80%" src="https://main.qcloudimg.com/raw/ea7272600ffa2a08a7068614529c3e1c.png">
4. Specify node affinity for pods where workloads need to be deployed. In this way, the pods will be deployed on the same batch of nodes. Meanwhile, specify pod anti-affinity so that the pods will be widely distributed among the batch of nodes. The YAML sample is as follows:
```
affinity:
  nodeAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
      nodeSelectorTerms:
      - matchExpressions:
        - key: "placement-set-uniq"
          operator: In
          values:
          - "rack1"
  podAntiAffinity:
    preferredDuringSchedulingIgnoredDuringExecution:
    - weight: 100
      podAffinityTerm:
        labelSelector:
          matchExpressions:
          - key: app
            operator: In
            values:
            - nginx
        topologyKey: kubernetes.io/hostname
```

<span id="PodDisruptionBudget"></span>
## Using PodDisruptionBudget to Avoid Service Unavailability Caused by Node Draining

Node draining involves negative impacts. The following describes the process of draining a node:
1. Cordon the node by setting it as unschedulable to prevent new pods from being scheduled to it.
2. Delete pods from the node.
3. Once detecting that the number of pods decreases, ReplicaSet controller will create a new pod to be scheduled to a new node.

Such a process first deletes the pods and then creates new pods instead of using rolling update. Therefore, if all replicas of a service are on the drained node, the service may become unavailable during the updating process. Normally, the service may become unavailable for two reasons:
- The service is exposed to single-point failure risks with all the replicas on the same node. Once the node is drained, the service may become unavailable.
 In such a case, you can refer to [using anti-affinity to prevent single-point failures](#PodAntiAffinity).
- The service is deployed on multiple nodes but these nodes are drained at the same time. All the replicas of the service are deleted simultaneously, which may cause the service to become unavailable.
  In such a case, you can configure PDB (PodDisruptionBudget) to prevent the simultaneous deletion of all replicas. See the example below:
 - Example 1: ensure that zookeeper has at least two available replicas at the time of node draining.
```
		apiVersion: policy/v1beta1
		kind: PodDisruptionBudget
		metadata:
		  name: zk-pdb
		spec:
		  minAvailable: 2
		  selector:
		    matchLabels:
		      app: zookeeper
```
 - Example 2: ensure that zookeeper has no more than one unavailable replica at the time of node draining, which means that only one replica is deleted at a time and is recreated on another node.
```
		apiVersion: policy/v1beta1
		kind: PodDisruptionBudget
		metadata:
		  name: zk-pdb
		spec:
		  maxUnavailable: 1
		  selector:
		    matchLabels:
		      app: zookeeper
```
For more details, please read Kubernetes documentation: [Specifying a Disruption Budget for your Application](https://kubernetes.io/docs/tasks/run-application/configure-pdb/).
<span id="update"></span>

## Using preStopHook and readinessProbe to Ensure Smooth and Uninterrupted Service Update
If configuration is not optimized for a service, some traffic errors may occur during the service update with the default configuration. Please refer to the following steps when making deployment.

### Service Update Scenarios
Some service update scenarios include:
- Manually adjusting the number of service replicas.
- Manually deleting pods to trigger re-scheduling.
- Draining nodes voluntarily or involuntarily where pods are deleted from the drained nodes and then recreated on other nodes.
- Triggering rolling update, such as modifying the image tag to upgrade the program version.
- HPA (HorizontalPodAutoscaler) automatically scales out or scale in services.
- VPA (VerticalPodAutoscaler) automatically scales up or scale down services.

### Reasons for connection errors during service update
During a rolling update, the pods corresponding to the service being updated will be created or terminated, and the endpoints of the service will also add and remove `Pod IP:Port` corresponding to the pods. Then kube-proxy will update the forwarding rules according to the updated `Pod IP:Port` list, but such rules are not updated immediately.

The forwarding rules are not updated immediately because Kubernetes components are decoupled from each other. Each component uses the controller mode to ListAndWatch the resources it is interested in and responds with actions. Therefore, all the steps in the process, including pod creation or termination, endpoint update, and forwarding rules update, happen in an asynchronous manner.

When forwarding rules are not immediately updated, some connection errors could occur during the service update. The following describes two possible scenarios to analyze the reasons behind the connection errors:


- <span id="CaseOne"></span>Scenario 1: Pods have been created but have not fully started yet. Endpoint controller adds the pods to the `Pod IP:Port` list of the service. kube-proxy watches the update and updates the service forwarding rules (iptables/ipvs). If there is a request made at this point, it could be forwarded to a pod that has not fully started yet. A connection error may occur because the pod is not able to properly process the request yet.

- <span id="CaseTwo"></span>Scenario 2: Pods have been terminated, but since all the steps in the process are asynchronous, the forwarding rules have not been updated when the Pods have been fully terminated. In such a case, new requests can still be forwarded to the terminated Pods, leading to connection errors.

### Smooth update
- To address problems in [scenario 1](#CaseOne), you can add readinessProbe to the containers in the pods. After a container fully starts, it will listen to an HTTP port to which kubelet will send readiness probe packets. If the container can respond normally, it means the container is ready, and the container’s status will be modified to Ready. Only when all the containers in a pod are ready will the pod be added by the endpoint controller to the `IP:Port` list in the corresponding endpoint of the Service. Then, kube-proxy will update the forwarding rules. In this way, even if a request is immediately forwarded to the new pod, it will be able to normally process the request, thereby avoiding connection errors.

- To address problems in [scenario 2](#CaseTwo), you can add preStop hook to the containers in the pods so that, before the pods are fully terminated, they will sleep for some time during which the endpoint controller and kube-proxy can update the endpoints and the forwarding rules. During that time, the pods will be in the Terminating state. Even if a request is forwarded to a terminating pod before the forwarding rules are fully updated, the pod can still normally process the request because it has not been terminated yet.

Below is a YAML sample:
```
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      component: nginx
  template:
    metadata:
      labels:
        component: nginx
    spec:
      containers:
      - name: nginx
        image: "nginx"
        ports:
        - name: http
          hostPort: 80
          containerPort: 80
          protocol: TCP
        readinessProbe:
          httpGet:
            path: /healthz
            port: 80
            httpHeaders:
            - name: X-Custom-Header
              value: Awesome
          initialDelaySeconds: 15
          timeoutSeconds: 1
        lifecycle:
          preStop:
            exec:
              command: ["/bin/bash", "-c", "sleep 30"]
```
For more information, please see Kubernetes documentation: [Container probes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#container-probes) and [Container Lifecycle Hooks](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/).
