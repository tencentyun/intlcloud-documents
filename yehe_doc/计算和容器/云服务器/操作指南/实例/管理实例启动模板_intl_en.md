## Overview
This document describes how to create, manage, and use an instance startup template in the CVM console to quickly create an instance. Such a template stores the configuration information required for CVM instance creation (excluding the instance password) and improves the efficiency and user experience.

## Notes
- After an instance startup template is created successfully, its configuration cannot be modified.
- You can create one or multiple versions of an instance startup template and set different configuration information for each version. You can also specify the default version, whose configuration will be used when you use the template to create an instance.


## Directions

### Creating and viewing instance template
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index?rid=1) and select **Instance Startup Template** on the left sidebar.
2. On the **Instance Startup Template** page, click **Create Template**.
3. On the **instance startup template** creation page, customize **Template Name** and **Template Description** and set other configuration items as instructed in [Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855).
4. In the **Confirm Configuration** step, read and indicate your consent to the **Tencent Cloud Terms of Service** and **Refund Policy** and click **Create Now**.
After successful creation, you can view the instance startup template in the console .
You can click the template ID to enter the template details page and view the specific information.


### Creating instance startup template version
1. On the **Instance Startup Template** page, select **Create Version** on the right of the target template .
2. On the **instance startup template** creation page, configure the version as instructed in [Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855).
3. In the **Confirm Configuration** step, read and indicate your consent to the **Tencent Cloud Terms of Service** and **Refund Policy**.
You can select **Compare with Original Configuration** to confirm the difference between the new version and original instance startup template in the **Compare with Original Configuration** pop-up window.
4. After confirming that everything is correct, click **Create Now**.
After successful creation, you can click <img src="https://main.qcloudimg.com/raw/bc4f9debb43518cdf0e1552f76f9b7fa.png" style="margin:-3px 0px"> before the target template on the **Instance Startup Template** page to view the version in the expanded list.


### Specifying default instance startup template version
1. On the **Instance Startup Template** page, click <img src="https://main.qcloudimg.com/raw/bc4f9debb43518cdf0e1552f76f9b7fa.png" style="margin:-3px 0px"> before the target template.
2. In the expanded list, click **Set as Default** on the right of the target version .
3. In the **Set Default Template** pop-up window, click **OK**.


### Using instance startup template to create instance
1. On the **Instance Startup Template** page, select **Create Instance** on the right of the target template.
<dx-alert infotype="explain" title="">
The configuration of the **default version** of the instance startup template will be used for instance creation by default. You can also click <img src="https://main.qcloudimg.com/raw/bc4f9debb43518cdf0e1552f76f9b7fa.png" style="margin:-3px 0px"> before the target instance and select another version in the expanded list to create an instance.
</dx-alert>
2. In the **Confirm Configuration** step on the **CVM instance** creation page, you can select **Compare with Original Configuration** to view the difference between the instance and instance startup template in the **Compare with Original Configuration** pop-up window as shown below:
3. After confirming that everything is correct, read and indicate your consent to the **Tencent Cloud Terms of Service** and click **Activate**.





### Deleting instance startup template
1. On the **Instance Startup Template** page, select **Delete** on the right of the target instance startup template.
2. In the **Delete** pop-up window, click **OK**.


## References
[Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855)
