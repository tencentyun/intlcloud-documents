SCF is billed by usage on a hourly basis in USD.

The SCF bill consists of the following three parts, with each calculated in a specific method based on the collected data. The calculated amount is in **USD**.

* Resource usage fee 
* Fee for number of invocations
* Fee for public network outbound traffic

## Resource Usage Fee

**Resource usage fee** = (**Resource usage** - **Free resource quota**) X **Resource unit price**

### Resource Unit Price

**Resource unit price**: 0.00001666 USD/GBs

### Resource Usage (GBs)

**Resource usage = Memory configured for the function X Charged running duration**

Memory configured for the function is calculated in GB, and charged duration is calculated in seconds (converted from milliseconds). So resource usage is calculated in **GBs** (GB-second).
For example, if a function is configured with a memory of 256 MB and runs for 1760 ms (billed by 1800 ms), the resources used in this single run are (256/1024) X (1800/1000) = 0.45 GBs.

Resources used in each run are calculated on an hourly basis.

## Fee for Number of Calls

**Fee for number of invocations** = (**Total number of invocations** - **Free invocation quota**) X **Invocation unit price**

Every time the function is triggered and execute, it is counted as one invocation. Sum up the total invocations on an hourly basis, and calculate the fee by a granularity of **1 million invocations**.



**Invocation unit price**: 0.2 USD/million invocations


## Fee for Public Network Outbound Traffic

**Fee for public network outbound traffic** = **Public network outbound traffic** X **Traffic unit price**

When you access public network resources from SCF, such as uploading a file to an external storage, outbound traffic is generated.

The public network outbound traffic has different prices for different regions. For details, see the "Bill-by-traffic" section in [Public Network Billing Methods](https://intl.cloud.tencent.com/document/product/213/10578).


## Fees for Other Products

If other products (such as CMQ, API gateway, and COS) are also used in addition to SCF, these products are billed according to their own billing rules.
