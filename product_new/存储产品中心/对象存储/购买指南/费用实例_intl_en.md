>- The following billing samples are based on cities in China. 
>- The prices in the samples are for reference only. For actual prices, see [Pricing](https://intl.cloud.tencent.com/document/product/436/6239).
>- A personal user is eligible for 50 GB of standard storage capacity per month free of charge for 6 months. For more information, see [Free Tier](https://intl.cloud.tencent.com/document/product/436/6240).
>An enterprise user is eligible for 1 TB of standard storage capacity per month free of charge for 6 months. For more information, see [Free Tier](https://intl.cloud.tencent.com/document/product/436/6240).

## Sample 1: Personal User in Guangzhou Region

### Background

User A runs a website and often publishes articles containing images, background music and videos. The website also contains a software download section. He stores the contents of the website in **standard storage** class in the **Guangzhou region** with the CDN acceleration service enabled.

### Demand

The images are expected to occupy 100 GB of standard storage capacity per month and generate 100 GB of CDN origin-pull traffic with 1 million read and write requests in total.

### Monthly Fees Calculation

During the validity period of the Free Tier (i.e., 6 months after the COS service is activated), the monthly fee is as follows:

| Item | Free Tier | Unit Price | Billable Usage | Fees (Unit Price * Billable Usage) |
| ---------------- | -------- | ------------- | ----------- | ------------------------ |
| Storage capacity | 50 GB | 0.024 USD/GB/month | (100 - 50) GB | 1.2 USD |
| Requests | 0 | 0.002 USD/10,000 requests | 1 million requests | 0.2 USD |
| CDN origin-pull traffic | 0 | 0.02 USD/GB | 100 GB | 2 USD |
| Monthly fee           | -        | -            | -           | **3.4 USD**                 |

After the user's Free Tier expires, the monthly fee is as follows:

| Item | Free Tier | Unit Price | Billable Usage | Fees (Unit Price * Billable Usage) |
| ---------------- | -------- | ------------- | -------- | ------------------------ |
| Storage capacity | 0 |  0.024 USD/GB/month | 100GB GB | 2.4 USD |
| Requests | 0 | 0.002 USD/10,000 requests | 1 million requests | 0.2 USD |
| CDN origin-pull traffic | 0 | 0.02 USD/GB | 100 GB | 2 USD |
| Monthly fee           | -       | -             | -        | **4.6 USD**               |


## Sample 2: Personal User in Guangzhou Region

### Background

User B runs a website and often publishes articles containing images, background music, and videos; the website also has a software download section.

He stores the contents of the website in **standard storage** class in the **Chengdu region** with CDN acceleration service enabled. 

### Demand

The images are expected to occupy 100 GB of standard storage capacity per month and generate 100 GB of CDN origin-pull traffic with 1 million read and write requests in total.

### Monthly Fees Calculation

During the validity period of the Free Tier (i.e., 6 months after the COS service is activated), the monthly fee is as follows:

| Item | Free Tier | Unit Price | Billable Usage | Fees (Unit Price \* Billable Usage) |
| ---------------- | -------- | -------------- | ----------- | ------------------------ |
| Storage capacity | 50 GB | 0.02 USD/GB/month | (100 - 50) GB | 1 USD |
| Requests | 0 | 0.002 USD/10,000 requests | 1 million requests | 0.2 USD |
| CDN origin-pull traffic | 0 | 0.02 USD/GB | 100 GB | 2 USD |
| Monthly fee           | -        | -            | -           | **3.2 USD**                 |

After the user's Free Tier expires, the monthly fee is as follows:

| Item |  Free Tier | Unit Price | Billable Usage | Fees (Unit Price \* Billable Usage) |
| ---------------- | -------- | -------------- | -------- | ------------------------ |
| Storage capacity | 0 | 0.02 USD/GB/month | 100 GB | 2 USD |
| Requests | 0 | 0.002 USD/10,000 requests | 1 million requests | 0.2 USD |
| CDN origin-pull traffic | 0 | 0.02 USD/GB | 100 GB | 2 USD |
| Monthly fee           | -        | -            | -           | **4.2 USD**                 |

## Sample 3: Enterprise User Using Standard Storage in Beijing Region With CDN Acceleration Enabled

### Background

Company B runs a website and often publishes articles containing images, background music, and videos; the website also has a software download section.

They store the contents of the website in **standard storage** class in the **Beijing region** with the CDN acceleration service enabled. 

### Demand

The files are expected to occupy 1.5 TB of standard storage capacity per month and generate 500 GB of CDN origin-pull traffic with 5 million read requests and 0.2 million write requests.

### Monthly Fees Calculation

During the validity period of the Free Tier (i.e., 6 months after the COS service is activated), the monthly fee is as follows:

| Item | Free Tier | Unit Price | Billable Usage | Fees (Unit Price \* Billable Usage) |
| ---------------- | -------- | ------------- | ------------------- | ------------------------ |
| Storage capacity | 1 TB | 0.024 USD/GB/month | ((1.5 - 1) TB * 1024) GB | 12.288 USD |
| Requests | 0 | 0.002 USD/10,000 requests | (5+0.2) million requests | 1.04 USD |
| CDN origin-pull traffic | 0 | 0.02 USD/GB | 500 GB | 10 USD |
| Monthly fee           | -        | -            | -           | **23.328 USD**                 |

After the user's Free Tier expires, the monthly fee is as follows:

| Item | Free Tier | Unit Price | Billable Usage | Fees (Unit Price \* Billable Usage) |
| ---------------- | -------- | ------------- | ------------- | ------------------------ |
| Storage capacity | 0 GB | 0.024 USD/GB/month | (1.5TB * 1024) GB | 36.864 USD |
| Requests | 0 | 0.002 USD/10,000 requests | (5+0.2) million requests | 1.04 USD |
| CDN origin-pull traffic | 0 | 0.02 USD/GB | 500 GB | 10 USD |
| Monthly fee           | -        | -            | -           | **47.904 USD**                 |

## Sample 4: Enterprise User Using Archive Storage in Chongqing Region Without CDN Acceleration Enabled

### Background 

Company B manages a hospital that has a large amount of medical records and imaging materials that need to be backed up and stored. They store the files in **archive storage** class in the **Chongqing region** without enabling CDN acceleration service.

### Demand

The files are expected to occupy 20 TB of archive storage capacity per month.

### Monthly Fees Calculation

| Item | Free Tier | Unit Price | Billable Usage | Fees (Unit Price \* Billable Usage) |
| ------------ | -------- | ------------- | ------------ | ------------------------ |
| Storage capacity | 0 GB | 0.0045 USD/GB/month | (20TB * 1024) GB | 92.16 USD |
| Monthly fee           | -        | -            | -           | **92.16 USD**                 |

If you have any questions, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

