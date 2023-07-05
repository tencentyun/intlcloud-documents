### How can I view regions and availability zones?

To view regions and availability zones, try the followings:
- Refer to [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/213/6091) document.
- Use APIs to query regions and availability zones.
 - To view regions, use the [DescribeRegions](https://intl.cloud.tencent.com/document/product/213/15708) API.
 - To view availability zones, use the [DescribeZones](https://intl.cloud.tencent.com/document/product/213/35071) API.


### What CVM regions and availability zones are available and how to choose?

For more information on available CVM regions and availability zones, see [Regions and Availability Zones](http://intl.cloud.tencent.com/document/product/213/6091).
For more information on how to choose regions and availability zones, see [How to Select the Region and Availability Zone](https://intl.cloud.tencent.com/document/product/213/6091#.E5.A6.82.E4.BD.95.E9.80.89.E6.8B.A9.E5.9C.B0.E5.9F.9F.E5.92.8C.E5.8F.AF.E7.94.A8.E5.8C.BA).


### Can I change the region of a purchased CVM?

No. You cannot change the regions of purchased CVMs. If you need to deploy an existing CVM to another region or availability zone, please try the following:
- [Terminate the instance](https://intl.cloud.tencent.com/document/product/213/4930) and then purchase a new one.

- Create a custom image for the original instance. Then, use the custom image to create an instance, launch it and update its configuration in a new availability zone.
  1. Create a custom image for the current instance. For more information, see [Create Custom Images](https://intl.cloud.tencent.com/document/product/213/4942).
  2. If the [network environment](https://intl.cloud.tencent.com/document/product/213/5227) of the current instance is VPC and you need to retain the private IP address after migration, please delete the subnet in the current availability zone and then create a subnet in the new availability zone with the same IP address range as that of the original subnet.
  > If the subnet to be deleted contains available instances, first migrate all instances in the subnet to the new subnet.
  >
  3. Use the newly created custom image to create a new instance in the new availability zone.
  You can choose the same instance type and configuration as that of the original instance, or configure new ones for the new instance. For more information, see [Creating an Instance](https://intl.cloud.tencent.com/document/product/213/4855).
  4. If an elastic public IP address is associated with the original instance, disassociate it from the original instance and associate it with the new instance. For more information, see [Elastic IP Addresses (EIPs)](https://intl.cloud.tencent.com/document/product/213/5733).
  5. (Optional) If the [pricing modes](https://intl.cloud.tencent.com/document/product/213/2180) of the original instance is pay-as-you-go, you can terminate it. For more information, see [Terminate Instances](https://intl.cloud.tencent.com/document/product/213/4930).

### Can Tencent Cloud users in China enjoy the same product quality and services for resources purchased in China and other regions or countries?
Yes. Tencent Cloud China Console provides all users with the same product quality and services. The purchase region will not affect your user rights on the console.

### Can I use the replication feature of a custom image to migrate a CVM in Mainland China to another country or region?
- No. Images can only be replicated within the same country or region. To replicate images between countries, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1) to apply.

### What are the differences between instances in and outside Mainland China, and how do I determine which region fits me the best?
Instances in other countries or regions are deployed outside Mainland China, providing geographical and market advantages for global users. The fast local network can also meet international customer needs, which is suitable for users who run businesses in other countries or regions.

- For more information on supported regions, see [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/213/6091).

### Can I change between Linux and Windows operating systems for a CVM instance purchased in a region outside Mainland China?
No. Switching OS between Windows and Linux is only available for CVM instances in Mainland China.

### How do I apply for after-sale services for products purchased in regions outside Mainland China?
If you purchased a product on the Tencent Cloud official website, call the Tencent Cloud 24/7 service hotline (4009100100) or [submit a ticket](https://console.cloud.tencent.com/workorder/category).

### How do I deploy CVM instances in regions outside China?
CVM instances in regions outside China have the same deployment method if they have the same type of operating system.

### Can I migrate instances to regions outside Mainland China?
The region and availability zone of an instance cannot be changed. To use an instance in other countries or regions, you need to purchase another instance.

### Why some instance types can only be purchased in China regions?
Some regions may not support certain instance types. For information on supported instance types, go to the [CVM purchase page](http://manage.qcloud.com/shoppingcart/shop.php?tab=cvm&_ga=1.78908498.770173325.1571651505) to view instance purchase information.

### If I build a website using a CVM instance from a region outside Mainland China and my users access the website through a domain name, does this domain name need ICP filing?
For websites in regions in Mainland China, ICP filing is required for domain names. For websites in other countries or regions, ICP filing is not required. 

### Do instances in different regions have the same price?
The pricing of a CVM instance includes its specifications, storage, network bandwidth, etc. The prices of these components vary by regions, so the instance price will be different.
For more information on pricing, see [Pricing](https://buy.cloud.tencent.com/price/cvm/calculator).
