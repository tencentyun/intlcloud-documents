>? This document introduces the updates to Tencent Container Registry (TCR) Enterprise Edition. For more information on the updates to Tencent Kubernetes Engine (TKE), see [Release Notes](https://intl.cloud.tencent.com/zh/document/product/1051/38387).

## November 2021

<table>
 <tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Related Documents</th></tr>
<tr><td>Changes the entry point of TCR Individual in the console</td><td>Starting from November 1, 2021 (UTC +8), entry of TCR Individual (the original path: TKE > Image Repository) in the console will be changed to be located in the TCR console and this will be in beta test. For the relationship of the existing features in the two consoles, see related documents.</td><td>Announcement on Merging the Entries of TCR Enterprise and TCR Individual</a></td></tr>
</table>

## October 2021

<table>
 <tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Related Documents</th></tr>
<tr><td>The logs of instance replication can be checked</td><td>The instance replication feature now supports checking replication logs, and supports querying via API.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/39845">Configuring Instance Replication</a></td></tr>
 <tr><td>TCR console supports unified management of image repositories of TCR Individual</td><td>The TCR console now supports unified management of image repositories of TCR Individual. You can check the instances of TCR Individual, and manage namespaces and image repositories, etc.</td><td>-</td></tr>
</table>

## July 2021

<table>
 <tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Related Documents</th></tr>
<tr><td>Supports cross-master account instance synchronization</td><td>The instance synchronization feature supports cross-master account target instances and realizes cross-master account instance data synchronization.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35494">Configuring Instance Synchronization</a></td></tr>
 <tr><td>Supports image tag immutability</td><td>Supports enabling the tag immutability feature for images hosted in TCR, which ensures that images of the same tag will only be successfully pushed once.</td><td><a href="https://intl.cloud.tencent.com/zh/document/product/1051/41707">Configuring Image Tag Immutability</a></td></tr>
</table>

## June 2021

<table>
<tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Related Documents</th></tr>
<tr><td>Enhances TCR console features</td><td>The original instance list page has been upgraded to an instance management page, where you can view the instance overview, the latest TCR features and product updates.</td><td>-</td></tr>
<tr><td>Supports batch adding/editing for public network access allowlist</td><td>TCR console supports entering multiple allowlists at a single time or importing existing security group.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35491">Public Network Access Control</a></td></tr>
<tr><td>Supports auto-parsing management and adds multiple supported regions</td><td>Adds Nanjing, HongKong, Singapore, Frankfurt, Chengdu, and Chongqing as the supported regions.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35492">Private Network Access Control</a></td></tr>
<tr><td>Supports removal of unused image data</td><td>Users can set custom rules to remove unused image data of Enterprise Edition instances in batch to release storage capacity. Dry runs are supported.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/41073">Releasing COS Storage Capacity</a></td></tr>
</table>

## April 2021

<table>
 <tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Related Documents</th></tr>
<tr><td>Supports querying audit logs</td><td>TCR Enterprise has been accessed to Tencent CloudAudit. You can check the logs of read and write operations of instances, namespaces, and image repositories in "Event History".</td><td>-</td></tr>
</table>

## March 2021

<table>
 <tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Related Documents</th></tr>
<tr><td>Supports custom domain names</td><td>TCR supports custom domain names. User can add custom domain names and SSL certificates to the Enterprise Edition instances, and access the instance through the HTTPS protocol.</td><td>Configuring Custom Domain Name</a></td></tr>
</table>


## January 2021

<table>
 <tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Related Documents</th></tr>
 <tr><td>Supports multi-region replication of a single instance</td><td>Users can create replicas of an Enterprise Premium instance in multiple regions with the same access domain name and credential as the original Enterprise Edition instance and synchronize underlying image data of the original instance to replicas in real time. After image data is uploaded, it can be downloaded through the local private network in multiple regions.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/39845">Configuring Instance Replication</a></td></tr>
 <tr><td>Supports cloud-native artifacts and multi-architecture images</td><td>Enterprise Edition instances are compatible with cloud-native artifacts (OCI). Image Registry can host Helm Charts, CNAB and other cloud-native artifacts. Enterprise Edition instances can host multi-architecture container images, such as amd64 and arm, to be applicable to IoT and edge computing scenarios.</td><td>-</td></tr>
 <tr><td>Supports on-demand container image loading</td><td>An Enterprise Premium instance can enable the on-demand container image loading feature. When cluster nodes pull image data from the instance, they can load pulled data as needed, improving the container startup speed.</td><td>Loading Container Images on Demand</a></td></tr>
 <tr><td>Optimizes the private network access feature</td><td>When a private network access linkage is created for an instance deployed in China, the VPCDNS can be used to configure private network resolution for the instance access domain name, without the need to use an external DNS or configure the host.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35492">Private Network Access Control</a></td></tr>
 <tr><td>TCR Enterprise Edition is available in regions of Beijing Finance and Taipei</td><td>TCR Enterprise Edition is now available in regions of Beijing Finance and Taipei. For more information on billing, see Billing Overview.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35483">Billing Overview</a></td></tr>


</table>

## December 2020

<table>
 <tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Related Documents</th></tr>
 <tr><td>Starts commercial billing for TCR Enterprise Edition</td><td>TCR Enterprise Edition instances have ended beta testing and will be billed. SLA guarantees are provided, and users can purchase instances in pay-as-you-go mode.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35483">Billing Overview</a></td></tr>
 <tr><td>TCR Enterprise Edition is available in Virginia and Frankfurt regions</td><td>TCR Enterprise Edition is now available in the Virginia and Frankfurt regions. For more information on billing, see Billing Overview.</td><td><ahref="https://intl.cloud.tencent.com/document/product/1051/35483">Billing Overview</a></td></tr>
</table>

## October 2020

<table>
 <tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Related Documents</th></tr>
 <tr><td>Adds support for multiple code sources in the image building feature</td><td>The private GitLab and TGit code sources are now supported, and the code source authorization process has been optimized.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/37252">Configuring Image Building</a></td></tr>
 <tr><td>Image filtering is supported in the delivery pipeline deployment feature</td><td>Local push images can be used to trigger the deployment process, and filtering rules can be configured to deploy only the most recently pushed images that meet the rules.</td><td>Using Delivery Pipeline to Implement Container DevOps</td></tr>
</table>

## September 2020

<table>
 <tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Related Documents</th></tr>
 <tr><td>Adds image tag retention feature</td><td>Automatic clearing rules can be configured for image tags in a namespace to periodically clear historical image tags.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/41657">Auto-Deleting Image Tags</a></td></tr>
</table>

## August 2020

<table>
 <tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Related Documents</th></tr>
 <tr><td>The TCR plug-in is supported in TKE clusters</td><td>A TKE cluster can install the TCR Enterprise Edition plug-in quickly to enable secret-free pulling of container images and Helm Charts through the private network. This significantly improves the application deployment experience.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/38386">TKE Clusters Use the TCR Plug-In to Enable Secret-Free Pulling of Container Images through Private Network</a></td></tr>
  <tr><td>Adds support for Tencent Cloud tags</td><td>Users can now bind Enterprise Edition instances with Tencent Cloud tags, with which they can perform instance resource filtering and permission management.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/39088">Creating an Enterprise Edition Instance</a></td></tr>
</table>

## July 2020

<table>
 <tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Related Documents</th></tr>
 <tr><td>Launches the delivery pipeline feature</td><td>After a delivery pipeline is configured, code updates can automatically trigger image building, image push, and application updates. When used with TKE, this feature can quickly implement container DevOps.</td><td>Using the Delivery Pipeline to Implement Container DevOps</a></td></tr>
  <tr><td>Updates the Helm Chart feature</td><td>Users can upload and download Chart packages through the console. TKE can use TCR private Helm repositories for application deployment.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35493">Managing Helm Charts</a></td></tr>
</table>

## June 2020

<table>
 <tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Related Documents</th></tr>
 <tr><td>Launches full beta test for TCR Enterprise Edition</td><td>TCR Enterprise Edition officially starts full beta test. Users can create secure and exclusive Enterprise Edition instances and use image security scanning, cross-region instance synchronization, and Helm Chart hosting.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35480">TCR Product Overview</a></td></tr>
</table>
