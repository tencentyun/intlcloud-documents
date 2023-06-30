## Mesh Mode

### Managed mode

Managed mode means that the control plane components of a mesh are managed by Tencent Cloud Mesh, and the Tencent Cloud Mesh team is responsible for ensuring the availability of the control plane of the mesh, eliminating deployment and operations costs of control plane resources for a user. The user only needs to focus on the use of the mesh. Currently, managed meshes are not separately billed, and therefore it is recommended that you choose the managed mode preferentially.

Feature differences between a managed mesh and a stand-alone mesh

| Capability | Managed Mesh | Stand-alone Mesh |
| --------------------- | -------- | -------- |
| Operations-free control plane  | Support | Not support |
| Login to a control plane host | Not support | Support |
| Mesh management through Istioctl | Not support | Support |

### Stand-alone mode

Stand-alone mode means that the control plane components of a mesh are deployed in a cluster specified by a user and are maintained by the user. In this mode, the user has greater autonomy, but also needs to assume a greater availability risk. Currently, a stand-alone mesh can be used after being added to an allowlist. If you need to use a stand-alone mesh, contact after-sales personnel or [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## Quota Limits

- Maximum number of meshes by default: 20
- Maximum number of clusters in a single mesh: 10
- Maximum number of regions in a single mesh: 3

- To use more resources, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for them.
