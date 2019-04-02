## Billing Method
CFS (Cloud File Storage) charges you for storage you actually used. There is no minimum amount you have to pay, nor cost of traffic or request. Storage is calculated by the maximum storage amount used every hour, and the charge cycle is on a hourly basis.

## Storage Space
The file system by default takes 3 KB of storage when it is created, and the 3KB will be counted as part of your used storage.

## Supported Regions
CFS is available in the following regions:

<table>
    <tr>
        <th>Region</th>
        <th>Availability Zone</th>
    </tr>
    <tr>
        <td rowspan="3">Beijing </td>
        <td>Beijing Zone 1</td>
    </tr>
    <tr>
        <td>Beijing Zone 2</td>
    </tr>
    <tr>
        <td>Beijing Zone 3</td>
    </tr>
    <tr>
        <td rowspan="2">Shanghai</td>
        <td>Shanghai Zone 2</td>
    </tr>
    <tr>
        <td>Shanghai Zone 3</td>
    </tr>
    <tr>
        <td rowspan="3">Guangzhou</td>
        <td>Guangzhou Zone 1</td>
    </tr>
    <tr>
        <td>Guangzhou Zone 2</td>
    </tr>
    <tr>
        <td>Guangzhou Zone 3</td>
    </tr>
    <tr>
        <td>HongKong </td>
        <td>HongKong Zone 1</td>
    </tr>
</table>


## Pricing Details
See below for CFS product pricing. NFS and CIFS/SMB file systems have the same price.

Billing Method/Region | Mainland China |
------- | ------- | 
Price | 0.058 USD/GB/Month (0.00008056 USD/GB/hr) |


## Billing Example
An organization has 20 Cloud Virtual Machine (CVM) to access two file systems in Mainland China. The file system A is used for cold data storage, with a maximum storage of 500 GB. The file system B is used as enterprise cloud storage, with a peak storage of 105.6 GB in the current hour. 

The total cost of CFS for this hour = (500+105.6)*0.00008056 = 0.05 USD



