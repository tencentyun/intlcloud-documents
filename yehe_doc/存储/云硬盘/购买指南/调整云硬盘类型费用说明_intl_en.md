Tencent Cloud's Cloud Block Storage (CBS) supports the adjustment of storage disk types while business is in operating status. By adjusting the cloud disk type, you can respond flexibly to business requirements for storage performance at different times. For more information on preconditions, precautions, and specific operations of adjusting cloud disk types, see [Adjusting cloud disk types](https://intl.cloud.tencent.com/document/product/362/50096).
Currently, adjustment of cloud disk types only supports upgrading elastic cloud disks. It does not support downgrading. Details are as follows:
- A Basic Cloud Block Storage cloud disk can be adjusted to Premium Cloud Disk or SSD cloud disk.
- A Premium Cloud Disk can only be adjusted to SSD.
- A SSD cloud disk cannot be upgraded currently.

## Adjusting the Type of Monthly Subscribed Cloud Disks
### Billing rules
- The price difference is charged by day for upgrading monthly subscribed cloud disks: fees = monthly price difference (calculated as 0 if smaller than 0) * remaining days of the lifecycle / (365/12) * applicable discount.
  - **Monthly price difference**: The difference between the monthly list price of the new and old disk configuration.
  - Remaining days of the lifecycle = resource expiration time - current time
    The time is accurate to second and calculated as 1 day if shorter than 1 day.
  - Applicable discount: The applicable discount is matched based on the number of remaining days of the lifecycle as effective at the official website.
- Adjusting the cloud disk type doesn't affect the resource expiration time.
- You can use vouchers and free credits for fees deduction when adjusting the cloud disk type.

### Examples

<dx-alert infotype="explain" title="">
The following prices are for demonstration only. The actual unit prices shall prevail, which may vary by region, promotions, or policy. For more information, see [Pricing | Cloud Block Storage](https://www.tencentcloud.com/pricing/cbs).
</dx-alert>





## Adjusting the Type of Pay-as-You-Go Cloud Disks
After you adjust the type of a pay-as-you-go cloud disk, fees will be charged based on the new configuration.


