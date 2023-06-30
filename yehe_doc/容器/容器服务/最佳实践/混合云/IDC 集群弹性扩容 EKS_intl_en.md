## Use Cases
As your IDC resources may be limited, if you need to handle business traffic surges, the computing resources in your IDC may be insufficient to meet the requirements. In this case, you can use public cloud resources to handle temporary traffic. Based on custom scheduling policies and by leveraging <a href="https://intl.cloud.tencent.com/zh/product/eks">TKE Serverless Container Service</a>, TKE Resilience Chart adds supernodes to elastically migrate workloads in your IDC cluster to the cloud, so your cluster can get greater elastic scalability and enjoy the following benefits:

1. The hardware and maintenance costs of your IDC/private cloud do not increase.
2. You can implement high availability for applications at the IDC/private cloud grade and public cloud grade.
3. You can use public cloud resources as needed in a pay-as-you-go manner.

## Notes
1. You have activated [TKE Serverless cluster](https://console.cloud.tencent.com/tke2/ecluster/startUp?rid=1).
2. Your IDC is connected to a VPC through Direct Connect over the private network.
3. The address of the API server in the IDC cluster can be accessed over the VPC.
4. Your own IDC cluster can access the public network, as it needs to call TencentCloud APIs over the public network.

## TKE Resilience Chart Feature Description
### Component description
TKE Resilience Chart mainly consists of a supernode manager, scheduler, and toleration controller as detailed below:

| Alias | Component Name | Description |
| -------------------- | -------------- | -------------------------------------------------------------------- |
| eklet                | Supernodes manager | It manages the lifecycle of PodSandboxes and provides APIs related to native kubelet and nodes.  |
| tke-scheduler        | Scheduler         | It migrates workloads to the cloud elastically according to scheduling policies and is only installed in non-TKE Kubernetes Distro K8s clusters. TKE Kubernetes Distro is a K8s distribution released by TKE to help you create exactly the same K8s cluster in TKE. Currently, it has been open sourced at GitHub. For more information, please see <a href="https://github.com/tkestack/tke-K8S-distro" target="_blank">TKE Kubernetes Distro</a>. |
| admission-controller | Toleration controller     | It adds a toleration to a Pod in `pending` status to make it able to be scheduled to a supernode.       |

### Main features
1. If you want to connect an TKE Serverless Pod to a Pod in your local cluster, the local cluster should be in an underlay network model (where a CNI plugin based on BGP routing instead of SDN encapsulation, such as Calico, is used), and you need to add the local Pod's CIDR block routing information in the VPC. For more information, see [Interconnection Between Cluster in GlobalRouter Mode and IDC](https://intl.cloud.tencent.com/document/product/457/46007)
2. The workload resilience feature switch `AUTO_SCALE_EKS=true|false` is available in global and local dimensions respectively to control whether workloads in `pending` status should be elastically scheduled to EKS as detailed below:
 - Global switch: `AUTO_SCALE_EKS` in `kubectl get cm -n kube-system eks-config` is enabled by default.
 - Local switch: `spec.template.metadata.annotations ['AUTO_SCALE_EKS']`
<table>
<thead>
<tr>
<th>Global Switch</th>
<th>Local Switch</th>
<th>Behavior</th>
</tr>
</thead>
<tbody><tr>
<td>AUTO_SCALE_EKS=true</td>
<td>AUTO_SCALE_EKS=false</td>
<td>Successfully scheduled</td>
</tr>
<tr>
<td> AUTO_SCALE_EKS=true </td>
<td> Undefined</td>
<td> Successfully scheduled</td>
</tr>
<tr>
<td> AUTO_SCALE_EKS=true </td>
<td> AUTO_SCALE_EKS=true </td>
<td> Successfully scheduled</td>
</tr>
<tr>
<td> AUTO_SCALE_EKS=false </td>
<td> AUTO_SCALE_EKS=false </td>
<td> Failed to be scheduled</td>
</tr>
<tr>
<td> AUTO_SCALE_EKS=false </td>
<td> Undefined</td>
<td> Failed to be scheduled</td>
</tr>
<tr>
<td> AUTO_SCALE_EKS=false </td>
<td> AUTO_SCALE_EKS=true </td>
<td> Successfully scheduled</td>
</tr>
<tr>
<td> Undefined</td>
<td> AUTO_SCALE_EKS=false </td>
<td> Successfully scheduled</td>
</tr>
<tr>
<td> Undefined</td>
<td> Undefined</td>
<td> Successfully scheduled</td>
</tr>
<tr>
<td> Undefined</td>
<td> AUTO_SCALE_EKS=true </td>
<td> Successfully scheduled</td>
</tr>
</tbody></table>

3. If you use K8s community edition, you need to specify the scheduler as `tke-scheduler` in workloads. In TKE Kubernetes Distro, you don't need to specify the scheduler.
4. In the workloads, set the number of retained replicas in the local cluster through `LOCAL_REPLICAS: N`.
5. Workload scale-out:
  - If the local cluster resources are insufficient and the settings of the global and local switches for the **"successfully scheduled"** behavior are satisfied, workloads in `pending` status will be scaled out to EKS.
  - If the number of actually created workload replicas reaches N and the settings of the global and local switches for the **"successfully scheduled"** behavior are satisfied, workloads in `pending` status will be scaled out to TKE Serverless cluster.
6. Workload scale-in:
  - For TKE Kubernetes Distro, instances in TKE Serverless cluster will be scaled in preferentially.
  - For K8s community edition, workloads will be scaled in randomly.
7. Scheduling rule restrictions:
  - DaemonSet Pods cannot be scheduled to supernodes. This feature is available only in TKE Kubernetes Distro. In K8s community edition, DaemonSet Pods will be scheduled to supernodes but `DaemonsetForbidden` will be displayed.
  - Pods in `kube-system` and `tke-eni-ip-webhook` namespaces cannot be scheduled to supernodes.
  - Ports whose `securityContext.sysctls ["net.ipv4.ip_local_port_range"]` value includes 61000–65534 cannot be scheduled.
  - Pods in `Pod.Annotations [tke.cloud.tencent.com/vpc-ip-claim-delete-policy]` cannot be scheduled.
  - Ports whose `container (initContainer).ports [].containerPort (hostPort)` value includes 61000–65534 cannot be scheduled.
  - Ports with a `container (initContainer)` where the probe points to 61000–65534 cannot be scheduled.
  - PersistentVolumes (PVs) except nfs, Cephfs, hostPath, and qcloudcbs cannot be scheduled.
  - Pods with fixed IP enabled cannot be scheduled to supernodes.
8. Supernodes support custom DNS configuration: after you add the `eks.tke.cloud.tencent.com/resolv-conf` annotation to a supernode, `/etc/resolv.conf` in the generated CVM instance will be updated to the custom content. 
>! The original DNS configuration on the supernodes will be overwritten, and your custom configuration will prevail.
>
```
eks.tke.cloud.tencent.com/resolv-conf: |
   nameserver 4.4.4.4
   nameserver 8.8.8.8
```


## Directions

### Getting `tke-resilience helm chart`
```bash
 git clone https://github.com/tkestack/charts.git
```

### Configuring relevant information

Edit `charts/incubator/tke-resilience/values.yaml` and configure the following information:
```bash
cloud:
  appID: "{Tencent Cloud account APPID}"
  ownerUIN: "{Tencent Cloud account ID}"
  secretID: "{Tencent Cloud account secretID}"
  secretKey: "{Tencent Cloud account secretKey}"
  vpcID: "{ID of the VPC where the EKS Pod resides}"
  regionShort: "{Abbreviation of the region where the EKS Pod resides}"
  regionLong: "{Full name of the region where the EKS Pod resides}"
  subnets:
    - id: "{ID of the subnet where the EKS Pod resides}"
      zone: "{AZ where the EKS Pod resides}" 
eklet:
  PodUsedApiserver: "{API server address of the current cluster}"
```
>? For more information on the regions and AZs where TKE Serverless container service is available, please see [Regions and AZs](https://intl.cloud.tencent.com/zh/document/product/457/41125). 

### Installing TKE Resilience Chart
You can use the [local Helm client to connect to the cluster](https://intl.cloud.tencent.com/document/product/457/30684).

Run the following command to use a Helm chart to install TKE Resilience Chart in a third-party cluster:
```bash
helm install tke-resilience --namespace kube-system ./tke-resilience --debug
```
Run the following command to check whether the required components in the Helm application are installed. This document uses a TKE Kubernetes Distro cluster with no tke-scheduler installed as an example.
```bash
# kubectl get Pod -n kube-system | grep resilience
eklet-tke-resilience-5f9dcd99df-rgsmc           1/1     Running   0          43h
eks-admission-tke-resilience-5bb588dc44-9hvhs   1/1     Running   0          44h
```
You can see that one supernode has been deployed in the cluster.
```bash
# kubectl get node
NAME                    STATUS   ROLES    AGE    VERSION
10.0.1.xx               Ready    <none>   2d4h   v1.20.4-tke.1
10.0.1.xx               Ready    master   2d4h   v1.20.4-tke.1
eklet-subnet-xxxxxxxx   Ready    <none>   43h    v2.4.6
```

### Creating test case
Create a demo application `nginx-deployment`, which has four replicas (three in TKE Serverless cluster and one in the local cluster). Below is the sample YAML configuration:
```bash
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 4
  strategy:
    type: RollingUpdate
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      annotations:
        AUTO_SCALE_EKS: "true"
        LOCAL_REPLICAS: "1" # Set the number of running replicas in the local cluster to 1
      labels:
        app: nginx
    spec:
      #schedulerName: tke-scheduler If it is a third-party cluster, you need to run the scheduler as `tke-scheduler`
      containers:
      - name: nginx
        image: nginx
        imagePullPolicy: IfNotPresent
```
Check whether the replica status and distribution meet the expectations.
```bash
# kubectl get Pod -owide
NAME                                READY   STATUS    RESTARTS   AGE   IP            NODE                    NOMINATED NODE   READINESS GATES
nginx-deployment-77b9b9bc97-cq9ds   1/1     Running   0          27s   10.232.1.88   10.0.1.xxx              <none>           <none>
nginx-deployment-77b9b9bc97-s9vzc   1/1     Running   0          27s   10.0.1.118    eklet-subnet-xxxxxxxx   <none>           <none>
nginx-deployment-77b9b9bc97-sd4z5   1/1     Running   0          27s   10.0.1.7      eklet-subnet-xxxxxxxx   <none>           <none>
nginx-deployment-77b9b9bc97-z86tx   1/1     Running   0          27s   10.0.1.133    eklet-subnet-xxxxxxxx   <none>           <none>
```

Check the scale-in feature. As a TKE Kubernetes Distro cluster is used, TKE Serverless cluster instances will be scaled in preferentially. Here, the number of application replicas is adjusted from 4 to 3.
```bash
# kubectl scale deployment nginx-deployment --replicas=3
```
As shown below, replicas in Tencent Cloud are scaled in first, which meets the expectation:
```bash
# kubectl get Pod -owide
NAME                                READY   STATUS    RESTARTS   AGE     IP            NODE                    NOMINATED NODE   READINESS GATES
nginx-deployment-77b9b9bc97-cq9ds   1/1     Running   0          7m38s   10.232.1.88   10.0.1.xxx              <none>           <none>
nginx-deployment-77b9b9bc97-s9vzc   1/1     Running   0          7m38s   10.0.1.118    eklet-subnet-xxxxxxxx   <none>           <none>
nginx-deployment-77b9b9bc97-sd4z5   1/1     Running   0          7m38s   10.0.1.7      eklet-subnet-xxxxxxxx   <none>           <none>
```
