You can grant a specified sub-account the API permission of a specified resource in CI. The authorization granularity of CI is divided into resource level and API level:

- Resource-level API: It supports the authorization of a specific resource.
- API-level API: It does not support the authorization of a specific resource.

For authentication through a resource-level API, CI will pass the specific 6-segment resource description to CAM for authentication, thereby supporting authorization and authentication of the specific resource.

For authentication through an API-level API, CI will not deliver the six-segment format of the specific resource to CAM for authentication. Instead, it will deliver the `*` of any resource. To be more specific, if a resource is specified in the policy syntax during authorization but not delivered through the API for authentication, CAM will identify the API as out of the authorization scope, that is, having no permission.

The following lists all API permissions of CI:

## List Operation

| API | Description | Authorization Granularity | 6-Segment Resource Description |
| :------------------- | ---------------------------------------- | :------- | :--------- |
| DescribeMediaBuckets | Queries buckets with media processing enabled       | API level   | *          |
| DescribeRiskLibImage | Queries the list of images in the risky image library preset for content moderation     | API level   | *          |
| DescribeRiskLibText | Queries the list of keywords in the risky text library preset for content moderation     | API level   | *          |

## Write Operation

### Basic features

| API | Description | Authorization Granularity | 6-Segment Resource Description |
| :------------------- | ---------------------------------- | :------- | :--------- |
| CreateCIBucket               | Binds a bucket to CI | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DeleteCIBucket               | Unbinds a bucket from CI | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| SetDomain                    | Sets a CI domain name | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| SetCDNAccelerate             | Sets a CDN acceleration domain name for CI | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| Set4XXResponse               | Sets the 4xx image configuration in CI | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| SetRefer                     | Sets the bucket hotlink protection feature in CI | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| SetOriginProtect             | Sets the original image protection feature in CI | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |

### Content moderation

