

You can bind specified security group to the ENI created in VPC-CNI mode through the following methods:

## Prerequisites

- The version of IPAMD component is v3.2.0 or later version. You can check the version through image tag.
- The IPAMD component has enabled the capability of security group (not enabled by default). The startup parameter is `--enable-security-groups`.
- Currently, only multi-Pod with shared ENI mode is supported.

## Adding Security Group Access Permission for the IPAMD Component Role

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/policy), select **Policies** in the left sidebar.
2. Click **Create Custom Policy** in the **Policies** page.
3. In the **Select Policy Creation Method** window that pops up, click **Create by Policy Syntax** to go to the policy template page.
4. Select a blank template and click **Next** to go to the **Edit Policy** page.
5. In the **Edit Policy** page, enter the policy name and the policy syntax, and click **Complete**.
>? The policy can be named as `SecurityGroupsAccessForIPAMD`.
```
{
        "version": "2.0",
        "statement": [
            {
                "action": [
                    "cvm:AssociateNetworkInterfaceSecurityGroups",
                    "cvm:DisassociateNetworkInterfaceSecurityGroups"
                ],
                "resource": "*",
                "effect": "allow"
            }
        ]
}
```
6. In [**CAM console** > **Roles**](https://console.cloud.tencent.com/cam/role), search for the role of the IPAMD component `IPAMDofTKE_QCSRole`, click the role name to go to the role details page.
7. Click **Associate Policies**.
8. In the pop-up window, select the created custom policy `SecurityGroupsAccessForIPAMD` and click **OK**.

## Enabling Security Features for IPAMD





- Modify the existing tke-eni-ipamd deployment: `kubectl edit deploy tke-eni-ipamd -n kube-system`.

- Run the following command to add the startup parameter to `spec.template.spec.containers[0].args`.
After modification, ipamd will restart automatically and take effect.
After ipamd takes effect, the ENIs of the newly added nodes and the ENIs of the existing nodes that do not bind security groups will bind the security group according to the following policy.
```yaml
- --enable-security-groups
# If you want to use the security groups of the primary ENI/instance by default, you do not add the security-Groups parameter.
- --security-groups=sg-xxxxxxxx,sg-xxxxxxxx
```
 If you want the security group policy to take effect on the existing nodes that have been bound the security groups, you need to manually disable the security group, and then enable the security group again to achieve synchronization. You can set as follows:
 1. Add an annotation to clear and disable the security groups bound to the ENIs of the node. After the annotation is added, the existing ENIs of the node will unbind all security groups:
```shell
kubectl annotate node <nodeName> --overwrite tke.cloud.tencent.com/disable-node-eni-security-groups="yes"
```
 2. After the value is reset to “no”, the existing ENIs of the node will rebind the security group configured in the above policy.
```shell
kubectl annotate node <nodeName> --overwrite tke.cloud.tencent.com/disable-node-eni-security-groups="no"
```










## Feature Logic

- If the startup parameter `--security-groups` is not set, or its value is empty, the security group of each node will use the security group bound to the node instance.

- After the feature is enabled, if `--security-groups` is set, the security group of each node is set to this security group set.

- Run the following command to view node security group. The `spec.securityGroups` contains the node security group information.
```
kubectl get nec <nodeName> -oyaml
```
Run the following command to modify the node security group. The modification will take effect immediately.
```
kubectl edit nec <nodeName> 
```

- After the feature is enabled, when the node is synchronized, for the new ENIs and the existing ENIs that do not bind a security group, the node security group will be bound to them. For the existing ENIs that have bound a security group, the bound security groups will be retained.
