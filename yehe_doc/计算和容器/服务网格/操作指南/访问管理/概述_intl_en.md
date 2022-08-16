Permission management of a service mesh contains management of [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/17848) permissions and [Tencent Kubernetes Engine (TKE) RBAC](https://intl.cloud.tencent.com/document/product/457/37366) permissions.

By default, a sub-account does not have CAM permissions, and a sub-account that is not a cluster creator does not have RBAC permissions for the related cluster. You need to create and associate CAM policies and TKE RBAC authorization policies to allow sub-accounts to access or normally use service mesh resources they need.

CAM permission policies are edited and granted by a CAM administrator (usually a root account or a sub-account with CAM permissions). For more basic information about CAM policies, see [CAM policies](https://intl.cloud.tencent.com/document/product/598/32668). RBAC permission policies of a TKE cluster are usually edited and granted by a corresponding cluster administrator (usually a root account or an account that creates the cluster). For information about authorization methods, see [TKE RBAC authorization](https://intl.cloud.tencent.com/document/product/457/37368).

>?Skip this chapter if you do not need to manage the access permission of sub-accounts for Tencent Cloud Mesh resources. This will not affect your understanding and use of the other sections of the document.

## CAM-based Permission Control
Currently, Tencent Cloud Mesh supports CAM-based resource-level permission control. In other words, Tencent Cloud Mesh can allow specified **sub-accounts** to perform specified **operations** on specified **resources**. The sub-accounts do not have Tencent Cloud Mesh-related CAM permissions by default. You need to associate policies with the sub-accounts to complete authorization.

In addition, Tencent Cloud Mesh supports CAM-based resource-level permission control at a granularity of mesh instance. In other words, you can control specified sub-account to perform specified operations on a specified mesh.

## RBAC Permission Management of TKE (Tencent Cloud Mesh-related Product)

The use of Tencent Cloud Mesh involves read and write operations on Kubernetes resources in the TKE clusters managed by Tencent Cloud Mesh. These operations require sufficient TKE RBAC permissions are available. By default, a sub-account that is not the cluster creator does not have the RBAC permissions for the cluster. The cluster administrator needs to grant the RBAC permissions for the corresponding cluster to the sub-account before the sub-account can use Tencent Cloud Mesh normally.

The following operations require administrator (tke:admin) permissions for the corresponding cluster: creating/deleting/updating a service mesh in the selected cluster, adding/dissociating a service discovery cluster, and creating/deleting an ingress gateway in the selected cluster. Operations on Istio resources (such as Gateway, VirtualService, DestinationRule, and ServiceEntry) in the mesh do not require RBAC permissions for the cluster.

For more information about TKE Kubernetes object-level permission control, see [TKE Kubernetes Object-level Permission Control](https://intl.cloud.tencent.com/document/product/457/37366). For information about TKE RBAC authorization modes, see [Comparison of Authorization Modes](https://intl.cloud.tencent.com/document/product/457/37367).
