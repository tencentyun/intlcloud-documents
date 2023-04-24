
If your website is deployed on your on-premise server, during the peak service hours, users are likely to experience slow image loading or loading problems due to server performance limits. To solve this problem, you can store static files on Tencent Cloud COS, and then connect your website to Tencent Cloud CDN to accelerate distribution of files stored on COS. 


### Recommended Configurations
See below for the sample configuration on CDN and COS: 

CDN configurations
- Domain: `www.qcdntest.cn`
- Target: Users in Chinese mainland
- Origin domain: The domain name assigned by the COS bucket
- Cache TTL: 2 days for JPG/PNG files; 7 days for GIF files and the directory; no cache for PHP files
- Daily bandwidth cap: 5 Gbps
- Bandwidth cap estimation: Suppose that the average number of daily visitors is 1,000, with the max concurrency of 40 visitors. The bandwidth requirement of each visitor is 50 Mbps, which means the bandwidth peak is around 50 Mbps * 40 = 2,000 Mbps. Counting in the bandwidth requirements for busty traffic, we recommend setting the bandwidth cap to 5,000 Mbps.

COS configurations
- Bucket region: Guangzhou
- Bucket name: pic
- Access permission: Private read and write
- Resource type: Image files, with an average file size of 500 KB. 
