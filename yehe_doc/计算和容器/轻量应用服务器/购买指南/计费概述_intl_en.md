This document lists the billing details of Lighthouse instances, including **[basic bundle](#basis)**, **[out-of-plan data transfer](#additional)**, **[custom image](#customizeOS)**, and **[cloud disk](#cbs)**.


## [Basic Bundle](id:basis)
Lighthouse is sold as instance bundles at favorable prices, which contain Tencent Cloud server resources such as CPU, memory, SSD cloud disk, and network data transfer plan. If the resources in a bundle cannot meet your requirements, you can apply for additional resources by purchasing out-of-plan data transfer.



### Billing Mode
The basic bundle currently is available only through monthly subscription. Monthly subscription is a prepaid billing mode, where you need to pay the fees for one or multiple months or even years in advance. The billing cycle is a natural month. For example,
If you purchased a Lighthouse instance at 00:00:00 on May 1, 2021 for 1 month, the monthly subscription billing cycle would be from 00:00:00 on May 1 to 23:59:59 on May 31.
If you purchased a Lighthouse instance at 00:00:00 on February 28, 2022 for 2 months, the monthly subscription duration would be from 00:00:00 on February 28 to 23:59:59 on April 30. The first billing cycle will end at 00:00:00 on March 31. The instance will expire at 23:59:59 on April 30.


### Service Suspension Due to Overdue Payments
An instance will enter the **pending released** status upon expiration and can be recovered if you renew it within 7 days.
If the "pending released" instance is not renewed, it will be released, and the data in the instance will be cleared and cannot be recovered. For details, see [Overdue Payments and Service Suspension](https://intl.cloud.tencent.com/document/product/1103/41405). Please note the instance status for renewing the instance or transferring data in time.

### Data transfer plan
The Lighthouse bundles are offered in the form of data transfer plans, which counts only the instance outbound data transfer. The data transfer plan will be reset every natural month from the time of instance purchase, and the reset time is consistent with that of the instance billing cycle. If your instance data transfer in the current month
 - **Does not exceed the limit**: The remaining data transfer of the current month will not be refunded.
 - **Exceeded the limit**: The excessive data transfer is billed by usage. For data transfer pricing, see [Out-of-plan Data Transfer Pricing](#additional).



### [Basic Bundle Pricing](id:basisPriceDetail)
For information on the basic bundle price and discounts, see [Basic Bundle Pricing](https://intl.cloud.tencent.com/document/product/1103/47794).



## [Out-of-plan Data Transfer](id:additional)
The out-of-plan data transfer is billed by the outbound data, i.e., total volume of data transferred over the public network in GB.

### Billing Mode
The data exceeded the monthly data transfer limit is billed at **out-of-plan data transfer price** and settled by hour.

### Service Suspension Due to Overdue Payments
When your account has overdue payments, all instances that exceed the monthly data transfer limit will transfer data and be deducted normally within 2 hours, but after that, they will be suspended. To make them available again, please top up your account until the balance is positive, or wait until the data transfer is reset on a monthly basis. Overdue payments will not affect the instances that do not exceed the monthly data transfer limit.


### [Out-of-plan Data Transfer Pricing](id:OverRatedPrice)
For more information, see [Out-of-plan Data Transfer Pricing](https://intl.cloud.tencent.com/document/product/1103/47794).


## [Custom Image Pricing](id:customizeOS)

### Billing Mode
The billing involves the **custom images that exceeded the free tier** in the region and is settled by hour. When deleting custom images, the part of the usage time less than one hour will be settled by one hour.

<dx-alert infotype="notice" title="">
A free tire of five custom images is provided in each region.
</dx-alert>


### Pricing information
The unit price of excessive custom images is 0.0015 USD/hour.

### Overdue Payment
If your account has overdue payments:
- The custom image feature will be disabled, and you cannot create more custom images.
- Existing custom images under the account (including images within the free tier) will be isolated and unavailable and enter the "pending released" status. **The unreleased images that exceed the free tier will continue to be billed** until them are deleted. If you do not top up your account to make the balance positive after the custom images are "pending released" for 7 days, the custom images will be automatically deleted.

### Related Operations
You can create the custom images in the Lighthouse console. For more information, see [Working with Custom Images](https://intl.cloud.tencent.com/document/product/1103/41395).

## [Cloud Disk Pricing](id:cbs)

### Billing Mode

The cloud disk currently is available only through monthly subscription. Monthly subscription is a prepaid billing mode, where you need to pay the fees for one or multiple months or even years in advance.


### Pricing information
For more information on cloud disk pricing and discounts, see [Cloud Disk Pricing](https://intl.cloud.tencent.com/document/product/1103/47794).


### Overdue Payment

A cloud disk will enter the **pending released** status upon expiration and can be recovered if you renew it within seven days.
If you do not renew the cloud disk within seven days, it will be released, and the data in it will be cleared and cannot be recovered. Please note the cloud disk status to renew the disk or transfer data in time.

### Refund Policy

Cloud disks support 5-day free returns and standard returns. For more information, see [Refund](https://intl.cloud.tencent.com/document/product/1103/41406).

### Related Operations

You can create, attach and terminate cloud disks in the Lighthouse console. For more information, see [Working with Cloud Disks](https://intl.cloud.tencent.com/document/product/1103/46567).
