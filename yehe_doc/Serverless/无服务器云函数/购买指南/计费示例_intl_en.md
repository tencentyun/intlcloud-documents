## Calculation Method
Currently, SCF resource usage is calculated by multiplying the memory configured for function by the **actually triggered execution duration** of function. Compared with the original billing mode of rounding up to the nearest 100-ms, this billing mode calculates less overall resource usage and fees, helping save your budget.



### Web and API services
For web services or API requests, the actual execution duration of code is usually only 30–50 ms. Billing by actual execution duration can lower the fees by up to 70%.

**Example**: user A uses an API service composed of SCF and API Gateway by configuring a function with 128 MB memory and an average execution duration of 37 ms. In the original billing mode, the billable duration of the function is 100 ms, and if the function is invoked 1 million times per day, a resource usage of 12,500 GB-s would be generated. In contrast, in the billing mode based on the actual execution duration, only 4,625 GB-s will be generated, which is a 63% reduction.

### Message processing

For message filtering, converting, and forwarding in message queue services, the actual execution duration of code is usually only 60–80 ms. Billing by actual execution duration can lower the fees by up to 40%.

**Example**: user B uses CKafka to trigger SCF and deliver filtered and converted messages to CKafka by configuring a function with 256 MB memory and an average execution duration of 67 ms. In the original billing mode, if the function is invoked 5 million times per day, a resource usage of 125,000 GB-s would be generated. In contrast, in the billing mode based on the actual execution duration, only 83,750 GB-s will be generated, which is a 37% reduction.


### Event forwarding

For forwarding COS events to downstream systems, the actual execution duration of code is usually only 50–80 ms. Billing by actual execution duration can lower the fees by up to 50%.

**Example**: user C uses SCF to forward file upload events of COS to their own file processing system by configuring a function with 128 MB memory and an average execution duration of 43 ms. In the original billing mode, if there are 200,000 files uploaded per day, a resource usage of 2,500 GB-s would be generated. In contrast, in the billing mode based on the actual execution duration, only 1,075 GB-s will be generated, which is a 57% reduction.



## Billing Example
### Web and API services
Suppose a function with 128 MB memory is configured with an API Gateway trigger. It is triggered by 100,000 URL requests per day, and its average execution duration per request is 70 ms.

**The daily resource usage and number of invocations are as follows:**
- Number of invocations per day: 100,000
- Resource usage per day: (128 / 1024) * (70 / 1000) * 100000 = 875 GB-s


**The monthly fees (for 30 days) are as follows:**
- Monthly resource usage fees: 875 * 30 = 26250 GB-s, which is less than 400,000 GB-s and does not incur fees
- Monthly invocation fees: (100000 * 30 / 10000 - 100) * 0.002 = 0.4 USD

In this case, the total fees are invocation fees of 0.4 USD.

### Message queue trigger

Suppose a function with 128 MB memory is configured with a CKafka trigger. It is triggered 3 times per second to process messages and then put them in CKafka, and its execution duration per message is 260 ms.

**The daily resource usage and number of invocations are as follows:**
- Resource usage per day: (128 / 1024) * (260 / 1000) * 3 * 3600 * 24 = 8424 GB-s
- Number of invocations per day: 3 * 3600 * 24 = 259200

**The monthly fees (for 30 days) are as follows:**
- Monthly resource usage fees: 8424 * 30 = 252720 GB-s, which is less than 400,000 GB-s and does not incur fees
- Monthly invocation fees: (259200 * 30 / 10000 - 100) * 0.002 = 1.36 USD

In this case, the total fees are invocation fees of 1.36 USD.


### External file upload

Suppose a function with 256 MB memory is invoked 50 times per second through TencentCloud API. It generates a 1 KB file each time and uploads the file to an external site, and its execution time per generated and uploaded file is 780 ms.

**The daily resource usage and number of invocations are as follows:**
- Resource usage per day: (256 / 1024) * (780 / 1000) * 50 * 60 * 24 = 14040 GB-s
- Number of invocations per day: 50 * 60 * 24 = 72000
- Traffic per day: 1 * 50 * 60 * 24 = 72000 KB = 70.31 MB

**The monthly fees (for 30 days) are as follows:**
- Monthly resource usage fees: (14040 * 30 - 400000) * 0.0000167 = 0.35 USD
- Monthly invocation fees: (72000 * 30 / 10000 - 100) * 0.002 = 0.23 USD
- Public network outbound traffic fees: (70.31 * 30 / 1024) * 0.12  = 0.25 USD

In this case, the total fees are resource usage fees of 0.35 USD + invocation fees of 0.23 USD + public network outbound traffic fees of 0.25 USD = 0.83 USD