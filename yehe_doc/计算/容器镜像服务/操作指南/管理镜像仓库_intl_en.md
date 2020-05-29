
## Scenario
In Tencent Container Registry (TCR), an image repository is used to manage container images. A single image repository may contain container images with different tags. An image repository belongs to a namespace and inherits the public or private attribute and security scan triggering mode from its namespace.

The image repository is the minimum unit for permission management in TCR. The instance admin can grant the management or read-only permission to a sub-user. For example, the instance admin can grant the "tom" sub-account only the permission to pull images from the "project-a-frontend" image repository, but disallow the sub-account to push or delete images. For more information about other permission management and authorization methods, please see Examples of Enterprise Edition Authorization Schemes. This document describes how to create and manage an image repository in a TCR Enterprise Edition instance.



## Prerequisites

Before creating and managing a synchronization rule for a TCR Enterprise Edition instance, complete the following tasks:
- [Create an Enterprise Edition instance](https://intl.cloud.tencent.com/document/product/1051/35486).
- If you are using a sub-account, grant the sub-account operation permissions for the corresponding instance in advance. For more information, see Examples of Enterprise Edition Authorization Schemes.

## Procedure


### Creating an image repository
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Image Repository** in the left sidebar.
On the "Image Repository" page, you can view the image repository list of the current instance. To change the instance, select the desired instance name from the "Instance Name" drop-down list at the top of the page.
2. Click **Create**. In the "Create an Image Repository" window, configure the following information for the image repository. See the figure below.

 - **Associated Instance**: currently selected instance, to which the created image repository belongs.
 - **Namespace**: namespace to which the image repository belongs. If the list is empty, you must [create a namespace](https://intl.cloud.tencent.com/document/product/1051/35487) in the instance.
 **Name**: name of the image repository. The value must be 2 to 200 characters in length and can only contain lowercase letters, numbers, and separators (including periods (.), underscores (_), hyphens (-), and slashes (/). It cannot start or end with a separator or contain several consecutive separators. The name can be a multi-level path, such as `team-01/front/nginx`. You can set the name flexibly based on your business requirements.
 - **Summary**: brief description of the image repository. It is a string of up to 100 characters. You can re-edit the summary after the image repository is created.
 - **Description**: detailed description of the image repository. This parameter supports the Markdown syntax. It is a string of up to 1000 characters. You can modify the description after the image repository is created.
3. Click **OK** to create the image repository.

### Basic image repository operations
After the image repository is created, you can view the image repository on the "Image Repository" page. Then, you can perform the following operations to manage the image repository. See the figure below.

- **Filtering namespaces**
Select <img src="https://main.qcloudimg.com/raw/cec7f1733d3e76d18c27b0bcbb65965b.png" style="margin: -3px 0px"> from the "Image Repository" list for filtering. Then, you can select a namespace to view from the drop-down list.
- **Viewing details of a repository**
Click the name of a specified image repository. The repository details page is displayed, where you can manage the image tag and edit the basic information of the image repository.
- **Deleting an image repository**
You can click **Delete** next to an image repository to delete it. Carefully review the deletion operation before confirming it to prevent important data from being deleted by mistake.
> After the image repository is deleted, **all container images in the image repository are deleted**. 


### Managing image tags
Click the name of a specified image repository. The repository details page is displayed, and the **Tag Management** tab is selected by default. On this page, you can manage all the image tags in the repository, perform security scans, and view the layer information. See the figure below.

- **Filtering image tags**
In the search box in the upper-right part of the tag list, you can enter an image tag to search for this image tag. Fuzzy search is supported.
- **Performing a security scan**
You can click **Scan** next to the target image tag to actively trigger a security scan. When the result is available for the corresponding "Security Level", click <img src="https://main.qcloudimg.com/raw/269b8df52ed30d1c102de61bcb5e1b6a.png" style="margin:-3px 0px"> to view the detailed result.
- **Viewing the image layer information**
You can click **Layer Information** next to a target image repository to view the layer information for this image in a pop-up window.
- **Deleting an image tag**
 You can click **Delete** next to the target image tag to delete this image tag. Carefully review the deletion operation before confirming it to prevent important data from being deleted by mistake.
 > When a specified image tag is deleted, other image tags that have the same image ID as the deleted image tag may also be deleted. Consequently, these image tags will become unavailable.

### Editing the repository information
On the details page of the image repository, you can select the **Repository Information** tab to view and edit basic information about the image repository. See the figure below.

- **Editing the summary**
Select <img src="https://main.qcloudimg.com/raw/f6a3c9acf9c397aa917299582b7b7523.png" style="margin:-3px 0px"> next to "Summary" to enter the editing state. After editing the summary, click **Save** to save the modification.
- **Editing the description**
Select <img src="https://main.qcloudimg.com/raw/f6a3c9acf9c397aa917299582b7b7523.png" style="margin:-3px 0px"> next to "Description" to enter the editing state. After editing the description, click **Save** to save the modification. "Description" supports the Markdown syntax. You can view the rendered text after the modification is saved.
