### Associated resource

An associated resource is a resource associated with the current resource; for example:
1. The current resource is contained in the associated resource; for example, a CVM instance is contained in a VPC.
2. The current resource is associated with the associated resource; for example, a CVM instance is associated with a CVM security group.
3. The associated resource is attached to the current resource; for example, an EIP is attached to a CVM instance.
4. The current resource contains the associated resource; for example, a VPC contains a NAT gateway.
For more information on the supported resource relationships, see [Supported Resource Types](https://www.tencentcloud.com/document/product/1164/51495).

### Rule

A rule is a function used to determine whether the resource configuration is compliant. Config uses functions to carry rule code and currently supports only managed rules, i.e., predefined rule templates. When creating a rule, you can directly select the target managed rule in the Config console. For more information, see [Rules](https://www.tencentcloud.com/document/product/1164/51502).

### Conformance pack

A conformance pack is a collection of rules tailored for compliance scenarios, which can be a preset or custom one. For more information, see [Supported Conformance Pack Templates](https://www.tencentcloud.com/document/product/1164/51526).

### Compliance evaluation result

The compliance evaluation result indicates the result of the evaluation of the associated resource against the rule at a certain time point.

### Configuration item

A configuration item is a collection of attributes of a resource at a certain time point, including metadata, attributes, relationships, and current configuration.

### Managed rule

A managed rule is predefined by Config. When creating a rule, you can directly select the target managed rule in the Config console. For more information, see [Supported Managed Rules](https://www.tencentcloud.com/document/product/1164/51503).


### Resource type

A resource type is a set of resources with the same characteristics in the same Tencent Cloud service, such as entity resources (computing and storage instances) and management resources (roles and policies). It has a dedicated name in the six-segment resource description.
Config resource types are described by resource identifiers. For more information, see [Supported Resource Types](https://www.tencentcloud.com/document/product/1164/51495).

### Resource timeline

The resource timeline indicates the full-lifecycle data of a resource, including configuration information, configuration change information, resource creation/deletion/modification operations, and resource compliance evaluation results. For more information, see [Viewing Resource Details](https://www.tencentcloud.com/document/product/1164/51501).
