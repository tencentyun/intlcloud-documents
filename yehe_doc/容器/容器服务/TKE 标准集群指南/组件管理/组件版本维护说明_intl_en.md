
## Release Notes

TKE provides enhanced add-ons to extend cluster features in various scenarios, including **network, storage, monitoring, image, scheduling, and GPU**. You can view the current add-on versions and manually upgrade them on the **Add-On Management** page in the TKE cluster details.

### Upgrade notice
1. The upgrade is an irreversible operation.
2. The add-ons can only be upgraded to a later version. By default, they are upgraded to the latest version compatible with the Kubernetes version.
3. **The TKE team no longer offers technical support for disused add-on versions.** We recommend you upgrade them in time.

## Version Iteration Records

### June 2022
<table>
<thead>
  <tr>
    <th width="18%">Add-On</th>
    <th width="12%">Release Date</th>
    <th width="10%">Version</th>
    <th width="32%">Update</th>
    <th width="28%">Limits and Impact</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/39146">DeScheduler</a><br>(rescheduler add-on)</td>
    <td>2022-06-07</td>
    <td>v1.0.1</td>
    <td>Supported TMP authentication: <li>Added `auth` authentication to `prom-probe`.</li><li>Passed in environment variables such as `token` and `appid` to DeScheduler and int containers and decoded them.</li><li>Added the Prometheus client authentication feature to DeScheduler.</li></td>
    <td>This upgrade doesn't affect the existing business. As the add-on may be unavailable during the upgrade, we recommend you upgrade it during off-peak hours.</td>
  </tr>
  <tr>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/42973">qGPU</a><br>(GPU isolation add-on)</td>
    <td>2022-06-08</td>
    <td>v1.0.3</td>
    <td><li>Updated the image of qgpu manager to `tkeimages/elastic-gpu-agent:v1.0.2`.</li><li>Updated the image of qgpu scheduler to `rtkeimages/elastic-gpu scheduler:v1.0.2`.</li><li>Supported using GPU CRD to manage GPU resources.</li></td>
    <td>This upgrade doesn't affect the existing business. As the add-on may be unavailable during the upgrade, we recommend you upgrade it during off-peak hours.</td>
  </tr>
    <tr>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/39119">DynamicScheduler</a><br>(Dynamic scheduler)</td>
    <td>2022-06-30</td>
    <td>v1.0.2</td>
    <td>Supported TMP authentication:<li>Added `auth` authentication to `probe-prometheus`.</li><li>Passed in environment variables such as `token` and `appid`to node-annotator and init containers and decoded them.</li><li>Added the Prometheus client authentication feature to node-annotator, and updated the image to v3.2.1.</li><br>Fixed the bug where data couldn't be queried for PromQL statements using the IP as the node exporter reporting label.</td>
    <td>This upgrade doesn't affect the existing business. As the add-on may be unavailable during the upgrade, we recommend you upgrade it during off-peak hours.</td>
  </tr>
</tbody>
</table>

### May 2022

<table>
<thead>
    <th width="18%">Add-On</th>
    <th width="12%">Release Date</th>
    <th width="10%">Version</th>
    <th width="32%">Update</th>
    <th width="28%">Limits and Impact</th>
</thead>
<tbody>
  <tr>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/39136">CBS-CSI</a><br>(CBS)</td>
    <td>2022-05-06</td>
    <td>v1.0.3</td>
    <td><li>Supported taint and toleration configuration.</li><li>Added the `type` startup parameter.</td>
    <td>This upgrade doesn't affect the existing business. As the add-on may be unavailable during the upgrade, we recommend you upgrade it during off-peak hours.</li></td>
  </tr>
  <tr>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/38706">COS-CSI</a><br>(COS)</td>
    <td>2022-05-06</td>
    <td>v1.0.1</td>
    <td>Supported taint and toleration configuration.</td>
    <td>This upgrade doesn't affect the existing business. As the add-on may be unavailable during the upgrade, we recommend you upgrade it during off-peak hours.</td>
  </tr>
  <tr>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/38707">CFS-CSI</a><br>CFS</td>
    <td>2022-05-06</td>
    <td>v1.0.4</td>
    <td>Supported the idempotency for `umount`.</td>
    <td>This upgrade doesn't affect the existing business. As the add-on may be unavailable during the upgrade, we recommend you upgrade it during off-peak hours.</td>
  </tr>
  <tr>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/38707">CFS-CSI</a><br>CFS</td>
    <td>2022-05-24</td>
    <td>v1.0.5</td>
    <td>Supported EKS cfs provisioner.</td>
    <td>This upgrade doesn't affect the existing business. As the add-on may be unavailable during the upgrade, we recommend you upgrade it during off-peak hours.</td>
  </tr>
  <tr>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/39136">CBS-CSI</a><br>(CBS)</td>
    <td>2022-05-31</td>
    <td>v1.0.4</td>
    <td><li>Optimized the add-on startup logic.</li><li>Adjusted the default number of concurrent csi-attacher requests to 50.</li></td>
    <td>This upgrade doesn't affect the existing business. As the add-on may be unavailable during the upgrade, we recommend you upgrade it during off-peak hours.</td>
  </tr>
