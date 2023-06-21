COS offers the following features:

## Operations

<table>
   <tr>
      <th style="width: 18%;">Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Bucket operations</td>
      <td>With COS, you can create, query, delete, and empty buckets. For detailed directions, see <a href="https://intl.cloud.tencent.com/document/product/436/13309">Bucket Management</a>.</td>
   </tr>
   <tr>
      <td>Object operations</td>
      <td>Storage classes: Currently, COS offers three object storage classes for different access frequencies and disaster recovery levels: MAZ_STANDARD, MAZ_STANDARD_IA, INTELLIGENT_TIERING, STANDARD, STANDARD_IA, ARCHIVE, and DEEP ARCHIVE. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/30925">Storage Class</a>.<br>Objects/folders: can be uploaded, queried, downloaded, copied, and deleted. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/13321">Object Management</a>.</td>
   </tr>
</table>	 

## Data Management

<table>
   <tr>
      <th style="width: 18%;">Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td>Lifecycle</td>
      <td>With COS, you can set lifecycle rules for objects to regularly perform automatic deletion on an object or storage class transitioning. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/17028">Lifecycle Overview</a>.</td>
   </tr>
   <tr>
      <td>Static website</td>
      <td>You can configure a bucket to host a static website and access the static website through the bucket's endpoint. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/30958">Static Website Hosting</a>.</td>
   </tr>
   <tr>
      <td>Inventory</td>
      <td>COS allows you to configure an inventory task to regularly scan your bucket for specified objects or objects with the same prefix. You can perform these tasks daily or weekly, and each task will output an inventory report, which is stored in the specified bucket as a CSV file. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/30622">Inventory Overview</a>.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Bucket tagging</td>
      <td>A bucket tag can be used for easier bucket grouping and management. You can set, query, and delete tags for a specified bucket. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/31509">Bucket Tag Overview</a>.</td>
   </tr>
   <tr>
      <td>Event notification</td>
      <td>Used in conjunction with the Serverless Cloud Function (SCF), COS can send you timely notifications about resource changes (such as when a new file has been uploaded or deleted). For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/31648">Event Notifications</a>.</td>
   </tr>
   <tr>
      <td>COS Select</td>
      <td>This feature uses Structured Query Language (SQL) statements to filter the objects stored in COS so as to extract specific objects and get desired data. With COS Select, you can reduce the amount of data transferred by COS for lower costs and latency during data extraction. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/32472">SELECT Overview</a>.</td>
   </tr>
   <tr>
      <td>Logging</td>
      <td>This feature is used to log the access details of a source bucket; these logs are then stored in a destination bucket for better bucket management. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/16920">Logging Overview</a>.</td>
   </tr>
   <tr>
      <td>Number of object tags</td>
      <td>This feature is designed to help group and manage objects in your bucket by adding a key-value pair as an object tag. An object tag consists of a `tagKey`, an equal sign `=`, and a `tagValue`, for example, `group = IT`. You can set, query, and delete tags for a specified object. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/35665">Object Tagging Overview</a>.</td>
   </tr>
   <tr>
      <td>CSG</td>
      <td>Cloud Storage Gateway (CSG) is a hybrid cloud storage service provided by Tencent Cloud. You can configure a CSG instance for a bucket in COS, and then the bucket can be mounted to any of your CVM instances as a storage device in the form of a network folder. For more information, see Setting CSG.</td>
   </tr>
</table>

## Remote Disaster Recovery

<table>
   <tr>
      <th style="width: 18%;">Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td>Versioning</td>
      <td>Enabling versioning allows you to store multiple versions of an object in the same bucket. You can query, delete, or restore the objects by version ID. Versioning enables you to recover data that was lost due to accidental deletion or application failure. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/19883">Versioning Overview</a>.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Cross-bucket replication</td>
      <td>By configuring a cross-bucket replication rule, incremental objects can be automatically and asynchronously replicated between buckets for disaster recovery and data backup. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/19237">Cross-Bucket Replication Overview</a>.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Multi-AZ</td>
      <td>MAZ refers to the multi-AZ storage architecture offered by COS, which can provide IDC-level disaster recovery capabilities for your data. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/35208">Overview of Multi-AZ Feature</a>.</td>
   </tr>
