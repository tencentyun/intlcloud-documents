Lighthouse is billed for the following three parts: **[basic package](#basis)**, **[excessive traffic](#additional)**, and **[custom image](#customizeOS)**.


## [Basic Package Overview](id:basis)
Lighthouse is sold as instance packages at favorable prices, which contain Tencent Cloud server resources such as CPU, memory, SSD cloud disk, and network traffic package. If the resources in a package cannot meet your requirements, you can apply for additional resources by purchasing excessive traffic.



### Billing mode
The basic package currently is available only through monthly subscription. Monthly subscription is a prepaid billing mode, where you need to pay the fees for one or multiple months or even years in advance. Here, the duration of monthly subscription is calculated by calendar month. For example: 
If you purchased Lighthouse at 00:00 on February 10, 2020 for 1 month, the monthly subscription duration would be 00:00:00 on February 10–23:59:59 on March 10. 
If you purchased Lighthouse at 00:00 on May 1, 2020 for 1 month, the monthly subscription duration would be 00:00:00 on May 1–23:59:59 on May 31.

### Overdue payments and service suspension
An instance will enter the **to be repossessed** status upon expiration and can be recovered if you renew it within seven days. 
If you don't renew an instance when it is in the **to be repossessed** status period, it will be released, and its data will be cleared and cannot be recovered. For more information, please see [Repossession Mechanism](https://intl.cloud.tencent.com/document/product/1103/41405). Please pay attention to the instance status and renew or transfer data promptly.

### Traffic package
Lighthouse packages are offered in the form of traffic package, which counts only the instance outbound traffic billed in the following way:
 - **If the monthly used traffic is within the limit of the monthly traffic package**, the traffic package will be reset monthly starting from the purchase time.
 - **If the monthly used traffic exceeds the monthly traffic package limit**, the excessive traffic will be billed by usage. 


## [Basic Package Pricing](id:basisPrice)
>? 
>- **Linux instance package**: uses a Linux system image or an application image based on Linux.
>- **Windows instance package**: uses a Windows Server system image or an ASP.NET application image.
>- Deactivated packages are no longer purchasable. We recommend you upgrade such instance packages. For more information, please see [Upgrading Instance Package](https://intl.cloud.tencent.com/document/product/1103/41407).
>

### Hong Kong/Singapore/Tokyo/Silicon Valley/Frankfurt/Mumbai

<dx-tabs>
::: Linux\sinstance\spackages
<table>
<thead>
<tr>
<th>CPU (Cores)</th><th>Memory (GB)</th><th>System Disk - SSD (GB)</th><th>Peak Bandwidth (Mbps)</th>
<th>Monthly Traffic Package (GB)</th><th>Price (USD/Month)</th>
</tr>
</thead>
<tbody>
<tr>
<tr>
<tr>
<td>2</td><td>2</td><td>30</td><td>30</td><td>1,024</td><td><strong>5.0</strong></td>
</tr>
<tr>
<td>2</td><td>2</td><td>50</td><td>30</td><td>2,048</td><td><strong>7.0</strong></td>
</tr>
<td>2</td><td>4</td><td>60</td><td>30</td><td>2,560</td><td><strong>9.0</strong></td>
</tr>
<tr>
<td>2</td><td>4</td><td>80</td><td>30</td><td>3,072</td><td><strong>11.0</strong></td>
</tr>
<tr>
<td>2</td><td>8</td><td>90</td><td>30</td><td>3,584</td><td><strong>16.0</strong></td>
</tr>
<tr>
<td>2</td><td>8</td><td>100</td><td>30</td><td>4,096</td><td><strong>22.0</strong></td>
</tr>
</tbody></table>

:::
::: Windows\s instance packages
<table>
<thead>
<tr>
<th>CPU (Cores)</th><th>Memory (GB)</th><th>System Disk - SSD (GB)</th><th>Peak Bandwidth (Mbps)</th>
<th>Monthly Traffic Package (GB)</th><th>Price (USD/Month)</th>
</tr>
</thead>
<tbody><tr>
<td>2</td><td>2</td><td>50</td><td>30</td><td>1,024</td><td><strong>8.5</strong></td>
</tr>
<tr>
<td>2</td><td>2</td><td>60</td><td>30</td><td>2,048</td><td><strong>11.0</strong></td>
</tr>
<td>2</td><td>4</td><td>70</td><td>30</td><td>2,560</td><td><strong>15.0</strong></td>
</tr>
<tr>
<td>2</td><td>4</td><td>80</td><td>30</td><td>3,072</td><td><strong>20.0</strong></td>
</tr>
<tr>
<td>2</td><td>8</td><td>90</td><td>30</td><td>3,584</td><td><strong>30.0</strong></td>
</tr>
<tr>
<td>2</td><td>8</td><td>100</td><td>30</td><td>4,096</td><td><strong>40.0</strong></td>
</tr>
</tbody></table>
:::
</dx-tabs>

## [Excessive Traffic Overview](id:additional)
If the actually used traffic exceeds the monthly traffic package limit of the basic package, Lighthouse will be billed by the outbound traffic, that is, it will be billed by the total amount of data (in GB) transferred over the public network.

### Billing mode
Excessive traffic is billed hourly at the excessive traffic price.

### Overdue payments
If your account has overdue payments, all instances generating excessive traffic will be suspended, while instances with traffic below the monthly traffic package limit will not be affected. If you want to recover suspended instances, please top up your account to a positive balance or use them after the monthly traffic package is reset.


## [Excessive Traffic Pricing](id:OverRatedPrice)
| Region | Price (USD/GB) |
|---------|---------|
| Tokyo | 0.13 |
|Hong Kong (China) | 	0.12 |
| Silicon Valley	\Frankfurt | 	0.5 |
| Mumbai | 	0.1 |
| Singapore | 	0.081 |

## [Custom Image Billing Overview](id:customizeOS)
### Billing mode
The **number of custom images exceeding the free tier** is billed hourly by region (usage duration shorter than one hour will be calculated as one hour).
>! Each region offers a free tier of five custom images.


### Pricing information
The unit price of excessive custom images is 0.0015 USD/hour.

### Overdue payments
If your account has overdue payments:
- The custom image feature will be disabled, and you cannot create more custom images.
- All custom images (including those within the free tier) under your account will enter the **to be repossessed** status. If you don't top up your account within seven (included) days, the custom images will be automatically released.

### Relevant operations
You can go to the Lighthouse console to create a custom image. 
