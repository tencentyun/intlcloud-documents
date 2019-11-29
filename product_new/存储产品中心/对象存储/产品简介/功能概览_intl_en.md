COS offers the following capabilities:

<table>
   <tr>
      <th colspan=2>Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td rowspan=2>Operation</td>
      <td nowrap="nowrap">Bucket operations</td>
      <td>Buckets can be created, queried, deleted, and emptied. For specific operations, please see the documents under <a href="https://intl.cloud.tencent.com/document/product/436/13309">Managing Bucket</a></td>
   </tr>
   <tr>
      <td>Object operations</td>
      <td>Multiple storage classes: COS offers three object storage classes for different access frequencies: standard storage, standard_IA storage, and archive storage. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/30925">Storage Class</a><br>Objects/folders can be uploaded, queried, downloaded, copied, and deleted. For more information, please see the documents under <a href="https://intl.cloud.tencent.com/document/product/436/13321">Managing Object</a></td>
   </tr>
   <tr>
      <td rowspan=8>Data management</td>
      <td>Lifecycle</td>
      <td>COS supports setting rules to automatically delete or transition the specified objects after a certain period of time (days). For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/17028">Lifecycle Overview</a></td>
   </tr>
   <tr>
      <td>Static website</td>
      <td>You can configure a bucket as a hosted static website and access the static website through the bucket's domain name. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/30958">Static Website Hosting</a></td>
   </tr>
   <tr>
      <td>Inventory</td>
      <td>COS can be configured according to your inventory task to regularly scan the specified objects or objects with the same object prefix in your bucket daily or weekly and output an inventory report, which is stored in the specified bucket as a CSV file. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/30622">Inventory Overview</a></td>
   </tr>
   <tr>
      <td nowrap="nowrap">Bucket tag</td>
      <td>A bucket tag can be used as an identifier for easier bucket grouping and management. You can set, query, and delete tags for the specified bucket. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/31509">Bucket Tag Overview</a></td>
   </tr>
   <tr>
      <td>Event notification</td>
      <td>Together with Serverless Cloud Function (SCF), when COS resources change (such as new file uploaded or files deleted), you will receive notification messages timely. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/31648">Event Notification</a></td>
   </tr>
   <tr>
      <td>Data extraction</td>
      <td>The COS Select feature uses Structured Query Language (SQL) statements to filter the objects stored in COS so as to extract a specific object and get the desired data. By filtering object data using this feature, you can reduce the amount of data transferred by COS, which helps lower the costs and delay in data extraction. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/32472">SELECT Overview</a></td>
   </tr>
   <tr>
      <td>Log management</td>
      <td>The log management feature is used to record the detailed access information of the specified source bucket and store the information in the specified bucket in the form of log files to facilitate bucket management. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/16920">Log Management Overview</a></td>
   </tr>
   <tr>
      <td>Monitoring and alarming</td>
      <td>COS statistics such as read and write requests and traffic are collected and displayed based on <a href="https://intl.cloud.tencent.com/doc/product/248">Cloud Monitor</a>. You can view detailed monitoring data of COS in the Cloud Monitor <a href="https://console.cloud.tencent.com/monitor/product/COS">Console</a>. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/31649">Monitoring and Alarming</a></td>
   </tr>
   <tr>
      <td rowspan=2>Remote disaster recovery</td>
      <td>Versioning</td>
      <td>By enabling versioning, you can store multiple versions of an object in the same bucket. You can query, delete, or restore the objects by version ID. Versioning enables you to recover data that was lost due to accidental deletion or application failure. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/19883">Versioning Overview</a></td>
   </tr>
   <tr>
      <td nowrap="nowrap">Cross-region replication</td>
      <td>By configuring a cross-region replication rule, incremental objects can be automatically and asynchronously replicated between buckets in different regions for remote disaster recovery and backup of data. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/19237">Cross-region Replication Overview</a></td>
   </tr>
   <tr>
      <td rowspan=2>Data security</td>
      <td>Encryption</td>
      <td>COS encrypts your data at the object level before it is written to IDC disks and automatically decrypts it when you access it. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/18145">Server-side Encryption Overview</a></td>
   </tr>
   <tr>
      <td>Hotlink protection</td>
      <td>COS supports configuring hotlink protection. You can configure a blacklist/whitelist through the hotlink protection feature in the console to protect your data resources. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/32466">Hotlink Protection Practice</a></td>
   </tr>
   <tr>
      <td rowspan=4>Access management</td>
      <td>Cross-origin access</td>
      <td>COS provides cross-origin access settings in the HTML5 standard to help implement cross-origin access. For cross-origin access, COS supports responding to OPTIONS requests and returning specific settings to the browser according to the rule you set. For detailed directions, please see <a href="https://intl.cloud.tencent.com/document/product/436/11488">Setting Cross-origin Access</a></td>
   </tr>
   <tr>
      <td>Bucket policy</td>
      <td>You can add a policy to a bucket to allow or forbid an account, IP, or IP range to access COS resources. For detailed directions, please see <a href="https://intl.cloud.tencent.com/document/product/436/30927">Adding Bucket Policy</a></td>
   </tr>
   <tr>
      <td>Access control</td>
      <td>You can manage the access permissions to buckets and objects. When receiving a request for a resource, COS will check the corresponding ACL to verify whether the requester has the required access permission. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/30581">Basic Concepts in Access Control</a> and <a href="https://intl.cloud.tencent.com/document/product/436/11714">Granting a Sub-account Access to COS Resources</a> </td>
   </tr>
   <tr>
      <td>CDN acceleration</td>
      <td>With the aid of the CDN service, you can extensively download and distribute the contents of COS buckets, which is especially suitable for use cases where the same contents are downloaded repeatedly. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/18669">CDN Overview</a></td>
   </tr>
   <tr>
      <td>Batch operation</td>
      <td nowrap="nowrap">Batch operation</td>
      <td>You can specify an operation for the specified list of objects in a bucket. Specifically, you can generate an inventory of objects through the inventory feature as the specified object list, or record the objects to be processed in a CSV file according to the format requirement of an inventory file. Then, COS will process the objects in batches based on the object inventory file. For more information.<!--, please see <a href="https://cloud.tencent.com/document/product/436/38601">Batch Operation Overview--></a></td>
   </tr>
   <tr>
      <td>Tool</td>
      <td nowrap="nowrap">Multiple management tools</td>
      <td>COS provides a variety of practical tools such as COSBrowser, COSCMD, and COS Migration to facilitate your data management or migration. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/6242">Tool Overview</a></td>
   </tr>
   <tr>
      <td>API/SDK</td>
      <td nowrap="nowrap">Multiple APIs and SDKs</td>
      <td><li>API: COS provides a rich set of APIs that come with usage and parameter descriptions, sample requests, sample responses, and error code descriptions. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/10111">List of Operations</a><br><li>COS offers SDKs for multiple programming languages, including Android, C, C++, .Net, Go, iOS, Java, JavaScript, Node.js, PHP, Python, and WeChat Mini Program. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/6474">SDK Overview</a></td>
   </tr>
</table>
