>- The following billing examples are based on usage in Mainland China.
>- The prices in the billing examples are for reference only. For the actual pricing, see [COS Pricing](https://intl.cloud.tencent.com/document/product/436/6239).
>- An individual user can enjoy 50 GB of standard storage capacity per month free of charge for 6 calendar months. For more information, see [Free Quotas](https://intl.cloud.tencent.com/document/product/436/6240).
>- A corporate user can enjoy 1 TB of standard storage capacity per month free of charge for 6 calendar months. For more information, see [Free Quotas](https://intl.cloud.tencent.com/document/product/436/6240).

## Case 1: Individual User

### Background

User A runs a website and often publishes articles containing images, background music, and videos at the website, and there is a software download section there. He stores the contents of the website in **standard storage** class in the **Guangzhou region** with the CDN acceleration service enabled.

### Demand

The images are expected to occupy 100 GB of standard storage capacity per month and incur CDN origin-pull traffic of 100 GB with 1 million read and write requests in total.

### Monthly Fees Calculation

During the period when the free quota is available (i.e., 6 calendar months after the first bucket is created), the monthly fees analysis is as follows:

| Item | Free Quota | Unit Price | Billable Usage | Fees (Unit Price * Billable Usage) |
| ---------------- | -------- | ------------- | ----------- | ------------------------ |
| Storage capacity | 50 GB | 0.024 USD/GB/month | (100 - 50) GB | 1.2 USD |
| Requests | 0 | 0.002 USD/10,000 requests | 1 million requests | 0.2 USD |
| CDN origin-pull traffic | 0 | 0.02 USD/GB | 100 GB | 2 USD |
| Monthly fees | - | - | - | **3.4 USD** |

After the user's free quota expires, the monthly fees analysis is as follows:

| Item | Free Quota | Unit Price | Billable Usage | Fees (Unit Price * Billable Usage) |
| ---------------- | -------- | ------------- | -------- | ------------------------ |
| Storage capacity | 0 | 0.024 USD/GB/month | 100 GB | 2.4 USD |
| Requests | 0 | 0.002 USD/10,000 requests | 1 million requests | 0.2 USD |
| CDN origin-pull traffic | 0 | 0.02 USD/GB | 100 GB | 2 USD |
| Monthly fees | - | - | - | **4.6 USD** |


## Case 2: Individual User

### Background

User B runs a website and often publishes articles containing images, background music, and videos at the website, and there is a software download section there.

He stores the contents of the website in **standard storage** class in the **Chengdu region** with the CDN acceleration service enabled. 

### Demand

The images are expected to occupy 100 GB of standard storage capacity per month and incur CDN origin-pull traffic of 100 GB with 1 million read and write requests in total.

### Monthly Fees Calculation

During the period when the free quota is available (i.e., 6 calendar months after the first bucket is created), the monthly fees analysis is as follows:

| Item | Free Quota | Unit Price | Billable Usage | Fees (Unit Price \* Billable Usage) |
| ---------------- | -------- | -------------- | ----------- | ------------------------ |
| Storage capacity | 50 GB | 0.02 USD/GB/month | (100 - 50) GB | 1 USD |
| Requests | 0 | 0.002 USD/10,000 requests | 1 million requests | 0.2 USD |
| CDN origin-pull traffic | 0 | 0.02 USD/GB | 100 GB | 2 USD |
| Monthly fees | - | - | - | **3.2 USD** |

After the user's free quota expires, the monthly fees analysis is as follows:

| Item | Free Quota | Unit Price | Billable Usage | Fees (Unit Price \* Billable Usage) |
| ---------------- | -------- | -------------- | -------- | ------------------------ |
| Storage capacity | 0 | 0.02 USD/GB/month | 100 GB | 2 USD |
| Requests | 0 | 0.002 USD/10,000 requests | 1 million requests | 0.2 USD |
| CDN origin-pull traffic | 0 | 0.02 USD/GB | 100 GB | 2 USD |
| Monthly fees | - | - | - | **4.2 USD** |

## Case 3: Corporate User

### Background

Company B runs a website and often publishes articles containing images, background music, and videos at the website, and there is a software download section there.

They store the contents of the website in **standard storage** class in the **Beijing region** with the CDN acceleration service enabled. 

### Demand

The files are expected to occupy 1.5 TB of standard storage capacity per month and incur CDN origin-pull traffic of 500 GB with 5 million read requests and 0.2 million write requests.

### Monthly Fees Calculation

During the period when the free quota is available (i.e., 6 calendar months after the first bucket is created), the monthly fees analysis is as follows:

| Item | Free Quota | Unit Price | Billable Usage | Fees (Unit Price \* Billable Usage) |
| ---------------- | -------- | ------------- | ------------------- | ------------------------ |
| Storage capacity | 1 TB | 0.024 USD/GB/month | (1.5 - 1) * 1024 GB | 12.288 USD |
| Requests | 0 | 0.002 USD/10,000 requests | (5 + 0.2) million requests | 1.04 USD |
| CDN origin-pull traffic | 0 | 0.02 USD/GB | 500 GB | 10 USD |
| Monthly fees | - | - | - | **23.328 USD** |

After the user's free quota expires, the monthly fees analysis is as follows:

| Item | Free Quota | Unit Price | Billable Usage | Fees (Unit Price \* Billable Usage) |
| ---------------- | -------- | ------------- | ------------- | ------------------------ |
| Storage capacity | 0 | 0.024 USD/GB/month | 1.5 * 1024 GB | 36.864 USD |
| Requests | 0 | 0.002 USD/10,000 requests | (5 + 0.2) million requests | 1.04 USD |
| CDN origin-pull traffic | 0 | 0.02 USD/GB | 500 GB | 10 USD |
| Monthly fees | - | - | - | **47.904 USD** |

## Case 4: Corporate User

### Background 

Company B manages a hospital that has a large amount of medical records and imaging materials that need to be backed up and stored. They store the files in **archive storage** class in the **Chongqing region** with no CDN acceleration service enabled.

### Demand

The files are expected to occupy 20 TB of archive storage capacity per month.

### Monthly Fees Calculation

| Item | Free Quota | Unit Price | Billable Usage | Fees (Unit Price \* Billable Usage) |
| ------------ | -------- | ------------- | ------------ | ------------------------ |
| Storage capacity | 0 | 0.0045 USD/GB/month | 20 * 1024 GB | 92.16 USD |
| Monthly fees | - | - | - | **92.16 USD** |

If you have any questions, feel free to contact us for technical support or price negotiation by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).

