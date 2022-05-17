## CAM Overview
When using Tencent Cloud EMR, different departments and roles need different permissions in order to avoid security risks such as leakages and maloperations. To this end, you can assign different permissions to different users through sub-accounts. By default, a sub-account does not have the permission to use EMR or related resources. Therefore, you need to create a policy to grant the required permission to the sub-account first.

Cloud Access Management (CAM) is a web-based Tencent Cloud service that helps you securely manage and control access permissions, resources, and use permissions of your Tencent Cloud account. Using CAM, you can create, manage, and terminate users (groups), and control the Tencent Cloud resources that can be used by the specified user through identity and policy management.

When using EMR, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks. For more information on CAM policies, see [Element Reference]. For more information on how to use CAM policies, see [Policy].

## CAM Use Cases

### 1. Resource management permissions need to be granted to sub-users

You can create users or roles in CAM and assign them separate security credentials (console login passwords, TencentCloud API keys, etc.) or request temporary credentials for them to access Tencent Cloud resources. You can also manage permissions to control the operations users and roles can perform and the resources they can access.

### 2. Users with external Tencent Cloud roles can access Tencent Cloud resources

You can use your existing authentication system through CAM to grant your employees and services the access permissions for Tencent Cloud services and resources.

### 3. Strengthen your security with an additional layer of protection

Currently, three authentication methods are supported: WeChat QR code, hardware/virtual MFA, and mobile verification code.

## Supported CAM Granularities
EMR supports **resource-level authentication** and **API-level authentication**. For API-level authentication, API input parameters include the cluster string ID, and the TencentCloud API directly forwards the authentication request to CAM for authentication. Resource-level authentication involves fine-granularity authentication on the EMR backend. EMR supports three authorization methods: resource-level authorization, API-level authorization, and authorization by tag.

**Resource-level and API-level authorization**: You can use policy syntax to grant sub-accounts permissions to manage individual resources. For more information, see [Authorization Granularity Scheme](https://intl.cloud.tencent.com/document/product/1026/44862).

**Authorization by tag**: You can tag resources and grant sub-accounts permissions to manage resources with particular tags. For more information, see [Authorization Granularity Scheme](https://intl.cloud.tencent.com/document/product/1026/44862).
