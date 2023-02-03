## Operations Supported by Kubectl

<table class="table-striped">
<tbody>
	<tr>
		<th>CRD Type</th>
		<th>Operation</th>
	</tr>
		<tr>
		<td rowspan="5">MachineSet</td>
		<td>Creating a native node pool<br>`kubectl create -f machineset-demo.yaml`</td>
	</tr>
	<tr>
		<td>Viewing the list of nodes in the native node pool<br>`kubectl get machineset`</td>
	</tr>
	<tr>
		<td>Viewing YAML details of a native node pool<br>`kubectl describe ms machineset-name`</td>
	</tr>
	<tr>
		<td>Deleting a native node pool<br>`kubectl delete ms machineset-name`</td>
	</tr>
	<tr>
		<td>Scaling out a native node pool<br>`kubectl scale --replicas=3 machineset/machineset-name`</td>
	</tr>
	<tr>
	  <td rowspan="3">Machine</td>
		<td>Viewing native nodes<br>`kubectl get machine`</td>
	</tr>
	<tr>
		<td>Viewing the YAML details of a native node<br>`kubectl describe  ma machine-name`</td>
	</tr>
	<tr>
		<td>Deleting a native node<br>`kubectl delete ma machine-name`</td>
	</tr>
  <tr>
    <td rowspan="4">HealthCheckPolicy</td>
    <td>Creating a fault self-healing rule<br>`kubectl create -f demo-HealthCheckPolicy.yaml`</td>
  </tr>
  <tr>
    <td>Viewing the fault self-healing rule list<br>`kubectl kubectl get HealthCheckPolicy`</td>
  </tr>
  <tr>
    <td>Viewing the YAML details of a fault self-healing rule<br>`kubectl describe HealthCheckPolicy HealthCheckPolicy-name`</td>
  </tr>
  <tr>
    <td>Deleting a fault self-healing rule<br>`kubectl delete HealthCheckPolicy HealthCheckPolicy-name`</td>
  </tr>
</table>


## Using CRD via YAML
### MachineSet
```
apiVersion: node.tke.cloud.tencent.com/v1beta1
kind: MachineSet
spec:
  type: Native
  displayName: mstest
  replicas: 2
  autoRepair: true
  deletePolicy: Random
  healthCheckPolicyName: test-all
  instanceTypes:
  - C3.LARGE8
  subnetIDs:
  - subnet-xxxxxxxx
  - subnet-yyyyyyyy
  scaling:
    createPolicy: ZonePriority
    maxReplicas: 100
  template:
    spec:
      displayName: mtest
      runtimeRootDir: /var/lib/containerd
      unschedulable: false
      metadata:
        labels:
          key1: "val1"
          key2: "val2"
      providerSpec:
        type: Native
        value:
          instanceChargeType: PostpaidByHour
          lifecycle:
            preInit: "echo hello"
            postInit: "echo world"
          management:
            hosts:
            - Hostnames:
              - lkongtest
              IP: 22.22.22.22
            nameservers:
            - 183.60.83.19
            - 183.60.82.98
            - 8.8.8.8
          metadata:
            creationTimestamp: null
          securityGroupIDs:
          - sg-xxxxxxxx
          systemDisk:
            diskSize: 50
            diskType: CloudPremium
```

## Kubectl Operation Demo
### MachineSet

1. Run the `kubectl create -f machineset-demo.yaml` command to create a MachineSet based on the preceding YAML file:
![](https://qcloudimg.tencent-cloud.cn/raw/fe738f177f96c69d537d17e7627ef7bc.png)

2. Run the `kubectl get machineset` command to view the status of the MachineSet np-pjrlok3w. At this time, the corresponding node pool already exists in the console, and its node is being created:
![](https://qcloudimg.tencent-cloud.cn/raw/0310234f91bfb13155e1836f6a4f3660.png)

![](https://staticintl.cloudcachetci.com/yehe/backend-news/iMG7238_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230105112642.png)

3. Run the `kubectl describe machineset np-pjrlok3w` command to view the description of the MachineSet np-pjrlok3w:
![](https://qcloudimg.tencent-cloud.cn/raw/175a797853bec72d6ae75bb488da8cbe.png)

4. Run the `kubectl scale --replicas=2 machineset/np-pjrlok3w` command to scale in the node pool:
![](https://qcloudimg.tencent-cloud.cn/raw/70c9803505718e7bfd5c3716cab87b80.png)

5. Run the `kubectl delete ms np-pjrlok3w` command to delete the node pool.
![](https://qcloudimg.tencent-cloud.cn/raw/14e3bba4321675852202e24855e5eb58.png)

### Machine
1. Run the `kubectl get machine` command to view the machine list. At this time, the corresponding nodes already exist in the console:
![](https://qcloudimg.tencent-cloud.cn/raw/de4d37e33c547cddd9c214ae55e093d4.png)
![](https://staticintl.cloudcachetci.com/yehe/backend-news/kFLI378_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230105143545.png)

2. Run the `kubectl describe ma np-14024r66-nv8bk` command to check the description of the machine np-14024r66-nv8bk:
![](https://qcloudimg.tencent-cloud.cn/raw/90545651c88836291914421607c0ed33.png)

3. Run the `kubectl delete ma np-14024r66-nv8bk` command to delete the node.

>?
>- If you delete the node directly without adjusting the expected number of nodes in the node pool, the node pool will create a new node to join the node pool when detecting that the actual number of nodes does not meet the declarative number of nodes. The recommended way to delete a node is as follows:
	1. Run the `kubectl scale --replicas=1 machineset/np-xxxxx` command to adjust the expected number of nodes.
	2. Run the `kubectl delete machine np-xxxxxx-dtjhd` command to delete the corresponding node.

