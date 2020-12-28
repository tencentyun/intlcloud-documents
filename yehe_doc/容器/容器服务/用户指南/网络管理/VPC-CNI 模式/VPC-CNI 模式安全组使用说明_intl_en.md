

You can bind specified security group to the ENI created in VPC-CNI mode through the following methods:

## Prerequisites

- The version of IPAMD component is v3.2.0 or later (Check the version through image tag).
- The IPAMD component has enabled the capability of security group (not enabled by default). The startup parameter is `--enable-security-groups`.
- Currently, only multiple Pods with shared ENI mode is supported.

## IPAMD Enabling Security Features

- Modify the existing tke-eni-ipamd deployment: `kubectl edit deploy tke-eni-ipamd -n kube-system`.
- Run the following command to add the startup parameter to `spec.template.spec.containers[0].args`.
  After modification, ipamd will restart automatically and take effect.
  After ipamd takes effect, the new ENI and the existing ENI without associated security group will bind the security group according to the following policy.
  
```yaml
- --enable-security-groups
# If you want to use the security groups from the primary ENI/instance by default, you do not add the security-Groups parameter.
- --security-groups=sg-xxxxxxxx,sg-xxxxxxxx
```



## Feature Logic

- If the startup parameter `--security-groups` is not set, or its value is empty, the security group of each node will use the security group bound to the node instance.
- After the feature is enabled, if `--security-groups` is set, the security group of each node is set to the security group set specified by `--security-groups`.
- Run the following command to view node security group. The `spec.securityGroups` domain contains node security group information.
  ```
	kubectl get nec <nodeName> -oyaml
	```
	Run the following command to modify the node security group, and it takes effect immediately.
	```
	kubectl edit nec <nodeName> 
	```
- After the feature is enabled, during node synchronization, for the existing ENI, if it does not bind a security group, it will bind the node security group; if it has bound a security group, no operation is performed and the original binding is retained; for the new ENI, it will bind the node security group.
