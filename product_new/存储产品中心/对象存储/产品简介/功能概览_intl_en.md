Before using COS, read [COS Glossary](https://cloud.tencent.com/document/product/436/18507) to learn the basics of using COS: bucket, object, region, access domain name, etc.
COS provides the following features:
<style>
table th:first-of-type {
    width: 300px;
}
</style>

| Feature |Description|  
|---------|---------|
| [Creating Bucket](https://cloud.tencent.com/document/product/436/13309)| You need to create a bucket before uploading objects to COS.| 
| [Deleting Bucket](https://cloud.tencent.com/document/product/436/32433)|Deletes the existing empty buckets. To delete a bucket, you first need to delete all objects in it and incomplete multipart uploads in **Incomplete Upload**. |
| [Querying Bucket](https://cloud.tencent.com/document/product/436/13313)| Queries the created buckets. |
| [Setting Bucket Access Permission](https://cloud.tencent.com/document/product/436/13315)| COS supports setting bucket access permission, and provides access policies and Access Control Lists (ACLs). For more information, see [Basic Concepts of Access Control](https://cloud.tencent.com/document/product/436/30749). |
| [Setting Hotlink Protection](https://cloud.tencent.com/document/product/436/13319)|COS is billed based on the actual usage. To reduce additional costs incurred due to hotlinking of your COS data, COS supports setting hotlink protection to ensure security. |
| [Setting Origin-pull](https://cloud.tencent.com/document/product/436/13310)|An origin server address is set to read the data retrieval requests in multiple origin-pull ways, to meet the needs of hot migration of data and redirection of specific requests. |
| [Setting Cross-Origin Access](https://cloud.tencent.com/document/product/436/13318)|COS provides the settings of cross-origin access in the HTML5 standard to allow cross-origin access. For this purpose, COS supports responding to OPTIONS requests and returning specific setting rules to browsers according to the rules set by developers. |
| [Setting up a Static Websites](https://cloud.tencent.com/document/product/436/14984)|By configuring a bucket for static website hosting, you can access the static website using the domain name of the bucket. |
| [Setting Lifecycle](https://cloud.tencent.com/document/product/436/14605)|COS supports user-defined rules and will automatically delete specified objects or change the storage class after certain time (days). |
| [Accessing Bucket List Using Sub-Account](https://cloud.tencent.com/document/product/436/17061)| The sub-account is granted access to buckets and bucket list by the root account. |
| [Adding Bucket Policy](https://cloud.tencent.com/document/product/436/33369)|Users can add policies to a bucket to allow or deny access to COS resources by an account or source IP (or IP segment). |
| [Deleting Incomplete Multipart Uploads](https://cloud.tencent.com/document/product/436/17313) | Users can delete partially uploaded fragmented files. |
| [Setting CDN Acceleration](https://cloud.tencent.com/document/product/436/18424)| You can bind custom domain names to the access domain name of COS through domain management, and thus the objects of your bucket can be accessed using custom domain names. You can also quick configure Tencent Cloud CDN to enable acceleration. |
| [Uploading Object](https://cloud.tencent.com/document/product/436/13321) | Objects(such as text files, images, videos, Apps, etc.) can be uploaded to a bucket. |
| [Downloading Object](https://cloud.tencent.com/document/product/436/13322)|Objects can be downloaded in multiple ways. |
| [Viewing Object Information](https://cloud.tencent.com/document/product/436/13326) | You can check the attributes (such as size and address) and configurations (setting object access permission, changing storage class, etc.).|
| [Searching for Objects](https://cloud.tencent.com/document/product/436/13325)| You can search for objects in buckets or folders by prefix. |
| [Modifying Storage Class](https://cloud.tencent.com/document/product/436/33492)  | Modify the storage class for objects uploaded to COS. |
| [Setting Object Access Permission](https://cloud.tencent.com/document/product/436/13327) | Object access permission allows access control at object dimension and has a higher priority than bucket access permission. |
| [Setting Object Encryption](https://cloud.tencent.com/document/product/436/33366) | Encrypt the object stored in the bucket to avoid information leakage. |
| [Custom Headers](https://cloud.tencent.com/document/product/436/13361)|Sets HTTP headers for an object. |
| [Deleting Object](https://cloud.tencent.com/document/product/436/13323)|Deletes an object or objects in batch. |
| [Recovering Archived Objects](https://cloud.tencent.com/document/product/436/32430) | Recovers archived objects so that you can access them or perform other operations. |
| [Creating Folder](https://cloud.tencent.com/document/product/436/13329)|Folders can be created to manage and classify data stored in COS. |
| [Deleting Folder](https://cloud.tencent.com/document/product/436/13330)|A folder and all files in it can be deleted. |
| [API Documentation](https://cloud.tencent.com/document/product/436/7751)| Provides API operations supported by COS and the related operation examples. |
| [SDK Documentation](https://cloud.tencent.com/document/product/436/6474)| Provides SDK development operations and related samples for mainstream languages. |