</table>


## Data Security

<table>
   <tr>
      <th style="width: 18%;">Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td>Encryption</td>
      <td>COS can apply an object-level encryption policy to your data before it is written to the disk, and automatically decrypt it when it is accessed. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/18145">Server-Side Encryption Overview</a> and <a href="https://intl.cloud.tencent.com/document/product/436/33457">Bucket Encryption Overview</a>.</td>
   </tr>
   <tr>
      <td>Hotlink protection</td>
      <td>COS supports configuring hotlink protection. You can configure a blocklist/allowlist through the hotlink protection feature on the console to protect your data resources. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/32466">Hotlink Protection Practice</a>.</td>
   </tr>
</table>

## Access Management

<table>
   <tr>
      <th style="width: 18%;">Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td>Cross-Origin Access</td>
      <td>With COS, you can set HTML5 CORS configurations to enable access among different origins. COS can respond to CORS OPTIONS requests and return specified rules to the browser as configured by the developer. For detailed directions, see <a href="https://intl.cloud.tencent.com/document/product/436/13318">Setting CORS</a>.</td>
   </tr>
   <tr>
      <td>Origin-pull</td>
      <td>COS allows you to set an origin-pull rule on your bucket so that it can pull data from an external origin if the requested object does not exist in your bucket, or a specific request needs to be redirected. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/31508">Setting Origin-Pull</a>.</td>
   </tr>
   <tr>
      <td>Bucket policy</td>
      <td>You can add a policy to a bucket to grant or deny an account or source IP (or IP range) access permission for a COS resource. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/30927">Adding Bucket Policies</a>.</td>
   </tr>
   <tr>
      <td>Access control</td>
      <td>You can manage the access permissions for your buckets and objects by configuring an Access Control List (ACL). When receiving a resource request, COS will check the ACL to determine whether the requester has the required access permission. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/30581">Basic Concepts of Access Control</a> and <a href="https://intl.cloud.tencent.com/document/product/436/11714">Granting Sub-accounts Access to COS</a>.</td>
   </tr>
</table>

## Access Speed

<table>
   <tr>
      <th style="width: 18%;">Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td>CDN Acceleration</td>
      <td>COS has integrated the CDN acceleration feature to download and distribute large amounts of data from COS buckets. It is most useful in scenarios where the same data is downloaded repeatedly. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/18669">CDN Acceleration Overview</a>.</td>
   </tr>
   <tr>
      <td>Global acceleration</td>
      <td>The COS global acceleration feature can help you quickly access your buckets and improve your access success rate, further improving business stability as well as the overall user experience. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/33409">Global Acceleration Overview</a>.</td>
   </tr>
   <tr>
      <td>Single-connection bandwidth limit</td>
      <td>COS allows setting a bandwidth limit on uploads and downloads to ensure sufficient bandwidth for your other applications. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/34072">Single-Connection Bandwidth Limit</a>.</td>
   </tr>
</table>

## Batch Job Processing

<table>
   <tr>
      <th style="width: 18%;">Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Batch operation</td>
      <td>You can specify an operation to be performed on a specified list of objects in a bucket. This involves generating an inventory of objects through the inventory feature to serve as the specified object list, or you can record the objects to be processed in a CSV file according to inventory file formatting requirements. Then, COS will perform the specified batch operation on the objects in the inventory file. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/32958">Overview</a>.</td>
   </tr>
</table>

## Data Monitoring and alarms

<table>
   <tr>
      <th style="width: 18%;">Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td>Dashboard</td>
      <td>COS supports data monitoring, with which you can view the amount of data stored in different storage classes by different periods, as well as the trends. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/36542">Dashboard</a> and <a href="https://intl.cloud.tencent.com/document/product/436/31634">Querying Monitoring Data.</a></td>
   </tr>
   <tr>
      <td>Setting alarm policies</td>
      <td>You can leverage the alarm policy feature of Cloud Monitor to set threshold-reaching alarms for COS monitoring metrics. An alarm policy must include the policy name, policy type, trigger condition, alarm object, and alarm notification template. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/39104">Setting Alarm Polices</a>.</td>
   </tr>
</table>

## Data Processing

