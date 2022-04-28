>!
> - Regions in China are used as examples.
>- The prices in the examples are for reference only. For the actual prices, see [COS Pricing](https://intl.cloud.tencent.com/pricing/cos).
> - New users are eligible for 50 GB STANDARD storage capacity per month for 6 months. For more information, see [Free Tier](https://intl.cloud.tencent.com/document/product/436/6240).
> - The storage capacity is calculated in binary, for example, 1 TB = 1024 GB.

## Example 1

#### Background

New user A runs a website that contains images, background music, videos, and a software download section. The user stores the contents of the website in the **STANDARD** storage class in the **Guangzhou region** with the CDN acceleration service enabled.

#### Demand

The images are expected to occupy 100 GB storage capacity of the STANDARD storage class per month and generate 100 GB of CDN origin-pull traffic with 1 million read and write requests in total.

#### Monthly fee calculation

The following table describes the monthly fees during the Free Tier period (that is, the first 6 months since the user activated the COS service):

| Item | Free Tier | Unit Price | Billable Usage | Fees (Unit Price x Billable Usage) |
| ---------------- | -------- | ------------- | ----------- | ------------------------ |
| Storage capacity | 50 GB | 0.024 USD/GB/month | (100 - 50) GB | 1.2 USD |
| Requests | 0 | 0.002 USD/10,000 requests | 1 million requests | 0.2 USD |
| CDN origin-pull traffic | 0 | 0.02 USD/GB | 100 GB | 2 USD |
| Monthly fee           | -        | -            | -           | **3.4 USD**                 |

After the user's Free Tier expires, the monthly fee is as follows:

| Item | Free Tier | Unit Price | Billable Usage | Fees (Unit Price x Billable Usage) |
| ---------------- | -------- | ------------- | -------- | ------------------------ |
| Storage capacity | 0 | 0.024 USD/GB/month | 100 GB | 2.4 USD |
| Requests | 0 | 0.002 USD/10,000 requests | 1 million requests | 0.2 USD |
| CDN origin-pull traffic | 0 | 0.02 USD/GB | 100 GB | 2 USD |
| Monthly fee           | -       | -             | -        | **4.6 USD**               |




## Example 2

#### Background 

Company B (new user) manages a hospital that needs to back up and store a large amount of medical records and imaging materials. They store the files in the **ARCHIVE** storage class in the **Chongqing region** with the CDN acceleration service disabled.

#### Demand

The files are expected to occupy 20 TB storage capacity of the ARCHIVE storage class per month.

#### Monthly fee calculation

>?The storage capacity is calculated in binary, for example, 1 TB = 1024 GB.

| Item | Free Tier | Unit Price | Billable Usage | Fees (Unit Price x Billable Usage) |
| ------------ | -------- | ------------- | ------------ | ------------------------ |
| Storage capacity | 0 GB | 0.0045 USD/GB/month | (20 TB x 1024) GB | 92.16 USD |
| Monthly fee           | -        | -            | -           | **92.16 USD**                 |

If you have any questions, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

