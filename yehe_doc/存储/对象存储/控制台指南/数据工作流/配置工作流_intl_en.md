## Overview

With a data processing workflow, you can quickly and flexibly create video processing processes as needed. A workflow is bound to a path of an input bucket. When a video file is **uploaded** to the path, the media workflow will be **automatically triggered** to perform the specified processing operation, with the processing result automatically saved to the specified path of the destination bucket.

You can use a data processing workflow to implement the following features: **audio/video transcoding (including top speed codec and broadcast media format transcoding)**, **video frame capturing**, **video to animated image conversion**, **intelligent thumbnail**, **audio/video splicing**, **voice separation**, **highlights generation**, **HLS adaptive multi-bitrate**, **SDR to HDR**, **video enhancement**, **super-resolution**, **audio/video segmentation**, **custom function**, and **image processing**.

>! 
> - Currently, workflows can process 3GP, ASF, AVI, DV, FLV, F4V, M3U8, M4V, MKV, MOV, MP4, MPG, MPEG, MTS, OGG, RM, RMVB, SWF, VOB, WMV, WEBM, MP3, AAC, FLAC, AMR, M4A, WMA, and WAV files. When initiating a media processing request, you must enter the complete file name and extension; otherwise, the format cannot be recognized and processed.
> - Currently, the workflow feature can only manipulate video files being uploaded. To perform media operations on cloud data, use the [job](https://intl.cloud.tencent.com/document/product/436/46409) feature.
> 

## Directions

### Creating workflow

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Select **Bucket List** on the left sidebar.
3. Click the name of the bucket for media processing.
4. On the left sidebar, select **Data Processing Workflow** > **Workflow** to go to the workflow management page.
5. Click **Create Workflow**.
6. On the **Create Workflow** page, configure the following items:
![](https://qcloudimg.tencent-cloud.cn/raw/d9dab85ebe9c2d6a93fd7069705680de.png)
  - **Workflow Name**: It is required and can contain up to 128 letters, digits, underscores (\_), and hyphens (-).
  - **Input Bucket Name**: It is the current bucket by default.
  - **Input Path**: It is optional and must start and end with `/`. If it is not specified, the workflow will be triggered for all paths in the input bucket. After the media workflow is enabled, when a video file is uploaded to this path, the workflow will be automatically triggered.
  - **Format**: Select the default audio, video, or image file filter rule or a custom rule. You can also select all files to process all objects in the bucket.
  - **Queue**: It is required. When you activate the service, the system will automatically create a user queue for you. When you submit a job, the job will be arranged in the queue first and executed in sequence according to the priority and order of submission. You can view the queue information in **Common Configuration**.
  - **Callback**: You can use the queue callback, i.e., callback URL bound to the queue. To modify it, please go to the corresponding queue list.
  - **Configure Workflow**: Click **+** on the right to add any of the following nodes: **audio/video transcoding (including top speed codec transcoding and broadcast media format transcoding)**, **video frame capturing**, **video to animated image conversion**, **intelligent thumbnail**, **audio/video splicing**, **voice separation**, **highlights generation**, **HLS adaptive multi-bitrate**, **SDR to HDR**, **video enhancement**, **super-resolution**, **audio/video segmentation**, **custom function**, and **image processing**. You need to configure at least one job node in a workflow and set the destination bucket, filename (see [Workflow Variable Description](#1)), path, and job template for each job node. For more information on templates and how to set them, see [Template](https://intl.cloud.tencent.com/document/product/436/46411).
<dx-tabs>
::: Audio/Video transcoding
![](https://qcloudimg.tencent-cloud.cn/raw/9c1ffe4db2bdcb2fb646c4b16902dea2.png)
:::
::: Video frame capturing
![](https://qcloudimg.tencent-cloud.cn/raw/b9845a77ef297cf0d1e4db1b2b82ec99.png)
:::
::: Video to animated image conversion
![](https://qcloudimg.tencent-cloud.cn/raw/6d6b8c9ef319f7cf4040f1379861b8c7.png)
:::
::: Intelligent thumbnail
![](https://qcloudimg.tencent-cloud.cn/raw/bd8637a44913e67deade1fc5aa9a6b0b.png)
Description: The intelligent thumbnail feature understands the video content with the aid of Tencent Cloud's advanced AI technologies to intelligently extract three optimal keyframes.
:::
::: Audio/Video splicing
![](https://qcloudimg.tencent-cloud.cn/raw/448ae50e96836187010eb7591971f9dd.png)
:::
</dx-tabs>
<dx-tabs>
::: Voice separation
![](https://qcloudimg.tencent-cloud.cn/raw/212f329b9675aeff7e42c09c38d06085.png)
:::
::: Highlights generation
![](https://qcloudimg.tencent-cloud.cn/raw/f4fc4cdbd12418b9ea869ddb5bdd8013.png)
:::
::: HLS adaptive multi-bitrate
![](https://qcloudimg.tencent-cloud.cn/raw/3157803ae06a4f5270b257169e2f4d7b.png)
Description: The HLS adaptive multi-bitrate feature encapsulates multiple files with multiple bitrates and audio tracks into one multi-bitrate adaptive video file.
:::
::: SDR to HDR
![](https://qcloudimg.tencent-cloud.cn/raw/de20698b2fcbd264a866802a9cb235db.png)
:::
::: Video enhancement
![](https://qcloudimg.tencent-cloud.cn/raw/ab8e4f29c3843b83510321a57177fbc7.png)
:::
</dx-tabs>
<dx-tabs>
::: Super-resolution
![](https://qcloudimg.tencent-cloud.cn/raw/d8baeec986771fd7b80266af801f97a5.png)
:::
::: Audio/Video segmentation
![](https://qcloudimg.tencent-cloud.cn/raw/39ad428b6792bf612293f1a764276724.png)
:::
::: Custom function
![](https://main.qcloudimg.com/raw/d2720047917038d5c9682e5d6c4bf51e.png)
:::
::: Image processing
![](https://qcloudimg.tencent-cloud.cn/raw/fd2ab4c60df5733debfeac15bafc2c98.png)
:::
</dx-tabs>
7. After confirming that the configuration is correct, click **Save**.
![](https://main.qcloudimg.com/raw/d72a2ce91f802bc4c5e65b78122319b9.png)
Workflows are disabled by default. To enable a workflow, click the toggle in the **Enable** column. Once enabled, the workflow will take effect in five minutes. Then, it will automatically perform media processing operations on video files uploaded subsequently. After processing files, it will output the new generated files to the specified file path.

### Managing workflow

You can view the list of created workflows on the workflow management page.
![](https://main.qcloudimg.com/raw/b603c8a249e36230eaf1ade521df2afd.png)
The workflow list displays the names, IDs, input paths, creation times, and statuses of workflows. You can search for workflows by name and ID to view, edit, or delete specified workflows.

 - **Enable**: Once a workflow is enabled, video files uploaded to the specified path in the input bucket will be automatically processed according to the workflow configuration. You can click the toggle again to pause the workflow.
>? Workflows are disabled by default. To enable a workflow, click the toggle in the **Enable** column. Once enabled, the workflow will take effect in five minutes.
>
 - **Details**: You can view the configuration details of the current workflow.
 - **View Execution Instance**: You can view the workflow execution status and time by time.
 - **More**:   
   - Click **More** > **Edit** in the **Operation** column to enter the **Edit Workflow** page, where you can modify the workflow configuration.
   - Click **More** > **Delete** in the **Operation** column to delete the workflow.

>! You cannot edit or delete an enabled workflow.
>

### Viewing execution instance

An execution instance will be generated after a workflow is executed for each video file. The execution instance page displays the source file address, workflow execution status, and execution time.

1. Go to the workflow management page and click **View Execution Instance** in the **Operation** column of the target workflow to enter the execution instance list page.
   ![](https://main.qcloudimg.com/raw/b603c8a249e36230eaf1ade521df2afd.png)
2. On the list page, click **Details** in the **Operation** column of the target instance to enter the instance details page.
   ![](https://main.qcloudimg.com/raw/9adfdda6e20fe90c1675a0192bbe4e95.png)
3. On the instance details page, you can view the job ID, execution status, start time, and end time of each workflow node.
   ![](https://main.qcloudimg.com/raw/0c2f798838b18d708e00edb66d5c36cb.png)

### Triggering workflow

After a workflow is created, it can be automatically triggered for files uploaded to the specified bucket or manually triggered for existing files in the bucket.

1. On the workflow management page, click **More** > **Create Execution Instance** of the target workflow.
2. On the **Create Execution Instance** page, select the file for which to trigger the workflow and click **Save** to immediately trigger and execute the workflow.
   You can view the workflow execution status on the execution instance page.
   ![](https://main.qcloudimg.com/raw/d5a70bbb33c4b75f64320a4660ce245e.png)


<span id="1"></span>

## Workflow Variable Description


Workflows support rendering destination file names and URLs with the following variables:

| Variable Name | Description |
| :-------------- | :--------------------------- |
| InputName       | Filename of the input file (without file extension) |
| InputNameAndExt | Filename of the input file (with file extension)   |
| InputPath       | File input path               |
| RunId           | Execution instance ID                  |
| Ext             | Destination file format               |
| Number          | Destination file number               |

#### Sample


If the names of your input files are `test1.mp4` and `test2.mp4`, and you want to convert them to the FLV format (the final filenames will be `test1.flv` and `test2.flv`), then set the parameter format of the destination filename to `${InputName}.${Ext}`.

If the parameter format of the destination filename is set to `${InputNameAndExt}_${RunId}.${Ext}`:

When the workflow generates two instances (`000001` and `000002`) during execution, the final filenames will be `test1.mp4_000001.flv` and `test2.mp4_000002.flv`.



