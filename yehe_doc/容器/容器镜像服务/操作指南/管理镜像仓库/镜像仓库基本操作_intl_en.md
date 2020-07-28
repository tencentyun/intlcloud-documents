
## Scenario
In Tencent Container Registry (TCR), an image repository is used to manage container images. A single image repository may contain container images with different tags. An image repository belongs to a namespace and inherits the public or private attributes and security scan triggering mode from its namespace.

The image repository is the minimum unit for permission management in TCR. The instance admin can grant the management or read-only permission to a sub-user. For example, the instance admin can grant the "tom" sub-account only the permission to pull images from the "project-a-frontend" image repository, but disallow the sub-account to push or delete images. For more information on other permission management and authorization methods, see [Examples of TCR Enterprise Edition Authorization Schemes](https://intl.cloud.tencent.com/document/product/1051/37248). This document describes how to create and manage an image repository in a TCR Enterprise Edition instance.



## Prerequisites

Before creating and managing an image repository for a TCR Enterprise Edition instance, you must complete the following preparations:
- You have [created a TCR Enterprise Edition instance](https://intl.cloud.tencent.com/document/product/1051/35486).
- If you are using a sub-account, ensure that you have granted the sub-account operation permissions for the corresponding instance in advance. For more information on how to grant the permissions, see [Examples of TCR Enterprise Edition Authorization Schemes](https://intl.cloud.tencent.com/document/product/1051/37248).

## Directions


### Creating an image repository
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and click **Image Repository** in the left sidebar.
On the "Image Repository" page, you can view the image repository list of the current instance. To change the instance, at the top of the page, select the desired instance name from the "Instance Name" drop-down list.
2. Click **Create**. In the "Create an Image Repository" window that appears, configure the image repository by referring to the following field description.
![](https://main.qcloudimg.com/raw/9c7c140240507d0b834e5c36103cadc2.png)
 - **Associated Instance**: indicates the currently selected instance, to which the created image repository belongs.
 - **Namespace**: indicates the namespace to which the image repository belongs. If the list is empty, first [create a namespace](https://intl.cloud.tencent.com/document/product/1051/35487) in the instance.
 - **Name**: indicates the name of the image repository. Its value must be 2 to 200 characters in length and can only contain lowercase letters, numbers, and separators including periods (`.`), underscores (`_`), hyphens (`-`), and slashes (`/`). This parameter cannot start or end with a separator or contain several consecutive separators. In addition, this name can be a cascaded path, such as `team-01/front/nginx`. You can set the name based on your business requirements.
 - **Image source**: supports "Local image push" and "Platform image building". For more information on how to build images on the platform, see [Configuring Image Building](https://intl.cloud.tencent.com/document/product/1051/37252).
 - **Summary**: indicates the brief description of the image repository. Its value is a string of up to 100 characters. You can edit the summary again after the image repository is created.
 - **Description**: indicates the detailed description of the image repository. This parameter supports the Markdown syntax. Its value is a string of up to 1,000 characters. You can modify the description after the image repository is created.
3. Click **OK** to create the image repository.

### Image repository operations
After the image repository is created, you can view the image repository on the "Image Repository" page. Then, you can perform the following operations to manage the image repository, as shown in the following figure:
![](https://main.qcloudimg.com/raw/da0a7ecad3c69b5df7bb63e64908c47f.png)
- **Filtering namespaces**
Select <img src="https://main.qcloudimg.com/raw/cec7f1733d3e76d18c27b0bcbb65965b.png" style="margin: -3px 0px"> from the "Image Repository" list for filtering. Then, you can select a namespace that you want to view from the drop-down list.
- **Viewing details of a repository**
Click the name of a specified image repository. The repository details page appears, where you can manage the image tag and edit the basic information of the image repository.
- **Deleting an image repository**
You can click **Delete** for an image repository to delete it. Exercise caution before confirming the deletion to prevent important data from being deleted by mistake.
>! After the image repository is deleted, **all container images in the image repository are directly deleted**. 


### Managing image tags
Click the name of a specified image repository. The repository details page appears, and you are directed to the **Tag Management** tab page by default. On this page, you can manage all image tags in the repository, perform security scans, and view the layer information, as shown in the following figure:
![](https://main.qcloudimg.com/raw/02373fdce067c3f10cc54d3a7293cc82.png)
- **Filtering image tags**
In the search box in the upper-right corner of the tag list, you can enter an image tag to search for this tag. Fuzzy search is supported.
- **Obtaining a pull command**
You can click **Pull Command** for the target image tag to copy the pull command of the image tag.
- **Performing a security scan**
You can click **Scan** for the target image tag to proactively trigger a security scan. When the scanning result is output for the corresponding "Security Level", click <img src="https://main.qcloudimg.com/raw/269b8df52ed30d1c102de61bcb5e1b6a.png" style="margin:-3px 0px"> to view the detailed result.
- **Viewing the image layer information**
You can click **Layer Information** for a target image repository to view the layer information for this image in a pop-up window.
- **Deleting an image tag**
 You can click **Delete** for a target image tag to delete this image tag. Excercise caution before confirming the deletion to prevent important data from being deleted by mistake.
 >! When a specified image tag is deleted, other image tags with the same image ID as the deleted image tag may also be deleted. If this is the case, these image tags will become unavailable.

### Building images
You can use source code hosted in GitHub, GitLab.com, Gitee.com, and CODING to perform compilation and building. For more information, see [Configuring Image Building](https://intl.cloud.tencent.com/document/product/1051/37252).

### Editing the repository information
On the details page of the image repository, you can click the **Repository Information** tab to view and edit the basic information about the image repository, as shown in the following figure:
![](https://main.qcloudimg.com/raw/7854bca0d060431b3d6af1e35848e2e7.png)
- **Editing the summary**
Click <img src="https://main.qcloudimg.com/raw/f6a3c9acf9c397aa917299582b7b7523.png" style="margin:-3px 0px"> for "Summary" to activate editing. After editing the summary, click **Save** to save the change.
- **Editing the description**
Click <img src="https://main.qcloudimg.com/raw/f6a3c9acf9c397aa917299582b7b7523.png" style="margin:-3px 0px"> for "Description" to activate editing. After editing the description, click **Save** to save the change. "Description" supports the Markdown syntax. You can view the rendered text after saving the change.
