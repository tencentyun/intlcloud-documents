## Billing

Users can estimate the usage by themselves and calculate the specific purchase price via [SCF Price Calculator](https://buy.cloud.tencent.com/price/scf/calculator). For the introduction to SCF Billing details, please see [Billing Methods](https://cloud.tencent.com/document/product/583/12284), [Product Pricing](https://cloud.tencent.com/document/product/583/12281) and [Instruction of Arrearage](https://cloud.tencent.com/document/product/583/12283). 

SCF is billed on an hourly basis in **Yuan**. The SCF bill consists of the following three parts, with each calculated in a specific method based on the collected data. The calculated amount is in **Yuan**.
* Resource usage fee 
* Fee for number of invocations
* Fee for public network outbound traffic
> For unit prices of resource usage, number of innovations and public network outbound traffic, please see [Product Pricing](https://cloud.tencent.com/document/product/583/12281). Among them, public network outbound traffic is calculated in GB. For more details, please see Traffic-based Billing of [Broadband Network Billing](https://buy.cloud.tencent.com/price/idc).

## Resource Usage Fee

### Resource Unit Price
**Resource usage fee = (Resource usage - Free resource quota) X Resource unit price**

**Resource unit price: 0.0000167 USD/GBs**

## Resource Usage (GBs)

**Resource usage = Memory configured for the function X Running duration**

Memory configured for the function is calculated in GB, and charged duration is calculated in seconds (converted from milliseconds). So resource usage is calculated in **GBs** (GB-second).

For example, if a function is configured with a memory of 256 MB and runs for 1760 ms (billed by 1760 ms), the resources used in this single run are (256/1024) X (1760/1000) = 0.44 GBs.

Resources used in each run are calculated on an hourly basis.

>- Current resource usage of SCF is billed as memory configured for the function* actual running duration. Compared with the billing method of 100ms CDN(Cloud Front), it will consume less resources and cause lower cost. Please see [Example of Fees](https://cloud.tencent.com/document/product/583/12285) for more details.
>- Due to the uncertainty of the computing resources when the cloud function is running, and the specific behavior inside the code, as well as the impact of network communications, the running time of the same function code when triggered will change slightly.

## Fee for Number of Calls

**Fee for number of invocations = (Total number of invocations - Free invocation quota) X Invocation unit price**

Every time the function is triggered and executed, it is counted as one invocation. Sum up the total invocations on an hourly basis, and calculate the fee by a granularity of **10K invocations**.

## Fee for Public Network Outbound Traffic

**Fee for public network outbound traffic = Public network outbound traffic X Traffic unit price**

When you access public network resources from SCF, such as uploading a file to an external storage, outbound traffic is generated.

## Fees for Other Products

If other products (such as CMQ, API gateway, and COS) are also used in addition to SCF, these products are billed according to their own billing rules.
