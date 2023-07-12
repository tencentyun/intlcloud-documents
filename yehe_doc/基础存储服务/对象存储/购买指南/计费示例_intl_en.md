>!
> - Regions in China are used as examples below.
> - Prices in the following examples are for reference only. For the actual prices, see [Pricing | Cloud Object Storage](https://intl.cloud.tencent.com/pricing/cos).
> - New users are eligible for a monthly free tier of 50 GB STANDARD storage usage for 6 months. For more information, see [Free Tier](https://intl.cloud.tencent.com/document/product/436/6240).
> - The storage capacity is calculated in binary, for example, 1 TB = 1024 GB.

## Free Tier Examples

### Example 1: New user with free tier

#### Background

New user A runs a website that contains images, background music, videos, and a software download section. The user stores the contents of the website in the **STANDARD** storage class in **Guangzhou region** with the CDN acceleration service enabled.

#### Demand

The images are expected to occupy 100 GB STANDARD storage capacity per day and generate 100 GB CDN origin-pull traffic, with 1 million requests in total.

#### Daily fees calculation

The following table describes the daily fees during the free tier term (i.e., the first 6 months after user A activates the COS service):

| Item | Free Tier | Unit Price | Billable Usage | Fees (Unit Price * Billable Usage) |
| ---------------- | -------- | ------------- | ----------- | ------------------------ |
| Storage usage fees | 50 GB | 0.024 USD/GB/month / 30 | (100 - 50) GB | 0.04 USD |
| Request fees | 0 | 0.002 USD/10,000 requests | 1 million requests | 0.2 USD |
| CDN origin-pull traffic | 0 | 0.02 USD/GB | 100 GB | 2 USD |
| Daily fees          | -        | -            | -           | **2.24 USD**                 |

After user A's free tier expires, the daily fees are as follows:

| Item | Free Tier | Unit Price | Billable Usage | Fees (Unit Price * Billable Usage) |
| ---------------- | -------- | ------------- | -------- | ------------------------ |
| Storage usage fees | 0 | 0.024 USD/GB/month / 30 | 100 GB | 0.08 USD |
| Request fees | 0 | 0.002 USD/10,000 requests | 1 million requests | 0.2 USD |
| CDN origin-pull traffic fees | 0 | 0.02 USD/GB | 100 GB | 2 USD |
| Daily fees           | -       | -             | -        | **2.28 USD**               |



### Example 2: New user without free tier

#### Background 

Hospital H needs to back up and store a large volume of medical records and imaging materials. They store the files in the **ARCHIVE** storage class in **Chongqing region** with the CDN acceleration service disabled.

#### Demand

The files are expected to occupy 20 TB ARCHIVE storage capacity per day, with 200,000 requests in total.

#### Daily fees calculation

>?The storage capacity is calculated in binary, for example, 1 TB = 1024 GB.

| Item | Free Tier | Unit Price | Billable Usage | Fees (Unit Price \* Billable Usage) |
| ------------ | -------- | ------------- | ------------ | ------------------------ |
| Storage usage fees | 0 | 0.0045 USD/GB/month / 30 | (20 * 1024) GB | 3.072 USD |
| Request fees | 0 | 0.002 USD/10,000 requests | 200,000 requests | 0.04 USD |
| Daily fees          | -        | -            | -           | **3.112 USD**                 |

If you have any questions, [contact us](https://www.tencentcloud.com/contact-us) for technical support or price negotiation.


## Pay-as-You-Go Billing Examples

If you don't have a valid free tier, pay-as-you-go billing is as demonstrated below:

- [Traffic Fees](https://intl.cloud.tencent.com/document/product/436/33776)
- [Storage Usage Fees](https://intl.cloud.tencent.com/document/product/436/40099)
- [Request Fees](https://intl.cloud.tencent.com/document/product/436/40100)
- [Data Retrieval Fees](https://intl.cloud.tencent.com/document/product/436/40097)
- [Management Feature Fees](https://intl.cloud.tencent.com/document/product/436/40098)