The COS console provides an **Overview** page where you can view the usage overview, basic information, domain names/endpoints, configuration, and alarms for your bucket.


## Directions

>?If a sub-account cannot be used to view **Overview** data, contact the root account admin to request the **GetBucket** permission.

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5). On the left sidebar, click **Bucket List**.
2. Locate the bucket you want, and click the bucket name.
3. Click the **Overview** tab to enter the bucket overview page.
![](https://main.qcloudimg.com/raw/a7d4fc49a5997ab22f7cccbf2fdcc436.png)

## Usage Overview

**Usage Overview** shows the number of objects, incomplete multipart uploads, storage usage, traffic, and requests in the current bucket.

 >!"Usage Overview" data is delayed for about two hours compared with real-time data. It is for monitoring purposes only. For accurate billing data, go to [Billing Center](https://console.cloud.tencent.com/expense/bill/dosageDownload) to download usage details.

- Number of objects/Number of incomplete multipart uploads: allows you to view the number of objects or incomplete multipart uploads in each COS storage class.
- Storage: allows you to view the storage usage for each available storage class including STANDARD, STANDARD_IA, ARCHIVE, and DEEP ARCHIVE.
  
  >!The DEEP ARCHIVE storage usage is available only for buckets in some regions. For the supported regions, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925).
- Traffic: allows you to view the total traffic, downstream traffic (public network), downstream traffic (private network), and CDN origin-pull traffic for the current month in STANDARD and STANDARD_IA storage classes.
- Requests: allow you to view the number of all requests, read requests and write requests for the current month.
- Retrievals: allow you to view the amount of data retrieved from STANDARD_IA and ARCHIVE.

## Basic Information

**Basic Information** includes bucket name, region, creation time and access permissions.

- Bucket Name: consists of a custom bucket name and APPID. For naming conventions, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312).
- Region: specifies the region where the bucket resides.
- Creation Time: specifies the time when the bucket was created.
- Access Permissions: specify the access permissions for the bucket. For more information on permissions, please see [Setting Access Permission](https://intl.cloud.tencent.com/document/product/436/13315).

## Domain Information

**Domain Information** shows all the domain names/endpoints configured for the bucket.

- Endpoint: the default COS access endpoint for this bucket. It is auto-generated based on the bucket’s name and region when you create a bucket.
- Default CDN acceleration domain: the auto-generated CDN domain name which uses CDN cache nodes for acceleration, and which you can choose whether to enable or not.
- Custom CDN acceleration domain: allows you to bind a custom domain name to Tencent Cloud CDN to speed up access to the objects in this bucket.
- Custom endpoint: allows you to bind your own domain name as a custom endpoint to the bucket for access to the objects in it.
- Global acceleration endpoint: the auto-generated endpoint after you enable global acceleration. You can use this endpoint to speed up uploads to the bucket globally. For more information on global acceleration, please see [Global Acceleration > Overview](https://intl.cloud.tencent.com/document/product/436/33409).
- Static website endpoint: allows you to access a bucket configured as a static website. For more information on static website, please see [Setting up a Static Website](https://intl.cloud.tencent.com/document/product/436/14984).

## Alarm Configuration

**Alarm Configuration** enables you to configure alarms on your bucket for daily monitoring purposes.

- Current alarms: show the number of ongoing alarms.
- Alarm policies: show the number of existing alarm policies.

## Bucket Configuration

**Bucket Configuration** shows the status of each bucket configuration.

- CORS: represents cross-origin access which requests resources from another origin over HTTP. Two origins that differ in any one of protocol, domain name, and port are treated as different origins. For more information, please see [Setting Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/13318).
- Origin-Pull: leads you from COS to another origin for data access using an origin-pull rule when the object you request does not exist in the COS bucket or a specific request needs to be redirected. For more information, please see [Setting Origin-Pull](https://intl.cloud.tencent.com/document/product/436/31508).
- Hotlink Protection: prevents malicious programs' cheating for public network traffic using resource URLs or stealing of resources by malicious means. For more information, please see [Setting Hotlink Protection](https://intl.cloud.tencent.com/document/product/436/13319).
- Cross Region Replication: automatically replicates **incremental objects** asynchronously from the source bucket to the destination bucket in another region after you enable cross-region replication. For more information, please see [Setting Cross-Region Replication](https://intl.cloud.tencent.com/document/product/436/19235).
- Tag: a bucket tag used as an identifier to help group and manage buckets. For more information, please see [Setting Bucket Tags](https://intl.cloud.tencent.com/document/product/436/30928).
- Versioning: retains multiple versions of an object after you enable versioning on your bucket. It helps to retrieve your data lost due to accidental deletion or application failure. For more information, see [Setting Versioning](https://intl.cloud.tencent.com/document/product/436/19881).
- Inventory: outputs an inventory report on object attributes, configuration details and other information for your bucket every day or every week. For more information, please see [Enabling Inventory](https://intl.cloud.tencent.com/document/product/436/30624).
- Lifecycle: automatically transitions or deletes specified objects within the specified time according to your lifecycle rule. For more information, please see [Setting Lifecycle](https://intl.cloud.tencent.com/document/product/436/14605).
- Logging: logs all kinds of COS requests for **bucket operations** after you enable logging to help you better manage and use your bucket. For more information, please see [Setting Logging](https://intl.cloud.tencent.com/document/product/436/17040).