<table>
   <tr>
      <th style="width: 18%;">Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Image processing</td>
      <td>COS is integrated with Cloud Infinite professional integrated media solution to offer various features such as image processing, moderation, and recognition. You can process media data through the upload and processing APIs of COS. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/35280">Image Processing Overview</a>. In addition, COS supports image advanced compression and blind watermarking. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/40115">Overview on Image Advanced Compression</a> and <a href="https://intl.cloud.tencent.com/document/product/436/46325">Blind Watermarking Overview</a>.</td>
   </tr>
   <tr>
      <td>Media processing</td>
      <td>Media processing is a multimedia file processing service provided by COS based on CI. It offers diverse features empowered by Tencent Cloud's cutting-edge AI technology, such as audio/video transcoding, video frame capturing, audio/video splicing, video-to-animated image conversion, video metadata query, and intelligent thumbnail. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/48303">Media Processing Overview</a> and <a href="https://intl.cloud.tencent.com/document/product/436/46387">Overview</a>.</td>
   </tr>
   <tr>
      <td>File processing</td>
      <td>File processing is a processing service provided by COS based on CI for all formats of files. Currently, it provides file hash calculation, file decompression and multi-file zipping capabilities. For details, see <a href="https://www.tencentcloud.com/document/product/436/54156">File Processing Overview</a>.</td>
   </tr>
   <tr>
      <td>Document preview</td>
      <td>Document preview is based on CI. After it is enabled, document files in buckets can be previewed online directly without download. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/49159">Document Preview Overview</a>.</td>
   </tr>
   <tr>
      <td>Smart audio</td>
      <td>Smart audio is based on CI. After it is enabled, you can perform operations such as text to speech, speech recognition, and audio noise reduction. For more information, see Smart Audio Overview.</td>
   </tr>

   <tr>
      <td>Function calculation</td>
      <td>COS supports CDN Purge Cache for specified buckets. For more information, see <a href="https://www.tencentcloud.com/document/product/436/38137">Function Calculation</a>.</td>
   </tr>
	 
	 
</table>

## Data Moderation

<table>
   <tr>
      <th style="width: 18%;">Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td>Content moderation</td>
      <td>The COS content moderation service intelligently moderates the multimedia content of images, videos, speeches, text, documents, and webpages. It helps you effectively identify non-compliant content such as pornographic, vulgar, violent, terrorist, illegal, disgusting, and offensive information to avoid operational risks. For more information, see Content Moderation Overview.</td>
   </tr>
</table>

## Application Integration

<table>
   <tr>
      <th style="width: 18%;">Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Integration with other Tencent Cloud services</td>
      <td>Based on Serverless Cloud Function (SCF), COS provides database backup, message backup, log backup, log analysis, and data export features. For more information, see <a href="https://www.tencentcloud.com/document/product/436/39924">Application Integration</a>.</td>
   </tr>
</table>

## Tools

<table>
   <tr>
      <th style="width: 18%;">Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Management tools</td>
      <td>COS provides a suite of tools such as COSBrowser, COSCMD, COSCLI, and COS Migration to help manage and/or migrate data. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/6242">Tool Overview</a>.</td>
   </tr>
</table>

## APIs/SDKs

<table>
   <tr>
      <th style="width: 18%;">Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td nowrap="nowrap">APIs and SDKs</td>
      <td><ul  style="margin: 0;"><li>APIs: COS provides a rich set of APIs and API-specific documentation that describes API usage, parameters, sample requests, responses, and error codes. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/10111">Operation List</a>.</li><li>SDKs: COS offers SDKs for various programming languages, including Android, C, C++, .NET(C#), Flutter, Go, iOS, Java, JavaScript, Node.js, PHP, Python, and Weixin Mini Programs. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/6474">SDK Overview</a>.</li></ul></td>
   </tr>
</table>

## Supported Protocols

<table>
   <tr>
      <th style="width: 18%;">Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td>Various protocols</td>
      <td>COS supports HTTP 1.0, HTTP 1.1, and QUIC transfer protocols. It also supports TLS 1.0, TLS 1.1, and TLS 1.2 encryption protocols. To try the QUIC protocol, <a href="https://intl.cloud.tencent.com/contact-sales">contact us</a> to add your account to the allowlist.</td>
   </tr>
</table>


