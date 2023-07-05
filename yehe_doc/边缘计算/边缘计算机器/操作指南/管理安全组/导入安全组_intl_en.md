## Overview

The security group feature of ECM is logically isolated from the public security group feature in the central cloud. Central cloud products such as CVM cannot be associated with a security group in ECM, and ECM resources such as ECM module, ECM instance, and ELB cannot be directly associated with a public security group in the central cloud. If you have already created a public security group, you can import its data, and a security group data record for ECM will be automatically generated after the import.

You can also create a security group by yourself. For more information, see [Creating Security Group](https://intl.cloud.tencent.com/document/product/1119/43432).

## Directions
1. Log in to the ECM console and select **Edge Network** > **[Security Group](https://console.cloud.tencent.com/ecm/safe)** on the left sidebar.
3. On the **Security Group** management page, click **Import**.
4. In the **Security Group** pop-up window, perform the operations as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/259544dc3982cc4a5d18622f08b627be.png)
  1. Select the central cloud region, and all security groups in this region will be displayed.
  2. Select the security group data to be imported.
 <dx-alert infotype="notice" title="">
- Currently, you cannot import the security group data in finance zones or regions outside the Chinese mainland.
- Only inbound rules in the security group are imported, while the parameter template rules and nested rules will be filtered out.
</dx-alert>
5. Click **OK** to import the public security group in the central cloud, and new data will be generated in the ECM security group management list.
