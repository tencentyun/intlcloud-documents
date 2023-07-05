 

To ensure a consistent user experience, TKE plans to deactivate the scaling group service on June 13, 2022. If your cluster has a created scaling group, you can convert it into a node pool through the **CreateClusterNodePoolFromExistingAsg API** or **in the console**. The conversion will not affect your business.

<dx-tabs>
::: Through the API
You can use the `CreateClusterNodePoolFromExistingAsg` API to convert the scaling group into a node pool. For detailed directions, see [CreateClusterNodePoolFromExistingAsg](https://intl.cloud.tencent.com/document/product/457/38780).
:::
::: Through the console

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** on the left sidebar.
2. On the cluster management list page, click the target cluster ID.
3. On the cluster details page, select **Node Management** > **Scaling group**.
4. On the node pool list page, select **More** > **Create Node Pool** on the right of the scaling group.
:::
</dx-tabs>

 

A node pool provides more stable and comprehensive elastic scaling capabilities than a scaling group, facilitating node creation, management, and termination. After the deactivation, you can use the node pool to manage created scaling groups. For more information, see [Node Pool Overview](https://intl.cloud.tencent.com/document/product/457/35900).



### Deactivation plan
- Creation entry closure: Starting from June 6, 2022, no more scaling groups can be created in the console or through the API.
- Feature deactivation and switch: The scaling group service will be deactivated on June 13, 2022. We recommend you convert your scaling group into the node pool as instructed in "Converting a scaling group into a node pool" before the deactivation date. Scaling groups that still exist after the date will be automatically converted into node pools for unified management.
