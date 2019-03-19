Before using COS, read [Basic Concepts](/document/product/436/6225) to learn the definitions of COS basic concepts including bucket, object, region, access domain name, etc.
COS offers the following capabilities:
<style>
table th:first-of-type {
    width: 300px;
}
</style>

| Feature | Description |
|---------|---------|
| [Creating Bucket](/document/product/436/13309) | You need to create a bucket before uploading objects to COS. |
| [Deleting Bucket](/document/product/436/13309) | To deleted a bucket, you first need to delete all objects in it and fragments in **Incomplete Upload**. |
| [Setting Bucket Access Permission](/document/product/436/13315) | COS supports setting bucket access permission, and provides access policies (Policies) and Access Control Lists (ACLs). For more information, see [Basic Concepts of Access Control](https://cloud.tencent.com/document/product/436/30749). |
| [Setting Hotlink Protection](/document/product/436/13319) | COS is billed based on the actual usage. To reduce additional costs incurred due to hotlinking of your COS data, COS supports setting hotlink protection to ensure security. |
| [Origin-pull Settings](/document/product/436/13310) | An origin server address is set to read the data requested by a request from the origin server in different ways, to meet the needs of hot migration of data and redirection of specific requests. |
| [Hosting Static Websites](/document/product/436/13320) | By configuring a bucket for static website hosting, you can access the static website using the domain name of the bucket. |
| [Setting Cross Origin Resource Sharing](/document/product/436/13318) | COS provides the CORS settings in the HTML5 standard. For this purpose, COS supports responding to OPTIONS requests and returning specific setting rules to browsers according to the rules set by developers. |
| [Domain Name Management](/document/product/436/13396) | You can bind custom domain names to the access domain name of COS through domain name management, and thus the objects of your bucket can be accessed using custom domain names. You can also configure Tencent Cloud CDN with one click to enable acceleration. |
| [Uploading Object](/document/product/436/13321) | Objects (such as text files, images, videos, Apps, etc.) can be uploaded to a bucket. |
| [Downloading Object](/document/product/436/13322) | Objects can be downloaded in multiple ways. |
| [Searching for Objects](/document/product/436/13325) | You can search for objects in buckets or folders by prefix. |
| [Setting Object Access Permission](/document/product/436/13327) | Object access permission allows access control at object dimension and has a higher priority than bucket access permission. |
| [Custom Headers](/document/product/436/13361) | Sets HTTP headers for an object. |
| [Deleting Object](/document/product/436/13323) | Deletes an object or objects in batch. |
| [Creating Folder](/document/product/436/13329) | Folders can be created to manage and classify data stored in COS. |
| [Deleting Folder](/document/product/436/13330) | A folder and all files in it can be deleted. |
| [API Documentation](/document/product/436/7751) | Provides API operations and related examples supported by COS. |
| [SDK Documentation](/document/product/436/6474) | Provides SDK development operations and related examples for mainstream languages. |

