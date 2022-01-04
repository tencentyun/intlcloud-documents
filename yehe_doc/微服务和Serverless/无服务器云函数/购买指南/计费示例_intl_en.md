## Calculation Method
Currently, SCF resource usage is calculated by multiplying the memory configured for function by the **actually triggered execution duration** of function. Compared with the original billing mode of rounding up to the nearest 100-ms, this billing mode calculates less overall resource usage and fees, helping save your budget.



### Web and API services
For web services or API requests, the actual execution duration of the code is usually only 30–50 ms. Billing by actual execution duration can lower fees by up to 70%.

**Example**: user A uses an API service composed of SCF and API Gateway by configuring a function with 128 MB memory and an average execution duration of 37 ms. In the original billing mode, the billable duration of the function is 100 ms, and if the function is invoked 1 million times per day, a resource usage of 12,500 GBs would be generated. In contrast, in the billing mode based on the actual execution duration, only 4,625 GBs will be generated, which is a 63% reduction.







### Message processing

For message filtering, converting, and forwarding in message queue services, the actual execution duration of the code is usually only 60–80 ms. Billing by actual execution duration can lower fees by up to 40%.

**Example**: user B uses CKafka to trigger SCF and deliver filtered and converted messages to CKafka by configuring a function with 256 MB memory and an average execution duration of 67 ms. In the original billing mode, if the function is invoked 5 million times per day, a resource usage of 125,000 GBs would be generated. In contrast, in the billing mode based on the actual execution duration, only 83,750 GBs will be generated, which is a 37% reduction.


### Event forwarding

For forwarding COS events to downstream systems, the actual execution duration of the code is usually only 50–80 ms. Billing by actual execution duration can lower fees by up to 50%.

**Example**: user C uses SCF to forward file upload events of COS to their own file processing system by configuring a function with 128 MB memory and an average execution duration of 43 ms. In the original billing mode, if there are 200,000 files uploaded per day, a resource usage of 2,500 GBs would be generated. In contrast, in the billing mode based on the actual execution duration, only 1,075 GBs will be generated, which is a 57% reduction.



## Billing Example
### Web and API services
Suppose a function with 128 MB memory is configured with an API Gateway trigger. It is triggered by 100,000 URL requests per day, and its average execution duration per request is 70 ms.

**Suppose the resource usage and number of invocations per day are as follows:**
- Number of invocations per day: 100,000
- Resource usage per day: (128 / 1024) * (70 / 1000) * 100000 = 875 GBs


**The monthly fees (for 30 days) are as follows:**
- Monthly resource usage fees: 875 * 30 = 26,250 GBs, which is less than 400,000 GBs and does not incur fees
- Monthly invocation fees: (100000 * 30 / 10000 - 100) * 0.002 = 0.4 USD

In this case, the total fees are the invocation fees of 0.4 USD.

### Message queue trigger

Suppose a function with 128 MB memory is configured with a CKafka trigger. It is triggered 3 times per second to process messages and then put them in CKafka, and its execution duration per message is 260 ms.

**Suppose the resource usage and number of invocations per day are as follows:**
- Resource usage per day: (128 / 1024) * (260 / 1000) * 3 * 3600 * 24 = 8,424 GBs
- Number of invocations per day: 3 * 3600 * 24 = 259,200

**The monthly fees (for 30 days) are as follows:**
- Monthly resource usage fees: 8424 * 30 = 252,720 GBs, which is less than 400,000 GBs and does not incur fees
- Monthly invocation fees: (259200 * 30 / 10000 - 100) * 0.002 = 1.36 USD

In this case, the total fees are the invocation fees of 1.36 USD.


### External file upload

Suppose a function with 256 MB memory is invoked 50 times per minute through the TencentCloud API. It generates a 1 KB file each time and uploads the file to an external site, and its execution duration per generated and uploaded file is 780 ms.

**Suppose the resource usage and number of invocations per day are as follows:**
- Resource usage per day: (256 / 1024) * (780 / 1000) * 50 * 60 * 24 = 14,040 GBs
- Number of invocations per day: 50 * 60 * 24 = 72,000
- Traffic per day: 1 * 50 * 60 * 24 = 72000 KB = 70.31 MB

**The monthly fees (for 30 days) are as follows:**
- Monthly resource usage fees: (14040 * 30 - 400000) * 0.0000167 = 0.35 USD
- Monthly invocation fees: (72000 * 30 / 10000 - 100) * 0.002 = 0.23 USD
- Public network outbound traffic fees: (70.31 * 30 / 1024) * 0.12 = 0.25 USD

