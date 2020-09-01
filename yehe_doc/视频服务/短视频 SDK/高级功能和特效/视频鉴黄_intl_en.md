In scenarios such as personal live streaming shoot and UGSV, the video content is unpredictable. To prevent non-compliant contents from being displayed on the VOD platform, you need to audit the uploaded videos first and transcode and distribute them after confirming that they are compliant. The Tencent Cloud UGSV solution supports AI-based porn detection in videos, which can automatically identify whether a video involves pornographic information.
## Using AI-based Porn Detection  
The AI-based porn detection feature can be used only after it is integrated into the video processing task flow. It depends on the [video AI - content audit](https://intl.cloud.tencent.com/document/product/266/33944) feature on the VOD backend, and the audit result will be sent to the application backend service as an event notification. VOD has a built-in task flow `QCVB_ProcessUGCFile` for UGSV porn detection scenarios. If you use this task flow and specify to perform AI-based porn detection, the porn detection task will be executed first, and whether to perform subsequent operations (such as transcoding, watermarking, and screencapturing) will be determined based on the porn detection result. The flowchart is as shown below:
<img src="https://main.qcloudimg.com/raw/6b05d91e221481b34c28da69cf90433c.jpg" width="330">

## AI Template Overview 

| Template ID | Porn Processing | Sample Rate |
| ------ | -------------------------------------------- | ------------------------------------------------------------ |
| 10     | End the task flow (operations such as transcoding, watermarking, and screencapturing will not be executed subsequently) | For videos whose duration is less than 500 seconds, sampling is performed once per second; for videos whose duration is greater than or equal to 500 seconds, sampling is performed once every 1% of the duration |
| 20 | Continue executing the task flow | None |







## AI-based Porn Detection Connection Sample
#### Step 1. Submit an AI-based porn detection task when generating an upload signature
``` 
/**
 * Generate a signature that contains an AI-based porn detection task
 */
function getUploadSignature(req, res) {
    res.json({
        code: 0,
        message: 'ok',
        data: {
            // Specify the template parameters and task flow during the upload
            signature: gVodHelper.createFileUploadSignature({ procedure: 'QCVB_SimpleProcessFile({1,1,1,1})' })
        }
    });
}
``` 
#### Step 2. Get the AI-based porn detection result when getting the event notification

``` 
/**
 * Get the AI-based porn detection result of the event
 */
function getAiReviewResult(event){
    let data = event.eventContent.data;
    if(data.aiReview){
        return data.aiReview;
    }
    return {};
}
``` 


