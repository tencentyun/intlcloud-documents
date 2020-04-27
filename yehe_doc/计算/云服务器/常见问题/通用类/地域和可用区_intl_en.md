### How do I view regions and availability zones?

To view regions and availability zones, use either of the following methods:
- View the [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/213/6091) document.
- Use APIs:
 - To view regions, use the [DescribeRegions](https://intl.cloud.tencent.com/document/product/213/15708) API.
 - To view availability zones, use the [DescribeZones](https://intl.cloud.tencent.com/document/product/213/35071) API.

### Can I change the region of a purchased CVM?

No. You cannot change the region of a purchased CVM or the availability zone for a started CVM. To change the region and availability zone, use either of the following methods:

- Create a custom image for the original instance. Then, in a new availability zone, use the custom image to create an instance, start the created instance, and update the instance configuration.
  1. Create a custom image for the current instance. For details, see [Creating Custom Images](https://intl.cloud.tencent.com/document/product/213/4942).
  2. If the [network environment](https://intl.cloud.tencent.com/document/product/213/5227) of the current instance is a VPC instance and the private IP address needs to be retained after the instance is migrated to another availability zone, delete the subnet in the current availability zone and then create a subnet in the new availability zone with the same IP address range as that of the original subnet.
  > If the subnet to be deleted contains available instances, first migrate all these instances in the subnet to the new subnet.
  >
  3. Use the created custom image to create an instance in the new availability zone.
  You can use the same instance type and configuration as those of the original instance. Also, you can modify them for the new instance. For details, see [Creating an Instance](https://intl.cloud.tencent.com/document/product/213/4855).
  4. If an elastic public IP address is associated with the original instance, dissociate it from the original instance and associate it with the new instance. For details, see [Elastic Public IP Addresses (EIPs)](https://intl.cloud.tencent.com/document/product/213/5733).
  5. (Optional) If the billing method of the original instance is [pay-as-you-go](https://intl.cloud.tencent.com/document/product/213/2180), you can terminate it. For details, see [Terminating Instances](https://intl.cloud.tencent.com/document/product/213/4930).
