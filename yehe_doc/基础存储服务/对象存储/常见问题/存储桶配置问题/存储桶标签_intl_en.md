### How many tags can be added to a bucket?

Up to 50 bucket tag keys can be added for a single bucket, and each tag key can have up to 1,000 tag values. Besides, each root account can add up to 1,000 tag keys. For more information about bucket tag restrictions, please see [Bucket Tag Overview](https://intl.cloud.tencent.com/document/product/436/31509).


### How can I use bucket tags for cost allocation?

After you [add a bucket tag](https://intl.cloud.tencent.com/document/product/436/30928) for your bucket, tags will be recorded in your monthly [usage bill](https://console.cloud.tencent.com/expense/bill/dosageDownload). You can download the bill and then create a pivot table (see [Cost Allocation Tags](https://intl.cloud.tencent.com/document/product/555/32276)) to analyze the tag-specific usage for your bucket.


### How can I use bucket tags to manage access permissions?

You can do so as follows:
1. Contact the root account to obtain permissions to create buckets (`PutBucket`) and operate resources that have a specified tag.
2. Create a bucket and add tags for it.
3. Operate COS objects with the authorized APIs.
