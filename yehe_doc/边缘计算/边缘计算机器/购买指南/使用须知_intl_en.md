Read the following use instructions before purchasing and using ECM.

## Edge Node Network

- The average packet loss rate measured by ping between a single edge node and a monitoring node in the same or neighboring province with the same ISP is less than or equal to 1%.
- ISP networks have the risks of interruption or jitter due to exceptions, which is monitored and reported to CM in real time by ECM 24/7. By configuring CM, you can sync the alarm information and stay up to date with the real-time node network status.

## Edge Node Resource

- Edge nodes use local disks for storage, which may vary by node.
- A local disk is on a single host, and its data reliability is subject to the reliability of the host, so risks of single points of failures and data loss may exist. If you have high requirements for data reliability, we recommend you implement data redundancy at the application layer for guarantee.

## Edge Node SLA

- The service availability (SLA) of ECM is no less than 99.9%.  
The duration of service unavailability resulting from any of the following shall not be included in the calculation of service unavailability or indemnity:
Exceptions of networks and devices that don't belong to Tencent Cloud, exceptions caused by system maintenance and upgrade that Tencent Cloud informs the customer of in advance, exceptions caused by the customer, and unavailability caused by force majeure events. 
- The local disk and instance reliability is subject to the reliability of the host. If a single point of failure occurs or a single edge node cannot be connected, ECM will help the instance reconnect as soon as possible but will not guarantee data reliability.

## Notes on Billing 

ECM has two billable items: computing storage and network bandwidth.
- The computing storage service is billed and settled daily by the daily peak usage.
>! The daily peak usage is the maximum usage of resources such as CPU, memory, and storage from 00:00 to 24:00 on a day. Resources you add before midnight every day will be included in the calculation of the daily peak resource usage and increase the total daily fees.
> For example, if you create a resource or create and immediately terminate a resource at 23:59:58, both operations will increase the daily fees.
> **You should pay attention to the time point when you create a resource to avoid losses caused by creating resources too late on a day or maloperations.**
> 
- The network bandwidth service is billed monthly by the 95th percentile of the monthly peak bandwidth counted by the ISP on each edge node.

For more information on billing, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1119/43404).

