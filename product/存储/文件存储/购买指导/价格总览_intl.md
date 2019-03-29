## Billing Method
CFS (Cloud File Storage) charges you for storage you actually used. There is no minimum amount you have to pay, nor cost of traffic or request. Storage is calculated by the maximum storage amount used every hour, and the charge cycle is on a hourly basis.

## Storage Space
The file system by default takes 3 KB of storage when it is created, and the 3KB will be counted as part of your used storage.

## Supported Regions
CFS is available in the following regions:

Region | Availability Zone | Notes
------- | ------- | :------
Beijing | Beijing Zone 1 | Out of stock. You are recommended to create a subnet within your VPC for Beijing Zone 2 or Beijing Zone 3 to access the CFS file system in either zone. [See mounting help>>](https://intl.cloud.tencent.com/document/product/582/9551#how-can-i-continue-using-cfs-in-an-availability-zone-with-the-cfs-resources-sold-out.3F) 
| Beijing Zone 2 | Available 
| Beijing Zone 3 | Available
Shanghai | Shanghai Zone 2 | Out of stock. You are recommended to create a subnet within your VPC for Shanghai Zone 3 to access the CFS file system in the zone. [See mounting help>>](https://intl.cloud.tencent.com/document/product/582/9551#how-can-i-continue-using-cfs-in-an-availability-zone-with-the-cfs-resources-sold-out.3F)
| Shanghai Zone 3 | Available 
Guangzhou | Guangzhou Zone 2 | Out of stock.
| Guangzhou Zone 3 | Available
| Guangzhou Zone 4 | Available
Hong Kong | Hong Kong Zone 1 | Out of stock.


## Pricing Details
See below for CFS product pricing. NFS and CIFS/SMB file systems have the same price.

Billing Method/Region | Mainland China |
------- | ------- | 
Price | 0.058 USD/GB/Month (0.00008056 USD/GB/hr) |


## Billing Example
An organization has 20 Cloud Virtual Machine (CVM) to access two file systems in Mainland China. The file system A is used for cold data storage, with a maximum storage of 500 GB. The file system B is used as enterprise cloud storage, with a peak storage of 105.6 GB in the current hour. 

The total cost of CFS for this hour = (500+105.6)*0.00008056 = 0.05 USD



