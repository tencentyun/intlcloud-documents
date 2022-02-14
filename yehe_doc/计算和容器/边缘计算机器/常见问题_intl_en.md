### How do I create (purchase) an ECM module and ECM instance?

- You can **create an ECM module and deploy an instance** in the following steps:
 1. Log in to the ECM console and click **Create Module** on the **ECM Module** page to create a module.
 When creating a module, you need to enter the basic module information and select the instance configuration.
 2. Enter the details page of the new module and click **Create and Deploy Instance** on the right to deploy an instance.
 3. Set the instance name and login password and confirm the default image and network bandwidth cap.
 4. Select the region, province, node, ISP, and instance quantity for instance deployment.
 5. Check configuration items such as security and monitoring and view the estimated fees.
 6. After confirming that everything is correct, click **Buy Now**.
 ECM will immediately start to deploy the instance on the specified node.
- You can **add an ECM instance to an existing ECM module** in the following steps:
 1. Log in to the ECM console, select the **Instance List** tab on the details page of an existing ECM module, and click **Add Instance**.
 You can also click **Add Instance** on the instance list management page for scaling.
 2. On the instance adding page, set the instance name and login password and confirm the default image and network bandwidth cap.
 3. Select the region, province, node, ISP, and instance quantity for instance deployment.
 4. Check configuration items such as security and monitoring and view the estimated fees.
 5. After confirming that everything is correct, click **Buy Now**.


### How do I view the details of an ECM module and instance?
- You can view the details of an ECM module as follows:
On the **ECM Module** page, click **Details** in the **Operation** column to enter the module details page.
- You can view the details of an ECM instance as follows:
On the **Instance List** page, click **Details** in the **Operation** column to enter the instance details page.


### How do I log in to an ECM instance?
You can log in to an ECM instance in the following two methods:
- Login at the instance's public IP address
 1. On the ECM instance list or details page, view the instance's public IP address.
 2. Use a remote login tool for login.
 You can also log in to a Linux instance over SSH.
- Login through VNC
 1. In the ECM console, click **Login** and select login through VNC.
 2. Enter the username and password in the pop-up window to log in.


### How do I use a custom image?

Custom images are provided through cloud-edge collaboration, and you can create up to 10 custom images under each account.
You can use a custom image in the following steps:
1. Create an image in image management in the CVM console. For detailed directions, see [Creating Custom Images](https://intl.cloud.tencent.com/document/product/213/4942).
2. Import the required custom image to ECM in image management in the ECM module. For detailed directions, see [Managing Image](https://intl.cloud.tencent.com/document/product/1119/43417).
3. Use the imported image when creating an ECM module. For detailed directions, see [Creating ECM Module](https://intl.cloud.tencent.com/document/product/1119/43421).

### How large is the default system disk space in an ECM instance?

The default system disk space of an ECM instance is 50 GB, which currently cannot be adjusted.

### How do I configure IP direct access for an ECM instance?

Currently, ECM instances are configured with IP direct access by default. You can log in to a Linux instance and run the `ip addr` command to get the public IP address for direct instance access.

