## Example of Billing Scheme

Current resource usage of SCF is billed as memory configured for the function multiplied by **actual running duration**. Compared with the previous billing mode of 100ms CDN(Cloud Front), it will consume less resources and cause lower cost to save  your budget.

### Web and API Service

For Web service or API request, the actual running duration of related codes is usually in the range of 30 ms to 50 ms. You can get a save up to 70% by billing based on actural running duration.

**Example**: A user used some API service consisting of SCF and API gateway. The SCF is configured with a memory of 128 MB, and its average execution duration is 37ms. In the previous billing scheme, the charging duration of the function was 100 ms and 1 million invocations would cause resouce usage of 12,500 GBs. However, billing based on actual running duration only cause resource usage of 4625 GBs, which brings a reduction of 63%.

### Message Handling

For the filtering, transformation, and forwarding of the messages in message quene, the actual running duration of related codes is usually in the range of 60 ms to 80 ms. You can get a save up to 40% by billing based on actural running duration.

**Example**: B user triggered SCF by the message of Ckakfa and reforwarded the message filtered and transformed to Ckafka. The SCF is configured with a memory of 256 MB, and its average execution duration is 67 ms. In the previous billing scheme, 5 million invocations per day would cause resouce usage of 125,000 GBs. However, billing based on actual running duration only cause resource usage of 83,750 GBs, which brings a reduction of 37%.

### Event Forwarding

For forwarding the event in object storage to the downstream system, the actual running duration of related codes is usually in the range of 50 ms to 80 ms. You can get a save up to 50% by billing based on actural running duration.

**Example**: C user forwarded the file upload event in COS to his own file processing system via SCF. The SCF is configured with a memory of 128 MB, and its average execution duration is 43 ms. In the previous billing scheme, 200,000 files to be uploaded per day would cause resource usage of 25,00 GBs. However, billing based on actual running duration only cause resource usage of 1075 GBs, which brings a reduction of 57%.

## Example of Billing

### Web and API Service

Assume that the function configured with API gateway is triggered and executed by URL. There are 100,000 requests per day. The SCF is configured with a memory of 128 MB and the average running duration of processing each request is 70 ms.

**The resource usage and number of invocations per day are as follows:

- Number of invocations per day: 100,000 invocations
- Resource usage per day:（128 / 1024）×（70 / 1000）× 100000 = 875 GBs

**The fee is calculated as follows based on 30 days of each month:

- Resource usage fee per month: 875 × 30 = 26250 GBs. No fee is caused for less than 400,000 GBs. 
- Fees for number of invocations per month: 100000 x 30 / 10000 - 100）x 0.002 = 0.3 USD

Under this circumstance, the total fee is 0.3 USD of fees for number of invocations.

### Message Queue Trigger

Assume that the function is configured with Ckafka trigger mode and is triggered 3 times per second. The SCF is configured with a memory of 128MB. The function will process the message and put the message processed into the processed message queue. For processing each message, the running duration of the function is 70 ms.


**The resource usage and number of invocations per day are as follows:

- Resource usage per day:（128 / 1024）×（260 / 1000）× 3 × 3600 × 24 = 8424GBs
- Number of invocations per day: 3 × 3600 × 24 = 259200 invocations

**The fee is calculated as follows based on 30 days of each month:

- Resource usage fee per month: 8424 × 30 = 252720 GBs. No fee is caused for less than 400,000 GBs. 
- Fees for number of invocations per month:（259200 × 30 / 10000 - 100）× 0.002 = 1.36 USD

Under this circumstance, the total fee is 1.36 USD of fees for number of invocations.

### External File Upload

Assume that the function is invocated directly by the user using the cloud API, and there are 50 invocations per minute. The SCF is configured with a memory of 256 MB. The function generates a file of 1KB and uploads the file to an external site built by the user. In this case, the function runs for 780 ms.

**The resource usage and number of invocations per day are as follows:

- Resource usage per day:（256 / 1024）×（780 / 1000）× 50 × 60 × 24 = 14040GBs
- Number of invocations per day: 50 × 60 × 24 = 72000 invocations
- Traffic per day: 1 × 50 × 60 × 24 = 72000KB = 70.31MB

**The fee is calculated as follows based on 30 days of each month:

- Resource usage fee per month: （14040 × 30 - 400000）× 0.0000167  = 0.35 USD
- Fees for number of invocations per month:（72000 × 30 / 10000 - 100）× 0.002 = 0.23 USD
- Fees for public network outbound traffic per month: （70.31 × 30 / 1024）× 0.12  = 0.25 USD

Under this circumstance, the total fee is: resource usage fee of 0.35 USD + fees of 0.23 USD for number of invocations + fees of 0.25 USD for public network outbound traffic = 0.83 USD
