>? This document introduces the updates to the Tencent Container Registry (TCR) Enterprise Edition. For the updates to Tencent Kubernetes Engine (TKE), see [Release Notes](https://intl.cloud.tencent.com/document/product/457/37358).
## October 2020

<table>
	<tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Document</th></tr>
	<tr><td>The image building feature added support for multiple code sources.</td><td>Support for private GitLab and TGit code sources was added, and the code source authorization process was optimized.</td><td>-</td></tr>
	<tr><td>The delivery assembly line deployment feature added support for image filtering.</td><td>Support was added for the use of local pushed images to trigger deployment. Users can also configure filter rules to deploy only the latest pushed images that meet the rules.</td><td>Using the Delivery Assembly Line to Implement Container DevOps</td></tr>
</table>

## September 2020

<table>
	<tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Document</th></tr>
	<tr><td>The image tag retention feature was added.</td><td>Users can create rules for the automatic clearing of image tags in a namespace. Such rules can be executed periodically to clear historical image tags.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/38942">Configuring Image Tag Retention</a></td></tr>
</table>


## August 2020

<table>
	<tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Document</th></tr>
	<tr><td>The dedicated TCR plug-in was launched for TKE.</td><td>Through one-click installation of the dedicated TCR Enterprise Edition plug-in, TKE clusters can enable secret-free pulling of container images and Helm charts via the private network. This greatly improves the application deployment experience.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/38386">TKE Clusters Use the TCR Plug-In to Enable Secret-free Pulling of Container Images via Private Network</a></td></tr>
  <tr><td>Added support for Tencent Cloud tags.</td><td>Users are now allowed to bind Enterprise Edition instances with Tencent Cloud tags, with which they can perform instance resource filtering and permission management.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35486">Creating an Enterprise Edition Instance</a></td></tr>
</table>

## July 2020

<table>
	<tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Document</th></tr>
	<tr><td>The delivery assembly line feature was launched.</td><td>Through quick configuration of a delivery assembly line, users can enable the automatic triggering of image building, push, and application updates by code updates. Used with TKE, this feature can quickly implement container DevOps</td><td>Using the Delivery Assembly Line to Implement Container DevOps</td></tr>
  <tr><td>The Helm Chart feature was updated.</td><td>Supports upload and download of chart packages via the console. TKE supports the use of TCR private Helm repositories for application deployment.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35493">Managing Helm Chart</a></td></tr>
</table>

## June 2020

<table>
	<tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Document</th></tr>
	<tr><td>The Enterprise Edition entered the stage of full beta testing.</td><td>The Enterprise Edition officially started its full beta testing and supports the creation of secure and exclusive Enterprise Edition instances, image security scanning, cross-regional synchronization, and Helm charts.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35480">TCR Product Overview</a></td></tr>
</table>
