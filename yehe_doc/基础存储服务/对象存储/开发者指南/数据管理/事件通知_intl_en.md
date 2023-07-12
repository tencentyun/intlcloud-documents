## Overview

If any change is made to COS resources (such as new files uploaded or files deleted), you will receive prompt notification. Event notification can be used together with [Serverless Cloud Function](https://intl.cloud.tencent.com/product/scf) to meet the needs of more application scenarios:

- **Interaction with other Tencent Cloud services**: For example, [purge CDN cache](https://intl.cloud.tencent.com/document/product/436/30611) or update the database when a new file is uploaded to COS.
- **System integration**: Your own service APIs can be called when files in COS are created, deleted, or overwritten. In user-generated content (UGC) scenarios, with the event notification feature, the client side will be able to interact with the server side.
- **Data processing**: Files in COS can be automatically processed, such as automatic decompression and AI recognition.
  ![COS event notification](https://main.qcloudimg.com/raw/4c6a24712462cd5a263f202d21ac18f5.png)

COS event notification has the following features:

- Async processing: sending notifications does not affect normal COS operations.
- Notification targets: notifications can only be sent to SCF functions in the same region.

Currently, the feature covers the following COS events:

<table>
   <tr>
      <th>Event Type</th>
      <th>Description</th>
   </tr>
   <tr>
      <td>cos: ObjectCreated:*</td>
      <td>All upload events mentioned below can trigger the SCF function</td>
   </tr>
   <tr>
      <td>cos: ObjectCreated:Put</td>
      <td>Creating a file via the Put Object API</td>
   </tr>
   <tr>
      <td>cos: ObjectCreated:Post</td>
      <td>Creating a file via the Post Object API</td>
   </tr>
   <tr>
      <td>cos: ObjectCreated:Copy</td>
      <td>Creating a file via the Put Object - Copy API</td>
   </tr>
   <tr>
      <td nowrap="nowrap">cos: ObjectCreated:CompleteMultipartUpload</td>
      <td>Creating a file with the CompleteMultipartUploadt API</td>
   </tr>
   <tr>
      <td nowrap="nowrap">cos:ObjectCreated:Origin</td>
      <td>Triggers the function when image origin-pull occurs</td>
   </tr>
    <tr>
      <td nowrap="nowrap">cos:ObjectCreated:Replication</td>
      <td>Triggers the function when an object is created through cross-region replication</td>
   </tr>
   <tr>
      <td>cos: ObjectRemove:*</td>
      <td>All deletion events mentioned below can trigger the SCF function</td>
   </tr>
   <tr>
      <td>cos: ObjectRemove:Delete</td>
      <td>Deleting an object via the Delete Object API or deleting an object with a specified version using `versionid` from a bucket for which versioning is not enabled</td>
   </tr>
   <tr>
      <td nowrap="nowrap">cos: ObjectRemove:DeleteMarkerCreated</td>
      <td>Deleting an object via the Delete Object API from a bucket for which versioning is enabled or suspended</td>
   </tr>
  <tr>
      <td nowrap="nowrap">cos:ObjectRestore:Post</td>
      <td>Triggers the function when an ARCHIVE restoration job is created</td>
   </tr>
    <tr>
      <td nowrap="nowrap">cos:ObjectRestore:Completed</td>
      <td>Triggers the function when an ARCHIVE restoration job is completed</td>
   </tr>
</table>

## How to Use COS Event Notification

Please follow the steps below:

1. Create an SCF function
   - You can create a function in the [SCF Console](https://console.cloud.tencent.com/scf?rid=1) or using the CLI. When creating the function, you need to select the runtime environment based on the language you will use to write the function and submit the function code either by editing online or uploading a local code package.
   - You can also use a preconfigured SCF template to simplify the creation. For more information, see [Creat a Function](https://intl.cloud.tencent.com/document/product/583/19806). The way to write the function varies by programming language. For more information, see the [SCF](https://intl.cloud.tencent.com/document/product/583/31458) documentation.
2. Test the function
   Once a function is created, you can test it with a test template which can simulate COS events and trigger the function. For more information, see [Testing a Function](https://intl.cloud.tencent.com/document/product/583/14572).
3. Add a trigger
   After you finish the testing, you can bind the SCF function with a bucket by creating a COS trigger in the console or using the command line. For more information, see [Creating a Trigger](https://intl.cloud.tencent.com/document/product/583/31441).
4. Check if the function works
   After completing the steps above, you can make changes to the bucket in COS to see if everything works. For example, you can upload or delete files in the console or using the COS Browser and then go to **[SCF Console](https://console.cloud.tencent.com/scf?rid=1)** > **Function Details** > **Execution Logs** to check if everything works properly.

For more information on SCF COS triggers, see [COS Trigger](https://intl.cloud.tencent.com/document/product/583/9707).

