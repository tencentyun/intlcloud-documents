## Purchase Notes

- CBM shares the <a href="https://buy.tencentcloud.com/cvm?tab=custom&step=1&devPayMode=hourly&regionId=1&zoneId=100006&projectId=-1&templateCreateMode=createLt">purchase page</a> and [console](https://console.cloud.tencent.com/cvm) with CVM, which means you can purchase CBM instances on the CVM purchase page. For more information, see [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517).
- Make sure that you understand CBM before purchase, including its [instance specification](https://www.tencentcloud.com/document/product/1171/52405) and [billing mode](https://www.tencentcloud.com/document/product/1171/52407).
- Make sure that you know the AZ of the CBM instance to be purchased. For more information, see [Available Regions](https://www.tencentcloud.com/document/product/1171/52408).

## How to Purchase

This document takes the **Standard BMS5** instance as an example to describe how to quickly purchase a CBM instance:

### Step 1. Log in to the purchase page

<div style="background-color:#00A4FF; width: 190px; height: 35px; line-height:35px; text-align:center;"><a href="https://buy.tencentcloud.com/cvm?regionId=1&projectId=-1" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.2764.btn2">Click here to enter the purchase page</a></div>


### Step 2. Select the billing mode, region, and model

On the purchase page, select the billing mode, network, region, and model. Here takes the **Standard BMS5 instance in Guangzhou Zone 3** as an example, and the actual information is as indicated on the purchase page:
- **Billing Mode**: **Spot instance**, **Pay-as-you-go**, or **Reserved instance**. For more information, see [Billing Mode](https://intl.cloud.tencent.com/document/product/213/2180).
- **Region and Availability Zone**: The AZ is subject to the information on the purchase page. For more information, see [Available Regions](https://www.tencentcloud.com/document/product/1171/52408).
- **Instance**: Here takes the **Standard BMS5** instance as an example, and you can select one as needed.


### Step 3. Select the image and storage

 1. Select the image for the CBM instance.
 CBM supports three image types: public, custom, and shared images. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/213/4940).
If you are a new user of Tencent Cloud, select the public image and then the version as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/avht237_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221220173309.png)
<dx-alert infotype="notice" title="">
GPU instances require the corresponding GPU driver to run properly, which can be installed in either of the following ways:
    - If you select **Public Image**, we recommend you select **Automatically install GPU driver on the backend** to preinstall the driver on the corresponding version. This method only supports certain Linux public images.
    - If you select **Custom Image**, you can manually install the driver as instructed in [Installing NVIDIA Driver](https://intl.cloud.tencent.com/document/product/560/8048) after the GPU instance is created successfully.
</dx-alert>

2. Select the storage for the CBM instance as shown below:
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/w2fi477_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221220173737.png"/>
<b>System disk</b> and <b>Data disk</b>: You can flexibly select the type and size (you cannot adjust the storage capacity of the local system disks).
3. Click **Next: Set Network and CBM**.


### Step 4. Set the network, security group, and instance
1. Select the network and bandwidth for the CBM instance as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/LS7e396_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221220174147.png)
 - **Network**: Select an existing VPC or create one.
 - **Public IP**: You need to select it if you require access to the public network. Then, a public IP will be assigned for the created instance.
 - **Bandwidth billing mode**: If you select **Public network bandwidth**, billing will be based on the fixed bandwidth or traffic usage.
    - **Bill-by-bandwidth**: Select a fixed bandwidth. Packet loss will occur when the bandwidth exceeds this value. This is applicable to scenarios where the network connection fluctuates slightly.
    - **Bill-by-traffic**: Billing is based on traffic that is actually used. You can specify a peak bandwidth. Packet loss will occur when the instantaneous bandwidth exceeds this value. This is applicable to scenarios where the network connection fluctuates significantly.
 - **Bandwidth value**: Public network bandwidth cap, which can be set as needed.
 - **IPv6 address**: The IPv6 address of the activated instance.
2. Select an existing security group or create one to control the port range as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/j6Ej878_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221220173935.png)
3. Set the login password or key for the CBM instance.
4. Set other custom configurations as needed.
5. Click **Next: Confirm Configuration Information**.


### Step 5. Confirm the configuration information

1. Check the following in the **Confirm Configuration Information** step as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/DTyn317_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221220174428.png)
 - Check whether the instance specification, image, storage, public network configuration, security group, and other configuration items are set as expected.
 - You can select or verify the quantity and purchase period.
2. Read and indicate your consent to the **Tencent Cloud Terms of Service** and click **Buy Now**.


### Step 6. Check the order and make the payment

Check the order information and select the payment method.
After the payment is made, you can log in to the instance after it is created and started.
