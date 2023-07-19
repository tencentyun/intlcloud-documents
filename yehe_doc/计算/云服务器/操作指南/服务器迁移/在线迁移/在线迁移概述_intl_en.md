Online migration supports migrating or synchronizing systems and applications on the source server or virtual machine from your IDCs or other cloud platforms to Tencent Cloud with no system downtime.
With go2tencentcloud, the migration tool provided by Tencent Cloud, you can directly migrate all systems and applications on the source server to the destination CVM, without the need to create, upload, and import images. It can meet enterprises' business requirements for cloud deployment, cross-cloud migration, cross-account or cross-region migration, and hybrid cloud deployment.

<dx-alert infotype="explain" title="">
The source server can be a physical server, a virtual machine, or a cloud server on third-party cloud platform, such as AWS, Google Cloud Platform, VMware, Alibaba Cloud, or Huawei Cloud.
</dx-alert>



## Use Cases

Online migration is applicable to the scenarios including but not limited to:
-	 IT architecture cloudification
-	Hybrid cloud architecture deployment
-	Cross-cloud migration
-	Cross-account or cross-region migration

## Differences from Offline Migration

In offline migration, you need to create images for system disks or data disks on source servers, and then migrate images to the Cloud Virtual Machine (CVM) or Cloud Block Storage (CBS). You do not need to create images for online migration. Instead, you can run the migration tool on source servers to migrate them to destination CVMs.

## Starting Migration
Two methods for online migration are available. You can select the appropriate one as needed.
<table class="tg">
<thead>
  <tr>
    <th width="25%">Migration method</th>
    <th width="25%">Overview</th>
    <th width="25%">Use cases</th>
    <th width="25%">Characteristics</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky"><a href=" https://www.tencentcloud.com/document/product/213/55046">Online Migration - Importing source by using the migration tool</a></td>
    <td class="tg-0pky">Log in to the source instance, import the migration source with the tool, and create a migration task in the console to implement the migration.</td>
    <td class="tg-0pky"><li>Migrate via the public and private network<br></li><li>Migrate from other cloud platforms to Tencent Cloud</li><li>Migrate from customer IDC to Tencent Cloud</li></td>
    <td class="tg-0pky">High compatibility</td>
  </tr>
  <tr>
    <td class="tg-0pky"><a href="https://intl.cloud.tencent.com/document/product/213/53265">Online Migration - Console</a></td>
    <td class="tg-0pky">Log in to the console, perform identity authentication, quickly import the migration source and create a migration task.</td>
    <td class="tg-0pky"><li>No need to log in to the source server</li><li>Migration via the public network</li><li>Cross-cloud migration: Applicable to the scenarios where the source instances are located in Alibaba Cloud</li></td>
    <td class="tg-0pky">Quick migration in batch</td>
  </tr>
</tbody>
</table>

## FAQs

For more information, please see [FAQs about Server Migration](https://www.tencentcloud.com/document/product/213/32395).
