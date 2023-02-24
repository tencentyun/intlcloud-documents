> ?
> This document introduces the updates to Tencent Container Registry (TCR) Enterprise Edition. For more information about the updates to Tencent Kubernetes Engine (TKE), see [Release Notes](https://www.tencentcloud.com/document/product/457/37358).



## September 2022
<table>
<tr>
<td rowspan="1" colSpan="1" >Update</td><td rowspan="1" colSpan="1" >Description</td><td rowspan="1" colSpan="1" >Related Documents</td>
</tr><tr>
<td rowspan="1" colSpan="1" >Supports image signing</td>
<td rowspan="1" colSpan="1" >The container image signing feature is launched to ensure image consistency across the entire linkage.</td>
<td rowspan="1" colSpan="1" ><a href="https://www.tencentcloud.com/document/product/1051/52645">Container Image Signature</a></td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Increases the number of accessed VPCs</td>
<td rowspan="1" colSpan="1" >The quota for accessed VPCs is increased for all versions. Up to 20 VPCs can be accessed.</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Adds the feature of checking whether a domain name has ICP filing</td>
<td rowspan="1" colSpan="1" >The feature of checking whether a domain name has ICP filing is added for custom domain names to meet compliance requirements.</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
</table>



## June 2022
<table>
<tr>
<td rowspan="1" colSpan="1" >Update</td>
<td rowspan="1" colSpan="1" >Description</td>
<td rowspan="1" colSpan="1" >Related Documents</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Adds the quick start feature</td>
<td rowspan="1" colSpan="1" >You can quickly instantiate TCR Enterprise instances that are newly created in five minutes to push your first container image.</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Upgrades the image retention capability</td>
<td rowspan="1" colSpan="1" >Advanced configuration is added to the TCR Enterprise image retention feature. It allows you to configure image filtering rules, which support regular expressions.</td>
<td rowspan="1" colSpan="1" ><a href="https://intl.cloud.tencent.com/document/product/1051/41657">Auto-Deleting Image Tags</a></td>
</tr>
</table>



## December 2021
<table>
<tr>
<td rowspan="1" colSpan="1" >Update</td>
<td rowspan="1" colSpan="1" >Description</td>
<td rowspan="1" colSpan="1" >Related Documents</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Upgrade of image acceleration to download the data in the image on demand</td>
<td rowspan="1" colSpan="1" >Upgrades the capability of image acceleration. It can be enabled with one click. The container can be started in seconds when deploying the application, without the need to pull all image data.</td>
<td rowspan="1" colSpan="1" ><a href="https://www.tencentcloud.com/document/product/1051/52656">Loading Container Images on Demand</a></td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >The TCR Individual service supports automatic image deployment in all regions</td>
<td rowspan="1" colSpan="1" >The TCR Individual service supports the automatic image deployment feature based on CODING DevOps in all available regions, which can automatically trigger image construction for code push and automatically push to the Individual edition image repository to update container applications in the specified cluster.</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
</table>



## November 2021
<table>
<tr>
<td rowspan="1" colSpan="1" >Update</td>
<td rowspan="1" colSpan="1" >Description</td>
<td rowspan="1" colSpan="1" >Related Documents</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >The TCR Individual service supports image building in all regions</td>
<td rowspan="1" colSpan="1" >The TCR Individual service supports image building based on CODING DevOps in all available regions, and you can select the specified image repository > image build in the unified product console to configure it.</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Changes the entry point of TCR Individual in the console</td>
<td rowspan="1" colSpan="1" >Starting from November 1, 2021 (UTC +8), entry of TCR Individual (the original path: TKE > Image Repository) in the console will be changed to be located in the TCR console and this will be in beta test. For the relationship of the existing features in the two consoles, see related documents.</td>
<td rowspan="1" colSpan="1" ><a href="https://intl.cloud.tencent.com/document/product/1051/46864">Announcement on Merging the Entries of TCR Enterprise and TCR Individual</a></td>
</tr>
</table>



## October 2021
<table>
<tr>
<td rowspan="1" colSpan="1" >Update</td>
<td rowspan="1" colSpan="1" >Description</td>
<td rowspan="1" colSpan="1" >Related Documents</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >The logs of instance replication can be checked</td>
<td rowspan="1" colSpan="1" >The instance replication feature now supports checking replication logs and supports querying via API.</td>
<td rowspan="1" colSpan="1" ><a href="https://intl.cloud.tencent.com/document/product/1051/43978">Configuring Instance Replication</a></td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >TCR console supports unified management of image repositories of TCR Individual</td>
<td rowspan="1" colSpan="1" >The TCR console now supports unified management of image repositories of TCR Individual. You can check the instances of TCR Individual, and manage namespaces and image repositories, etc.</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
</table>



## July 2021
<table>
<tr>
<td rowspan="1" colSpan="1" >Update</td>
<td rowspan="1" colSpan="1" >Description</td>
<td rowspan="1" colSpan="1" >Related Documents</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Supports cross-master account instance synchronization</td>
<td rowspan="1" colSpan="1" >The instance synchronization feature supports cross-master account target instances and realizes cross-master account instance data synchronization.</td>
<td rowspan="1" colSpan="1" ><a href="https://intl.cloud.tencent.com/document/product/1051/43979">Cross-Tenant Synchronization</a></td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Supports image tag immutability</td>
<td rowspan="1" colSpan="1" >Supports enabling the tag immutability feature for images hosted in TCR, which ensures that images of the same tag will only be successfully pushed once.</td>
<td rowspan="1" colSpan="1" ><a href="https://intl.cloud.tencent.com/document/product/1051/41707">Configuring Image Tag Immutability</a></td>
</tr>
</table>



## June 2021
<table>
<tr>
<td rowspan="1" colSpan="1" >Update</td>
<td rowspan="1" colSpan="1" >Description</td>
<td rowspan="1" colSpan="1" >Related Documents</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Enhances TCR console features</td>
<td rowspan="1" colSpan="1" >The original instance list page has been upgraded to an instance management page, where you can view the instance overview, the latest TCR features and product updates.</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Supports batch adding/editing for public network access allowlist</td>
<td rowspan="1" colSpan="1" >TCR console supports entering multiple allowlists at a single time or importing existing security group.</td>
<td rowspan="1" colSpan="1" ><a href="https://intl.cloud.tencent.com/document/product/1051/35491">Public Network Access Control</a></td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Adds multiple supported regions for auto-parsing management</td>
<td rowspan="1" colSpan="1" >Adds Nanjing, Hong Kong (China), Singapore, Frankfurt, Chengdu, and Chongqing as the supported regions.</td>
<td rowspan="1" colSpan="1" ><a href="https://intl.cloud.tencent.com/document/product/1051/35492">Private Network Access Control</a></td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Supports removal of unused image data</td>
<td rowspan="1" colSpan="1" >Users can set custom rules to remove unused image data of TCR Enterprise instances in batches to release storage capacity. Dry runs are supported.</td>
<td rowspan="1" colSpan="1" ><a href="https://intl.cloud.tencent.com/document/product/1051/41073">Releasing COS Storage Capacity</a></td>
</tr>
</table>



## April 2021
<table>
<tr>
<td rowspan="1" colSpan="1" >Update</td>
<td rowspan="1" colSpan="1" >Description</td>
<td rowspan="1" colSpan="1" >Related Documents</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Supports querying audit logs</td>
<td rowspan="1" colSpan="1" >TCR Enterprise has been accessed to Tencent CloudAudit. You can check the logs of read and write operations of instances, namespaces, and image repositories in "Event History".</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
</table>


## March 2021
<table>
<tr>
<td rowspan="1" colSpan="1" >Update</td>
<td rowspan="1" colSpan="1" >Description</td>
<td rowspan="1" colSpan="1" >Related Documents</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Supports custom domain names</td>
<td rowspan="1" colSpan="1" >TCR supports custom domain names. User can add custom domain names and SSL certificates to the TCR Enterprise instances, and access the instance through the HTTPS protocol.</td>
<td rowspan="1" colSpan="1" ><a href="https://intl.cloud.tencent.com/document/product/1051/43983">Configuring Custom Domain Name</a></td>
</tr>
</table>



## January 2021
<table>
<tr>
<td rowspan="1" colSpan="1" >Update</td>
<td rowspan="1" colSpan="1" >Description</td>
<td rowspan="1" colSpan="1" >Related Documents</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Supports multi-region replication of a single instance</td>
<td rowspan="1" colSpan="1" >Users can create replicas of an Enterprise Premium instance in multiple regions with the same access domain name and credential as the original TCR Enterprise instance and synchronize underlying image data of the original instance to replicas in real time. After image data is uploaded, it can be downloaded through the local private network in multiple regions.</td>
<td rowspan="1" colSpan="1" ><a href="https://intl.cloud.tencent.com/document/product/1051/43978">Configuring Instance Replication</a></td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Supports cloud-native artifacts and multi-architecture images</td>
<td rowspan="1" colSpan="1" >TCR Enterprise instances are compatible with cloud-native artifacts (OCI). Image Registry can host Helm Charts, CNAB and other cloud-native artifacts. TCR Enterprise instances can host multi-architecture container images, such as amd64 and arm, to be applicable to IoT and edge computing scenarios.</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Supports on-demand container image loading</td>
<td rowspan="1" colSpan="1" >A TCR Enterprise Premium instance can enable the on-demand container image loading feature. When cluster nodes pull image data from the TCR Enterprise Premium instance, they can mount pulled data as needed, improving the container startup speed.</td>
<td rowspan="1" colSpan="1" ><a href="https://www.tencentcloud.com/document/product/1051/52656">Loading Container Images on Demand</a></td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Optimizes the private network access feature</td>
<td rowspan="1" colSpan="1" >When a private network access linkage is created for an instance deployed in China, the VPCDNS can be used to configure private network resolution for the instance access domain name, without the need to use an external DNS or configure the host.</td>
<td rowspan="1" colSpan="1" ><a href="https://intl.cloud.tencent.com/document/product/1051/35492">Private Network Access Control</a></td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >TCR Enterprise is available in regions of Beijing Finance and Taipei</td>
<td rowspan="1" colSpan="1" >TCR Enterprise is now available in regions of Beijing Finance and Taipei. For more information on billing, see Billing Overview.</td>
<td rowspan="1" colSpan="1" ><a href="https://intl.cloud.tencent.com/document/product/1051/35483">Billing Overview</a></td>
</tr>
</table>



## December 2020
<table>
<tr>
<td rowspan="1" colSpan="1" >Update</td>
<td rowspan="1" colSpan="1" >Description</td>
<td rowspan="1" colSpan="1" >Related Documents</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Starts commercial billing for TCR Enterprise</td>
<td rowspan="1" colSpan="1" >TCR Enterprise instances have ended beta testing and will be billed. SLA guarantees are provided, and users can purchase instances in pay-as-you-go mode.</td>
<td rowspan="1" colSpan="1" ><a href="https://intl.cloud.tencent.com/document/product/1051/35483">Billing Overview</a></td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >TCR Enterprise is available in Virginia and Frankfurt regions</td>
<td rowspan="1" colSpan="1" >TCR Enterprise is now available in the Virginia and Frankfurt regions. For more information on billing, see Billing Overview.</td>
<td rowspan="1" colSpan="1" ><a href="https://intl.cloud.tencent.com/document/product/1051/35483">Billing Overview</a></td>
</tr>
</table>



## October 2020
<table>
<tr>
<td rowspan="1" colSpan="1" >Update</td>
<td rowspan="1" colSpan="1" >Description</td>
<td rowspan="1" colSpan="1" >Related Documents</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Adds support for multiple code sources in the image building feature</td>
<td rowspan="1" colSpan="1" >The private GitLab and TGit code sources are now supported, and the code source authorization process has been optimized.</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Image filtering is supported in the delivery pipeline deployment feature</td>
<td rowspan="1" colSpan="1" >Local push images can be used to trigger the deployment process, and filtering rules can be configured to deploy only the most recently pushed images that meet the rules.</td>
<td rowspan="1" colSpan="1" ><a href="https://www.tencentcloud.com/document/product/1051/53613">Implementation of Container DevOps Using Delivery Pipeline</a></td>
</tr>
</table>



## September 2020
<table>
<tr>
<td rowspan="1" colSpan="1" >Update</td>
<td rowspan="1" colSpan="1" >Description</td>
<td rowspan="1" colSpan="1" >Related Documents</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Adds the image tag retention feature</td>
<td rowspan="1" colSpan="1" >Automatic clearing rules can be configured for image tags in a namespace to periodically clear historical image tags.</td>
<td rowspan="1" colSpan="1" ><a href="https://intl.cloud.tencent.com/document/product/1051/41657">Auto-Deleting Image Tags</a></td>
</tr>
</table>



## August 2020
<table>
<tr>
<td rowspan="1" colSpan="1" >Update</td>
<td rowspan="1" colSpan="1" >Description</td>
<td rowspan="1" colSpan="1" >Related Documents</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >The TCR plug-in is supported in TKE clusters</td>
<td rowspan="1" colSpan="1" >A TKE cluster can install the TCR Enterprise plug-in quickly to enable secret-free pulling of container images and Helm Charts through the private network. This significantly improves the application deployment experience.</td>
<td rowspan="1" colSpan="1" ><a href="https://intl.cloud.tencent.com/document/product/1051/38386">TKE Clusters Use the TCR Plug-In to Enable Secret-Free Pulling of Container Images through Private Network</a></td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Supports Tencent Cloud tags</td>
<td rowspan="1" colSpan="1" >Users can now bind TCR Enterprise instances with Tencent Cloud tags, with which they can perform instance resource filtering and permission management.</td>
<td rowspan="1" colSpan="1" ><a href="https://intl.cloud.tencent.com/document/product/1051/35486">Creating a TCR Enterprise Instance</a></td>
</tr>
</table>



## July 2020
<table>
<tr>
<td rowspan="1" colSpan="1" >Update</td>
<td rowspan="1" colSpan="1" >Description</td>
<td rowspan="1" colSpan="1" >Related Documents</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Launches the delivery pipeline feature</td>
<td rowspan="1" colSpan="1" >After a delivery pipeline is configured, code updates can automatically trigger image building, image push, and application updates. When used with TKE, this feature can quickly implement container DevOps.</td>
<td rowspan="1" colSpan="1" ><a href="https://www.tencentcloud.com/document/product/1051/53613">Implementation of Container DevOps Using Delivery Pipeline</a></td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Updates the Helm Chart feature</td>
<td rowspan="1" colSpan="1" >Users can upload and download Chart packages through the console. TKE can use TCR private Helm repositories for application deployment.</td>
<td rowspan="1" colSpan="1" ><a href="https://intl.cloud.tencent.com/document/product/1051/35493">Managing Helm Charts</a></td>
</tr>
</table>



## June 2020
<table>
<tr>
<td rowspan="1" colSpan="1" >Update</td>
<td rowspan="1" colSpan="1" >Description</td>
<td rowspan="1" colSpan="1" >Related Documents</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Launches full beta test for TCR Enterprise</td>
<td rowspan="1" colSpan="1" >TCR Enterprise officially starts full beta test. Users can create secure and exclusive TCR Enterprise instances and use image security scanning, cross-region instance synchronization, and Helm Chart hosting.</td>
<td rowspan="1" colSpan="1" ><a href="https://intl.cloud.tencent.com/document/product/1051/35480">Product Overview</a></td>
</tr>
</table>



