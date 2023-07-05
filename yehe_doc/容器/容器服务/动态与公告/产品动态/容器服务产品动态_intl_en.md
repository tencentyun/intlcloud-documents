## August 2022
<table>
<tr><th style="width:20%">Update</th>	<th style="width:50%">Description</th> 
<th style="width:15%">Release Date</th>	<th style="width:15%">Documentation</th> </tr>
<tbody>
  <tr>
    <td>Released the brand-new native node.</td>
    <td>A native node is a brand-new node type of TKE. It supports declarative APIs and adopts the FinOps concept, facilitating cost reduction and efficiency improvement for Tencent Cloud resources through the "visual resource management dashboard", "smart request recommendation", and "dynamic dedicated scheduler".</td>
    <td>2022-08-04</td>
    <td>-</td>
  </tr>
	 <tr>
    <td>Supported managing image caches through CRD.</td>
    <td>Image caches can be managed through CRD on super nodes. Currently, management can be performed in the console and through TencentCloud API. With the image caching feature, Pods can be started within seconds.</td>
    <td>2022-08-04</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/44484">Image Cache</a></td>
  </tr>
	  <tr>
    <td>Supported declaring the size of resources required by a Pod.</td>
    <td>You can declare the size of the system disk required by a Pod through an annotation on super nodes. If the size exceeds 20 GiB, the excessive part will be billed based on the pay-as-you-go published price of CBS Premium Cloud Storage, meeting your requirements for system disk resources in special scenarios.</td>
    <td>2022-08-03</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/36162">Annotation</a></td>
  </tr>
  <tr>
    <td>Added third-party nodes.</td>
    <td>The TencentOS Server 2.4 (TK4) operating system is supported, which is compatible with the CentOS 7 user mode. The entry to create Cilium-Overlay clusters is added in the TKE console for easier use. In Cilium-Overlay network mode, the check for a conflict between the IP range of a container and that of another container in another cluster within the same VPC can be ignored, thereby solving your problem of IP resource insufficiency.</td>
    <td>2022-08-01</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/49152">Cilium-Overlay Mode</a></td>
  </tr>
</tbody>
</table>

## July 2022
<table>
<tr><th style="width:20%">Update</th>	<th style="width:50%">Description</th> 
<th style="width:15%">Release Date</th>	<th style="width:15%">Documentation</th> </tr>
<tbody>
  <tr>
    <td>Released all the super nodes.</td>
    <td>A super node is a brand-new node form of TKE, which supports custom node size and flexible configuration adjustment. The monthly subscription mode is more cost-effective, while the pay-as-you-go mode eliminates the need to reserve resource buffer, contributing to your cost reduction and efficiency improvement. Node management and resource operations are simplified, so that you can concentrate on the business.</td>
    <td>2022-07-26</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/39759">Supernodes Overview</a></td>
  </tr>
	  <tr>
    <td>Supported productized Nginx-ingress.</td>
    <td>The Nginx-ingress add-on can be quickly deployed for out-of-the-box Nginx services. By default, CM and CLS are integrated to meet the observability requirement.</td>
    <td>2022-07-25</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/38981">Installing Nginx-ingress Instance</a></td>
  </tr>
	  <tr>
    <td>Quickly cleared invalid RBAC resources.</td>
    <td>RBAC resource objects can be quickly cleared. De-registered Tencent Cloud accounts can be automatically detected, which is suitable for scenarios where cluster permissions need to be reclaimed after personnel turnover.</td>
    <td>2022-07-15</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/48776">Clearing De-registered Tencent Cloud Account Resources</a></td>
  </tr>
  <tr>
    <td>Released the deletion protection feature for the node pool.</td>
    <td>This feature is suitable for node resource protection, fixing the issue where node resources were batched released due to maloperations.</td>
    <td>2022-07-13</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/35900">Node Pool Overview</a></td>
  </tr>
	<tr>
    <td>Supported associating with a TMP instance.</td>
    <td>A cluster can be associated with a TMP instance during creation, simplifying the association process.</td>
    <td>2022-07-06</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/46736">Quick Migration from TPS to TMP</a></td>
  </tr>
</tbody>
</table>







