Cloud Security Configuration Management provides the security configuration check feature for relevant cloud products on Tencent Cloud. The security configuration check and management cover computing and application configuration security, network configuration security, storage and data security, and identity authentication security. This lays a solid foundation for the secure operation of your business on Tencent Cloud.


## Prerequisites
- To use the Cloud Security Configuration Management feature, you must have [Security Operation Center Premium](https://buy.cloud.tencent.com/soc) enabled.
- If you have not created a preset role for the service and granted permissions to the Security Operation Center, on the [Cloud Security Configuration Manager](https://console.cloud.tencent.com/ssav2/config) page, click **Go to access manager**. On the Role Manager page that appears, click **Agree to grant permissions**. If you have granted such permissions, skip this step.

## Definitions

| **Term** | **Definition**                                                     |
| ------------ | ------------------------------------------------------------ |
| Configuration check item | Each configuration check item indicates a specific security requirement for a configuration, which often comes from a specification. The security of the configurations for products on Tencent Cloud is checked based on such items. |
| Configuration check policy | The check policy that requires a specific range of products on Tencent Cloud to meet the requirements of a collection of configuration check items.   |
| Configuration check results | The actual result of configuration check, namely, the cases that are non-compliant/compliant with configuration requirements.      |
| Specification         | The collection of configuration check items that often corresponds to a law regulation or company specification, such as the requirements for IT systems and networks of Level-3 in Multi-Level Protection Scheme 2.0. |
| Check object     | The cloud product that is checked based on a configuration check item.                               |
| Configuration risk     | An instance of a check object that violates the configuration requirements under a policy is a configuration risk. The check results of the same configuration items under different policies are regarded as different configuration risks. |


