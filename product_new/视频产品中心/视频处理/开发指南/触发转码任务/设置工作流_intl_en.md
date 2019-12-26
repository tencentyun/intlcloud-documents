Workflow settings mainly include the following parts:
- Configuration of trigger bucket, output bucket, and path.
- Configuration items of tasks such as transcoding, screencapturing (animated image generating and image sprite generating), and watermarking.
- CMQ address for event notification.
 
You need to use various created templates in task configuration. You can select [MPS Console > Template Settings](https://console.cloud.tencent.com/mps/templates) to query all parameter templates. For more information on how to create a custom parameter template, please see [Template Parameter Description](https://cloud.tencent.com/document/product/862/37037).

## Workflow Configuration Description

### <span id ="p1">Configuring the trigger bucket, output bucket, and path

- Trigger bucket: The bucket where a source file is stored. You can select a bucket in the corresponding region.
- Trigger bucket directory: Name of the bucket directory for which transcoding will be triggered. The default value is the root directory, i.e., transcoding will be triggered for files in all directories in the bucket. **If this parameter is set, transcoding tasks will be initiated only for files in the specified directory.**
- Output bucket: The bucket where an output file will be stored. **Currently, only buckets in the same region as the trigger bucket are supported.**
- Output directory: Name of the bucket directory where an output file will be stored. The output path is the same as the source path by default. In this case, you need to ensure that the output file has a name different from that of the source file; otherwise, the source file will be overwritten. If this parameter is set, output files will be stored in the specified directory.
  > If you set the output path in each task's configuration separately, the path settings in the task configuration will prevail.

### Configuring event notification
MPS uses the queue model in CMQ as the event notification model, which is a messaging model where messages are written to one end and read from the other end. The writer is called producer, while the reader consumer.
In this model, one message can be consumed only once. In the simplest case, there are only one producer and one consumer. In complex cases, there can be multiple producers and multiple consumers, and each consumer can obtain only an equal portion of all messages.
> Only COS v4 regions are supported, i.e., Shanghai (`sh`), Guangzhou (`gz`), Chengdu (`cd`), Chongqing (`cq`), and Beijing (`bj`).

For more information on CMQ, please see [CMQ Overview](https://intl.cloud.tencent.com/document/product/406/4541).

### Configuring a transcoding task
Transcoding task configuration includes configuration of tasks such as video transcoding, audio transcoding, and watermarking. You only need to select the corresponding transcoding template.

**Output path settings description**

| Path Type | Description | Configuration Example | Output Example |
| --- | --- | --- | ---- |
| Root directory | The "output path" set in [Configuring the trigger bucket, output bucket, and path](#p1) is ignored | Output directory: <br>`/output/` <br> Output path: <br>`/transcode/{inputName}_{definition}.{format}`  |  Output file: <br>`/transcode/testvideo_20.mp4` |
| Relative directory | The "output path" set in [Configuring the trigger bucket, output bucket, and path](#p1) will be as the directory prefix | Output directory: <br>`/output/` <br> Output path: <br>`transcode/{inputName}_{definition}.{format}` | Output file: <br>`/output/transcode/testvideo_20.mp4` |

### Configuring a screencapturing task
Screencapturing task configuration includes configuration of tasks such as sampled screencapturing, time point screencapturing, and image sprite generating.
- Sampled screencapturing: The system captures screenshots at a regular interval, which can be a fixed time or percent value, e.g., 1s or 1%.
- Time point screencapturing: The system captures screenshots at specified time points, e.g., taking screenshots at 00:00:00, 00:05:00, and 00:15:30, respectively (three screenshots in total).
- Image sprite generating: The system combines multiple screenshots into a larger image. You can set the width and height of each subimage.

### Configuring an animated image generating task
Animated image generating is to take screenshots of a video and combining them into an animated image in GIF or WEBP format. You can set the start and end time points for screencapturing.
