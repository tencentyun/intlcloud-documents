

To quickly familiarize you with Tencent Cloud Infrastructure as Code (TIC), this document describes the following basic features of TIC:

- [Authorizing TIC](#tic-.E6.8E.88.E6.9D.83): allows you to authorize TIC to orchestrate cloud resources such as CVM, COS, and MySQL.
- [Creating a stack](#.E6.96.B0.E5.BB.BA.E8.B5.84.E6.BA.90.E6.A0.88): allows you to compile stack code and perform the plan and apply operations to create cloud resources and build cloud infrastructures.
- [Viewing cloud resources](#.E6.9F.A5.E7.9C.8B.E4.BA.91.E8.B5.84.E6.BA.90): allows you to view cloud resources created using TIC.
- [Destroying cloud resources](#.E9.94.80.E6.AF.81.E4.BA.91.E8.B5.84.E6.BA.90): allows you to release cloud resources to return to the initial status.


>!TIC is free to use, but you may need to pay for the cloud resources (such as CVM and MySQL) created using TIC. Modify configuration files based on your business requirements to avoid incurring unexpected costs.

## Authorizing TIC

Upon first use of TIC, you must authorize the service to access cloud resources under your Tencent Cloud account for orchestration. Without authorization, TIC is unable to orchestrate Tencent Cloud resources.

1. Log in to the [TIC console](https://console.cloud.tencent.com/tic).
2. In the left sidebar, choose **Settings** -> **API Credentials** to go to the **API Credentials** page.
3. Click the **TIC Authorization** switch. In the **Service authorization** dialog box that appears, click **Access Management** to go to the CAM page.
	 ![](https://main.qcloudimg.com/raw/61927cdb1e465a042333f6c8ce6a9ee4.jpg)
4. On the CAM page, click **Grant** to complete authorization.
5. Go back to the **API Credentials** page after authorization is complete. The TIC authorization feature is enabled.
	![](https://main.qcloudimg.com/raw/501c35dff65440679589f2287c225627.jpg)

## Creating a Stack

<span id="step1"></span>

### Step 1: Select Mode

1. In the left sidebar, choose **Orchestration** -> **Stacks** to go to the **Stacks** page.
2. Click **New**. On the **New Stack** page that appears, configure the parameters as follows:
 - **Provider**: the default value is **Tencent Cloud**. Currently, only **Tencent Cloud** is available.
 - **Region**: select a region where resources in the stack belong. To facilitate testing, select **Chengdu**. You can also select another region for testing.
3. In the **Specify Template** area, specify how you want to create the stack.
   - **URL**: only [Tencent Cloud COS](https://intl.cloud.tencent.com/document/product/436) and GitHub are supported. Only 1 file can be obtained at a time.
   - **Private templates**: select a private template. For more information, see [Template Management](https://intl.cloud.tencent.com/document/product/1043/37185).
   - **Public templates**: select a public template. For more information, see [Template Management](https://intl.cloud.tencent.com/document/product/1043/37185).
   - **Enter template content**: enter infrastructure code. Multi-file compiling is supported.
   In this example, **Enter template content** is selected to configure a new stack from scratch.
![](https://main.qcloudimg.com/raw/e7a0aaebaf3c3c7f59d187068b2136d8.jpg)
4. Click **Next** to go to Step 2.	 

### Step 2: Configure Stack

TIC parameter configuration is compatible with Terraform's HCL syntax. For more information about the HCL syntax, see [Terraform Configuration Language](https://www.terraform.io/docs/configuration/index.html).

1. Create resource parameter configuration files. In this example, to simulate the real operating environment of the live network, the following resources are created: 2 CVMs, 1 VPC, 1 subnet, 1 route table, 1 security group (including 1 security group rule), and 1 TencentDB for MySQL instance. Corresponding to these resources, the following configuration files are created, respectively: `cvm.tf`, `vpc.tf`, `subnet.tf`, `route_table.tf`, `security_group.tf`, and `mysql.tf`. The following figure shows the file structure.
![](https://main.qcloudimg.com/raw/9d7c09bf68f6eb7ecf661b7fd23dda12.jpg)
2. To enable the template to be used universally, create `variable.tf`. In this example, `variable.tf` defines 2 variables: the default region `ap-chengdu` and the default availability zone `ap-chengdu-1`. Note that the region name must be the same as that selected in [Step 1](#step1).
   ```
   // variable.tf
   variable "default_region" {
     type = string
     default = "ap-chengdu"
   }
   variable "default_az" {
     type = string
     default = "ap-chengdu-1"
   }
   ```
3. The variables defined in `variable.tf` are referenced by other `.tf` files. The `cvm.tf` file is used as an example to describe the syntax. To obtain the complete content of the `.tf` configuration file, download [tic-demo-config.zip](https://tic-demo-1259649581.cos.ap-nanjing.myqcloud.com/templates/tic-demo-config.zip).
   ```
   // Create cvm
   resource "tencentcloud_instance" "cvm_demo" {
     instance_name = "ajaxhe-cvm-demo"
     availability_zone = var.default_az
     image_id = "img-pi0ii46r"
     instance_type = "S2.SMALL1"
     system_disk_type = "CLOUD_PREMIUM"
     allocate_public_ip = true
   
     security_groups = [
       tencentcloud_security_group.sg_demo.id
     ]
   
     vpc_id = tencentcloud_vpc.vpc_demo.id
     subnet_id = tencentcloud_subnet.subnet_demo.id
     count = 2
   
     tags = {
       role = "cgi"
       env = "prod"
     }
   }
   ```
**resource "tencentcloud_instance"**: indicates that the cloud resources to be created are CVM instances. For more information about cloud resources, see [Resource Types](https://intl.cloud.tencent.com/document/product/1043/37186).
	- cvm_demo: local resource name, which is used for cross-cloud resource referencing.
	- instance_name: name of the CVM instance.
	- availability_zone: availability zone of the CVM instance. The default_az variable in the variable.tf file is referenced.
	- image_id: image ID of the CVM instance. The value "img-pi0ii46r" indicates Ubuntu Server 18.04.1 LTS (64-bit). You can obtain the image ID from the [Images](https://console.cloud.tencent.com/cvm/image?rid=16&imageType=PUBLIC_IMAGE) page in the Tencent Cloud Console.
	- instance_type: [instance type](https://intl.cloud.tencent.com/document/product/213/11518).

 **system_disk_type**: type of the system disk. The value `CLOUD_PREMIUM` indicates premium cloud storage. For more information, see the DiskType description in [CreateDisks](https://intl.cloud.tencent.com/document/api/362/16312).
	- allocate_public_ip: whether to configure a public IP address. To configure a public IP address, set the value to true.
	- security_groups: list of security groups to associate with the CVM instance. The value tencentcloud_security_group.sg_demo.id indicates that the CVM instance is associated with the security group defined in the security_group.tf file.
	- vpc_id: ID of the VPC to associate with the CVM instance. The value tencentcloud_vpc.vpc_demo.id indicates that the CVM instance is associated with the VPC defined in the vpc.tf file.
	- count: reserved field. A value of 2 indicates that 2 CVM instances with the preceding configurations will be created.
	- tags: used to classify CVM instances.


### Step 3: Plan

After you finish compiling the configuration files, click **Next** to go to the **Plan** step. In this step, TIC verifies the configuration syntax and preprocesses the resource change operations.
According to the plan results shown in the following figure, 8 cloud resources will be created, and no resource will be changed or destroyed.
![](https://main.qcloudimg.com/raw/90d833a5cf1ce79044794ef4cda44de2.jpg)


### Step 4: Apply

If the plan results meet your requirements, perform the following operations:

1. Click **Next**. In the dialog box that appears, enter the stack name and description, and then click **Confirm**.
![](https://main.qcloudimg.com/raw/41a2ebc30fa001e75b45f7e73d31a83b.jpg)
2. In the confirmation dialog box that appears, click **Confirm**.
![](https://main.qcloudimg.com/raw/4a7fd61b3edfc2dca1a4cc03cc7b68a6.jpg)
3. TIC performs the apply operation to create the cloud resources. You are redirected to the **Event** tab on the corresponding stack details page. The status **APPLY_IN_PROGRESS** indicates that the cloud resources are being created. The creation process takes several minutes.
![](https://main.qcloudimg.com/raw/adf3eb77416462a241eb5488a1baf44c.jpg)
4. Click **Refresh** in the upper-right corner of the **Event** tab to refresh the status. When the status becomes **APPLY_COMPLETED**, the cloud resources are successfully created.
![](https://main.qcloudimg.com/raw/0687d0db51cff6dd8c093deec7d3d4b2.jpg)

## Viewing Cloud Resources

1. On the [**Stacks**](https://console.cloud.tencent.com/tic/stacks) page, find the created stack and click **Details** in the **Operation** column to go to the stack details page.
2. Click the **Resource** tab and view the TIC-managed cloud resources.
![](https://main.qcloudimg.com/raw/f4f04c2473250553af66fc688bb67076.jpg)
3. The **Resource** tab displays only several key fields of cloud resources. To view resource details, go to the corresponding Tencent Cloud service console. For example, you can log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index?rid=1) to view the 2 CVM instances created using TIC.
![](https://main.qcloudimg.com/raw/cb736132e7e65b99bb25540384240f9c.jpg)


## Destroying Cloud Resources

TIC is free to use, but you may need to pay for the cloud resources created using TIC. To avoid costs incurred by idle cloud resources, destroy cloud resources at the earliest possible time if they are only used for testing.

1. Go to the [**Stacks**](https://console.cloud.tencent.com/tic/stacks) page, select the desired stack, and click **Destroy**.
![](https://main.qcloudimg.com/raw/90667b976aa416830d8a045f87b1036c.jpg)
2. Before the stack is destroyed, information about cloud resources in the stack is displayed. After the stack is destroyed, cloud resources in the stack cannot be recovered.
![](https://main.qcloudimg.com/raw/b372a24d549287f091468dddc09c0fc6.jpg)
3. Click **Destroy**. In the confirmation dialog box that appears, click **Confirm**. TIC then begins to destroy the cloud resources. The following figure shows the destruction process.
![](https://main.qcloudimg.com/raw/b1adc71d068329f5c32436f2afb769b7.jpg)
4. Wait several minutes until all cloud resources are destroyed.
![](https://main.qcloudimg.com/raw/14064084402114d47ddedf5b295c4c9b.jpg)
5. Click **Finish** to return to the stack list page, where you will find that the status of the stack has become **DESTROY_COMPLETED**.
![](https://main.qcloudimg.com/raw/5b636a3c749475565d566f8a6c7a9bd2.jpg)

