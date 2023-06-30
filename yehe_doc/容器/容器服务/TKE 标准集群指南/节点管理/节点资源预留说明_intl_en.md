

TKE clusters occupy node resources to run add-ons (such as kubelet, kube-proxy, and runtime). Therefore, **the total number of node resources** and **the number of allocable resources in a cluster** may differ from each other. This document describes the policies and notes in terms of node resource reservation in TKE clusters so that you can set reasonable numbers of requested resources and limited resources for Pods when deploying an application.

## Policy for Calculating Allocable Node Resources

### Calculation formula
Allocable = Capacity - Reserved - Eviction - Threshold

### Node CPU reservation rules

<table>
<thead>
  <tr>
    <th width="30%">Node CPU</th>
    <th width="30%">Reservation Rule</th>
    <th>Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>1c &lt;= CPU &lt;= 4c</td>
    <td>0.1c is reserved.</td>
    <td>-</td>
  </tr>
  <tr>
    <td>4c &lt; CPU &lt;= 64c</td>
    <td>0.1c is reserved for the 4c part, and 2.5% for the excessive part.</td>
    <td>For example, if CPU = 32c, <br>reserved resources = 0.1 + (32 - 4) * 2.5% = 0.8c.</td>
  </tr>
  <tr>
    <td>64c &lt; CPU &lt;= 128c</td>
    <td>0.1c is reserved for the 4c part, 2.5% for the 4c to 64c part, and 1.25% for the excessive part.</td>
    <td>For example, if CPU = 96c, <br>reserved resources = 0.1 + (64 - 4) * 2.5% + (96 - 64) * 1.25% = 1.2c.</td>
  </tr>
  <tr>
    <td>CPU &gt; 128c</td>
    <td>0.1c is reserved for the 4c part, 2.5% for the 4c to 64c part, 1.25% for the 64c to 128c part, and 0.5% for the excessive part.</td>
    <td>For example, if CPU = 196c, <br>reserved resources = 0.1 + (64 - 4) * 2.5% + (96 - 64) * 1.25% + (196 - 128) * 0.5% = 1.54c.</td>
  </tr>
</tbody>
</table>

### Node memory reservation rules

<table>
<thead>
  <tr>
    <th width="30%">Node Memory</th>
    <th width="30%">Reservation Rule</th>
    <th>Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>1 GB &lt;= Memory &lt;= 4 GB</td>
    <td>25% is reserved.</td>
    <td>For example, if memory = 2 GB, <br>reserved resources = 2 * 25% = 500 MB.</td>
  </tr>
  <tr>
    <td>4 GB &lt; Memory &lt;= 8 GB</td>
    <td>25% is reserved for the 4 GB part, and 20% for the excessive part.</td>
    <td>For example, if memory = 8 GB, <br>reserved resources = 4 * 25% + (8 - 4) * 20% = 1,843 MB.</td>
  </tr>
  <tr>
    <td>8 GB &lt; Memory &lt;= 16 GB</td>
    <td>25% is reserved for the 4 GB part, 20% for the 4 GB to 8 GB part, and 10% for the excessive part.</td>
    <td>For example, if memory = 12 GB, <br>reserved resources = 4 * 25% + (8 - 4) * 20% + (16 - 8) * 10% = 2,252 MB.</td>
  </tr>
  <tr>
    <td>16 GB &lt; Memory &lt;= 128 GB</td>
    <td>25% is reserved for the 4 GB part, 20% for the 4 GB to 8 GB part, 10% for the 8 GB to 16 GB part, and 6% for the excessive part.</td>
    <td>For example, if memory = 32 GB, <br>reserved resources = 4 * 25% + (8 - 4) * 20% + (16 - 8) * 10% + (32 - 16) * 6% = 3,645 MB.</td>
  </tr>
  <tr>
    <td>Memory &gt; 128 GB</td>
    <td>25% is reserved for the 4 GB part, 20% for the 4 GB to 8 GB part, 10% for the 8 GB to 16 GB part, 6% for the 16 GB to 128 GB part, and 2% for the excessive part.</td>
    <td>For example, if memory = 320 GB, <br>reserved resources = 4 * 25% + (8 - 4) * 20% + (16 - 8) * 10% + (128 - 16) * 6% + (320 - 128) * 2% = 13,475 MB.</td>
  </tr>
</tbody>
</table>

>? You can use custom kubelet parameters to modify `kube-reserved` for node resource reservation. We recommend you reserve sufficient CPU and memory resources for add-ons to ensure node stability.

## Viewing Allocable Node Resources
Run the following command (replace `NODE_NAME` with the actual node name) to check the allocable node resources in a cluster. The output result contains `Capacity` and `Allocatable` fields, along with measurements of CPU, memory, and temporary storage.

```
kubectl describe node NODE_NAME | grep Allocatable -B 7 -A 6
```

## Notes
- The reservation policy automatically takes effect for K8s v1.16 or later and nodes created after June 24, 2022, without no manual configuration required.
- To ensure your business stability, the reservation policy won't take effect for existing nodes. This is because allocable resources may become fewer based on the calculation method, which means possible node eviction for nodes requiring a large number of resources.
- If you want to apply the reservation policy to existing nodes, remove them from the cluster without termination and then add them in the [TKE console](https://console.cloud.tencent.com/tke2/cluster). In this case, they become newly added nodes subject to the policy by default.
