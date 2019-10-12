SCF is billed by usage on a monthly postpaid basis. The bill for the current month is issued on the 3rd to 5th day of the next month and is settled in USD.

The monthly bill of SCF consists of three parts, with each calculated in a specific method based on the collected data. The calculated amount is in USD and retains two decimal places.

* Fee for resource usage 
* Fee for calls
* Fee for public network outbound traffic

## Fee for Resource Usage

Fee for resource usage = (Resource usage - Free resource quota) X Resource unit price

### Resource unit price

Resource unit price: 0.00001666 USD/GBs

### Resource usage (GBs)

Resource usage = Memory configured for SCF X Billable runtime

Memory configured for SCF is calculated in GB, and the billable runtime is calculated in seconds (converted from milliseconds). Therefore, resource usage is calculated in **GBs** (GB-second).

For example, if SCF is configured with a memory of 256 MB and runs for 1760 ms (calculated by 1800 ms), the resources used in this single run are (256/1024) X (1800/1000) = 0.45 GBs.

Resources used in each run are calculated and aggregated on a monthly basis.

## Invocations

Fee for Invocations = (Total number of Invocations - Free Invocations quota) X Invocations unit price

SCF counts an invocation each time it starts executing in response to a client request. The invocations are aggregated on a monthly basis and charged by a granularity of **1 million invocations**.

### Invocations unit price

Invocations unit price: 0.2 USD/million calls


## Fee for Public Network Outbound Traffic

**Fee for public network outbound traffic** = **Public network outbound traffic** X **Traffic unit price**

When you access public network resources from SCF, such as uploading a file to an external storage, outbound traffic is generated.

For public network outbound traffic, you are also [charged by the actual traffic usage](https://intl.cloud.tencent.com/document/product/213/10578#.E6.8C.89.E4.BD.BF.E7.94.A8.E6.B5.81.E9.87.8F.E8.AE.A1.E8.B4.B9).

### Unit price for public network outbound traffic

The public network outbound traffic has different prices for different regions. For details, see the "Bill-by-traffic" section in [Public Network Billing Methods](https://intl.cloud.tencent.com/document/product/213/10578).


## Fees for Other Products

If other products (such as CMQ, API gateway, and COS) are also used in addition to SCF, these products are billed according to their own billing rules.

