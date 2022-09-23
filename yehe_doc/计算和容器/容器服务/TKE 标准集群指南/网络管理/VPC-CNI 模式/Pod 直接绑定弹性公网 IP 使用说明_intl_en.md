You can directly bind an EIP to a Pod that adopts the VPC-CNI mode as instructed below.

## Prerequisites and Limitations

- The role policy that is used by IPAMD has been granted with EIP API permission.
- Currently, it only supports auto-creating an EIP and does not support using an existing EIP.
- The EIP feature is not available in exclusive ENI with non-static IP address of VPC-CNI mode (it is available in v3.3.9 and later versions).
- The EIPs auto-created in the cluster cannot be reclaimed when the cluster is deleted.

## Adding EIP API Access Permission for the IPAMD Component Role

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/policy), select **Roles** in the left sidebar.
2. In **CAM console** > **[Roles](https://console.cloud.tencent.com/cam/role)**, search for the role `IPAMDofTKE_QCSRole`, and click the role name to go to the role details page.
3. Click **Associate Policies**.
4. In the pop-up window, search for and select the preset policy `QcloudAccessForIPAMDRoleInQcloudAllocateEIP`, and click **OK**. This policy contains all permissions required by the IPAMD component to operate an EIP.

## Auto-creating an EIP

See the following Yaml sample to associate with an EIP automatically:
```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  labels:
    k8s-app: busybox
  name: busybox
  namespace: default
spec:
  replicas: 1
  selector:
    matchLabels:
      k8s-app: busybox
      qcloud-app: busybox
  serviceName: ""
  template:
    metadata:
      annotations:
        tke.cloud.tencent.com/networks: "tke-route-eni"
        tke.cloud.tencent.com/vpc-ip-claim-delete-policy: Never
        tke.cloud.tencent.com/eip-attributes: '{"Bandwidth":"100","ISP":"BGP"}'
        tke.cloud.tencent.com/eip-claim-delete-policy: "Never"
      creationTimestamp: null
      labels:
        k8s-app: busybox
        qcloud-app: busybox
    spec:
      containers:
      - args:
        - "10000000000"
        command:
        - sleep
        image: busybox
        imagePullPolicy: Always
        name: busybox
        resources:
          limits:
            tke.cloud.tencent.com/eni-ip: "1"
            tke.cloud.tencent.com/eip: "1"
          requests:
            tke.cloud.tencent.com/eni-ip: "1"
            tke.cloud.tencent.com/eip: "1"
```

- **spec.template.annotations：tke.cloud.tencent.com/eip-attributes: '{"Bandwidth":"100","ISP":"BGP"}'** indicates that the Pod for the workload needs to automatically associate with an EIP. The bandwidth of the EIP is 100 Mbps and the ISP is BGP.
- **spec.template.annotations: tke.cloud.tencent.com/eip-claim-delete-policy: "Never"** indicates that the EIP of the Pod for the workload is a static IP address, and it cannot be changed after the Pod is terminated. If it is not a static IP address, do not add the annotation.
-**spec.template.spec.containers.0.resources**: to associate a Pod with an EIP, you need to add “requests” and “limits”, that is, `tke.cloud.tencent.com/eip`, so that the scheduler can ensure that the node to which the Pod scheduled still have EIPs available.


#### Key configurations
- The EIPs that each node can bind to are subject to the relevant quota restrictions and the bound number of CVMs.
The maximum number of EIPs that each node can bind to is **the bound number of CVMs - 1**.
- **tke.cloud.tencent.com/eip-attributes: '{"Bandwidth":"100","ISP":"BGP"}'**: only "bandwidth" and "ISP" can be configured for now. "ISP" can be set to `BGP`, `CMCC`, `CTCC` or `CUCC`, which corresponds to ordinary BGP IP and static single-line IP (China Mobile, China Telecom and China Unicom) respectively. If the two parameters are left empty, the default values of 100 Mbps and BGP will be used.
- Fees will not be charged on IPs after an auto-created EIP is bound. The default billing method for public network access is `postpaid by traffic on an hourly basis`.

## Retaining and Reclaiming of an EIP

After "auto-associate with an EIP" is enabled for the Pod, the network component will create a CRD object `EIPClaim` with the same name of the Pod in the same namespace. This object describes the Pod's requirements for the EIP.

For a Pod to which a non-static EIP is bound, `EIPClaim` will be terminated and the EIP associated with the Pod will also be terminated and reclaimed after the Pod is terminated. For a Pod to which a static EIP is bound, `EIPClaim` and the EIP will be retained after the Pod is terminated. After the Pod **with the same name** is enabled, it will use the EIP associated with the `EIPClaim` of the same name, so as to retain the EIP.

Below are three methods for reclaiming an EIP, including reclaiming after expiration, manual reclaiming and cascade reclaiming.

### Reclaiming after expiration (by default)
On [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637) page, select **VPC-CNI** for **Container Network Add-on** and check **Enable Support** for **Static Pod IP**, as shown in the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/bdef5073803ca51eb6d7be57b2d4a0d1.png)
Set **IP Reclaiming Policy** in **Advanced Settings**. You can set how many seconds after the Pod is terminated to reclaim the static IP address.
![](https://qcloudimg.tencent-cloud.cn/raw/5772282abc084605c87f765a69ae3366.png)
You can modify the **existing clusters** with the following method:
- Run the command `kubectl edit deploy tke-eni-ipamd -n kube-system` to modify the existing tke-eni-ipamd deployment.
- Run the following command to add the launch parameter to `spec.template.spec.containers[0].args` or modify the launch parameter.
```yaml
- --claim-expired-duration=1h # You can enter a value that is not less than 5m 
```

### Manual reclaiming
For an EIP that needs to be reclaimed urgently, you need to find the namespace and name of the corresponding Pod, and run the following command to reclaim it manually.
>! You must ensure the Pod corresponding to the reclaimed EIP have been terminated. Otherwise, the EIP will be associated with and bound to the Pod again.
>
```
kubectl delete eipc <podname> -n <namespace>
```

### Cascade reclaiming
Currently, the static EIP is strongly bound to the Pod, regardless of the specific workload (e.g., deployment, statefulset). After the Pod is terminated, it is uncertain when to reclaim the static EIP. TKE has implemented that the static EIP is deleted once the workload to which the Pod belongs is deleted. **The version of the IPAMD component needs to be v3.3.9 or later version (you can check the version through image tag)**.

You can enable cascade reclaiming by the following steps:
1. **Run the command `kubectl edit deploy tke-eni-ipamd -n kube-system` to modify the existing tke-eni-ipamd deployment**.
2. Run the following command to add the launch parameter to `spec.template.spec.containers[0].args`.
```yaml
- --enable-ownerref
```

After the modification, ipamd will automatically restart and take effect. At that time, a new workload can implement the cascade deletion of the static EIP, which is not supported for an existing workload.
