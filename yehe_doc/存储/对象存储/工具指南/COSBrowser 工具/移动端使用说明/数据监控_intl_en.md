The data overview feature of COSBrowser Mobile Version displays your COS data usage in the past 30 days, including total traffic, total read and write requests, storage trend, traffic trends (for public network downstream traffic, private network traffic, and CDN origin-pull traffic), trend in the number of requests, trend in the ratio of effective requests, amount of STANDARD_IA data retrieved, and amount of archive data retrieved.

>? 
> - Current, you cannot view data with a sub-account on Mobile Version. You can log in to a sub-account to view data in the console as instructed in [Viewing Statistics](https://intl.cloud.tencent.com/document/product/436/36542).
> - The data in this feature isn't real-time but has a delay of about two hours, so it is for reference only. You can view more accurate billing and usage data in the console as instructed in [Viewing Statistics](https://intl.cloud.tencent.com/document/product/436/36542).
> 

<span id="UsageOverview"></span>
## Usage Overview
COSBrowser provides the storage data overview page, where you can view the number of objects, storage usage, number of requests, and traffic.


<span id="BucketMonitoring"></span>
## Bucket Monitoring

COSBrowser provides data overview by bucket. You can view the bucket monitoring data in the following two ways:

1. Tap **Home** at the bottom and tap **User Overview** to switch between buckets to view their monitoring data.

2. Tap **Resources** at the bottom and tap **More** on the right of the target bucket. In the pop-up operation list, tap **Monitoring** to enter the bucket page.


<span id="TheWidget"></span>
## Widget
COSBrowser can be added to the Home Screen as a widget, so you can view the monitoring data anywhere, anytime with no need to open COSBrowser.

### Adding widget

1. Download and install COSBrowser for iOS on your iPhone. Then, touch and hold an empty area on the Home Screen until apps jiggle and tap **+** in the top-left corner.

2. Find and tap COSBrowser.

3. Select a layout and tap **Add Widget** at the bottom.




### Customizing displayed data
The widget allows you to customize the scope of data to be displayed. You can specify a certain bucket or storage class for tracking and monitoring. The following storage classes can be displayed: STANDARD, STANDARD_IA, and ARCHIVE.

The detailed steps are as follows:
1. Open COSBroswer for iOS and tap **Me** > **Settings** > **Widget Configuration** to enter the widget settings page.

2. Set the configuration items as follows:

 - **Select Bucket**: If no bucket is selected, the overview data of all buckets under the current account will be displayed. If a bucket is selected, its overview data will be displayed.
 - **Select Storage Class**: The widget displays the monitoring data of the STANDARD storage class by default. You can manually select another storage class such as STANDARD_IA and ARCHIVE.

>? If you want to quickly reset the configured bucket and storage class, simply tap **Reset**. Then, the monitoring data of all buckets in the STANDARD storage class under the current account will be displayed.
>

### Removing widget

Touch and hold the widget and tap **Remove Widget**.


