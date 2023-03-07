## Background

Configuring Terraform via the backend involves the execution environment and remote state sync. Terraform introduces a lock mechanism to prevent the state from being out of sync when multiple execution environments manipulate the same backend. Different vendors can adopt Terraform's lock interface to implement their state lock. This document describes the implementation and troubleshooting of the COS backend lock.

## State Lock and File Write Lock

As indicated by the [source code](https://github.com/hashicorp/terraform/blob/v1.2.1/internal/backend/remote-state/cos/client.go#L75), the COS backend involves two locks during execution.
- State lock: It is in the form of the `terraform.tfstate.tflock` file that records the information of the current process and is written to the backend bucket.

   ``` json
   {
       "ID":"1234abcd-1234-cdef-5678-1234567890ab",
       "Operation":"OperationTypePlan",
       "Info":"",
       "Who":"UserName@Host",
       "Version":"1.3.0",
       "Created":"2006-01-02T15:04:05Z07:00",
       "Path":"terraform.tfstate.tflock"
   }
   ```
- File write lock: It prevents multiple processes from writing the `terraform.tfstate.tflock` file to the bucket at the same time. The COS backend implements the lock as a Tencent Cloud tag in the format of `tencentcloud-terraform-lock:xxxxxxxxx` (here, `xxxxxxxxx` is the MD5 of the `bucket:lockfile`), which is released automatically after the file is written successfully.


## Locking Steps

In general, running a Terraform command involves the following steps:
1. Terraform executes the command (such as `plan` or `apply).

2. The backend service adds the Tencent Cloud tag to the current account as the file write lock.

3. The bucket checks and writes `terraform.tfstate.tflock` as the state lock.

4. Delete the tag and release the file write lock.

5. Wait for Terraform to complete the execution.

6. The bucket checks and deletes `terraform.tfstate.tflock` to cancel the state lock.

7. Terraform completes the execution.


## Exception Handling

### Scenario 1

When a process is performing step 4, 5, 6, or 7 in [Locking Steps](https://www.tencentcloud.com/document/product/1172/52394) and another process tries manipulating the same backend, a lock error will be reported as follows:
``` text
╷
│ Error: Error acquiring the state lock
│ 
│ Error message: lock file terraform.tfstate.tflock exists
│ Lock Info:
│   ID:        1234abcd1234cdef56781234567890ab
│   Path:      terraform.tfstate.tflock
│   Operation: OperationTypePlan
│   Who:       UserName@Host
│   Version:   1.1.2
│   Created:   2006-01-02T15:04:05Z07:00
│   Info:      
│ 
│ 
│ Terraform acquires a state lock to protect the state from being written
│ by multiple users at the same time. Please resolve the issue above and try
│ again. For most commands, you can disable locking with the "-lock=false"
│ flag, but this is not recommended.
╵
```

At this point, other execution environments need to wait for the current process to complete. Or you can add `-lock=false` as prompted to ignore the state lock for re-execution **(not recommended)**.

At this time, if a Terraform process exits unexpectedly and does not release the state lock, you need to manually release it.
- Run the following force-unlock command by lock ID as indicated above.

   ``` html
   terraform force-unlock -force 1234abcd1234cdef56781234567890ab
   ```
- Or you can delete the `terraform.tfstate.tflock` file in the bucket to unlock.


### Scenario 2

If a process exits due to interruption when performing step 3 or 4 in [Locking Steps](https://www.tencentcloud.com/document/product/1172/52394) and does not release the tag lock, Terraform executions will lead to the exception indicating that the tag cannot be created:
``` text
│ Error: Error acquiring the state lock
│
│ Error message: 2 errors occurred:
│       * failed to create tag: tencentcloud-terraform-lock -> xxxxxxxxx: [TencentCloudSDKError] Code=ResourceInUse.TagDuplicate, Message=tagKey-tagValue have exists.,
│ RequestId=47c57b0b-2491-42cd-9f29-0b14802681e5
│       * lock file terraform/state/terraform.tfstate.tflock not exists
│
│
│
│ Terraform acquires a state lock to protect the state from being written
│ by multiple users at the same time. Please resolve the issue above and try
│ again. For most commands, you can disable locking with the "-lock=false"
│ flag, but this is not recommended.
```

At this point, Terraform has no command to release the lock, and you need to manually delete the `tencentcloud-terraform-lock:xxxxxxxxx` tag in the console or via the TencentCloud API [DeleteTags](https://www.tencentcloud.com/document/product/651/46534). Below are directions you can follow in the console:
1. Log in to the tag console and select [**Tag List**](https://console.cloud.tencent.com/tag/taglist) on the left sidebar.

2. Click **Delete** on the right of the target tag and click **OK** in the pop-up window.


   ![](https://staticintl.cloudcachetci.com/yehe/backend-news/SVDx301_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221221165754.png)
