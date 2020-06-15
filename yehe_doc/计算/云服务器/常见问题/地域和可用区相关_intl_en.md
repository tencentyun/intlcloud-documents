### How can I view regions and availability zones?

To view regions and availability zones, use either of the following methods:
- View the [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/213/6091) document.
- Use APIs to view regions and availability zones.
 - To view regions, use the [DescribeRegions](https://intl.cloud.tencent.com/document/product/213/15708) API.
 - To view availability zones, use the [DescribeZones](https://intl.cloud.tencent.com/document/product/213/35071) API.


### Which CVM regions and availability zones are available, and how do I choose from them?

For more information on available CVM regions and availability zones, see [Regions and Availability Zones](http://intl.cloud.tencent.com/document/product/213/6091).
For more information on how to choose regions and availability zones, see [How to Choose Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/213/6091#.E5.A6.82.E4.BD.95.E9.80.89.E6.8B.A9.E5.9C.B0.E5.9F.9F.E5.92.8C.E5.8F.AF.E7.94.A8.E5.8C.BA).


### Can I change the region of a purchased CVM?

No. Region change is not supported for purchased CVMs. To change regions or availability zones, use either of the following methods:
- [Terminate the instance](https://intl.cloud.tencent.com/document/product/213/4930) and then repurchase the instance.

- Use the original instance to create a custom image. Then, use the custom image to create an instance, start the instance, and update the instance configuration in a new availability zone.
  1. Create a custom image for the current instance. For more information, see [Creating Custom Images](https://intl.cloud.tencent.com/document/product/213/4942).
  2. If the [network environment](https://intl.cloud.tencent.com/document/product/213/5227) of the current instance is a VPC instance and the private IP address needs to be retained after the instance is migrated to a new availability zone, delete the subnet in the current availability zone and then create a subnet in the new availability zone with the same IP address range as that of the original subnet.
  > If the subnet to be deleted contains available instances, first migrate all instances in the subnet to the new subnet.
  >
  3. Use the created custom image to create another instance in the new availability zone.
  You can choose the instance type and configuration to be the same as those of the original instance or new ones for the new instance. For more information, see [Creating Instances](https://intl.cloud.tencent.com/document/product/213/4855).
  4. If an elastic public IP address is associated with the original instance, disassociate it from the original instance and associate it with the new instance. For more information, see [Elastic IP Addresses (EIPs)](https://intl.cloud.tencent.com/document/product/213/5733).
  5. (Optional) If the [billing method](https://intl.cloud.tencent.com/document/product/213/2180) of the original instance is pay-as-you-go, you can terminate it. For more information, see [Terminating Instances](https://intl.cloud.tencent.com/document/product/213/4930).

### Can Tencent Cloud users in China enjoy the same product quality and services as resources in China for resources that they have purchased in other countries or regions?
Yes. The Tencent Cloud Chinese website provides products and services of the same quality to all users. Service benefits on the Tencent Cloud Chinese website do not vary with the purchase region.

### Can I use the replication feature of a custom image to migrate a CVM in China to another country or region?
- No. Images can be replicated only within the same country or region. To replicate images between different countries, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1).

### What are the differences between instances in regions in and outside China, and how do I determine which region is suitable for me?
Instances in other countries or regions are deployed in regions outside China. For users outside China, regions outside China have obvious geographical and market advantages. They provide fast local network connections and can meet international customers' requirements. Therefore, regions outside China are suitable for users who run businesses in other countries or regions.

- For more information on supported regions, see [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/213/6091).

### Can I change the OS of a CVM instance purchased in a region outside China between Linux and Windows?
CVM instances in all regions support reinstalling an operating system (OS) of the same type. For example, reinstalling the Linux OS on CVM with a Linux OS or reinstalling the Windows OS on a CVM with a Windows OS.
Only CVM instances in Mainland China support reinstalling an OS of a different type. For example, reinstalling a Linux OS on a CVM with a Windows OS or reinstalling a Windows OS on a CVM with a Linux OS.

### How do I apply for after-sales services for products purchased in regions outside China?
If you have purchased a product on the Tencent Cloud official website, call the Tencent Cloud 24/7 service hotline (95716) or [submit a ticket](https://console.cloud.tencent.com/workorder/category).

### How do I deploy CVM instances in regions outside China?
CVM instances in regions in and outside China adopt the same deployment method if they have the same type of OS.

### Can I migrate instances from Chinese regions to overseas regions?
The region and availability zone of an instance are not changeable. To use an instance in other countries or regions, you need to repurchase the instance.

### Why can I purchase some instance types in Chinese regions but cannot do so in overseas regions?
Some regions may not support certain instance types. For information on supported instance types, you can go to the [CVM purchase page](http://manage.qcloud.com/shoppingcart/shop.php?tab=cvm&_ga=1.78908498.770173325.1571651505) to view instance purchase information.

### If I am using an instance in an overseas region to build a website and my customers use a domain name to access the website, is ICP filing required for the domain name?
The ICP filling is required for domain names of websites in Mainland China, and unnecessary for those in Hong Kong, Macao and Taiwan regions (China) and other countries. For more information, see [ICP Filing Overview](https://intl.cloud.tencent.com/document/product/1022/30453).

### Do instances in different regions have the same price?
The price of an instance includes the prices for the instance type, storage, and network bandwidth. If the prices for the instance type, storage, and network bandwidth are different, the instance price will be different.
For more information on pricing, see [Pricing](https://buy.cloud.tencent.com/price/cvm/calculator).



