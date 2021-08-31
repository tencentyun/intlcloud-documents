
## Overview
In Tencent Container Registry (TCR), an image repository is used to manage container images. A single image repository may contain container images with different tags. An image repository belongs to a namespace and inherits the public or private attribute and security scan triggering mode from its namespace.

An image repository is the minimum unit for permission management in TCR. The instance admin can grant image repository management or read-only permission to a sub-user. For example, the instance admin can grant the "tom" sub-account only the permission to pull images from the "project-a-frontend" image repository, but disallow the sub-account to push or delete images. For more information about other permission management and authorization methods, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248). This document describes how to create and manage an image repository in a TCR enterprise edition instance.



## Prerequisites

Before creating and managing an image repository for a TCR enterprise edition instance, complete the following tasks:
- [Create an Enterprise Edition instance](https://intl.cloud.tencent.com/document/product/1051/39088).
- If you are using a sub-account, you must have granted the sub-account operation permissions for the corresponding instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).

## Directions


### Creating an image repository
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Image Repository** in the left sidebar.
On the "Image Repository" page, you can view the image repository list of the current instance. To change the instance, select the desired instance name from the "Instance Name" drop-down list at the top of the page.
2. Click **Create**. In the "Create an Image Repository" window, configure the following shown in the figure below for the image repository.
![](https://main.qcloudimg.com/raw/d2c65e5fb0dfcad5b119c39bca4506d0.png)
 - **Associated Instance**: currently selected instance, to which the created image repository belongs.
 - **Namespace**: namespace to which the image repository belongs. If the list is empty, you must [create a namespace](https://intl.cloud.tencent.com/document/product/1051/35487) in the instance.
 - **Name**: name of the image repository. The value must be 2 to 200 characters in length and can only contain lowercase letters, numbers, and separators (including periods (.), underscores (_), hyphens (-), and slashes (/). It cannot start or end with a separator or contain several consecutive separators. The name can be a multi-level path, such as `team-01/front/nginx`. You can set the name flexibly based on your business requirements.
 - **Image Source**: "Local" and "Platform" are supported. For more information on how to create images through the platform, see [Creating Images](https://intl.cloud.tencent.com/document/product/1051/37252).
 - **Brief Description**: brief description of the image repository. It is a string of up to 100 characters. You can re-edit the description after the image repository is created.
 - **Detailed Description**: detailed description of the image repository. This parameter supports the Markdown syntax. It is a string of up to 1000 characters. You can modify the description after the image repository is created.
3. Click **Confirm** to create the image repository.

### Basic image repository operations
After the image repository is created, you can view the image repository on the "Image Repository" page. Then, you can perform the operations shown in the figure below to manage the image repository.
![](https://main.qcloudimg.com/raw/4670963ae339d0a177d29a247294281e.png)
- **Filtering namespaces**
Select <img src="https://main.qcloudimg.com/raw/cec7f1733d3e76d18c27b0bcbb65965b.png" style="margin: -3px 0px"> from the "Image Repository" list for filtering. Then, you can select a namespace to view from the drop-down list.
- **Viewing details of a repository**
Click the name of a specified image repository. The repository details page is displayed, where you can manage the image tag and edit the basic information of the image repository.
- **Deleting an image repository**
You can click **Delete** next to an image repository to delete it. Carefully review the deletion operation before confirming it to prevent important data from being deleted by mistake.
>! After the image repository is deleted, **all container images in the image repository are deleted**. 


### Managing image tags
Click the name of a specified image repository. The repository details page is displayed, and the **Tag Management** tab is selected by default. On this page, you can manage all the image tags in the repository, perform security scans, and view the layer information, as shown in the figure below.
![](https://main.qcloudimg.com/raw/ce5ffd78da771800385e27118a9c98be.png)
- **Filtering image tags**
In the search box in the upper-right part of the tag list, you can enter an image tag to search for this image tag. Fuzzy search is supported.
- **Obtaining the pulling command**
You can click **Copy command** next to the target image tag to copy the pulling command of the image tag.
- **Performing a security scan**
You can click **Scan** next to the target image tag to actively trigger a security scan. When the result is available for the corresponding "Security Level" attribute, click <img src="https://main.qcloudimg.com/raw/269b8df52ed30d1c102de61bcb5e1b6a.png" style="margin:-3px 0px"> to view the detailed result.
- **Viewing the image layer information**
You can click **Layer Information** next to a target image repository to view the layer information for this image in the pop-up window.
- **Deleting an image tag**
 You can click **Delete** next to the target image tag to delete this image tag. Carefully review the deletion operation before confirming it to prevent important data being deleted by mistake.
 >! When a specified image tag is deleted, other image tags that have the same image ID as the deleted image tag may also be deleted. Consequently, these image tags will become unavailable.

### Building images
You can use the source code hosted on GitHub, GitLab.com, Gitee code cloud, or CODING to compile and build an image. For more information, see [Configuring Image Building](https://intl.cloud.tencent.com/document/product/1051/37252).

### Editing the repository information
On the details page of the image repository, you can select the **Repository Information** tab to view and edit basic information about the image repository, as shown in the figure below.
![](https://main.qcloudimg.com/raw/cba04ac5a3c628095d8d02b95b4b1581.png)
- **Editing the brief description**
Select <img src="https://main.qcloudimg.com/raw/f6a3c9acf9c397aa917299582b7b7523.png" style="margin:-3px 0px"> next to "Brief Description" to enter the editing state. After editing the description, click **Save** to save the modification.
- **Editing the detailed description**
Select <img src="https://main.qcloudimg.com/raw/f6a3c9acf9c397aa917299582b7b7523.png" style="margin:-3px 0px"> next to "Detailed Description" to enter the editing state. After editing the description, click **Save** to save the modification. "Detailed Description" supports the Markdown syntax. You can view the rendered text after the modification is saved.





## Relevant Operations
### Using regular expression to create rules[](id:RE)
#### Regular matching rules
The following are the matching rules supported by the regular expression when you enter “repository name” or “version tag”:
- `*`: matches all strings of any length that do not contain the path separator (`/`).
- `**`: match all strings of any length that contain the path separator (`/`).
<dx-alert infotype="notice" title="">
`**` must be used as a complete relative path. If you use `/path**`, it will be the same as `/path*` and will only match the first-level repositories whose names are prefixed with path. To match all repositories under path, you should use `/path/**`; to match all repositories whose names are prefixed with path, you should use `/path*/**`.
</dx-alert>
- `?`: matches any single character except ‘/’.
- `{alt1, alt2, …}`: matches multiple regular expressions at the same time.


#### Use cases

<table>
<tbody>
<tr>
<td>Matches all repositories in the specified namespace.</td>
<td><code>**</code> or leave it blank</td>
</tr>
<tr>
<td>Matches all first-level repositories whose names are prefixed with path in the specified namespace.</td>
<td><code>/path*</code> 
</tr>
<tr>
<td>Matches all first-level repositories whose names are prefixed with path1 and path2 in the specified namespace.</td>
<td><code>/{path1, path2}*</code></td>
</tr>
<tr>
<td>Matches all repositories under the path1 and path2 directories in the specified namespace.</td>
<td><code>/{path1, path2}/**</code></td>
</tr>
<tr>
<td>Matches all repositories whose names are prefixed with path1 and path2 in the specified namespace.</td>
<td><code>/{path1, path2}*/**</code> </td>
</tr>
<tr>
<td>Matches all 1.x version tags in the specified repositories.</td>
<td><code>1.?</code> </td>
</tr>
<tr>
<td>Matches all version tags whose names are prefixed with env1 and env2 in the specified repository.</td>
<td><code>{env1*, env2*}</code> </td>
</tr>
</tbody>
</table>
