
<!--Before reading this document, you need to learn about Tencent Cloud CVM's [Overview of Billing Methods for Public Network]().
This document describes the billing methods in shared network. For more information on the billing methods in exclusive network, please see [Billing of Exclusive Public Network]().-->

The bandwidth of shared network is calculated based on the total traffic curve of multiple CVMs under the same account and user is billed by the total bandwidth.

This billing method saves the public network cost by staggering the use of public network bandwidth for multiple CVMs during peak hours. If CVM A and CVM B reach their peak bandwidth of 100 Mbps at 12:00 and 13:00 respectively, the total peak bandwidth is also 100 Mbps, which is used as the basis for billing.

Tencent Cloud offers a shared network service: bandwidth package.

>**Note:**
>You can apply to activate the shared network by submitting a ticket.


### Billing by bandwidth package
Bandwidth package is a monthly billing method for shared network. After bandwidth package is activated, user will be billed by its account CVM's shared bandwidth's **monthly peak**.

#### Billing standard
After a ticket is submitted and shared network is activated, CVMs and LBs under your account will be billed automatically by shared bandwidth. You do not need to adjust configurations.

| Region | Price of Bandwidth in Bandwidth Package |
|---------|---------|
| Beijing, Shanghai, Guangzhou, Hong Kong, Singapore & Silicon Valley | 16.97 USD/Mbps |
| Toronto | 16.97 USD/Mbps |

When we calculate your bills, (at the end of a calendar month or when users cancel the package),  "average daily bandwidth peak" will be calculated as follows:
1. Calculate the daily bandwidth peak
You can check the value in the console by entering the **Cloud Monitor** tab and the **Traffic Monitoring** page. By default,  bandwidth peak value is captured every 5 minutes so a total of 288 values are collected each day. The top four values are taken out and the fifth largest value is recorded as the daily bandwidth peak.
2. Calculate the average daily bandwidth peak
The average daily bandwidth peak is the average of the bandwidth peaks for the top 5 days ranked by daily bandwidth peak for the usage period of the bandwidth package.
3. Calculate the bandwidth package charge
	- If the bandwidth package is used for not less than 30 days, the charge=Average daily bandwidth peak * Unit price.
	- If the bandwidth package is used for less than 30 days, the charge for the bandwidth package in Step 3 is calculated based on the average daily bandwidth peak calculated in Step 2. Actual charge=Bandwidth package charge * Actual number of usage days/number of days of the month.



#### Purchase procedure
To apply for activating this billing method, please submit a [ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=7&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%20CVM).

#### Billing description
- If project-based billing is enabled, the system calculates the total charge for bandwidth package as described above and the average daily bandwidth peak individually for each project (as described in Step 2), and then calculates the charge payable for each project based on the proportions.
- For the bandwidth package purchased under an ordinary account, the bandwidth fee of the CVM originally prepaid by bandwidth will be returned to the complimentary account according to the number of usage days remaining.

#### Example
Assume that a user activates a bandwidth package on March 1. The package takes effect on the day of purchase. If the actual average daily bandwidth peak for March is 120 Mbps, then charge=120*108=12,960 CNY.



