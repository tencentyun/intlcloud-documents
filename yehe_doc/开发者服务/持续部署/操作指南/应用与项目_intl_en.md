This document describes the applications and projects in CODING Continuous Deployment (CODING-CD).

## Prerequisites
You must activate the CODING DevOps service for your Tencent Cloud account before you can use CODING Project Management (CODING-PM).

## Open Project
1. Log in to the CODING Console and click **Use Now** to go to CODING.
2. On the Workspace homepage, click <img src ="https://main.qcloudimg.com/raw/12230547b45d5eae85ad1c4fa86fba68.png" width="15"style ="margin:0" data-nonescope="true" > on the left to go to the CODING-CD Console.

## Function Overview
All the applications and projects in CODING-CD are level-1 resources belonging to an enterprise or team. There is a one-to-many relationship between them; that is, one project can contain multiple applications, and one application can belong to multiple projects.
![](https://qcloudimg.tencent-cloud.cn/raw/714889a702a966a1f24ecd2fb9704e9a.png)
With this design, Ops personnel can focus on the management of the continuous deployment of the applications (deployment pipelines, infrastructure, etc.), while non-Ops personnel (generally developers) only need to handle the project dimension (submitting release orders, viewing release details, etc.), so that the former can focus on infrastructure Ops in the cloud, and the latter can carry out most of the business Ops within projects and create a complete closed loop from the requirement to the release.

## Application
An application is the basic deployment unit in CODING-CD. Each includes several application clusters as well as security groups and load balancers. It abstracts the set of deployed software and usually represents the services you want to deploy, their configurations, and the basic settings required for their execution. The recommended approach is for one application to correspond to one service in the microservice architecture.
![](https://qcloudimg.tencent-cloud.cn/raw/0f80cb25c0e5b5be70c2b6a30c9a092b.png)

### One-to-one correspondence examples
In the microservice architecture, a microservice corresponds to a CODING-CD application. You can set the corresponding relationships based on your preferences. The following example shows the relationships among a team, projects, applications, clusters, and cloud accounts:
<table>
    <tr>
        <th colspan="4">Team: XXX Technology Co., Ltd.</th>
    </tr>
    <tr>
        <td>Cloud account</td>
        <td><ul style="margin:0;list-style-type:disc;">
            <li>Self-built Kubernetes Service Account</li>
            <li>Tencent Cloud Beijing TKE Cluster Service Account</li>
            <li>Tencent Cloud Hong Kong API Key</li></ul>
        </td>
    </tr>
    <tr>
        <td>Project 1: An E-Commerce Site for In-Vehicle Products</td>
        <td><ul style="margin:0;list-style-type:disc;">
            <li>Application 1: Backend of the In-Vehicle Product E-Commerce Site</li>
            <li>Application 2: Frontend of the In-Vehicle Product E-Commerce Site</li>
            <li>Application 3: Logistics Management Service</li></ul>
        </td>
    </tr>
    <tr>
        <td>Project 2: An E-Commerce Site for Clothes</td>
        <td><ul style="margin:0;list-style-type:disc;">
            <li>Application 1: Backend of the Clothes E-Commerce Site</li>
            <li>Application 2: Frontend of the Clothes E-Commerce Site</li>
            <li>Application 3: Logistics Management Service</li></ul>
        </td>
    </tr>
    <tr>
        <td>CODING-CD Console</td>
        <td><ul style="margin:0;list-style-type:disc;">
            <li>Application 1: Backend of the In-Vehicle Product E-Commerce Site
                <ul><li>Test cluster</li><li>Production cluster</li></ul></li>
            <li>Application 2: Frontend of the In-Vehicle Product E-Commerce Site
                <ul><li>Test cluster</li><li>Production cluster</li></ul></li>
            <li>Application 3: Logistics Management Service
                <ul><li>Test cluster for the in-vehicle product e-commerce site</li><li>Production cluster for the in-vehicle product e-commerce site</li><li>Test cluster for the clothes e-commerce site</li><li>Production cluster for the clothes e-commerce site</li></ul></li>
            <li>Application 4: Backend of the Clothes E-Commerce Site
                <ul><li>Test cluster</li><li>Production cluster</li></ul></li>
            <li>Application 5: Frontend of the Clothes E-Commerce Site
                <ul><li>Test cluster</li><li>Production cluster</li></ul></li>
        </ul>
        </td>
    </tr>
</table>

## Cloud Account Binding
A cloud account is the token for accessing cloud resources. To create an application in the CODING-CD Console, click **Application** > **Create App** in the navigation bar. Before you create an application, make sure that you have completed [Cloud Account Binding](https://intl.cloud.tencent.com/document/product/1137/45451).
![](https://qcloudimg.tencent-cloud.cn/raw/174263bb417add3d117ef3f3753396ac.png)

## Application Creation
Click "Deployment Console" on the left side of the homepage, and then click **Create App** in the upper-right corner.
![](https://qcloudimg.tencent-cloud.cn/raw/eaf08309ec593918a183be205b11e8c1.png)

## Associate with Project
After creating an application in the CODING-CD Console, you can directly associate it with a project on the homepage of the console.
![](https://qcloudimg.tencent-cloud.cn/raw/786ae80a6693a3983e2cf461f46611bc.png)

## Create Release Order
When Ops personnel completes the [Deployment Pipeline Configuration](https://intl.cloud.tencent.com/document/product/1137/45455) of an application, developers can create a complete closed DevOps loop from project collaboration to application release within a project. For example, when a new version needs to be released, developers go to **Continuous Deployment** > **Kubernetes** to create a release order, which automatically triggers the execution of the deployment pipeline. Developers can view the release status and historical details at any time.
![](https://qcloudimg.tencent-cloud.cn/raw/28468af7631eab5b5fade4e4bd00e31a.png)

## Manage Applications
After you create an application in the CODING-CD Console, you can change the application fields and notifications in the **Configuration** of the application, or delete it.
![](https://qcloudimg.tencent-cloud.cn/raw/81e64ce6c1f364038c30c364e989dae3.png)

### Application notifications
Notifications can be sent through CODING, WeCom, DingTalk, and Feishu.

### Show or hide function entry
You can disable the function entries that you do not need in the **Features** section. This will merely hide the function entries in the console, and will not delete their data.The function entries of deployment pipelines, clusters, load balancers, and security groups can be hidden:
![](https://qcloudimg.tencent-cloud.cn/raw/af92e7393d6069f86dd620ccde9cfe76.png)

### Add custom field link to instance
You can click **Cluster** > **Service Group** > **Instance Details** to view the custom link of the running instance. The link offers brief information on the instance, such as the log and health status.
![](https://qcloudimg.tencent-cloud.cn/raw/d561cda1441048648539a19fcb2ce68e.png)
The IP address that corresponds to the custom link can be a public or private IP address. The default port is 80. But you can set another port number that starts with `:` in the "Path" text field, such as `:7002/health`.

1. Click **Add Section** in the **Link** section.
2. Enter a custom link title in **Section Heading**.
3. Enter the custom link name and URL in the **Links** field.

>? You can enter an expression in the URL field to reference more instance fields. For example, a Tencent Cloud instance can use `{region}` to reference the region where the instance resides.

5. Click **Add Link** to add more links to the same field.
6. Click **Add Section** to add a new custom field link.
7. Click **Cancel** to cancel the add operation. ** Canceling** an operation will not delete the saved custom field links.
8. Click **Save**.

### Traffic protection
>? Traffic protection is designed to ensure that at least one instance is operating normally at any time.

Once the function is enabled, when a user or script tries to delete, disable or scale a service group, the CODING Console will verify if at least one instance in the cluster is running normally. If not, the request will be rejected.
1. In the **Traffic Protection** section, click **Add Traffic Protection**.
2. Enter the following fields:

<table>
   <tr>
      <th width="0px" style="text-align:center">Field</td>
      <th width="0px" style="text-align:center">Required?</td>
      <th width="0px"  style="text-align:center">Description</td>
   </tr>
   <tr>
      <td>Cloud account</td>
      <td>Yes</td>
      <td>The cloud account for enabling traffic protection</td>
   </tr>
   <tr>
      <td>Region</td>
      <td>Yes</td>
      <td>Choose the region(s). `*` indicates all the regions.</td>
   </tr>
   <tr>
      <td>Group</td>
      <td>No</td>
      <td>The cluster group for enabling traffic protection. If this field is left empty, the cluster does not belong to any group.</td>
   </tr>
   <tr>
      <td>Details</td>
      <td>No</td>
      <td>A level-3 field that differentiates clusters. The service groups with the same `${Application}-${Stack}-${Detail}` belong to the same cluster.</td>
   </tr>

</table>

3. Click **Save**.

### Application deletion
If there is a service group in an application, you need to delete the service group first.
In the [CODING-CD Console](https://console.cloud.tencent.com/coding), click the **gear icon** in the lower-right corner of the application. After you open the application configuration page, click **Delete**.
![](https://qcloudimg.tencent-cloud.cn/raw/f5d78c4b4527e0e98004e587814741a4.png)
