High availability (HA) refers to the ability of an application system to maintain uninterrupted operation, which is usually achieved by improving the fault tolerance of the system. In general, the application fault tolerance can be improved by configuring `replicas` to create multiple replicas of the application, but this does not necessarily mean that the application will have high availability.  
This document describes best practices for deploying application high availability. You can choose from them based on your situation.

- [Distributing and scheduling business workloads](#PodAntiAffinity)
- [Using a placement group to achieve disaster recovery in the physical layer](#PlacementSet)
- [Using PodDisruptionBudget to avoid service unavailability caused by node draining](#PodDisruptionBudget)
- [Using preStopHook and readinessProbe to ensure smooth and uninterrupted service update](#update)


[](id:PodAntiAffinity)
## Distributing and Scheduling Business Workloads
### 1. Using anti-affinity to prevent single-point failures
Kubernetes assumes that nodes are unreliable, so the more nodes there are, the higher the probability of nodes being unavailable due to software or hardware failures will be. Therefore, we usually have to deploy multiple replicas of applications and adjust the `replicas` value based on the actual situation. If its value is 1, there must be risks of single-point failures. Even if its value is greater than 1 but all replicas are scheduled to the same node, the single-point failure risks will still be there.  

To prevent single-point failures, we need to have an appropriate number of replicas, and we also need to make sure different replicas are scheduled to different nodes. We can do so with anti-affinity. See the example below:
```yaml
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
This sets anti-affinity as a required condition that must be met when Pods are scheduled. If no node meets the condition, Pods will not be scheduled to any node (pending).  
If you do not want to set anti-affinity as a required condition, you can use `preferredDuringSchedulingIgnoredDuringExecution` to instruct the scheduler to always try to meet the anti-affinity condition. If no node meets the condition, Pods can still be scheduled to certain nodes.  
- **labelSelector.matchExpressions**
This marks the keys and values of the labels in the service’s corresponding Pod.  
- **topologyKey**
This example uses `kubernetes.io/hostname` to indicate that Pods are prevented from being scheduled to the same node.  
If you have higher requirements, such as preventing Pods from being scheduled to nodes in the same availability zone to achieve remote multi-site active-active disaster tolerance, you can use `failure-domain.beta.kubernetes.io/zone`. Generally, all the nodes in the same cluster are in one region. If there are cross-region nodes, there will be considerable latency even if direct connect is used. If Pods have to be scheduled to nodes in the same region, you can use `failure-domain.beta.kubernetes.io/region`.  


### 2. Using topologySpreadConstraints 
The topologySpreadConstraints feature defaults to be enabled in K8s v1.18. It is recommended that you use `topologySpreadConstraints` to distribute Pods in clusters of v1.18 or later versions to improve the service availability.

Widely distribute and schedule Pods to each node:
For example, widely distribute and schedule all Pods of nginx to different nodes as evenly as possible. The max allowed number variance of nginx copies on different nodes is `1`. If no more Pods can be scheduled to a node due to reasons such as insufficient resources of the node, the remaining nginx copies are pending.
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    k8s-app: nginx
    qcloud-app: nginx
  name: nginx
  namespace: default
spec:
  replicas: 1
  selector:
    matchLabels:
      k8s-app: nginx
      qcloud-app: nginx
  template:
    metadata:
      labels:
        k8s-app: nginx
        qcloud-app: nginx
    spec:
      topologySpreadConstraints:
      - maxSkew: 1
        whenUnsatisfiable: DoNotSchedule
        topologyKey: topology.kubernetes.io/region
        labelSelector:
          matchLabels:
            k8s-app: nginx
      containers:
      - image: nginx
        name: nginx
        resources:
          limits:
            cpu: 500m
            memory: 1Gi
          requests:
            cpu: 250m
            memory: 256Mi
      dnsPolicy: ClusterFirst
```
- topologyKey: It is similar to configurations in podAntiAffinity.
- labelSelector: It is similar to configurations in podAntiAffinity. It supports selecting labels of multiple Pods.
- maxSkew: It must be an integer larger than 0, indicating the max allowed variation of Pod number in different topological domain. `1` means the max allowed variation of Pod number is one.
- whenUnsatisfiable: It indicates how to deal with the situations where the conditions are not met. `DoNotSchedule` means do not schedule (keep pending), and it is similar to strong anti-affinity. `ScheduleAnyway` means widely distribute and schedule Pods on node as evenly as possible, and it is similar to weak anti-affinity (change `DoNotSchedule` to `ScheduleAnyway`).
```yaml
    spec:
      topologySpreadConstraints:
      - maxSkew: 1
        whenUnsatisfiable: ScheduleAnyway
        topologyKey: topology.kubernetes.io/region
        labelSelector:
          matchLabels:
            k8s-app: nginx
```

If the cluster node supports cross-AZ scheduling, you can widely distribute and schedule Pods to the AZs as evenly as possible to achieve higher levels of high availability (change `topologyKey` to `topology.kubernetes.io/zone`).
```yaml
    spec:
      topologySpreadConstraints:
      - maxSkew: 1
        topologyKey: topology.kubernetes.io/zone
        whenUnsatisfiable: ScheduleAnyway
        labelSelector:
          matchLabels:
            k8s-app:: nginx
```

Moreover, you can widely distribute the Pods within each AZ when you schedule the Pods to the AZs.
```yaml
    spec:
      topologySpreadConstraints:
      - maxSkew: 1
        whenUnsatisfiable: ScheduleAnyway
        topologyKey: topology.kubernetes.io/zone
        labelSelector:
          matchLabels:
            k8s-app: nginx
      - maxSkew: 1
        whenUnsatisfiable: ScheduleAnyway
        topologyKey: kubernetes.io/hostname
        labelSelector:
          matchLabels:
            k8s-app: nginx
```

## Using a Placement Group to Achieve Disaster Recovery in the Physical Layer[](id:PlacementSet)
When the underlying hardware or software of a CVM is faulty, multiple nodes may have exceptions at the same time. Even if anti-affinity is used to distribute Pods to different nodes, business exceptions may still be unavoidable. You can use a [placement group](https://intl.cloud.tencent.com/document/product/213/15486) to distribute nodes in a physical layer, such as the CPM, exchange, or rack layer, to prevent underlying hardware or software faults from causing multiple node exceptions. The steps are as follows:
1. Log in to the [Placement Group console](https://console.cloud.tencent.com/cvm/ps) to create a placement group and select a layer (CPM layer, exchange layer, or rack layer) as the node distribution policy. For more information, see [Spread Placement Group](https://intl.cloud.tencent.com/document/product/213/17020).  
>! The placement group and the TKE self-deployed cluster need to be in the same region.  
>
2. Add a batch of nodes, check **Add the instance to a placement group** in **Advanced configuration**, and select the created placement group. For more information, see [Adding Nodes](https://intl.cloud.tencent.com/document/product/457/30652).
<img style="width:100%" src="https://main.qcloudimg.com/raw/294da8f8cbc472dd479880d5af553a5e.png">
3. On the "Node list" page, edit the same label for this batch of nodes to mark them. These nodes are simultaneously added to the placement group as a single batch.
>!The placement group policy takes effect only for nodes of the same batch. Therefore, you need to add a label for each batch of nodes and specify different values to mark different batches.  
>
<img style="width:100%" src="https://main.qcloudimg.com/raw/ea7272600ffa2a08a7068614529c3e1c.png">
4. Specify node affinity for Pods where workloads need to be deployed. In this way, the Pods will be deployed on the same batch of nodes. Meanwhile, specify Pod anti-affinity so that the Pods will be widely distributed among the batch of nodes. The YAML sample is as follows:
```yaml
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



## Using PodDisruptionBudget to Avoid Service Unavailability Caused by Node Draining[](id:PodDisruptionBudget)

Node draining involves negative impacts. The following describes the process of draining a node:
1. Cordon the node by setting it as unschedulable to prevent new Pods from being scheduled to it.  
2. Delete Pods from the node.  
3. Once detecting that the number of Pods decreases, ReplicaSet controller will create a new Pod to be scheduled to a new node.  

Such a process first deletes the Pods and then creates new Pods instead of using rolling update. Therefore, if all replicas of a service are on the drained node, the service may become unavailable during the updating process. Normally, the service may become unavailable for two reasons:
1. The service is exposed to single-point failure risks with all the replicas on the same node. Once the node is drained, the service may become unavailable.  
 In such a case, you can refer to [using anti-affinity to prevent single-point failures](#PodAntiAffinity).  
2. The service is deployed on multiple nodes, but these nodes are drained at the same time. All the replicas of the service are deleted simultaneously, which may cause the service to become unavailable.  
    In such a case, you can configure PDB (PodDisruptionBudget) to prevent the simultaneous deletion of all replicas. See the example below:
    <dx-tabs>
    ::: Example 1
    Ensure that zookeeper has at least two available replicas at the time of node draining.  
```yaml
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
:::
::: Example 2
Ensure that zookeeper has no more than one unavailable replica at the time of node draining, which means that only one replica is deleted at a time and is recreated on another node.  
```yaml
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
:::
</dx-tabs>

For more details, please read Kubernetes documentation: [Specifying a Disruption Budget for your Application](https://kubernetes.io/docs/tasks/run-application/configure-pdb/).  



[](id:update)
## Using preStopHook and readinessProbe to Ensure Smooth and Uninterrupted Service Update
If configuration is not optimized for a service, some traffic errors may occur during the service update with the default configuration. Please refer to the following steps when making deployment.  

### Service update scenarios
Some service update scenarios include:
- Manually adjusting the number of service replicas.  
- Manually deleting Pods to trigger re-scheduling.  
- Draining nodes voluntarily or involuntarily, where Pods are deleted from the drained nodes and then recreated on other nodes.  
- Triggering rolling update, such as modifying the image tag to upgrade the program version.  
- HPA (HorizontalPodAutoscaler) automatically scales out or scale in services.  
- VPA (VerticalPodAutoscaler) automatically scales up or scale down services.  

### Reasons for connection errors during service update
During a rolling update, the Pods corresponding to the service being updated will be created or terminated, and the endpoints of the service will also add and remove `Pod IP:Port` corresponding to the Pods. Then kube-proxy will update the forwarding rules according to the updated `Pod IP:Port` list, but such rules are not updated immediately.  

The forwarding rules are not updated immediately because Kubernetes components are decoupled from each other. Each component uses the controller mode to ListAndWatch the resources it is interested in and responds with actions. Therefore, all the steps in the process, including Pod creation or termination, endpoint update, and forwarding rules update, happen in an asynchronous manner.  

When forwarding rules are not immediately updated, some connection errors could occur during the service update. The following describes two possible scenarios to analyze the reasons behind the connection errors:


- [](id:CaseOne)Scenario 1: Pods have been created but have not fully started yet. Endpoint controller adds the Pods to the `Pod IP:Port` list of the service. kube-proxy watches the update and updates the service forwarding rules (iptables/ipvs). If there is a request made at this point, it could be forwarded to a Pod that has not fully started yet. A connection error may occur because the Pod is not able to properly process the request yet.  

- [](id:CaseTwo)Scenario 2: Pods have been terminated, but since all the steps in the process are asynchronous, the forwarding rules have not been updated when the Pods have been fully terminated. In such a case, new requests can still be forwarded to the terminated Pods, leading to connection errors.  

### Smooth update
- To address problems in [scenario 1](#CaseOne), you can add readinessProbe to the containers in the Pods. After a container fully starts, it will listen to an HTTP port to which kubelet will send readiness probe packets. If the container can respond normally, it means the container is ready, and the container’s status will be modified to Ready. Only when all the containers in a Pod are ready will the Pod be added by the endpoint controller to the `IP:Port` list in the corresponding endpoint of the Service. Then, kube-proxy will update the forwarding rules. In this way, even if a request is immediately forwarded to the new Pod, it will be able to normally process the request, thereby avoiding connection errors.  

- To address problems in [scenario 2](#CaseTwo), you can add preStop hook to the containers in the Pods so that, before the Pods are fully terminated, they will sleep for some time during which the endpoint controller and kube-proxy can update the endpoints and the forwarding rules. During that time, the Pods will be in the Terminating status. Even if a request is forwarded to a terminating Pod before the forwarding rules are fully updated, the Pod can still normally process the request because it has not been terminated yet.  

Below is a YAML sample:
```yaml
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
