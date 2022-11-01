COS offers the following features:

## Operations

<table>
   <tr>
      <th style="width: 18%;">Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Bucket operations</td>
      <td>With COS, you can create, query, delete, and empty buckets. For detailed directions, see <a href="https://intl.cloud.tencent.com/document/product/436/13309">Creating Bucket</a>.</td>
   </tr>
   <tr>
      <td>Object operations</td>
      <td>Storage classes. You can choose a storage class from INTELLIGENT TIERING, STANDARD, STANDARD_IA, ARCHIVE, or DEEP ARCHIVE provided by COS according to the access frequency and disaster recovery degree of your objects. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/30925">Overview</a>.<br>Objects/Folders: Can be uploaded, queried, downloaded, copied, and deleted. For detailed directions, see <a href="https://intl.cloud.tencent.com/document/product/436/13321">Uploading Objects</a>.</td>
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
      <td>With COS, you can set rules that will allow you to automatically delete an object or transition it between storage classes after a specified number of days. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/17028">Lifecycle Overview</a>.</td>
   </tr>
   <tr>
      <td>Static website</td>
      <td>You can configure a bucket to host a static website and access the static website through the bucket's endpoint. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/30958">Static Website Hosting</a>.</td>
   </tr>
   <tr>
      <td>Inventory</td>
      <td>COS allows you to configure an inventory job to regularly scan your bucket for specified objects or objects with the same prefix. You can perform these jobs daily or weekly, and each job will output an inventory report, which is stored in the specified bucket as a CSV file. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/30622">Inventory Overview</a>.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Bucket tagging</td>
      <td>A bucket tag can be used for easier bucket grouping and management. You can set, query, and delete tags for a specified bucket. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/31509">Bucket Tag Overview</a>.</td>
   </tr>
   <tr>
      <td>Event notification</td>
      <td>Used in conjunction with the Serverless Cloud Function (SCF), COS can send you timely notifications about resource changes (such as new file upload and file deletion). For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/31648">Event Notifications</a>.</td>
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
      <td>Object tagging</td>
      <td>This feature is designed to help group and manage objects in your bucket by adding a key-value pair as an object tag. An object tag consists of a `tagKey`, an equal sign `=`, and a `tagValue`, for example, `group = IT`. You can set, query, and delete tags for a specified object. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/35665">Object Tag Overview</a>.</td>
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
      <td>Enabling versioning allows you to store multiple versions of an object in the same bucket. You can query, delete, or restore the objects by version ID. Versioning enables you to recover data that was lost due to accidental deletion or application failure. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/19883">Overview</a>.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Cross-bucket replication</td>
      <td>By configuring a cross-bucket replication rule, incremental objects can be automatically and asynchronously replicated between buckets for disaster recovery and data backup. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/19237">Overview</a>.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Cloud database backup</td>
      <td>Cloud database backup is a database backup feature provided by COS based on SCF. It helps you transfer backup files in TencentDB to COS for persistent storage to avoid data loss or corruption. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/41112">MySQL Data Backup</a>.</td>
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
      <td>COS supports configuring hotlink protection. You can configure a blocklist/allowlist through the hotlink protection feature in the console to protect your data resources. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/32466">Hotlink Protection Practice</a>.</td>
   </tr>
</table>

## Access Management

<table>
   <tr>
      <th style="width: 18%;">Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td>CORS</td>
      <td>With COS, you can set HTML5 CORS configurations to enable access among different origins. COS can respond to CORS OPTIONS requests and return specified rules to the browser as configured by you. For detailed directions, see <a href="https://intl.cloud.tencent.com/document/product/436/13318">Setting CORS</a>.</td>
   </tr>
   <tr>
      <td>Origin-pull</td>
      <td>COS allows you to set an origin-pull rule on your bucket so that it can pull data from an external origin if the requested object does not exist in your bucket, or a specific request needs to be redirected. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/31508">Setting Origin-Pull</a>.</td>
   </tr>
   <tr>
      <td>Bucket policy</td>
      <td>You can add a policy to a bucket to grant or deny an account or source IP (or IP range) access permission for a COS resource. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/30927">Adding Bucket Policy</a>.</td>
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
      <td>CDN acceleration</td>
      <td>COS has integrated the CDN acceleration feature to download and deliver large amounts of data from COS buckets. It is most useful in scenarios where the same data is downloaded repeatedly. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/18669">CDN Acceleration Overview</a>.</td>
   </tr>
   <tr>
      <td>Global acceleration</td>
      <td>The COS global acceleration feature can help you quickly access your buckets and improve your access success rate, further improving business stability as well as the overall user experience. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/33409">Overview</a>.</td>
   </tr>
   <tr>
      <td>Single-connection bandwidth limit</td>
      <td>COS supports traffic control for file uploads and downloads to guarantee a normal network bandwidth for your other applications. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/34072">Single-Connection Bandwidth Limit</a>.</td>
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

## Data Monitoring

