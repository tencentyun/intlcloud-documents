COS offers the following features:

<table>
   <tr>
      <th colspan=2>Features</td>
      <th>Description</td>
   </tr>
   <tr>
      <td rowspan=2>Operations</td>
      <td nowrap="nowrap">Bucket Operations</td>
      <td>With COS, you can create, query, delete, and empty buckets. For detailed directions, see <a href="https://intl.cloud.tencent.com/document/product/436/13309">Bucket Management.</a></td>
   </tr>
   <tr>
      <td>Object Operations</td>
      <td>Storage classes: Currently, COS offers three object storage classes for different access frequencies: STANDARD, STANDARD_IA, and ARCHIVE. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/30925">Storage Class</a><br>Objects/folders: can be uploaded, queried, downloaded, copied, and deleted. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/13321">Object Management.</a></td>
   </tr>
   <tr>
      <td rowspan=8>Data Management</td>
      <td>Lifecycle</td>
      <td>With COS, you can set rules that will allow you to automatically delete an object or transition it between storage classes after a specified number of days. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/17028">Lifecycle Overview.</a></td>
   </tr>
   <tr>
      <td>Static Website</td>
      <td>You can configure a bucket to host a static website and access the static website through the bucket's endpoint. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/30958">Static Website Hosting.</a></td>
   </tr>
   <tr>
      <td>Inventory</td>
      <td>COS allows you to configure an inventory task to regularly scan your bucket for specified objects or objects with the same prefix. You can perform these tasks daily or weekly, and each task will output an inventory report, which is stored in the specified bucket as a CSV file. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/30622">Inventory Overview.</a></td>
   </tr>
   <tr>
      <td nowrap="nowrap">Bucket Tagging</td>
      <td>A bucket tag can be used as an identifier for easier bucket grouping and management. You can set, query, and delete tags for a specified bucket. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/31509">Bucket Tag Overview.</a></td>
   </tr>
   <tr>
      <td>Event Notification</td>
      <td>Used in conjunction with the Serverless Cloud Function (SCF), COS can send you timely notifications about resource changes (such as when a new file has been uploaded or deleted). For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/31648">Event Notifications.</a></td>
   </tr>
   <tr>
      <td>COS Select</td>
      <td>This feature uses Structured Query Language (SQL) statements to filter the objects stored in COS so as to extract specific objects and get desired data. With COS Select, you can reduce the amount of data transferred by COS for lower costs and latency during data extraction. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/32472">SELECT Overview.</a></td>
   </tr>
   <tr>
      <td>Logging</td>
      <td>This feature is used to log the access details of a source bucket; these logs are then stored in a destination bucket for better bucket management. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/16920">Logging Overview.</a></td>
   </tr>
   <tr>
      <td>Object Tagging</td>
      <td>This feature is designed to help you group and manage objects in your bucket by adding a key-value pair as an object identifier. An object tag consists of a `tagKey`, an equal sign `=`, and a `tagValue`, such as `group = IT`. You can set, query and delete tags for a specified object. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/35665">Object Tagging Overview.</a></td>
   </tr>
   <tr>
      <td rowspan=2>Remote Disaster Recovery</td>
      <td>Versioning</td>
      <td>Enabling versioning allows you to store multiple versions of an object in the same bucket. You can query, delete, or restore the objects by version ID. Versioning enables you to recover data that was lost due to accidental deletion or application failure. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/19883">Versioning Overview.</a></td>
   </tr>
   <tr>
      <td nowrap="nowrap">Cross-Region Replication</td>
      <td>By configuring a cross-region replication rule, incremental objects can be automatically and asynchronously replicated between buckets in different regions for remote disaster recovery and data backup purposes. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/19237">Cross-region Replication Overview.</a></td>
   </tr>
   <tr>
      <td rowspan=2>Data Security</td>
      <td>Encryption</td>
      <td>COS encrypts your data at the object level before it is written to IDC disks and automatically decrypts it when accessed. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/18145">Server-side Encryption Overview.</a></td>
   </tr>
   <tr>
      <td>Hotlink Protection</td>
      <td>COS supports configuring hotlink protection. You can configure a blocklist/allowlist through the hotlink protection feature on the console to protect your data resources. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/32466">Hotlink Protection Practice.</a></td>
   </tr>
   <tr>
      <td rowspan=5>Access Management</td>
      <td>Cross-Origin Access</td>
      <td>With COS, you can set HTML5 CORS configurations to enable access among different origins. COS can respond to CORS OPTIONS requests and return specified rules to the browser as configured by the developer. For detailed directions, see <a href="https://intl.cloud.tencent.com/document/product/436/13318">Setting CORS.</a></td>
   </tr>
   <tr>
      <td>Bucket Policy</td>
      <td>You can add a policy to a bucket to grant or deny an account or source IP (or IP range) access permission for a COS resource. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/30927">Adding Bucket Policies.</a></td>
   </tr>
   <tr>
      <td>Access Control</td>
      <td>You can manage the access permissions for your buckets and objects by configuring an Access Control List (ACL). When receiving a resource request, COS will check the ACL of the bucket/object to determine whether the requester has the required access permission. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/30581">Concepts</a> and <a href="https://intl.cloud.tencent.com/document/product/436/11714">Granting Sub-accounts Access to COS.</a> </td>
   </tr>
   <tr>
      <td>CDN Acceleration</td>
      <td>COS has integrated the CDN acceleration feature to download and distribute large amounts of data from COS buckets. It is most useful in scenarios where the same data is downloaded repeatedly. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/18669">CDN Acceleration Overview</a></td>
   </tr>
   <tr>
      <td>Global Acceleration</td>
      <td>The COS global acceleration feature can help you quickly access your buckets and improve your access success rate, further improving business stability as well as the overall user experience. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/33409">Global Acceleration Overview.</a></td>
   </tr>
   <tr>
      <td>Batch Jobs</td>
      <td nowrap="nowrap">Batch Operations</td>
      <td>You can specify an operation to be performed for a specified list of objects in a bucket. This involves generating an inventory of objects through the inventory feature to serve as the specified object list, or you can record the objects to be processed in a CSV file according to inventory file formatting requirements. Then, COS will perform the specified batch operation on the objects in the inventory file. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/32958">Batch Processing Overview.</a></td>
   </tr>
   <tr>
      <td rowspan=2>Data Monitoring</td>
      <td>Monitoring and Alarming</td>
      <td>COS data such as read/write requests and traffic are collected and displayed on the <a href="https://intl.cloud.tencent.com/document/product/248">Cloud Monitor</a>. You can view COS monitoring details on the Cloud Monitor <a href="https://console.cloud.tencent.com/monitor/product/COS">console</a>. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/31649">Monitoring and Alarming.</a></td>
   </tr>
   <tr>
      <td>Dashboard</td>
      <td>The COS console features a Dashboard monitoring window where you can see the amount of storage data for different storage classes over different periods as well as associated trends. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/36542">Dashboard</a></td>
   </tr>
   <tr>
      <td rowspan=4>Data Processing</td>
      <td nowrap="nowrap">Image Processing</td>
      <td>COS has integrated the professional all-in-one media solution, Cloud Infinite (CI), to perform image processing, content moderation, detection, and many more services. You can use the COS upload and process APIs to process media data. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/35280">Image Processing Overview.</a></td>
   </tr>
   <tr>
      <td>Content Moderation</td>
      <td>This COS feature is provided based on Tencent Cloud CI. Once enabled, newly uploaded images will be automatically detected for content violations, with any non-compliant content blocked automatically (allowing no public read access).</td>
   </tr>
   <tr>
      <td>File Decompression</td>
      <td>The file decompression feature is a data processing solution provided through SCF. Once enabled, when a compressed file is uploaded to COS, SCF will be triggered automatically to decompress the file into the specified directory and bucket. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/35663"> File Decompression.</a></td>
   </tr>
   <tr>
      <td>CDN Cache Purging</td>
      <td>This COS feature is provided through SCF to help you automatically purge data that is cached on CDN edge servers. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/37273"> CDN Cache Purging.</a></td>
   </tr>
   <tr>
      <td>Tools</td>
      <td nowrap="nowrap">Management Tools</td>
      <td>COS provides a suite of practical tools such as COSBrowser, COSCMD, and COS Migration to help manage and/or migrate data. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/6242">Tools Overview.</a></td>
   </tr>
   <tr>
      <td>APIs/SDKs</td>
      <td nowrap="nowrap">APIs & SDKs</td>
      <td><li>APIs: COS provides a rich set of APIs and API-specific documentation that describes API usage, parameters, sample requests, responses, and error codes. For more information, see <a href="https://cloud.tencent.com/document/product/436/10111">Operation List</a><br><li>SDKs: COS offers SDKs for various programming languages, including Android, C, C++, .NET, Go, iOS, Java, JavaScript, Node.js, PHP, Python, and WeChat Mini Programs. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/6474">SDK Overview.</a></td>
   </tr>
</table>
