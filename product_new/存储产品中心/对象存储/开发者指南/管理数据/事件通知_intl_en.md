## Overview

When COS resources change (such as new file uploaded or files deleted), you will receive notification messages in a timely manner. Event notification can be used together with [SCF](https://intl.cloud.tencent.com/product/scf) to meet the needs of more application scenarios:

- **Product linkage**: For example, when a new file is uploaded to COS, [the CDN cache can be automatically purged](https://intl.cloud.tencent.com/document/product/436/30611); after a new file is uploaded to COS, the database can be automatically updated.
- **System integration**: Your own service APIs can be called when files in COS are created, deleted, or overwritten. In user-generated content scenarios, you can implement the linkage between mobile devices and servers based on the event notification feature.
- **Data processing**: Files in COS can be automatically processed, such as automatic decompression and AI recognition.
  ![COS event notification](https://main.qcloudimg.com/raw/4c6a24712462cd5a263f202d21ac18f5.png)

COS event notification has the following characteristics:

- Async processing: Sending notifications does not affect normal COS operations.
- Notification targets: Notifications can only be sent to SCF functions in the same region.

Currently, the following COS events are supported:

<table>
   <tr>
      <th>Event Type</th>
      <th>Description</th>
   </tr>
   <tr>
      <td>cos: ObjectCreated:*</td>
      <td>All upload events mentioned below can trigger the function</td>
   </tr>
   <tr>
      <td>cos: ObjectCreated:Put</td>
      <td>The function will be triggered when a file is created using the Put Object API</td>
   </tr>
   <tr>
      <td>cos: ObjectCreated:Post</td>
      <td>The function will be triggered when a file is created using the Post Object API</td>
   </tr>
   <tr>
      <td>cos: ObjectCreated:Copy</td>
      <td>The function will be triggered when a file is created using the Put Object - Copy API</td>
   </tr>
   <tr>
      <td nowrap="nowrap">cos: ObjectCreated:CompleteMultipartUpload</td>
      <td>The function will be triggered when a file is created using the CompleteMultipartUploadt API</td>
   </tr>
   <tr>
      <td>cos: ObjectRemove:*</td>
      <td>All deletion events mentioned below can trigger the function</td>
   </tr>
   <tr>
      <td>cos: ObjectRemove:Delete</td>
      <td>The function will be triggered when an object in a bucket for which versioning is not enabled is deleted using the Delete Object API, or an object with a specified version is deleted using `versionid`</td>
   </tr>
   <tr>
      <td nowrap="nowrap">cos: ObjectRemove:DeleteMarkerCreated</td>
      <td>The function will be triggered when an object in a bucket for which versioning is enabled or suspended is deleted using the Delete Object API</td>
   </tr>
</table>

## How to Use COS Event Notification

COS event notification can be used in the following steps:

1. Create an SCF function
   - You can create a function in the [SCF Console](https://console.cloud.tencent.com/scf?rid=1) or on the CLI. In the process of function creating, you need to select the runtime environment (based on the language you will use to write the function) and submit the function code (which can be edited online or submitted by uploading a local code package).
   - You can also use a preset SCF template to simplify the creation process. For more information, see [Creating a Function](https://intl.cloud.tencent.com/document/product/583/19806). The function writing method varies by programming language. For more information, see the [SCF](https://intl.cloud.tencent.com/document/product/583/31458) documentation.
2. Test the function
   Once the function is created, you can use a test template to test it, which can simulate COS events and trigger the function. For more information, see [Testing a Function](https://intl.cloud.tencent.com/document/product/583/14572).
3. Add a trigger
   After the testing is completed, you can bind the SCF function to a bucket by creating a COS trigger in the console or on the command line. For more information, see [Creating a Trigger](https://intl.cloud.tencent.com/document/product/583/31441).
4. Verify
   After completing the steps above, you can manipulate the bucket in COS and verify whether the overall process is correct. For example, you can upload or delete files in the console or using the COS Browser and then go to **[SCF Console](https://console.cloud.tencent.com/scf?rid=1)** > **Function Details** > **Execution Logs** to check whether everything works properly.

For more information on SCF COS triggers, see [COS Trigger](https://intl.cloud.tencent.com/document/product/583/9707).
