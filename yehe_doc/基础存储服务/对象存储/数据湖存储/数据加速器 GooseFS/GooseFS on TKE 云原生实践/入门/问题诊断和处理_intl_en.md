## About Fluid Installation

### Why do I fail to install Fluid with Helm?

You are advised to follow the [Fluid installation document](https://intl.cloud.tencent.com/document/product/436/42230) to confirm whether the Fluid components are operating properly.

The Fluid installation document uses `Helm 3` as an example. If you use a version below `Helm 3` to deploy Fluid and encounter the situation of `CRD not starting properly`, this may be because `Helm 3` and above versions will automatically install CRD during `helm install` but the lower version of Helm will not. See the [Helm official documentation](https://helm.sh/docs/chart_best_practices/custom_resource_definitions/).

In this case, you need to install CRD manually:

```bash
$ kubectl create -f fluid/crds
```

### Why can't I delete Runtime?

Please check the related Pod running status and Runtime events. As long as any active Pod is still using the Volume created by Fluid, Fluid will not complete the delete operation.

The following commands can quickly find these active Pods. When using it, replace `<dataset_name>` and `<dataset_namespace>` with yours:

```bash
kubectl describe pvc <dataset_name> -n <dataset_namespace> | \
	awk '/^Mounted/ {flag=1}; /^Events/ {flag=0}; flag' | \
	awk 'NR==1 {print $3}; NR!=1 {print $1}' | \
	xargs -I {} kubectl get po {} | \
	grep -E "Running|Terminating|Pending" | \
	cut -d " " -f 1
```


### Why does the `driver name fuse.csi.fluid.io not found in the list of registered CSI drivers` error appear when I create a task to mount the PVC created by Runtime?

1. Check whether the kubelet configuration of the node on which the task is scheduled is the default value `/var/lib/kubelet`.
2. Check whether Fluid's CSI component is operating properly.
The following command can find the Pod quickly. When using it, replace the `<node_name>` and `<fluid_namespace>` with yours:
```bash
kubectl get pod -n <fluid_namespace> | grep <node_name>

# <pod_name> indicates the pod name in the last step
kubectl logs <pod_name> node-driver-registrar -n <fluid_namespace>
kubectl logs <pod_name> plugins -n <fluid_namespace>
```
 - If there is no error in the log data of the above steps, check whether the `csidriver` object exists:
```
kubectl get csidriver
```
 - If the `csidriver` object exists, check whether the `csi` registered node contains `<node_name>`:
```
kubectl get csinode | grep <node_name>
```

If the above command has no output, check whether the kubelet configuration of the node on which the task is scheduled is the default value `/var/lib/kubelet`. Because Fluid's CSI component is registered with kubelet through a fixed address socket, the default value is `--csi-address=/var/lib/kubelet/csi-plugins/fuse.csi.fluid.io/csi.sock --kubelet-registration-path=/var/lib/kubelet/csi-plugins/fuse.csi.fluid.io/csi.sock`.


### After Fluid is upgraded, why does the dataset created in the older version miss some fields compared with the newly created dataset, when I query them via the `kubectl get` command?

During the Fluid upgrade, we may have upgraded CRDs. The dataset created in the older version will set the new fields in the CRDs to null. For example, if you upgrade from v0.4 or before, the dataset did not have a `FileNum` field in those earlier versions. After Fluid is upgraded, if you use the `kubectl get` command, you cannot query the `FileNum` of the dataset.

You can recreate the dataset, and the new dataset will display these fields properly.


### Why does Volume Attachment timeout occur when PVC is used in an application?

The Volume Attachment timeout problem is a timeout caused by the kubelet not receiving a response from the CSI Driver when making a request to it. This problem is caused by the fact that the CSI Driver of Fluid is not installed, or kubelet does not have permission to access the CSI Driver.

Since the CSI Driver is called back by kubelet, if the CSI Driver is not installed or kubelet does not have permission to view the CSI Driver, the CSI Plugin will not be triggered correctly.

Run the command `kubectl get csidriver` to check whether the CSI Driver is installed.
- If the CSI Driver is not installed, run the command `kubectl apply -f charts/fluid/fluid/templates/csi/driver.yaml` to install it, and then observe whether the PVC is successfully mounted to the application.
- If the problem persists, run the command `export KUBECONFIG=/etc/kubernetes/kubelet.conf && kubectl get csidriver` to check whether kubelet has permission to view the CSI Driver.




