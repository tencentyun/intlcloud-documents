### What is COSBrowser?

COSBrowser is a visual interface tool that Tencent Cloud COS released to make it easier for you to view, transfer and manage COS resources with simpler interactions. Currently, it is available for desktops (Windows, macOS, Linux), and mobile clients (Android, iOS). For more information, see [COSBrowser Overview](https://intl.cloud.tencent.com/document/product/436/11366).


### How to download COSBrowser?

For the download URL and instructions, see [COSBrowser Overview](https://intl.cloud.tencent.com/document/product/436/11366).


### Why isn’t the storage path displayed when I log in with a sub-account?

1. Please make sure the sub-account has the permission to access COS. See [Granting Sub-accounts Access to COS](https://intl.cloud.tencent.com/document/product/436/11714).
2. If the sub-account only has the permission to access a specified bucket or a specified directory under a bucket, then you need to manually add a storage path (format: “Bucket” or “Bucket/Object-prefix”, e.g. `examplebucket-1250000000`), and select the region where the bucket should reside when you log in.


### How to increase the transfer speed for a massive number of files?

Take Windows COSBrowser as an example. You can do so by navigating to **Advanced Settings**, and configuring a greater number of concurrent files and parts for **Upload** and **Download**.
