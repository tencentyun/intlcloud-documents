### How is INTELLIGENT TIERING billed?

INTELLIGENT TIERING fees include **INTELLIGENT TIERING storage usage fees** and **INTELLIGENT TIERING object monitoring fees**.
1. INTELLIGENT TIERING storage usage fees are charged differently depending on the storage tier of objects.
 - When objects are stored in the frequent access tier, STANDARD storage usage fees are charged.
 - When objects are stored in the infrequent access tier, STANDARD_IA storage usage fees are charged.
 >?
 > - STANDARD and STANDARD_IA storage usage fees vary by region. For details about their pricing, see [Product Pricing](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=).
 > - Request fees and traffic fees are also incurred during object upload and download. For the billing examples, see [Traffic Fees](https://intl.cloud.tencent.com/document/product/436/33776) and [Request Fees](https://intl.cloud.tencent.com/document/product/436/40100).
 > 
2. INTELLIGENT TIERING object monitoring fees are charged based on the number of objects stored (excluding files smaller than 64 KB). For details about their pricing, see [Product Pricing](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=).

**Sample**

Assume that an organization has 100,000 objects (10 MB per object, 1 TB in total), and the data is stored in the INTELLIGENT TIERING storage class in Beijing region. If 20% of the objects (i.e., 20,000 objects) transition to the infrequent access tier every month, the object monitoring fees and storage usage fees for each month will be as follows:

| Month | Object Monitoring Fees (USD) | INTELLIGENT TIERING Storage Usage Fees (USD) | STANDARD Storage Usage Fees (USD)     | 
|----|----|----|----|
|1| 0.25|1024 x 0.024 = 24.58  |   1024 x 0.024 = 24.58  |
|2|0.25|819.2 x 0.024 + 204.8 x 0.018 = 23.35| 1024 x 0.024 = 24.58  |
|3|0.25|655.36 x 0.024 + 368.64 x 0.018 = 22.36 |  1024 x 0.024 = 24.58  |
|4|0.25|524.288 x 0.024 + 499.712 x 0.018 = 21.58 |  1024 x 0.024 = 24.58 |
|5|0.25|419.4304 x 0.024 + 604.5696 x 0.018 = 20.95  |  1024 x 0.024 = 24.58  |
|6|0.25|335.54432 x 0.024 + 688.45568 x 0.018 = 20.45  | 1024 x 0.024 = 24.58 |

As you can see, using INTELLIGENT TIERING reduces storage costs over time. Only a small amount of monitoring fees is incurred each month.

### What types of objects is INTELLIGENT TIERING suitable for?

INTELLIGENT TIERING is suitable for large objects (such as audios, videos, and logs) whose access patterns change. Larger average object sizes mean that you pay less for monitoring per GB of objects. If your business has relatively fixed data access patterns, you can set lifecycle configuration to specify the time to transition objects to STANDARD_IA without the need to use INTELLIGENT TIERING.

### How do I store objects in INTELLIGENT TIERING?
You can store objects in INTELLIGENT TIERING as follows:
- Incremental objects: You just need to specify the storage class as INTELLIGENT TIERING when uploading objects.
- Existing objects: You can modify the storage class to INTELLIGENT TIERING by using the `COPY` API. You can also use the lifecycle feature to transition STANDARD or STANDARD_IA objects to INTELLIGENT TIERING.

>!INTELLIGENT TIERING objects smaller than 64 KB will always be stored in STANDARD. For such objects, we recommend you upload them to the STANDARD, STANDARD_IA, ARCHIVE, or DEEP ARCHIVE storage class as needed to reduce costs.
>

### How do I disable INTELLIGENT TIERING configuration?

INTELLIGENT TIERING configuration **can't be disabled** once enabled. If you don't need to store your objects in INTELLIGENT TIERING, you just need to specify the storage class as a non-INTELLIGENT TIERING class such as STANDARD, STANDARD_IA, ARCHIVE, or DEEP ARCHIVE when uploading objects.