| API | Description | Authorization Granularity | 6-Segment Resource Description |
| :------------------------ | ------------------------------------ | :------- | :----------------------------------------------------------- |
| SetAuditingPicture        | Sets automatic image moderation                     | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| SetAuditingVideo          | Sets automatic video moderation                     | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| SetAuditingAudio          | Sets automatic audio moderation                     | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| SetAuditingText           | Sets automatic text moderation                     | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| SetAuditingDocument       | Sets automatic file moderation                     | Resource level  | qcs::ci::uid/${appid}:bucket/examplebucket-1250000000/*        |
| CreateAuditingJobs        | Creates a video moderation job                     | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateAuditingPictureJob  | Calls image moderation                         | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateAuditingTextJob     | Creates a text moderation job                     | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateAuditingAudioJob    | Creates an audio moderation job                     | Resource level   | qcs::ci:${region}:uid/${appid}:bucket/examplebucket-1250000000/* |
| CreateAuditingWebpageJob  | Creates a webpage moderation job                     | Resource level   | qcs::ci:${region}:uid/${appid}:bucket/${bucket}/*            |
| CreateAuditingDocumentJob | Creates a file moderation job                     | Resource level   | qcs::ci:${region}:uid/${appid}:bucket/examplebucket-1250000000/* |
| CreateAuditingExistTask   | Creates an existing data moderation job                     | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CancelAuditingExistTask   | Cancels an existing data moderation job                     | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DeleteRiskLibText         | Deletes the risky text library preset for content moderation           | API level   | *                                                            |
| DeleteRiskLibImage | Deletes an image in the risky image library preset for content moderation     | API level   | *          |
| CreateRiskLibText         | Adds a keyword to the risky text library for content moderation | API level   | *                                                            |
| CreateRiskLibImage | Adds an image to the risky image library preset for content moderation     | API level   | *          |
| CreateAuditingVirusJob    | Creates a cloud virus detection job                       | Resource level   | qcs::ci:${region}:uid/${appid}:bucket/${bucket}/*            |

### Media processing

| API | Description | Authorization Granularity | 6-Segment Resource Description |
| :------------------ | ---------------------- | :------- | :----------------------------------------------------------- |
| CreateMediaBucket   | Enables media processing for a bucket | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DeleteMediaBucket   | Disables media processing for a bucket | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateMediaTemplate | Creates a media processing template       | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| UpdateMediaTemplate | Updates a media processing template       | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DeleteMediaTemplate | Deletes a media processing template       | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| UpdateMediaQueue    | Updates a media processing queue       | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateMediaJobs     | Creates a media processing job       | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CancelMediaJob      | Cancels a media processing job       | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| GenerateSnapshot    | Captures video frames           | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| GenerateMediaInfo   | Queries the video information           | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DeleteMediaWorkflow | Deletes a workflow             | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| UpdateMediaWorkflow | Updates a workflow             | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateMediaWorkflow | Creates a workflow             | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |

### Image processing

| API | Description | Authorization Granularity | 6-Segment Resource Description |
| :-------------------------- | ------------------- | :------- | :----------------------------------------------------------- |
| SetImageGuetzli             | Enables image Guetzli compression | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| SetImageAdvancedCompression | Enables image advanced compression    | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| SetImageBlindWatermark      | Enables image blind watermarking      | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| SetImageStyleSeparator      | Sets the image style separator  | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| SetImageStyle               | Sets the image style        | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |


### File processing

| API | Description | Authorization Granularity | 6-Segment Resource Description |
| :--------------------- | ---------------------- | :------- | :----------------------------------------------------------- |
| CreateDocProcessBucket | Enables file preview for a bucket | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| UpdateDocProcessQueue  | Updates a file preview queue       | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DeleteDocProcessBucket | Disables file preview for a bucket | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CancelDocProcessJob    | Cancels a file preview job       | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateDocProcessJobs   | Creates a file preview job       | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |

### AI-based content recognition

| API | Description | Authorization Granularity | 6-Segment Resource Description |
| :--------------------------- | ------------------------------- | :------- | :----------------------------------------------------------- |
| CreateDetectQRcodeJob        | Calls the QR code recognition API              | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateDetectLabelJob         | Calls the image tag recognition API            | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateFaceEffectJob          | Calls the face filter API                | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| UpdateAsrQueue               | Updates a speech recognition queue                | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DeleteAsrBucket              | Disables speech recognition for a bucket          | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateAsrBucket              | Enables speech recognition for a bucket          | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateAsrJobs                | Creates a speech recognition job                | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateGetActionSequenceJob   | Calls the face verification - motion sequence acquisition API   | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateGetLiveCodeJob         | Calls the face verification - verification code acquisition API | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateLivenessRecognitionJob | Calls the face verification API                | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateIDCardOCRJob           | Calls the ID card recognition API               | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateQRcodeGenerateJob      | Calls the QR code generation API              | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| TriggerMediaWorkflow         | Triggers a workflow                      | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreatePetDetectJob           | Calls the pet recognition API                | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DeleteImage                  | Deletes an image in the image search library        | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| AddImage                     | Adds an image to the image search library          | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateImageSearchBucket      | Enables a bucket as the image search library      | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateContentAnalysisJob     | Calls the image tag recognition API            | Resource level   | qcs::ci:${region}:uid/${appid}:bucket/examplebucket-1250000000/* |
| CreateBodyJointsDetectJob    | Calls the body keypoint analysis API          | Resource level   | qcs::ci:${region}:uid/${appid}:bucket/examplebucket-1250000000/* |
| CreateOCRJob                 | Calls the image OCR API             | Resource level   | qcs::ci:${region}:uid/${appid}:bucket/examplebucket-1250000000/* |
| CreateLicensePlateJob        | Calls the license plate recognition API                | Resource level   | qcs::ci::uid/${appid}:bucket/examplebucket-1250000000/*        |
| CreateDetectFaceJob          | Calls the face detection API                | Resource level   | qcs::ci:${region}:uid/${appid}:bucket/examplebucket-1250000000/* |
| CreateAssessQualityJob       | Calls the image quality analysis API            | Resource level   | qcs::ci::uid/${appid}:bucket/examplebucket-1250000000/*        |
| CreateAiRecognitionJob       | Calls the all-in-one AI API                | Resource level   | qcs::ci:${region}:uid/${appid}:bucket/examplebucket-1250000000/* |
| CreateEnhanceImageJob        | Calls the image enhancement API          | Resource level   | qcs::ci:${region}:uid/${appid}:bucket/${bucket}/*            |
| CancelPicProcessJob          | Cancels an image processing job                | Resource level   | qcs::ci::uid/${appid}:bucket/examplebucket-1250000000/*        |
| CreatePicProcessJobs         | Creates an image processing job                | Resource level   | qcs::ci::uid/${appid}:bucket/examplebucket-1250000000/*        |
| UpdatePicProcessQueue        | Updates an image processing job queue            | Resource level   | qcs::ci::uid/${appid}:bucket/examplebucket-1250000000/*        |
| DeletePicProcessBucket       | Disables image processing for a bucket      | Resource level   | qcs::ci::uid/${appid}:bucket/examplebucket-1250000000/*        |
| CreatePicProcessBucket       | Enables image processing for a bucket      | Resource level   | qcs::ci::uid/${appid}:bucket/examplebucket-1250000000/*        |

## Read Operation

### Basic features

| API | Description | Authorization Granularity | 6-Segment Resource Description |
| :-------------------- | -------------------------------- | :------- | :----------------------------------------------------------- |
| DescribeCIBuckets     | Queries the CI binding status of a bucket     | API level   | *                                                            |
| DescribeDomain        | Queries the information of a CI domain name            | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeOriginProtect | Queries the enablement status of the original image protection feature in CI | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeCDNAccelerate | Queries the binding status of a CDN acceleration domain name in CI  | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| Describe4XXResponse   | Queries the status of 4xx image configuration in CI      | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeRefer         | Queries the status of bucket hotlink protection in CI     | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |

### Content moderation

| API | Description | Authorization Granularity | 6-Segment Resource Description |
| :---------------------------- | ---------------------------- | :------- | :----------------------------------------------------------- |
| DescribeAuditingJobs          | Queries video moderation jobs             | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeAuditingVideo         | Queries whether automatic video moderation is enabled     | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeAuditingAudio         | Queries whether automatic audio moderation is enabled     | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeAuditingPicture       | Queries whether automatic image moderation is enabled     | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeAuditingText          | Queries whether automatic text moderation is enabled     | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeAuditingDocument      | Queries whether automatic file moderation is enabled     | Resource level   | qcs::ci::uid/${appid}:bucket/examplebucket-1250000000/*        |
| DescribeAuditingCallback      | Queries the callback permission for content moderation | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeAuditingBlockRule     | Queries the blocking rule permission for content moderation | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeAuditingPictureFiles  | Queries the list of files for image moderation         | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeAuditingVideoFiles    | Queries the list of files for video moderation         | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeAuditingAudioFiles    | Queries the list of files for audio moderation         | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeAuditingTextFiles     | Queries the list of files for text moderation         | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeAuditingExistTasks    | Queries historical data moderation jobs         | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeAuditingTextJob       | Queries the result of a text moderation job         | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeAuditingAudioJob      | Queries the result of an audio moderation job         | Resource level   | qcs::ci:${region}:uid/${appid}:bucket/examplebucket-1250000000/* |
| DescribeAuditingDocumentJob   | Queries the result of a file moderation job         | Resource level   | qcs::ci:${region}:uid/${appid}:bucket/examplebucket-1250000000/* |
| DescribeAuditingWebpageJob    | Queries the result of a webpage moderation job         | Resource level   | qcs::ci:${region}:uid/${appid}:bucket/${bucket}/*            |
| DescribeAuditingDocumentFiles | Queries the result of a file moderation job         | Resource level   | qcs::ci::uid/${appid}:bucket/examplebucket-1250000000/*        |
| DescribeAuditingVirusJob      | Queries the result of a cloud virus detection job           | Resource level   | qcs::ci:${region}:uid/${appid}:bucket/${bucket}/*            |

### Media processing

| API | Description | Authorization Granularity | 6-Segment Resource Description |
| :------------------------------ | -------------------- | :------- | :----------------------------------------------------------- |
| DescribeMediaTemplates          | Queries media processing templates     | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeMediaQueues             | Queries media processing queues     | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeMediaJob                | Queries a media processing job     | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeMediaJobs               | Queries the list of media processing jobs | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeMediaWorkflowExecutions | Queries workflow execution instances   | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeMediaWorkflows          | Queries the status of workflows       | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| GetPrivateM3U8                  | Generates a private M3U8 video     | API level   | *                                                            |
| GenerateMediaInfo   | Gets the media information           | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| GenerateSnapshot    | Calls a frame capturing job           | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| ModifyM3U8Token                 | Refreshes HLS encrypted token    | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateMediaTemplate | Creates a media processing template       | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| UpdateMediaTemplate | Updates a media processing template       | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DeleteMediaTemplate | Deletes a media processing template       | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateMediaWorkflow | Creates a media processing workflow             | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| UpdateMediaWorkflow | Updates a media processing workflow             | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DeleteMediaWorkflow | Deletes a media processing workflow             | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| TriggerMediaWorkflow         | Triggers a media processing workflow                      | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| UpdateMediaQueue    | Updates a media processing queue       | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| AddMediaQueue    | Adds a media processing queue       | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateMediaBucket   | Binding the media processing service | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeMediaBuckets             | Queries the status of the media processing service     | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DeleteMediaBucket   | Unbinding the media processing service | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateMediaJobs     | Submits a media processing job       | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CancelMediaJob      | Cancels a media processing job       | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateInventoryTriggerJob     | Initiates a batch media processing job       | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeInventoryTriggerJob                | Queries a batch media processing job     | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeInventoryTriggerJobs          | Queries the status batch operation jobs in batches              | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CancelInventoryTriggerJob      | Cancels a batch operation job       | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
|  UpdateSpeedTranscodingProcessQueue  | Updates an accelerated transcoding queue       | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeSpeedTranscodingProcessQueues | Queries accelerated transcoding queues           | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| CreateSpeedTranscodingProcessQueues   | Creates an accelerated transcoding queue    | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |

### Image processing

| API | Description | Authorization Granularity | 6-Segment Resource Description |
| :------------------------------- | --------------------------------- | :------- | :----------------------------------------------------------- |
| DescribeImageGuetzli             | Queries the enablement status of image Guetzli compression for a bucket | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeImageAdvancedCompression | Queries the enablement status of image advanced compression for a bucket    | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeImageBlindWatermark      | Queries the enablement status of blind watermarking for a bucket          | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeImageStyleSeparator      | Queries the image style separator                | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeImageStyles              | Queries image styles                      | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |

### File processing

| API | Description | Authorization Granularity | 6-Segment Resource Description |
| :----------------------- | -------------------------- | :------- | :----------------------------------------------------------- |
| DescribeDocProcessQueues | Queries file preview queues           | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeDocProcessBucket | Queries the enablement status of file preview for a bucket | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeDocProcessJobs   | Queries the list of file preview jobs       | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeDocProcessJob    | Queries a file preview job           | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |

### AI-based content recognition

| API | Description | Authorization Granularity | 6-Segment Resource Description |
| :----------------------- | ------------------------------ | :------- | :----------------------------------------------------------- |
| DescribeAsrQueues        | Queries speech recognition queues               | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeAsrBuckets       | Queries the enablement status of speech recognition for buckets | API level   | *                                                            |
| DescribeAsrJobs          | Queries the list of speech recognition jobs               | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribeAsrJob           | Queries a speech recognition job           | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| SearchImage              | Searches for an image in the image search library       | Resource level   | qcs::ci:ap-shanghai:uid/1250000000:bucket/examplebucket-1250000000/* |
| DescribePicProcessJobs   | Queries the list of image processing jobs           | Resource level   | qcs::ci::uid/${appid}:bucket/examplebucket-1250000000/*        |
| DescribePicProcessJob    | Queries an image processing job               | Resource level   | qcs::ci::uid/${appid}:bucket/examplebucket-1250000000/*        |
| DescribePicProcessQueues | Queries image processing queues               | Resource level   | qcs::ci::uid/${appid}:bucket/examplebucket-1250000000/*        |
| DescribePicProcessBucket | Queries the list of buckets for image processing         | Resource level   | qcs::ci::uid/${appid}:bucket/examplebucket-1250000000/*        |