</tbody>
</table>

### April 2022

<table>
<thead>
  <tr>
    <th width="18%">Add-On</th>
    <th width="12%">Release Date</th>
    <th width="10%">Version</th>
    <th width="32%">Update</th>
    <th width="28%">Limits and Impact</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/38707">CFS-CSI</a><br>CFS</td>
    <td>2022-04-12</td>
    <td>v1.0.2</td>
    <td>Supported the idempotency for `umount`.</td>
    <td>This upgrade doesn't affect the existing business. As the add-on may be unavailable during the upgrade, we recommend you upgrade it during off-peak hours.</td>
  </tr>
  <tr>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/38707">CFS-CSI</a><br>CFS</td>
    <td>2022-04-19</td>
    <td>v1.0.3</td>
    <td><li>Added the resource label field to tcfs crd.</li><li>Installed no tcfs resources on Kubernetes 1.12 or earlier.</li><li>Optimized the registration and startup of cfs-csi startServer.</li></td>
    <td>This upgrade doesn't affect the existing business. As the add-on may be unavailable during the upgrade, we recommend you upgrade it during off-peak hours.</td>
  </tr>
  <tr>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/42973">qGPU</a><br>(GPU isolation add-on)</td>
    <td>2022-04-21</td>
    <td>v1.0.2</td>
    <td><li>Updated the image version of qgpu manager. Supported automatic settings of GPU driver version and other information on the current node.</li><li>Updated the `qgpu-manager` ClusterRole to add operation permissions for nodes.</li></td>
    <td>This upgrade doesn't affect the existing business. As the add-on may be unavailable during the upgrade, we recommend you upgrade it during off-peak hours.</td>
  </tr>
  <tr>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/39136">CBS-CSI</a><br>(CBS)</td>
    <td>2022-04-24</td>
    <td>v1.0.2</td>
    <td><li>Canceled the directory clearance logic in the `NodeUnpublishVolume` API.</li><li>Supported getting the driver letter through the serial number.</li><li>Retained the corresponding CRD resources while deleting the add-on.</li></td>
    <td>This upgrade doesn't affect the existing business. As the add-on may be unavailable during the upgrade, we recommend you upgrade it during off-peak hours.</td>
  </tr>
</tbody>
</table>

### March 2022

<table>
<thead>
  <tr>
    <th width="18%">Add-On</th>
    <th width="12%">Release Date</th>
    <th width="10%">Version</th>
    <th width="32%">Update</th>
    <th width="28%">Limits and Impact</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/39136">CBS-CSI</a><br>(CBS)</td>
    <td>2022-03-16</td>
    <td>v1.0.1</td>
    <td>Supported in-place lossless migration of workloads using `intree cbs` to CSI while upgrading the cluster from v1.18 to v1.20.</td>
    <td>This upgrade doesn't affect the existing business. As the add-on may be unavailable during the upgrade, we recommend you upgrade it during off-peak hours.</td>
  </tr>
  <tr>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/38707">CFS-CSI</a><br>CFS</td>
    <td>2022-03-24</td>
    <td>v1.0.1</td>
    <td>Supported using automatically generated subdirectories for data isolation in the shared storage instance during dynamic creation.</td>
    <td>This upgrade doesn't affect the existing business. As the add-on may be unavailable during the upgrade, we recommend you upgrade it during off-peak hours.</td>
  </tr>
</tbody>
</table>
