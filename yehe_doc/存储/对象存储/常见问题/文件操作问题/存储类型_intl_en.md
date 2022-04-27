### How is INTELLIGENT TIERING billed?

INTELLIGENT TIERING fees include **INTELLIGENT TIERING storage usage fees** and **INTELLIGENT TIERING object monitoring fees**.
1. INTELLIGENT TIERING storage usage fees are charged differently depending on the storage tier of objects.
 - When objects are stored in the frequent access tier, STANDARD storage usage fees are charged.
 - When objects are stored in the infrequent access tier, STANDARD_IA storage usage fees are charged.
 >?
 > - STANDARD and STANDARD_IA storage usage fees vary by region. For details about their pricing, see [Product Pricing](https://buy.cloud.tencent.com/price/cos).
 > - Request fees and traffic fees are also incurred during object upload and download. For the billing examples, see [Traffic Fees](https://intl.cloud.tencent.com/document/product/436/33776) and [Request Fees](https://intl.cloud.tencent.com/document/product/436/40100).
 > 
2. INTELLIGENT TIERING object monitoring fees are charged based on the number of objects stored. 0.025 USD is charged per 10,000 monitored objects per month.

**Sample**

Assume that an organization has 1 TB objects, 100,000 objects in total (10 MB per object), and the data is stored in the INTELLIGENT TIERING storage class in the Beijing region. If 20% of the objects (i.e., 20,000 objects) transition to the infrequent access tier every month, the object monitoring fees and storage usage fees for each month will be as follows:

| Month | Object Monitoring Fees (USD) | INTELLIGENT TIERING Storage Usage Fees (USD) | STANDARD Storage Usage Fees (USD)
|----|----|----|----|
|1| 0.25|1024 x 0.024 = 24.58  |   1024 x 0.024 = 24.58  |
|2|0.25|819.2 x 0.024 + 204.8 x 0.018 = 23.35| 1024 x 0.024 = 24.58  |
|3|0.25|655.36 x 0.024 + 368.64 x 0.018 = 22.36 |  1024 x 0.024 = 24.58  |
|4|0.25|524.288 x 0.024 + 499.712 x 0.018 = 21.58 |  1024 x 0.024 = 24.58 |
|5|0.25|419.4304 x 0.024 + 604.5696 x 0.018 = 20.95  |  1024 x 0.024 = 24.58  |
|6|0.25|335.54432 x 0.024 + 688.45568 x 0.018 = 20.45  | 1024 x 0.024 = 24.58 |

As you can see, using INTELLIGENT TIERING reduces storage costs over time. Only a small amount of monitoring cost is required each month.

### What types of objects is INTELLIGENT TIERING suitable for?

INTELLIGENT TIERING is suitable for large objects (such as audio and video, logs, etc.) whose access patterns change. Larger average object sizes mean you pay less for monitoring per GB objects. If your business has relatively fixed data access patterns, you can set lifecycle configuration to specify the time to transition objects to STANDARD_IA without the need to use INTELLIGENT TIERING.

### How can I store objects in INTELLIGENT TIERING?
You can store objects in INTELLIGENT TIERING as follows:
- Incremental objects: You just need to specify the storage class as INTELLIGENT TIERING when uploading the objects.
- Existing objects: You can modify the storage class to INTELLIGENT TIERING using the `COPY` API. You can also use the lifecycle feature to transition STANDARD or STANDARD_IA objects to INTELLIGENT TIERING.

>! INTELLIGENT TIERING has a minimum storage object size of 64 KB. Therefore, objects smaller than 64 KB will always be stored in STANDARD. For objects smaller than 64 KB, we recommend you upload them to the STANDARD, STANDARD_IA, ARCHIVE, or DEEP_ARCHIVE storage class as needed to reduce costs.
>

### How do I disable INTELLIGENT TIERING configuration?

INTELLIGENT TIERING configuration **can't be disabled** once enabled. If you don't need to store your objects in INTELLIGENT TIERING, you just need to specify the storage class as a non-INTELLIGENT TIERING class such as STANDARD, STANDARD_IA, ARCHIVE, or DEEP_ARCHIVE when uploading the objects.
