## Overview
Tencent Container Registry (TCR) is a container image cloud hosting service provided by Tencent Cloud. It has the following features:

**Cloud native artifacts hosting**: TCR supports the hosting of multi-architecture container images, such as Linux, Windows, ARM, etc. It also supports the management of Helm Chart v2/v3 and other cloud native artifacts that meet the OCI specifications.

**Multi-dimensional security protection**: TCR supports the encryption and storage of image data. It can perform image security scanning and block the high-risk image deployment. It also supports the network access control. It provides fine-grained permission management and operation audit to ensure the compliance of the business data operations.

**Multi-regional fast distribution**: TCR supports on-demand synchronization in global multi-region and fast image replication in domestic multi-region, implementing the image pulling from the nearest region. It supports P2P accelerated distribution and on-demand image mounting, significantly reducing the image pulling time for large-scale clusters, and ensuring the quick deployment and update of services.

**Container DevSecOps**: TCR is closely integrated with other products such as CODING DevOps and TKE. It provide delivery assembly line. With simple configuration, the code updates can automatically trigger image building, image scanning, and then update container applications, improving the delivery efficiency of enterprise cloud native applications, and ensuring the business safety.

With the TCR service, you can enjoy secure and efficient image hosting and distribution services in the cloud, without building or maintaining the image hosting service. In addition, you can use TCR together with [Tencent Kubernetes Engine](https://intl.cloud.tencent.com/document/product/457) to smoothly deploy containers in the cloud.  


## Product Type
TCR provides the Enterprise Edition and Personal Edition:

#### Enterprise Edition
TCR Enterprise Edition provides an enterprise-class, exclusive, and secure image hosting service. It is suitable for individual or enterprise users who need to use the hosting service of cloud native artifacts in their businesses. TCR supports the preceding features and is constantly updated. TCR Enterprise Edition currently supports pay-as-you-go billing mode.

#### Personal Edition
TCR Personal Edition provides basic on-cloud image hosting and distribution services. With limited usage quotas, it is only applicable to temporary R&D process testing of individual or enterprise users. TCR Personal Edition is a shared service in the cloud. That is, all TCR Personal Edition users share the service backend and data storage, and quotas are imposed on image hosting, uploading, and downloading. TCR Personal Edition is free of charge. You can start using it directly .

## Specification
The TCR specifications are as follows (**✓**: supported; **-**: not supported).

<dx-alert infotype="notice" title="">
When the instance is using the features of Standard Edition or Advanced Edition, it is not allowed to degrade the instance specifications to editions which do not support the features. If you want to degrade the specifications, please delete related feature configurations manually first.
</dx-alert>
<table>
<tbody><tr>
<th rowspan="2" style="
    width: 13%;
">Feature Module</th>
<th rowspan="2" style="
    width: 27%;
">Features</th>
<th rowspan="2" style="
    width: 5%;
">TCR Individual</th>
<th colspan="3" style="
    width: 55%;
">TCR Enterprise</th>
</tr>
<tr>
<th>Basic</th><th>Standard</th><th>Advanced</th>
</tr>
<tr>
<td rowspan="1">Service guarantee</td>
<td>SLA</td>
<td>Not supported</td><td>99.9% (compensation supported)</td><td>99.9% (compensation supported)</td><td>99.9% (compensation supported)</td>
</tr>
<tr>
<td rowspan="5">Instance management</td>
<td>Dedicated registry service</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Dedicated domain name access</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Custom access domain name</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Dedicated data storage backend</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Temporary/long-term access credential management</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td rowspan="5">Repository management</td>
<td>Multi-level repository directory</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Helm chart hosting</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Namespace quota</td><td>10</td><td>50</td><td>100</td><td>500<br>Submit a ticket to increase the quota.</td>
</tr>
<tr>
<td>Image repository quota</td><td>Guangzhou region: 500, Other regions: 100</td><td>1000</td><td>3000</td><td>5000 <br>Submit a ticket to increase the quota.</td>
</tr>
<tr>
<td>Helm repository quota</td><td>-</td><td>1000</td><td>3000</td><td>5000 <br>Submit a ticket to increase the quota.</td>
</tr>
<tr>
<td rowspan="8">Data security</td>
<td>Encrypted storage of data</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Image vulnerability scanning</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Block Vulnerable Images</td><td>-</td><td>-</td><td>✓</td><td>✓</td>
</tr>
<tr>   
<td>Image tag protection</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Public network access control</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>VPC access control</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>VPC access quota</td><td>-</td><td>5</td><td>10</td><td>20</td>
</tr>
<tr>
<td>Operation log retention</td><td>-</td><td>7 days</td><td>15 days</td><td>30 days</td>
</tr>
<tr>
<td rowspan="3">Synchronous backup</td>
<td>Multi-region replications for single instance and nearby access</td>
<td>-</td><td>-</td><td>-</td><td>✓</td>
</tr>
<tr>
<td>Cross-instance custom synchronization rules</td><td>-</td><td>-</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Multi-AZ disaster recovery in the same city</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td rowspan="5">Container DevOps</td>
</tr>
<tr>
<td>Webhook trigger</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Container image compilation and building *</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Cloud native delivery workflow</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>P2P accelerated distribution of images</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
</tbody></table>

>? **Container image compilation and building** feature is based on CODING DevOps service and provides free usage quota. If you need advanced features or want to add quota, please go to [CODING DevOps service](https://console.cloud.tencent.com/coding).



## Free Usage of the Personal Edition
The Personal Edition service is provided for individual developers. The free usage quota is limited. SLA commitments and relevant compensation are not provided.