<table>
   <tr>
      <th style="width: 18%;">Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td>Monitoring and alarms</td>
      <td>COS statistics such as read and write requests and traffic are collected and displayed based on <a href="https://www.tencentcloud.com/document/product/248">CM</a>. You can view detailed monitoring data of COS in the <a href="https://console.cloud.tencent.com/monitor/product/COS">CM console</a>. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/31649">Monitoring and Alarms</a>.</td>
   </tr>
   <tr>
      <td>Dashboard</td>
      <td>COS supports data monitoring, with which you can view the amount of data stored in different storage classes by different periods, as well as the trends. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/36542">Viewing Statistics</a> and <a href="https://intl.cloud.tencent.com/document/product/436/31634">Querying Monitoring Data</a>.</td>
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
      <td>COS is integrated with Cloud Infinite professional integrated media solution to offer various features such as image processing, moderation, and recognition. You can process media data through the upload and processing APIs of COS. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/35280">Image Processing Overview</a>. In addition, COS supports image advanced compression and blind watermarking. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/40115">Image Compression Overview</a> and <a href="https://intl.cloud.tencent.com/document/product/436/46325">Blind Watermarking Overview</a>.</td>
   </tr>
   <tr>
      <td>File preview</td>
      <td>File preview is based on CI. After it is enabled, document files in buckets can be previewed online directly without download. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/49159">File Preview Overview</a>.</td>
   </tr>
   <tr>
      <td>Media processing</td>
      <td>Media processing is a multimedia file processing service provided by COS based on CI. It offers diverse features empowered by Tencent Cloud's cutting-edge AI technology, such as audio/video transcoding, video frame capturing, audio/video splicing, video-to-animated image conversion, video metadata query, and intelligent thumbnail. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/48303">Media Processing Overview</a> and <a href="https://intl.cloud.tencent.com/document/product/436/46387">Overview</a>.</td>
   </tr>
   <tr>
      <td>Speech recognition</td>
      <td>Speech recognition is based on CI. Once enabled, it recognizes recording files in buckets and asynchronously returns recognized text. For more information, see Speech Recognition Overview.</td>
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
      <td>The COS content moderation service intelligently moderates the multimedia content of images, videos, speeches, and text. It helps you effectively identify non-compliant content such as pornographic, vulgar, violent, terrorist, illegal, disgusting, and offensive information to avoid operational risks. For more information, see Content Moderation Overview.</td>
   </tr>
</table>

## Application Integration

<table>
   <tr>
      <th style="width: 18%;">Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td>CKafka message backup</td>
      <td>CKafka message backup is provided by COS based on SCF to dump CKafka messages to COS, which facilitates data analysis and download. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/39926">CKafka Message Backup</a>.</td>
   </tr>
   <tr>
      <td>TDMQ message backup</td>
      <td>TDMQ message backup is provided by COS based on SCF to dump TDMQ messages to COS, which facilitates data analysis and download. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/40541">TDMQ Message Backup</a>.</td>
   </tr>
   <tr>
      <td>CDN log backup</td>
      <td>The CDN log backup feature is provided by COS based on SCF to dump CDN logs to COS, which facilitates access behavior analysis and service quality monitoring. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/40485">CDN Log Backup</a>.</td>
   </tr>
   <tr>
      <td>Log cleansing</td>
      <td>Log cleansing is a log file processing solution provided by COS based on SCF. After it is enabled or you upload log files on your own, the function preconfigured by COS will be automatically triggered to filter and cleanse log content according to the preset SQL search statements. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/39925">Log Cleansing</a>.</td>
   </tr>
   <tr>
      <td>File decompression</td>
      <td>The file decompression feature is a data processing solution provided through SCF. Once enabled, when a compressed file is uploaded to COS, SCF will be triggered automatically to decompress the file into the specified directory and bucket. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/35663">Setting File Decompression</a>.</td>
   </tr>
   <tr>
      <td>CDN cache purging</td>
      <td>This COS feature is provided through SCF to help you automatically purge data that is cached on CDN edge nodes. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/37273">Setting CDN Cache Purge</a>.</td>
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
      <td>COS provides a suite of tools such as COSBrowser, COSCMD, and COS Migration to help manage and/or migrate data. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/6242">Tool Overview</a>.</td>
   </tr>
</table>

## API/SDK

<table>
   <tr>
      <th style="width: 18%;">Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td nowrap="nowrap">APIs and SDKs</td>
      <td><ul  style="margin: 0;"><li>APIs: COS provides a rich set of APIs and API-specific documentation that describes API usage, parameters, sample requests, responses, and error codes. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/10111">Operation List</a>.</li><li>SDKs: COS offers SDKs for various programming languages, including Android, C, C++, .NET, Go, iOS, Java, JavaScript, Node.js, PHP, Python, and WeChat Mini Programs. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/6474">SDK Overview</a>.</li></ul></td>
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
      <td>COS supports HTTP 1.0, HTTP 1.1 transfer protocols. It also supports TLS 1.0, TLS 1.1, and TLS 1.2 encryption protocols.  </td>
   </tr>
</table>
