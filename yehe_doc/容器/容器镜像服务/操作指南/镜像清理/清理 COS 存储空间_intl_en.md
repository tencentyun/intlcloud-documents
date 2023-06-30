## Overview
TCR allows users to set up rules to remove unused image tags of the Enterprise Edition instances in batch. However, after you delete the image tags, the image data stored in the COS bucket associated with the instance still exists. You can use the garbage collection feature to delete the invalid image tag data in COS bucket to release the occupied storage capacity, and reduce the storage costs. This document describes how to use the garbage collection feature to release the occupied storage capacity of a COS bucket.

## Notes

The garbage collection will affect the instance service status and the data in the instance. Please note the following points:
- During garbage collection, the instance becomes read-only. You can pull images from the image repositories, but cannot push images to image repositories.
- The garbage collection task will clean up the image layer data in all image repositories of the instance that is no longer associated with valid image tags. The deletion operation is irreversible. We recommend that you perform a dry run to evaluate the impacts before performing the garbage collection.
- The time required for the garbage collection task depends on the image data size stored in the COS bucket and the number of historical image tags. The temporary suspension of tasks is not supported. We recommend that you perform the garbage collection tasks during non-business time, or perform a dry run to estimate the required time.

## Directions
### Dry run
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Garbage Collection** in the left sidebar.
2. On the **Garbage Collection** page, you can view the garbage collection tasks of the current instance. To change the instance, select the desired instance name from the **Instance Name** drop-down list at the top of the page.
3. Click **Dry Run** and read the note.
<dx-alert infotype="notice" title="">
In a dry run, the instance is fully scanned for unused data. You can estimate the cleanup range and the required time. During the dry run, the instance's basic features are not affected. You can still pull and push the images. However, the intensive computing tasks of the cleanup may affect the speed of image pulling and push.
</dx-alert>
4. Click **Confirm** to execute the dry run.
 
### Running garbage collection
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Garbage Collection** in the left sidebar.
2. On the **Garbage Collection** page, you can view the garbage collection tasks of the current instance. To change the instance, select the desired instance name from the **Instance Name** drop-down list at the top of the page.
3. Click **Run Garbage Collection** and read the note.
<dx-alert infotype="notice" title="">
During garbage collection, the instance becomes read-only. You can pull images from it, but not push images to it. The time required for the job depends on the data size and usage duration of the instance.
</dx-alert>
4. Click **Confirm** to run the garbage collection.


