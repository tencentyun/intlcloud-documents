

You can bind specified security group to the ENI created in VPC-CNI mode through the following methods:

## Prerequisites

- The version of IPAMD component is v3.2.0 or later version. You can check the version through image tag.
- The IPAMD component has enabled the capability of security group (not enabled by default). The launch parameter is `--enable-security-groups`.
- Currently, only multiple Pods with shared ENI mode is supported.

## Enabling Security Group Feature for the IPAMD Component

### tke-eni-ipamd v3.5.0 or later

1. Log in to the [TKE console](https://console.qcloud.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster Management** page, click the ID of the target cluster to go to the cluster details page.
3. On the cluster details page, select **Add-On Management** in the left sidebar.
4. On the **Add-On Management** page, click **Update configuration** in the **Operation** column of the **eniipamd** add-on.
5. On the **Update configuration** page, select **Security group**.
6. If you want to use the security group of the primary ENI, do not specify a security group. Otherwise, specify one and click **Done**.

### tke-eni-ipamd earlier than v3.5.0 or no eniipamd to manage

- Modify the existing tke-eni-ipamd deployment:
```
kubectl edit deploy tke-eni-ipamd -n kube-system
```
- Run the following command to add the launch parameter to `spec.template.spec.containers[0].args`.
After the modification, ipamd will restart and take effect automatically.
For a secondary ENI that is not associated with a security group on an existing node, a security group will be bound to it based on the following policy. If a security group has been bound, strong synchronization will be performed for the set security group unless the feature has been enabled before and a security group has been set on the node. The following security group will be bound to all ENIs on a new node.
```yaml
- --enable-security-groups
# If you want to use the security groups of the primary ENI/instance by default, do not add the security-groups parameter.
- --security-groups=sg-xxxxxxxx,sg-xxxxxxxx
```

### Method of synchronizing ENI security group settings of existing nodes

 If you want the security group policy to take effect on the existing nodes that have been set the security groups, you need to manually disable the security group, and then enable the security group again to achieve synchronization. You can operate as follows:
 1. Add an annotation to clear and disable the security groups bound to the ENIs of the node. After the annotation is added, the existing ENIs of the node will unbind all security groups:
```shell
kubectl annotate node <nodeName> --overwrite tke.cloud.tencent.com/disable-node-eni-security-groups="yes"
```
 2. After the value is reset to “no”, the security groups configured based on the above policy can be rebound.
```shell
kubectl annotate node <nodeName> --overwrite tke.cloud.tencent.com/disable-node-eni-security-groups="no"
```


## Feature Logic

- If the launch parameter `--security-groups` is not set, or its value is empty, the security group of each node will use the security group bound to the node instance.
- After the feature is enabled, if `--security-groups` is set, the security group of each node is set to this security group set.
- After the feature is enabled, if `--security-groups` is modified, the settings of security groups on new nodes will be synced with global parameters, and the settings of security groups on existing nodes will remain unchanged. If you want to sync the settings of security groups on existing nodes, you need to disable security group on the node and enable it again. For operation details, see [Enabling Security Group Feature for the IPAMD Component](https://intl.cloud.tencent.com/document/product/457/38977).
- The priority for setting a security group is consistent with the sequence of setting a security group on a node. If the security group of the primary ENI is used, the priority is consistent with that of the primary ENI.
- Run the following command to view the security group of the node. The `spec.securityGroups` contains the information of the security group of the node.
```
kubectl get nec <nodeName> -oyaml
```
Run the following command to modify the security group of the node. The modification will take effect immediately.
```
kubectl edit nec <nodeName> 
```
- After the feature is enabled, if an existing ENI is not bound with a security group, security group of the node will be bound to it at the time of node synchronization. Security group of an existing ENI will be strong synced with the security group of the node to ensure consistency with the security group of the node. A new ENI will be bound with security group of the node.
