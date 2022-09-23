## Overview

This document describes how to create, update, roll back, and delete applications in the TKE console.

## Note

- Application management applies only to clusters with Kubernetes v1.8 or later.

## Directions

### Creating an application

1. Log in to the [TKE Console](https://console.cloud.tencent.com/tke2/helm) and click **Applications** in the left sidebar.
2. At the top of the **Applications** page, select the cluster and region where you wish to create the application and click **Create**.
3. On the **Create Application** page, set the basic information about the application according to the following parameters, as shown in the following figure.
![](https://main.qcloudimg.com/raw/f636846a914a1ec71c4f6c1870cfa831.png)
The main parameters are described as follows:
 - **Application Name**: enter a custom application name.
 - **Source**: select **Marketplace**, **TCR Private Repository**, or **Third-party Source**. For details, see the following table.
 <table>
 <tr>
	 <th width="17%">Source</th>
	 <th>Configuration</th>
 </tr>
 <tr>
	 <td>Marketplace</td>
	 <td>
	 Filter charts by cluster type or application scenario. Select the required application package and chart version. You can also edit the parameters.
	 </td>
 </tr>
  <tr>
	 <td>TCR Private Repository</td>
	 <td><ul class="params">
	 <li>TCR instance name: select a <a href="https://intl.cloud.tencent.com/document/product/1051/35480">TCR</a> Enterprise instance as needed.</li>
	 <li>Namespace: select a namespace of the specified TCR instance as needed. After the namespace is specified, charts under the namespace will be displayed on the application list page.</li>
	 <li>Chart version and parameters: select the applicable version. You can also edit the parameters.</li>
	 </ul></td>
 </tr>
  <tr>
	 <td>Third-party Source</td>
	 <td><ul class="params">
	 <li>Chart address: official and self-built Helm repositories are supported. Note that the value of this parameter must start with <code>http</code> and end with <code>.tgz</code>. In this example, the value is <code>http://139.199.162.50/test/nginx-0.1.0.tgz</code>.</li>
	 <li>Type: **Public** and **Private** are available. Select one of them as needed.</li>
	 <li>Parameters: edit the parameters as needed.</li>
	 </ul></td>
 </tr>
 </table>
4. Click **Done**.

### Updating an application

1. Go to the [TKE Console](https://console.cloud.tencent.com/tke2/helm) and click **Application** in the left sidebar to go to the **Application** page.
2. In the application list, locate the application to update and click **Update Application** on the right.
3. In the displayed **Update Application** window, configure the key information as needed and click **Done**.

### Rolling back an application

1. Go to the [TKE Console](https://console.cloud.tencent.com/tke2/helm) and click **Application** in the left sidebar to go to the **Application** page.
2. In the application list, click the application to update to go to the application details page.
3. On the application details page, click the **Version History** tab, locate the required version, and click **Roll Back** on the right, as shown in the following figure.
   ![](https://main.qcloudimg.com/raw/47fc42e6601945f665fa270c31c8b085.png)
4. In the displayed **Rollback Application** window, click **OK**, as shown in the following figure.
   ![](https://main.qcloudimg.com/raw/c0b642ce3f89898c1c59c85911c484d6.png)

### Deleting an application

1. Go to the [TKE Console](https://console.cloud.tencent.com/tke2/helm) and click **Application** in the left sidebar to go to the **Application** page.
2. In the applications list, locate the application to delete and select **Delete** on the right.
3. In the displayed **Delete Application** window, click **OK**.
