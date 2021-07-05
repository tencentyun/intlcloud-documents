### How can I restore archived objects to STANDARD in batches? 

You can do so as follows:

1. Enable the [Inventory](https://intl.cloud.tencent.com/document/product/436/30622) feature. Then, generate an inventory file for objects that need to be restored to STANDARD, and wait for the inventory file to be generated.
2. Create a task that restores archived objects in batches. When configuring the task, select the inventory file and set the copies’ effective period (e.g., 7 days). For detailed directions, please see [Batch Operation](https://intl.cloud.tencent.com/document/product/436/34075).
3. As the data volume is large, the restoration may take a long time. You can wait for 48 hours after the task is created for the restoration to complete. After this, you can generate and download the inventory for filtering. You need to remove STANDARD objects in the inventory file and keep only the archived objects. Then, upload the modified inventory file to COS.
4. Create a batch replication task. When configuring the task, select the newly uploaded inventory file, set the storage class to STANDARD, and wait for the task to complete.

### Does COS have the batch compression feature?

Currently, COS does not support batch compression. You can use SCF to add a file decompression rule for a bucket to automatically decompress files to a specified bucket and path. For more information, please see [File Decompression](https://intl.cloud.tencent.com/document/product/436/35663).

### How can I obtain the inventory file for the batch operation task?

You can obtain the inventory file in either of the following ways:
- Use [COS’s Inventory feature](https://intl.cloud.tencent.com/document/product/436/30624) to generate an inventory file. Once the inventory file is generated, you can go to the bucket to pull the `manifest.json` file.
- Save files that need to be processed in a local `CSV` file and then upload it to COS. Fields required are shown below. For more information, please see [Inventory Overview](https://intl.cloud.tencent.com/document/product/436/30622).
```plaintext
Bucket,Key,VersionId
examplebucket-1250000000,testFile.txt,testVersionId
```

### Why is my data not restored after the batch archived file restoration task is completed?

After the restoration request is sent, the backend will restore files to STANDARD in sequence according to the restoration mode. However, there is a time difference. The completion message displayed in the frontend only indicates that all restoration requests are sent, but not the completion of the restoration task. You can wait for a while and then log in to the console to view the status.
