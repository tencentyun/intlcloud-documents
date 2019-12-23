>
- The following billing sample is based on the Singapore region.
- The prices in the sample are for reference only. For actual prices, see [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).


## Case
### Background

User A runs an image website. Visitors can upload local images to the website, process images online, and download images. User A stores the content of the website in COS buckets in the **Singapore region**, and uses the **Cloud Infinite** service with CDN acceleration enabled.

### Demands

Every month, the user requires 100 GB basic image processing capacity, 100 GB CDN origin-pull traffic, 10,000 times of QR code recognition, and 10,000 times of blind watermarking.

### Monthly cost calculation

| Billing Item | Unit Price | Billable Usage | Cost (Unit Price × Billable Usage) |
| ---------------- | -------------- | ---------------- | ---------------------- |
| Basic image processing | 0.01 USD/GB/month | 100 GB | 1 USD |
| QR code recognition | 0.025 USD/1,000 times | 10,000 times | 0.25 USD |
| Blind watermarking | 0.025 USD/1,000 times | 10,000 times | 0.25 USD |
| CDN origin-pull | 0.072 USD/GB | 100 GB | 7.2 USD |
| Monthly cost | - | - | **8.7 USD** |
