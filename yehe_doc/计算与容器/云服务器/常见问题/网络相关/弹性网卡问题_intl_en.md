### What is ENI?

[Elastic Network Interface](https://intl.cloud.tencent.com/product/eni) (ENI) is an elastic network interface bound to CVMs in a VPC, which can be migrated among multiple CVMs. ENI is very useful for configuring management networks and establishing highly reliable network solutions.

ENI has VPC, availability zone and subnet attributes. You can only bind it to CVMs under the same availability zone. A CVM can be bound with multiple ENIs, and the maximum number allowed varies by CVM specifications.

### What are the restrictions to use ENIs on CVMs?

For details, please see use limits section in [Use Limits Overview](https://intl.cloud.tencent.com/document/product/213/15379).

### What is the basic information of an ENI?

Please see **Concepts** in [Elastic Network Interface (ENI)](https://intl.cloud.tencent.com/document/product/213/6514).

### How do I create an ENI?

Please see [Creating an ENI](https://intl.cloud.tencent.com/document/product/576/18534).

### How do I view the ENI information?

Please see [Viewing ENI Information](https://intl.cloud.tencent.com/document/product/576/18533).

### How do I bind an ENI to a CVM instance?

Please see [Binding and Configuring CVMs](http://intl.cloud.tencent.com/document/product/576/18535).

### How do I configure an ENI in the CVM instance?

Please see [Binding and Configuring CVMs](http://intl.cloud.tencent.com/document/product/576/18535).

### How do I modify or customize the private IP of an ENI?

CVMs in VPC support modifying and customizing the private IP of an ENI. Follow the steps below:

1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. In the left side bar, click **IP and Interface** > **ENI** to enter the ENI list page.
3. Click the **ID/Name** of an ENI to enter its details page to view its information.
4. Select the **IPv4 address management** tab and click **Assign Private IP**.
5. In the pop-up window, select the IP assigning method as **Enter manually** to enter the IP address you want to modify.
6. Click **OK** to complete the operation.

After the modification is made on the console, you also need to modify the configuration file of the ENI. For more information, please see [Binding and Configuring CVMs](https://intl.cloud.tencent.com/document/product/576/18535).
