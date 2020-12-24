
TKE supports the Kubernetes RBAC authorization method, allowing you to perform fine-grained access control for sub-accounts. With this authorization method, you can access resources in a cluster through the TKE console and kubectl. For more information, see the following figure.
![](https://main.qcloudimg.com/raw/3bd92966b4b7a5d6ac4e5e0463b0a20a.png)


## Glossary
#### RBAC
Role-Based Access Control (RBAC) associates users and permissions with roles to indirectly grant permissions to users.
In Kubernetes, RBAC is implemented through the `rbac.authorization.k8s.io` API group, which allows cluster administrators to dynamically configure policies through Kubernetes APIs.

#### Role
A Role is used to define access permissions for resources in a single namespace.

#### ClusterRole
A ClusterRole is used to define access permissions for resources in an entire cluster.

#### RoleBinding
RoleBinding grants the permissions defined in a role to a user or group of users in order to grant authorization for a namespace.

#### ClusterRoleBinding
ClusterRoleBinding grants the permissions defined in a role to a user or group of users in order to grant cluster-wide authorization.

For more information, see the [Kubernetes official documentation](https://kubernetes.io/zh/docs/reference/access-authn-authz/rbac/).


## Solutions for TKE Kubernetes Object-Level Permission Control
### Verification method
Kubernetes API servers support various verification policies, such as x509 certificates, bearer tokens, and basic auth. Of these, only individual bearer token verification policies support verification based on the tokens of specified known-token csv files, such as bearer tokens, serviceaccount tokens, OIDC tokens, and webhook token servers.

With implementation complexity and different usage scenarios in mind, TKE has chosen to use x509 certificates as the verification method. This verification method offers the following advantages:
- This method is easier for users to understand.
- No complex changes need to be made to existing clusters.
- You can sort by users and groups, which facilitates subsequent scaling.

TKE implements the following features based on x509 certificate verification:
- Each sub-account has a unique client certificate used for accessing Kubernetes API servers.
- When a sub-account accesses Kubernetes resources on the console, the backend uses the sub-account’s client certificate to access the Kubernetes API server by default.
- A sub-account can update its unique client certificate to prevent credential disclosure.
- A root account or an account that has `tke:admin` permission for a cluster can view and update the certificates of other sub-accounts.

### Authorization method
Kubernetes supports two main authorization methods: RBAC and Webhook Server. In order to provide a consistent experience for users who are familiar with and work with native Kubernetes, TKE has chosen RBAC as its authorization method. This authorization method provides preset Roles and ClusterRoles. You only need to create the corresponding RoleBinding or ClusterRoleBinding to implement authorizations for a cluster or namespace. This authorization method has the following advantages:
- It is friendly to users who have a basic knowledge of Kubernetes.
- It allows you to reuse Kubernetes RBAC capabilities and supports various verb-based permission controls for namespaces, API groups, and resources.
- It supports custom policies.
- It allows you to manage custom extended API resources.


## Features of TKE Kubernetes Object-level Permission Control
By using the authorization management feature provided by TKE, you can perform more fine-grained permission control. For example, you can configuring sets of permissions such as assigning read-only permissions to a sub-account or assigning read/write permissions to only a certain namespace under a sub-account. For more information on configuring more fine-grained sets of permissions for sub-accounts, see the following documents:
- [Using a preset identity for authorization](https://intl.cloud.tencent.com/document/product/457/37368)
- [Using custom policies for authorization](https://intl.cloud.tencent.com/document/product/457/37369)