In this case, the total fees are the resource usage fees of 0.35 USD + invocation fees of 0.23 USD + public network outbound traffic fees of 0.25 USD = 0.83 USD.


### Idle provisioned concurrency fees

The idle provisioned concurrency fees are independent of the other three billable items. After provisioned concurrency is configured, small idle fees will be charged only for the instances that have been configured and started but are not in use. This section describes how such fees are calculated with an example where the concurrency fluctuates sharply and the provisioned concurrency quota is adjusted.


**Example 1:** if a function version with 128 MB memory has a provisioned concurrency quota of 12,800 MB (10 instances), is invoked 50 times per second on average, generates a 1 KB file during each invocation, uploads the file to a self-built external site, and has 8 concurrent instances in 10 seconds, then:

- Number of idle instances = max(10 - 8, 0) = 2
- Configured memory size = 128MB
- Idle duration = 10s
- Idle provisioned concurrency price = 0.00000847 USD/GBs

**Idle provisioned concurrency fees** = 2 * 128 / 1024 GB * 10s * 0.00000847 USD/GBs = 0.000021175 USD

**Prices of resource usage and invocations:**

- Resource usage = 0.00011108 USD/GBs
- Invocations = 0.0133 USD/10000 invocations
- Public network outbound traffic = 0.12 USD/GB

**Pay-as-You-Go fees:**

- Resource usage: (128 * 8 / 1024) * 10 * 50 = 500 GBs, which is less than 20,000 GBs and does not incur fees
- Invocations: 50 * 10  = 500 invocations, which is less than 100,000 invocations (50,000 for event-triggered functions and 50,000 for HTTP-triggered functions) and does not incur fees
- Traffic: 1 * 50 * 10= 500 KB, which is less than 0.5 GB and does not incur fees

In this case, the **pay-as-you-go fees** are 0.

**Total fees** = pay-as-you-go fees + idle provisioned concurrency fees = 0 + 0.000021175 USD = 0.000021175 USD

**Example 2:** suppose function A is configured with 256 MB memory, is invoked 50 times per minute on average, generates a 1 KB file during each invocation, uploads the file to a self-built external site, and is configured with 100 provisioned instances at 18:01, and the number of provisioned instances is increased to 120 at 18:07 due to business surge and then is lowered to 80 at 18:10. **Taking the minute of 18:01 as an example**, this minute has 100 provisioned instances, and the number of actually running concurrent instances is 30, then:

- **Number of idle instances** = 100 - 30 = 70
- **Idle resources** = number of idle instances * configured memory size * idle duration = 70 * 256 MB * 60s = 70 * (256 / 1024) GB * 60s = 1,050 GBs
**Idle provisioned concurrency fees** = idle resources * idle provisioned concurrency price = 11050 GBs * 0.00000847 USD/GBs = 0.009 USD

**Pay-as-You-Go fees:**

- Resource usage: (256 * 8 / 1024) * 60 * 50 = 3000 GBs, which is less than 20,000 GBs and does not incur fees
- Invocations: 50 * 60  = 3000 invocations, which is less than 100,000 invocations (50,000 for event-triggered functions and 50,000 for HTTP-triggered functions) and does not incur fees
- Traffic: 1 * 50 * 60= 3000 KB, which is less than 0.5 GB and does not incur fees

In this case, the **pay-as-you-go fees** are 0.

**Total fees** = pay-as-you-go fees + idle provisioned concurrency fees = 0 + 0.009 USD = 0.009 USD

In the same calculation method as shown in the above example, the detailed billing for the 10 minutes of function A can be calculated, the accumulated idle fees for the 10 minutes are 0.009 USD, and the total fees are 0.009 USD as shown below:

| Billable Item         | 18:01 | 18:02 | 18:03 | 18:04 | 18:05 | 18:06 | 18:07 | 18:08 | 18:09 | 18:10 | Total  |
| :------------- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| Configured provisioned concurrency | 100   | 100   | 100   | 100   | 100   | 100   | 120   | 120   | 120   | 80    |    -  |
| Number of concurrent instances for this version   | 30    | 66    | 88    | 100   | 120   | 150   | 180   | 160   | 100   | 30    |   -   |
| Number of idle instances     | 70    | 34    | 12    | 0     | 0     | 0     | 0     | 0     | 20    | 50    |   -   |
| Idle instance fees       | 0.009 | 0.004 | 0.002 | 0.000 | 0.000 | 0.000 | 0.000 | 0.000 | 0.003 | 0.006 | 0.024 |
| Pay-as-You-Go fees   | 0     | 0     | 0     | 0     | 0     | 0     | 0     | 0     | 0     | 0     | 0     |

