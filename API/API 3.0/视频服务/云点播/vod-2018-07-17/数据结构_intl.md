## AdaptiveDynamicStreamingInfoItem
Information of the conversion to adaptive bitrate  
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Required | Description |
|------|------|----------|------|
| Definition | Integer | Yes | Type of the conversion to adaptive bitrate. |
| Package | String | Yes | Packaging format, which can be hls or dash. |
| DrmType | String | Yes | Encryption type. |
| Url | String | Yes | Playback address. |
## AdaptiveDynamicStreamingTaskInput
Input parameter type of the conversion to adaptive bitrate  
Used for calling the following APIs: CreateProcedureTemplate, DescribeProcedureTemplates, DescribeTaskDetail, ProcessMedia, PullEvents, ResetProcedureTemplate.
| Name | Type | Required | Description |
|------|------|----------|------|
| Definition | Integer | Yes | ID of the template for conversion to adaptive bitrate. |
## AiAnalysisResult
Intelligent analysis result  
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Type | String | Task type; value range: <br/><li>Classification: Intelligent categorization </li><li>Cover: Intelligent cover generating </li><li>Description: Intelligent description generating </li><li>Highlight: Intelligent highlight generating </li><li>Tag: Intelligent tagging </li><li>FrameTag: Intelligent frame-specific tagging</li> |
| ClassificationTask | [AiAnalysisTaskClassificationResult](#AiAnalysisTaskClassificationResult) | Query result of the intelligent categorization task in video content analysis, which is valid if task type is Classification. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| CoverTask | [AiAnalysisTaskCoverResult](#AiAnalysisTaskCoverResult) | Query result of the intelligent cover generating task in video content analysis, which is valid if task type is Cover. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| TagTask | [AiAnalysisTaskTagResult](#AiAnalysisTaskTagResult) | Query result of the intelligent tagging task in video content analysis, which is valid if task type is Tag. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## AiAnalysisTaskClassificationInput
Input type of the intelligent categorization task
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Definition | Integer | ID of the intelligent video categorization template, which is fixed as 10. |
## AiAnalysisTaskClassificationOutput
Information of the intelligent categorization result
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| ClassificationSet | Array of [MediaAiAnalysisClassificationItem](#MediaAiAnalysisClassificationItem) | List of intelligently created video categories. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## AiAnalysisTaskClassificationResult
Result type of the intelligent categorization task
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Status | String | Task status; value range: PROCESSING, SUCCESS, and FAIL. |
| ErrCode | Integer | Error code; 0 - success, other values - failure. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Input | [AiAnalysisTaskClassificationInput](#AiAnalysisTaskClassificationInput) | Input of the intelligent categorization task. |
| Output | [AiAnalysisTaskClassificationOutput](#AiAnalysisTaskClassificationOutput) | Output of the intelligent categorization task. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## AiAnalysisTaskCoverInput
Input type of the intelligent categorization task
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Definition | Integer | ID of the intelligent video cover generating template, which is fixed as 10. |
## AiAnalysisTaskCoverOutput
Information of the intelligent cover generating result
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| CoverSet | Array of [MediaAiAnalysisCoverItem](#MediaAiAnalysisCoverItem) | List of intelligently generated covers. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## AiAnalysisTaskCoverResult
Result type of the intelligent cover generating task
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Status | String | Task status; value range: PROCESSING, SUCCESS, and FAIL. |
| ErrCode | Integer | Error code; 0 - success, other values - failure. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Input | [AiAnalysisTaskCoverInput](#AiAnalysisTaskCoverInput) | Input of the intelligent cover generating task. |
| Output | [AiAnalysisTaskCoverOutput](#AiAnalysisTaskCoverOutput) | Output of the intelligent cover generating task. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## AiAnalysisTaskInput
Input parameter type of the AI-based intelligent video analysis
Used for calling the following APIs: CreateProcedureTemplate, DescribeProcedureTemplates, ProcessMedia, ProcessMediaByUrl, ResetProcedureTemplate.
| Name | Type | Required | Description |
|------|------|----------|------|
| Definition | Integer | Yes | ID of the video analysis template, which is fixed as 10. Intelligent category analysis, tag analysis, and cover analysis are performed simultaneously. |
## AiAnalysisTaskTagInput
Input type of the intelligent tagging task
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Definition | Integer | ID of the intelligent video categorization template, which is fixed as 10. |
## AiAnalysisTaskTagOutput
Information of the intelligent tagging result
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| TagSet | Array of [MediaAiAnalysisTagItem](#MediaAiAnalysisTagItem) | List of intelligently generated video tags. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## AiAnalysisTaskTagResult
Result type of the intelligent tagging task
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Status | String | Task status; value range: PROCESSING, SUCCESS, and FAIL. |
| ErrCode | Integer | Error code; 0 - success, other values - failure. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Input | [AiAnalysisTaskTagInput](#AiAnalysisTaskTagInput) | Input of the intelligent tagging task. |
| Output | [AiAnalysisTaskTagOutput](#AiAnalysisTaskTagOutput) | Output of the intelligent tagging task. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## AiContentReviewResult
Content review result
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Type | String | Task type; value range: <br/><li>Porn: Pornographic information detection in image </li><li>Terrorism: Terrorism information detection in image </li><li>Political: Politically sensitive information detection in image </li><li>Porn.Asr: ASR-based pornographic information detection in text </li><li>Porn.Ocr: OCR-based pornographic information detection in text </li><li>Political.Asr: ASR-based politically sensitive information detection in text </li><li>Political.Ocr: OCR-based politically sensitive information detection in text</li> |
| PornTask | [AiReviewTaskPornResult](#AiReviewTaskPornResult) | Query result of the intelligent pornographic information detection in image task in video content review, which is valid if task type is Porn. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| TerrorismTask | [AiReviewTaskTerrorismResult](#AiReviewTaskTerrorismResult) | Query result of the intelligent terrorism information detection in image task in video content review, which is valid if task type is Terrorism. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| PoliticalTask | [AiReviewTaskPoliticalResult](#AiReviewTaskPoliticalResult) | Query result of the intelligent politically sensitive information detection in image task in video content review, which is valid if task type is Political. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| PornAsrTask | [AiReviewTaskPornAsrResult](#AiReviewTaskPornAsrResult) | Query result of the ASR-based pornographic information detection in text task in video content review, which is valid if task type is Porn.Asr. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| PornOcrTask | [AiReviewTaskPornOcrResult](#AiReviewTaskPornOcrResult) | Query result of the OCR-based pornographic information detection in text task in video content review, which is valid if task type is Porn.Ocr. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| PoliticalAsrTask | [AiReviewTaskPoliticalAsrResult](#AiReviewTaskPoliticalAsrResult) | Query result of the ASR-based politically sensitive information detection in text task in video content review, which is valid if task type is Political.Asr. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| PoliticalOcrTask | [AiReviewTaskPoliticalOcrResult](#AiReviewTaskPoliticalOcrResult) | Query result of the OCR-based politically sensitive information detection in text task in video content review, which is valid if task type is Political.Ocr. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## AiContentReviewTaskInput
Type of the intelligent content review task
Referenced by: CreateProcedureTemplate, DescribeProcedureTemplates, ProcessMedia, ProcessMediaByUrl, ResetProcedureTemplate.
| Name | Type | Required | Description |
|------|------|----------|------|
| Definition | Integer | Yes | Video content review template ID, which can be 10 or 20. <li>10: Perform detection of pornographic, terrorism, and politically sensitive information on the video image; </li><li>20: Perform detection of pornographic, terrorism, and politically sensitive information on the video image, and perform detection of pornographic and politically sensitive information on the text recognized by ASR and OCR. </li> |
## AiRecognitionTaskInput
Input parameter type of the AI-based video content recognition
Used for calling the following APIs: CreateProcedureTemplate, DescribeProcedureTemplates, ResetProcedureTemplate.
| Name | Type | Required | Description |
|------|------|----------|------|
| Definition | Integer | Yes | Intelligent video recognition template ID, which is fixed as 10, i.e., simultaneously recognizing frame-specific tags, highlights, opening and closing credits, segments, faces, text, and speeches in the video, and performing full-video text and speech recognition. Custom templates will be available soon, enabling you to select the desired recognition tasks. |
## AiReviewPoliticalAsrTaskInput
Input parameter type of the ASR-based politically sensitive information detection in text task in content review
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Definition | Integer | ID of the politically sensitive information detection template. |
## AiReviewPoliticalAsrTaskOutput
ASR-detected politically sensitive information in text
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Confidence | Float | Score of the ASR-detected politically sensitive information in text from 0 to 100. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Suggestion | String | Suggestion for the ASR-detected politically sensitive information in text; value range: <br/><li>pass. </li><li>review. </li><li>block. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| SegmentSet | Array of [MediaContentReviewAsrTextSegmentItem](#MediaContentReviewAsrTextSegmentItem) | List of video segments that contain ASR-detected politically sensitive information in text. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## AiReviewPoliticalOcrTaskInput
Input parameter type of the OCR-based politically sensitive information detection in text task in content review
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Definition | Integer | ID of the politically sensitive information detection template. |
## AiReviewPoliticalOcrTaskOutput
OCR-detected politically sensitive information in text
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Confidence | Float | Score of the OCR-detected politically sensitive information in text from 0 to 100. |
| Suggestion | String | Suggestion for the OCR-detected politically sensitive information in text; value range: <br/><li>pass. </li><li>review. </li><li>block. </li> |
| SegmentSet | Array of [MediaContentReviewOcrTextSegmentItem](#MediaContentReviewOcrTextSegmentItem) | List of video segments that contain OCR-detected politically sensitive information in text. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## AiReviewPoliticalTaskInput
Input parameter type of the politically sensitive information detection task in content review
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Definition | Integer | ID of the politically sensitive information detection template. |
## AiReviewPoliticalTaskOutput
Politically sensitive information
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Confidence | Float | Score of the detected politically sensitive information in the video from 0 to 100. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Suggestion | String | Suggestion for the detected politically sensitive information; value range: <br/><li>pass. </li><li>review. </li><li>block. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Label | String | Tag of the detected politically sensitive information in the video; value range: <br/><li>politician: Politically sensitive figure. </li><li>violation_photo: Violating photo. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| SegmentSet | Array of [MediaContentReviewPoliticalSegmentItem](#MediaContentReviewPoliticalSegmentItem) | List of video segments that contain detected politically sensitive information. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## AiReviewPornAsrTaskInput
Input parameter type of the ASR-based pornographic information detection in text task in content review
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Definition | Integer | ID of the pornographic information detection template. |
## AiReviewPornAsrTaskOutput
ASR-detected pornographic information in text
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Confidence | Float | Score of the ASR-detected pornographic information in text from 0 to 100. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Suggestion | String | Suggestion for the ASR-detected pornographic information in text; value range: <br/><li>pass. </li><li>review. </li><li>block. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| SegmentSet | Array of [MediaContentReviewAsrTextSegmentItem](#MediaContentReviewAsrTextSegmentItem) | List of video segments that contain ASR-detected pornographic information in text. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## AiReviewPornOcrTaskInput
Input parameter type of the OCR-based pornographic information detection in text task in content review
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Definition | Integer | ID of the pornographic information detection template. |
## AiReviewPornOcrTaskOutput
OCR-detected pornographic information in text
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Confidence | Float | Score of the OCR-detected pornographic information in text from 0 to 100. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Suggestion | String | Suggestion for the OCR-detected pornographic information in text; value range: <br/><li>pass. </li><li>review. </li><li>block. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| SegmentSet | Array of [MediaContentReviewOcrTextSegmentItem](#MediaContentReviewOcrTextSegmentItem) | List of video segments that contain OCR-detected pornographic information in text. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## AiReviewPornTaskInput
Input parameter type of the pornographic information detection task in content review
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Required | Description |
|------|------|----------|------|
| Definition | Integer | Yes | ID of the pornographic information detection template. |
## AiReviewPornTaskOutput
Pornographic information detection result
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Confidence | Float | Score of the detected pornographic information in the video from 0 to 100. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Suggestion | String | Suggestion for the detected pornographic information; value range: <br/><li>pass. </li><li>review. </li><li>block. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Label | String | Tag of the detected pornographic information in the video; value range: <br/><li>porn: Pornography. </li><li>sexy: Sexiness. </li><li>vulgar: Vulgarity. </li><li>intimacy: Intimacy. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| SegmentSet | Array of [MediaContentReviewSegmentItem](#MediaContentReviewSegmentItem) | List of video segments that contain detected pornographic information. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## AiReviewTaskPoliticalAsrResult
Result type of the ASR-based politically sensitive information detection in text task in content review
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Status | String | Task status; value range: PROCESSING, SUCCESS, and FAIL. |
| ErrCode | Integer | Error code; 0 - success, other values - failure. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Input | [AiReviewPoliticalAsrTaskInput](#AiReviewPoliticalAsrTaskInput) | Input of the ASR-based politically sensitive information detection in text task in content review. |
| Output | [AiReviewPoliticalAsrTaskOutput](#AiReviewPoliticalAsrTaskOutput) | Output of the ASR-based politically sensitive information detection in text task in content review. |
## AiReviewTaskPoliticalOcrResult
Result type of the OCR-based politically sensitive information detection in text task in content review
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Status | String | Task status; value range: PROCESSING, SUCCESS, and FAIL. |
| ErrCode | Integer | Error code; 0 - success, other values - failure. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Input | [AiReviewPoliticalOcrTaskInput](#AiReviewPoliticalOcrTaskInput) | Input of the OCR-based politically sensitive information detection in text task in content review. |
| Output | [AiReviewPoliticalOcrTaskOutput](#AiReviewPoliticalOcrTaskOutput) | Output of the OCR-based politically sensitive information detection in text task in content review. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## AiReviewTaskPoliticalResult
Result type of the politically sensitive information detection task in content review
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Status | String | Task status; value range: PROCESSING, SUCCESS, and FAIL. |
| ErrCode | Integer | Error code; 0 - success, other values - failure. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Input | [AiReviewPoliticalTaskInput](#AiReviewPoliticalTaskInput) | Input of the politically sensitive information detection task in content review. |
| Output | [AiReviewPoliticalTaskOutput](#AiReviewPoliticalTaskOutput) | Output of the politically sensitive information detection task in content review. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## AiReviewTaskPornAsrResult
Result type of the ASR-based pornographic information detection in text task in content review
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Status | String | Task status; value range: PROCESSING, SUCCESS, and FAIL. |
| ErrCode | Integer | Error code; 0 - success, other values - failure. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Input | [AiReviewPornAsrTaskInput](#AiReviewPornAsrTaskInput) | Input of the ASR-based pornographic information detection in text task in content review. |
| Output | [AiReviewPornAsrTaskOutput](#AiReviewPornAsrTaskOutput) | Output of the ASR-based pornographic information detection in text task in content review. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## AiReviewTaskPornOcrResult
Result type of the OCR-based pornographic information detection in text task in content review
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Status | String | Task status; value range: PROCESSING, SUCCESS, and FAIL. |
| ErrCode | Integer | Error code; 0 - success, other values - failure. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Input | [AiReviewPornOcrTaskInput](#AiReviewPornOcrTaskInput) | Input of the OCR-based pornographic information detection in text task in content review. |
| Output | [AiReviewPornOcrTaskOutput](#AiReviewPornOcrTaskOutput) | Output of the OCR-based pornographic information detection in text task in content review. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## AiReviewTaskPornResult
Result type of the pornographic information detection task in content review
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Status | String | Task status; value range: PROCESSING, SUCCESS, and FAIL. |
| ErrCode | Integer | Error code; 0 - success, other values - failure. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Input | [AiReviewPornTaskInput](#AiReviewPornTaskInput) | Input of the pornographic information detection task in content review. |
| Output | [AiReviewPornTaskOutput](#AiReviewPornTaskOutput) | Output of the pornographic information detection task in content review. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## AiReviewTaskTerrorismResult
Result type of the terrorism information detection task in content review
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Status | String | Task status; value range: PROCESSING, SUCCESS, and FAIL. |
| ErrCode | Integer | Error code; 0 - success, other values - failure. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Input | [AiReviewTerrorismTaskInput](#AiReviewTerrorismTaskInput) | Input of the terrorism information detection task in content review. |
| Output | [AiReviewTerrorismTaskOutput](#AiReviewTerrorismTaskOutput) | Output of the terrorism information detection task in content review. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## AiReviewTerrorismTaskInput
Input parameter type of the terrorism information detection task in content review
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Definition | Integer | ID of the terrorism information detection template. |
## AiReviewTerrorismTaskOutput
Terrorism information
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Confidence | Float | Score of the detected terrorism information in the video from 0 to 100. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Suggestion | String | Suggestion for the detected terrorism information; value range: <br/><li>pass. </li><li>review. </li><li>block. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Label | String | Tag of the detected terrorism information in the video; value range: <br/><li>guns: Weapons and guns. </li><li>crowd: Crowd. </li><li>police: Police force. </li><li>bloody: Bloody scenes. </li><li>banners: Terrorism flags. </li><li>militant: Militants. </li><li>explosion: Explosions and fires. </li><li>terrorists: Terrorists. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| SegmentSet | Array of [MediaContentReviewSegmentItem](#MediaContentReviewSegmentItem) | List of video segments that contain detected terrorism information. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## AnimatedGraphicTaskInput
Type of the animated image generating task
Used for calling the following APIs: CreateProcedureTemplate, DescribeProcedureTemplates, DescribeTaskDetail, ProcessMedia, PullEvents, ResetProcedureTemplate.
| Name | Type | Required | Description |
|------|------|----------|------|
| Definition | Integer | Yes | ID of the animated image generating template.
| StartTimeOffset | Float | Yes | Start time of the animated image in the video in seconds. |
| EndTimeOffset | Float | Yes | End time of the animated image in the video in seconds. |
## AudioTemplateInfo
Audio stream configuration parameter
Used for calling the following APIs: CreateTranscodeTemplate, DescribeTranscodeTemplates.
| Name | Type | Required | Description |
|------|------|----------|------|
| Codec | String | Yes | Codec of the audio stream; value range: <br/><li>libfdk_aac: More suitable for mp4 and hls; </li><li>libmp3lame: More suitable for flv; </li><li>mp2.</li> |
| Bitrate | Integer | Yes | Bit rate of the audio stream; value range: 0 or [26, 256] in Kbps. <br/>If the value is 0, the bitrate of the audio stream is the same as that of the original audio. |
| SampleRate | Integer | Yes | Sample rate of the audio stream; value range: <br/><li>32000</li><li>44100</li><li>48000</li><br/>Unit: Hz. |
| AudioChannel | Integer | No | Channel of the audio; value range: <br/><li>1: 1 channel </li><li>2: 2 channels </li><li>6: Stereo </li><br/>Default value: 2. |
## AudioTemplateInfoForUpdate
Audio stream configuration parameter  
Used for calling the following APIs: ModifyTranscodeTemplate.
| Name | Type | Required | Description |
|------|------|----------|------|
| Codec | String | No | Codec of the audio stream; value range: <br/><li>libfdk_aac: More suitable for mp4 and hls; </li><li>libmp3lame: More suitable for flv; </li><li>mp2.</li> |
| Bitrate | Integer | No | Bit rate of the audio stream; value range: 0 or [26, 256] in Kbps. If the value is 0, the bitrate of the audio stream is the same as that of the original audio. |
| SampleRate | Integer | No | Sample rate of the audio stream; value range: <br/><li>32000</li><li>44100</li><li>48000</li><br/>Unit: Hz. |
| AudioChannel | Integer | No | Channel of the audio; value range: <br/><li>1: 1 channel </li><li>2: 2 channels </li><li>6: Stereo </li> |
## ClipFileInfo2017
Information of the file generated by video cropping (v2017)  
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| ErrCode | Integer | Error code <br/><li>0: Success; </li><li>Other values: Failure. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| FileId | String | ID of the output target file. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| FileUrl | String | Address of the output target file. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| FileType | String | Type of the output target file. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## ClipTask2017
Information of the video clipping task. This structure is only used for tasks initiated by the [video clipping](https://cloud.tencent.com/document/product/266/10156) API in v2017.  
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| TaskId | String | ID of the video clipping task. |
| SrcFileId | String | ID of the source file for the video clipping task. |
| FileInfo | [ClipFileInfo2017](#ClipFileInfo2017) | Information of the file outputted by clipping the video. |
## ConcatFileInfo2017
Information of the source file for video stitching (v2017)
Used for calling the following APIs: DescribeTaskDetail, PullEvents.  
| Name | Type | Description |
|------|------|-------|
| ErrCode | Integer | Error code <br/><li>0: Success; </li><li>Other values: Failure. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| FileId | String | ID of the source file for video stitching. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| FileUrl | String | Address of the source file for video stitching. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| FileType | String | Type of the source file for video stitching. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## ConcatTask2017
Information of the video stitching task. This structure is only used for tasks initiated by the [video stitching](https://cloud.tencent.com/document/product/266/7821) API in v2017.
Used for calling the following APIs: DescribeTaskDetail, PullEvents.  
| Name | Type | Description |
|------|------|-------|
| TaskId | String | ID of the video stitching task. |
| FileInfoSet | Array of [ConcatFileInfo2017](#ConcatFileInfo2017) | Information of the source file for video stitching. |
## CoverBySnapshotTaskInput
Input parameter type of the cover generating task
Used for calling the following APIs: CreateProcedureTemplate, DescribeProcedureTemplates, DescribeTaskDetail, ProcessMedia, PullEvents, ResetProcedureTemplate.  
| Name | Type | Required | Description |
|------|------|----------|------|
| Definition | Integer | Yes | ID of the time point-based screencapturing template. |
| PositionType | String | Yes | Screencapturing method. Value range: <br/><li>Time: Screencapture by time point </li><li>Percent: Screencapture by percentage </li> |
| PositionValue | Float | Yes | Screencapturing position: <br/><li>For time point-based screencapturing, this means to take a screenshot at the specified time point (in seconds) and use it as the cover </li><li>For percentage screencapturing, this means to take a screenshot at the specified percentage of the video duration and use it as the cover </li> |
| WatermarkSet | Array of [WatermarkInput](#WatermarkInput) | No | List of up to 10 image or text watermarks. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## CoverBySnapshotTaskOutput
Output type of the cover generating task
Used for calling the following APIs: DescribeTaskDetail, PullEvents.  
| Name | Type | Description |
|------|------|-------|
| CoverUrl | String | Cover URL. |
## CreateImageSpriteTask2017
Image sprite generating task. This structure is only used for tasks initiated by the [image sprite generating](https://cloud.tencent.com/document/product/266/8101) API in v2017.
Used for calling the following APIs: DescribeTaskDetail, PullEvents.  
| Name | Type | Description |
|------|------|-------|
| TaskId | String | Image sprite generating task ID. |
| ErrCode | Integer | Error code <br/><li>0: Success; </li><li>Other values: Failure. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| FileId | String | Image sprite file ID. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Definition | Integer | Image sprite type. For more information, see [Image Sprite Generating Template](https://cloud.tencent.com/document/product/266/11702#.E9.9B.AA.E7.A2.A7.E5.9B.BE.E6.88.AA.E5.9B.BE.E6.A8.A1.E6.9D.BF). <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| TotalCount | Integer | Total number of sub-images in the image sprite. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| ImageSpriteUrlSet | Array of String | Address of the output image sprite. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| WebVttUrl | String | Address of the WebVtt file for the position-time relationship among sub-images in the image sprite. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## EditMediaFileInfo
Information of VOD video file editing
Used for calling the following APIs: DescribeTaskDetail, PullEvents.  
| Name | Type | Required | Description |
|------|------|----------|------|
| FileId | String | Yes | Video ID. |
| StartTimeOffset | Float | No | Start time offset of video editing in seconds. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| EndTimeOffset | Float | No | End time offset of video editing in seconds. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## EditMediaStreamInfo
Information of video stream editing
Used for calling the following APIs: DescribeTaskDetail, PullEvents.  
| Name | Type | Required | Description |
|------|------|----------|------|
| StreamId | String | Yes | ID of the recorded stream |
| StartTime | String | No | Start time of stream editing in [ISO date format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| EndTime | String | No | End time of stream editing in [ISO date format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## EditMediaTask
Information of the video editing task
Used for calling the following APIs: DescribeTaskDetail, PullEvents.  
| Name | Type | Description |
|------|------|-------|
| TaskId | String | Task ID. |
| Status | String | Task flow status; value range: <br/><li>PROCESSING: Processing; </li><li>FINISH: Finished. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| ErrCode | Integer | Error code <br/><li>0: Success; </li><li>Other values: Failure. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Input | [EditMediaTaskInput](#EditMediaTaskInput) | Input of the video editing task. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Output | [EditMediaTaskOutput](#EditMediaTaskOutput) | Output of the video editing task. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| ProcedureTaskId | String | If a video processing flow is specified when the video editing task is initiated, this field is the ID of the task flow. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## EditMediaTaskInput
Input of the video editing task.
Used for calling the following APIs: DescribeTaskDetail, PullEvents.  
| Name | Type | Description |
|------|------|-------|
| InputType | String | Source type of the input video; value range: File and Stream. |
| FileInfoSet | Array of [EditMediaFileInfo](#EditMediaFileInfo) | Information of the input video file. This field has a value only when InputType is File. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| StreamInfoSet | Array of [EditMediaStreamInfo](#EditMediaStreamInfo) | Information of the input stream. This field has a value only when InputType is Stream. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## EditMediaTaskOutput
Output of the video editing task
Used for calling the following APIs: DescribeTaskDetail, PullEvents.  
| Name | Type | Description |
|------|------|-------|
| FileType | String | File type, such as mp4 and flv. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| FileId | String | Media file ID. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| FileUrl | String | Media file playback address. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## EventContent
Event notification content, where TranscodeCompleteEvent, ConcatCompleteEvent, ClipCompleteEvent, CreateImageSpriteCompleteEvent, and SnapshotByTimeOffsetCompleteEvent are event notifications for tasks that are initiated by v2017-compatible APIs.
Used for calling the following APIs: PullEvents.  
| Name | Type | Description |
|------|------|-------|
| EventHandle | String | Event handler. The caller must call ConfirmEvents to confirm that the message has been received, and the confirmation is valid for 30 seconds. After it expires, the event can be obtained again. |
| EventType | String | <b>Supported event types: </b><br/><li>NewFileUpload: Video upload completion; </li><li>ProcedureStateChanged: Task flow status change; </li><li> FileDeleted: Video deletion completion; </li><li>PullComplete: Video pull completion; </li><li>EditMediaComplete: Video editing completion; </li><li>WechatPublishComplete: Publishing on WeChat completion. </li><br/><b>v2017-compatible event types: </b><br/><li>TranscodeComplete: Video transcoding completion; </li><li>ConcatComplete: Video stitching completion; </li><li>ClipComplete: Video clipping completion; </li><li>CreateImageSpriteComplete: Image sprite generating completion; </li><li>CreateSnapshotByTimeOffsetComplete: Time point-based screencapturing completion. </li> |
| FileUploadEvent | [FileUploadTask](#FileUploadTask) | Video upload completion event, which is valid if the event type is NewFileUpload. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| ProcedureStateChangeEvent | [ProcedureTask](#ProcedureTask) | Task flow status change event, which is valid if the event type is ProcedureStateChanged. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| FileDeleteEvent | [FileDeleteTask](#FileDeleteTask) | File deletion event, which is valid if the event type is FileDeleted. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| PullCompleteEvent | [PullFileTask](#PullFileTask) | Video pull completion event, which is valid if the event type is PullComplete. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| EditMediaCompleteEvent | [EditMediaTask](#EditMediaTask) | Video editing completion event, which is valid if the event type is EditMediaComplete. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| WechatPublishCompleteEvent | [WechatPublishTask](#WechatPublishTask) | Publishing on WeChat completion event, which is valid if the event type is WechatPublishComplete. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| TranscodeCompleteEvent | [TranscodeTask2017](#TranscodeTask2017) | Video transcoding completion event, which is valid if the event type is TranscodeComplete. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| ConcatCompleteEvent | [ConcatTask2017](#ConcatTask2017) | Video stitching completion event, which is valid if the event type is ConcatComplete. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| ClipCompleteEvent | [ClipTask2017](#ClipTask2017) | Video clipping completion event, which is valid if the event type is ClipComplete. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| CreateImageSpriteCompleteEvent | [CreateImageSpriteTask2017](#CreateImageSpriteTask2017) | Image sprite generating completion event, which is valid if the event type is CreateImageSpriteComplete. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| SnapshotByTimeOffsetCompleteEvent | [SnapshotByTimeOffsetTask2017](#SnapshotByTimeOffsetTask2017) | Time point-based screencapturing completion event, which is valid if the event type is CreateSnapshotByTimeOffsetComplete. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## FileDeleteTask
File deleting task
Used for calling the following APIs: PullEvents.  
| Name | Type | Description |
|------|------|-------|
| FileIdSet | Array of String | List of file IDs to be deleted. |
## FileUploadTask
Information of the file upload task
Used for calling the following APIs: PullEvents.  
| Name | Type | Description |
|------|------|-------|
| FileId | String | Unique ID of the file. |
| MediaBasicInfo | [MediaBasicInfo](#MediaBasicInfo) | Basic information of the media file generated after the upload is completed. |
| ProcedureTaskId | String | If a video processing flow is specified when the video is uploaded, this field is the ID of the task flow. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## ImageSpriteTaskInput
Input parameter type of the image sprite generating task  
Used for calling the following APIs: CreateProcedureTemplate, DescribeProcedureTemplates, DescribeTaskDetail, ProcessMedia, PullEvents, ResetProcedureTemplate.
| Name | Type | Required | Description |
|------|------|----------|------|
| Definition | Integer | Yes | ID of the image sprite generating template. |
## ImageWatermarkInput
Input parameter of the image watermarking template  
Used for calling the following APIs: CreateWatermarkTemplate.
| Name | Type | Required | Description |
|------|------|----------|------|
| ImageContent | String | Yes | The string generated by [Base64-encoding](https://tools.ietf.org/html/rfc4648) the watermark image. jpeg and png formats are supported. |
| Width | String | No | Watermark width. % and px formats are supported: <br/><li>If the string ends in %, the watermark width is the specified percentage of the video width, for example, 10% means that Width is 10% of the video width; </li><li>if the string ends in px, the watermark width is in px, for example, 100px means that Width is 100px. </li><br/>Default value: 10%. |
| Height | String | No | Watermark height. % and px formats are supported: <br/><li>If the string ends in %, the watermark height is the specified percentage of the video height, for example, 10% means that Height is 10% of the video height; </li><li>if the string ends in px, the watermark height is in px, for example, 100px means that Height is 100px. </li><br/>Default value: 0px, which means that Height is proportionally scaled according to the video width. |
## ImageWatermarkInputForUpdate
Input parameter of the image watermarking template  
Used for calling the following APIs: ModifyWatermarkTemplate.
| Name | Type | Required | Description |
|------|------|----------|------|
| ImageContent | String | No | The string generated by [Base64-encoding](https://tools.ietf.org/html/rfc4648) the watermark image. jpeg and png formats are supported. |
| Width | String | No | Watermark width. % and px formats are supported: <br/><li>If the string ends in %, the watermark width is the specified percentage of the video width, for example, 10% means that Width is 10% of the video width; </li><li>if the string ends in px, the watermark width is in px, for example, 100px means that Width is 100px. </li> |
| Height | String | No | Watermark height. % and px formats are supported: <br/><li>If the string ends in %, the watermark height is the specified percentage of the video height, for example, 10% means that Height is 10% of the video height; </li><li>if the string ends in px, the watermark height is in px, for example, 100px means that Height is 100px. </li><br/>0px means that Height is proportionally scaled according to the video width. |
## ImageWatermarkTemplate
Image watermarking template  
Used for calling the following APIs: DescribeWatermarkTemplates.
| Name | Type | Description |
|------|------|-------|
| ImageUrl | String | Watermark image address. |
| Width | String | Watermark width. % and px formats are supported: <br/><li>If the string ends in %, the watermark width is the specified percentage of the video width, for example, 10% means that Width is 10% of the video width; </li><li>if the string ends in px, the watermark width is in px, for example, 100px means that Width is 100px. </li> |
| Height | String | Watermark height. % and px formats are supported: <br/><li>If the string ends in %, the watermark height is the specified percentage of the video height, for example, 10% means that Height is 10% of the video height; </li><li>if the string ends in px, the watermark height is in px, for example, 100px means that Height is 100px; </li><br/>0px means that Height is proportionally scaled according to the video width. |
## MediaAiAnalysisClassificationItem
Intelligent categorization result  
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Classification | String | Name of the intelligent category. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Confidence | Float | Confidence of the intelligent categorization; value range: 0-100. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaAiAnalysisCoverItem
Information of the intelligent cover  
Referenced by: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| CoverUrl | String | Intelligent cover address. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Confidence | Float | Confidence of the intelligent cover; value range: 0-100. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaAiAnalysisTagItem
Information of the intelligent tagging result
Referenced by: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Tag | String | Tag name. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Confidence | Float | Confidence of the tag; value range: 0-100. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaAnimatedGraphicsInfo
Information of the animated image generating result in the VOD file
Referenced by: DescribeMediaInfos, SearchMedia.
| Name | Type | Description |
|------|------|-------|
| AnimatedGraphicsSet | Array of [MediaAnimatedGraphicsItem](#MediaAnimatedGraphicsItem) | Information of the animated image generating result. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaAnimatedGraphicsItem
Information of the animated image generating result  
Used for calling the following APIs: DescribeMediaInfos, DescribeTaskDetail, PullEvents, SearchMedia.
| Name | Type | Description |
|------|------|-------|
| Url | String | Address of the generated animated image. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Definition | Integer | ID of the animated image generating template. For more information, see [Animated Image Generating Parameter Template](https://cloud.tencent.com/document/product/266/11701#.E9.A2.84.E7.BD.AE.E8.BD.AC.E5.8A.A8.E5.9B.BE.E6.A8.A1.E6.9D.BF). <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Container | String | Animated image format, such as gif. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Height | Integer | Height of the animated image in px. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Width | Integer | Width of the animated image in px. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Bitrate | Integer | Bit rate of the animated image in bps. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Size | Integer | Size of the animated image in bytes. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Md5 | String | MD5 value of the animated image. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| StartTimeOffset | Float | Start time offset of the animated image in the video in seconds. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| EndTimeOffset | Float | End time offset of the animated image in the video in seconds. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaAudioStreamItem
Information of the audio stream in the VOD file  
Used for calling the following APIs: DescribeMediaInfos, DescribeTaskDetail, LiveRealTimeClip, PullEvents, SearchMedia, SimpleHlsClip.
| Name | Type | Description |
|------|------|-------|
| Bitrate | Integer | Bit rate of the audio stream in bps. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| SamplingRate | Integer | Sample rate of the audio stream in Hz. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Codec | String | Codec of the audio stream, such as aac. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaBasicInfo
Basic information of the VOD media file  
Used for calling the following APIs: DescribeMediaInfos, PullEvents, SearchMedia.
| Name | Type | Description |
|------|------|-------|
| Name | String | Name of the media file. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Description | String | Description of the media file. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| CreateTime | String | Creation time of the media file in [ISO date format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| UpdateTime | String | Last update time of the media file (operations that trigger updating of media file information such as modifying video attributes or initiating video processing) in [ISO date format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| ExpireTime | String | Expiry time of the media file in [ISO date format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). After the expiry, the media file and its related resources (such as transcoded results and image sprites) will be permanently deleted. "9999-12-31T23:59:59Z" means "never expire". <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| ClassId | Integer | Category ID of the media file. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| ClassName | String | Category name of the media file. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| ClassPath | String | Category path of the media file separated by "-", such as "New First-level Category - New Second-level Category". <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| CoverUrl | String | Cover image address of the media file. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Type | String | Container of the media file, such as mp4 and flv. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| MediaUrl | String | URL of the original media file. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| SourceInfo | [MediaSourceData](#MediaSourceData) | Source information of the media file. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| StorageRegion | String | Storage region of the media file, such as ap-guangzhou. For more information, see [Region List](https://cloud.tencent.com/document/api/213/15692#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| TagSet | Array of String | Tag information of the media file. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Vid | String | Unique ID of the LVB recording file. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaClassInfo
Category information description  
Used for calling the following APIs: DescribeAllClass.
| Name | Type | Description |
|------|------|-------|
| ClassId | Integer | Category ID |
| ParentId | Integer | Parent category ID, which is -1 for a first-level category. |
| ClassName | String | Category name |
| Level | Integer | Category level. 0 for first-level category, up to 3, i.e., up to 4 levels of categories are allowed. |
| SubClassIdSet | Array of Integer | Set of immediate subcategories in the current category. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaContentReviewAsrTextSegmentItem
Suspected segment identified during ASR-based text review in content review  
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| StartTimeOffset | Float | Start time offset of the suspected segment in seconds. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| EndTimeOffset | Float | End time offset of the suspected segment in seconds. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Confidence | Float | Confidence of the suspected segment. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Suggestion | String | Suggestion for suspected segment review; value range: <br/><li>pass. </li><li>review. </li><li>block. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| KeywordSet | Array of String | List of suspected keywords. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaContentReviewOcrTextSegmentItem
Suspected segment identified during OCR-based text review in content review  
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| StartTimeOffset | Float | Start time offset of the suspected segment in seconds. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| EndTimeOffset | Float | End time offset of the suspected segment in seconds. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Confidence | Float | Confidence of the suspected segment. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Suggestion | String | Suggestion for suspected segment review; value range: <br/><li>pass. </li><li>review. </li><li>block. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| KeywordSet | Array of String | List of suspected keywords. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| AreaCoordSet | Array of Integer | Zone coordinates (at the pixel level) of the suspected text: [x1, y1, x2, y2], i.e., the coordinates of the top-left and bottom-right corners. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaContentReviewPoliticalSegmentItem
Suspected politically sensitive segment identified in content review  
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| StartTimeOffset | Float | Start time offset of the suspected segment in seconds. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| EndTimeOffset | Float | End time offset of the suspected segment in seconds. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Confidence | Float | Score of the suspected politically sensitive segment. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Suggestion | String | Suggestion for politically sensitive information detection of the suspected segment; value range: <br/><li>pass. </li><li>review. </li><li>block. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Name | String | Name of the politically sensitive figure or image. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Label | String | Tag of politically sensitive information detection result of the suspected segment. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Url | String | URL of the suspected image (which will not be permanently stored <br/>and will be deleted after PicUrlExpireTime). <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| AreaCoordSet | Array of Integer | Zone coordinates (at the pixel level) of the politically sensitive figure or image: [x1, y1, x2, y2], i.e., the coordinates of the top-left and bottom-right corners. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| PicUrlExpireTimeStamp | Integer | Expiry time of the suspected image URL in [ISO date format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaContentReviewSegmentItem
Suspected pornographic/terrorism segment identified in content review  
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| StartTimeOffset | Float | Start time offset of the suspected segment in seconds. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| EndTimeOffset | Float | End time offset of the suspected segment in seconds. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Confidence | Float | Score of the suspected pornographic segment. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Label | String | Tag of pornographic information detection result of the suspected segment. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Suggestion | String | Suggestion for pornographic information detection of the suspected segment; value range: <br/><li>pass. </li><li>review. </li><li>block. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Url | String | URL of the suspected image (which will not be permanently stored <br/>and will be deleted after PicUrlExpireTime). <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| PicUrlExpireTimeStamp | Integer | Expiry time of the suspected image URL in [ISO date format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaDeleteItem
Specify things to delete when deleting a VOD video
Referenced by: DeleteMedia.
| Name | Type | Required | Description |
|------|------|----------|------|
| Type | String | Yes | The specified part to be deleted. If this field is left blank, the parameter is invalid. Value range: <br/><li>TranscodeFiles: Delete the transcoded files. </li><li>WechatPublishFiles: Delete the files published on WeChat. </li> |
| Definition | Integer | No | ID of the template to delete the videos of the types specified by the Type parameter. For the template definition, see [Transcoding Template](https://cloud.tencent.com/document/product/266/11701#.E8.BD.AC.E7.A0.81.E6.A8.A1.E6.9D.BF). <br/>0 by default, which means to delete all videos in the type specified by the Type parameter. |
## MediaImageSpriteInfo
The image sprite of the VOD file  
Used for calling the following APIs: DescribeMediaInfos, SearchMedia.
| Name | Type | Description |
|------|------|-------|
| ImageSpriteSet | Array of [MediaImageSpriteItem](#MediaImageSpriteItem) | Information set of the image sprite of the specified type. Each element represents a set of image sprites in the same type. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaImageSpriteItem
Detailed information of the image sprite  
Used for calling the following APIs: DescribeMediaInfos, DescribeTaskDetail, PullEvents, SearchMedia.
| Name | Type | Description |
|------|------|-------|
| Definition | Integer | Image sprite type. For more information, see [Image Sprite Parameter Template](https://cloud.tencent.com/document/product/266/11702#.E9.9B.AA.E7.A2.A7.E5.9B.BE.E6.88.AA.E5.9B.BE.E6.A8.A1.E6.9D.BF). <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Height | Integer | Sub-image height of the image sprite. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Width | Integer | Sub-image width of the image sprite. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| TotalCount | Integer | Total number of sub-images in each image sprite. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| ImageUrlSet | Array of String | Address of each image sprite. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| WebVttUrl | String | Address of the WebVtt file for the position-time relationship among sub-images in the image sprite. The WebVtt file indicates the corresponding time points of each sub-image and their coordinates in the image sprite, which is typically used by the player for implementing preview. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaInfo
Information of the VOD file  
Used for calling the following APIs: DescribeMediaInfos, SearchMedia.
| Name | Type | Description |
|------|------|-------|
| BasicInfo | [MediaBasicInfo](#MediaBasicInfo) | Basic information. It includes video name, size, duration, cover image, etc. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| MetaData | [MediaMetaData](#MediaMetaData) | Metadata. It includes video stream information, audio stream information, etc. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| TranscodeInfo | [MediaTranscodeInfo](#MediaTranscodeInfo) | Information of the video transcoding result. It includes address, type, bitrate, resolution, etc. of the videos in various bitrates generated by transcoding the video. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| AnimatedGraphicsInfo | [MediaAnimatedGraphicsInfo](#MediaAnimatedGraphicsInfo) | Information of the animated image generating result. It includes information related to the animated image (such as .gif) generated from the video. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| SampleSnapshotInfo | [MediaSampleSnapshotInfo](#MediaSampleSnapshotInfo) | Information of the sampled screenshots. It includes information related to the sampled screenshots of the video. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| ImageSpriteInfo | [MediaImageSpriteInfo](#MediaImageSpriteInfo) | Information of the image sprites. It includes information related to the image sprites generated from the video. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| SnapshotByTimeOffsetInfo | [MediaSnapshotByTimeOffsetInfo](#MediaSnapshotByTimeOffsetInfo) | Information of the time point screenshots. It includes information of each screenshot generated by screencapturing the video at the specified time points. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| KeyFrameDescInfo | [MediaKeyFrameDescInfo](#MediaKeyFrameDescInfo) | Information of the timestamps. It includes information of each timestamp set for the video. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| FileId | String | Unique ID of the media file. |
## MediaInputInfo
Information, name, and customer ID of the source video to be processed
Referenced by: ProcessMediaByUrl.
| Name | Type | Required | Description |
|------|------|----------|------|
| Url | String | Yes | Video URL. |
| Name | String | No | Video name. |
| Id | String | No | Custom ID of the video. |
## MediaKeyFrameDescInfo
Information of the video timestamps
Referenced by: DescribeMediaInfos, SearchMedia.
| Name | Type | Description |
|------|------|-------|
| KeyFrameDescSet | Array of [MediaKeyFrameDescItem](#MediaKeyFrameDescItem) | Information array of the video timestamps. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaKeyFrameDescItem
Information of the video timestamps
Referenced by: DescribeMediaInfos, ModifyMediaInfo, SearchMedia.
| Name | Type | Required | Description |
|------|------|----------|------|
| TimeOffset | Float | Yes | Offset time of the timestamp in seconds. |
| Content | String | Yes | Content string of the timestamp of 1-128 characters. |
## MediaMetaData
Metadata of the VOD media file
Referenced by: DescribeMediaInfos, DescribeTaskDetail, LiveRealTimeClip, PullEvents, SearchMedia, SimpleHlsClip.
| Name | Type | Description |
|------|------|-------|
| Size | Integer | Size of the uploaded media file in bytes (which is the sum of the size of the m3u8 file and that of the ts file if the video is HLS). <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Container | String | Container, such as m4a and mp4. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Bitrate | Integer | Sum of the average bitrate of the video stream and that of the audio stream in bps. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Height | Integer | Maximum value of the video stream height in px. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Width | Integer | Maximum value of the video stream width in px. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Duration | Float | Video duration in seconds. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Rotate | Integer | Selected angle during video recording in degrees. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| VideoStreamSet | Array of [MediaVideoStreamItem](#MediaVideoStreamItem) | Information of the video stream. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| AudioStreamSet | Array of [MediaAudioStreamItem](#MediaAudioStreamItem) | Information of the audio stream. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| VideoDuration | Float | Video duration in seconds. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| AudioDuration | Float | Audio duration in seconds. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaOutputInfo
Information parameter of the output file of video processing
Referenced by: ProcessMediaByUrl.
| Name | Type | Required | Description |
|------|------|----------|------|
| Region | String | No | Region of the bucket where the output file is stored, such as ap-guangzhou. |
| Bucket | String | No | Bucket of the output file. |
| Dir | String | No | Path of the output file which must end in "/". |
## MediaProcessTaskAdaptiveDynamicStreamingResult
Result type of the conversion to adaptive bitrate task
Referenced by: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Status | String | Task status; value range: PROCESSING, SUCCESS, and FAIL. |
| ErrCode | Integer | Error code; 0 - success, other values - failure. |
| Message | String | Error message. |
| Input | [AdaptiveDynamicStreamingTaskInput](#AdaptiveDynamicStreamingTaskInput) | Input of the conversion to adaptive bitrate task. |
| Output | [AdaptiveDynamicStreamingInfoItem](#AdaptiveDynamicStreamingInfoItem) | Output of the conversion to adaptive bitrate task. |
## MediaProcessTaskAnimatedGraphicResult
Result type of the animated image generating task
Referenced by: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Status | String | Task status; value range: PROCESSING, SUCCESS, and FAIL. |
| ErrCode | Integer | Error code; 0 - success, other values - failure. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Input | [AnimatedGraphicTaskInput](#AnimatedGraphicTaskInput) | Input of the animated image generating task. |
| Output | [MediaAnimatedGraphicsItem](#MediaAnimatedGraphicsItem) | Output of the animated image generating task. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaProcessTaskCoverBySnapshotResult
Result type of the cover generating task
Referenced by: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Status | String | Task status; value range: PROCESSING, SUCCESS, and FAIL. |
| ErrCode | Integer | Error code; 0 - success, other values - failure. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Input | [CoverBySnapshotTaskInput](#CoverBySnapshotTaskInput) | Input of the cover generating task. |
| Output | [CoverBySnapshotTaskOutput](#CoverBySnapshotTaskOutput) | Output of the cover generating task. |
## MediaProcessTaskImageSpriteResult
Result type of the image sprite generating task
Referenced by: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Status | String | Task status; value range: PROCESSING, SUCCESS, and FAIL. |
| ErrCode | Integer | Error code; 0 - success, other values - failure. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Input | [ImageSpriteTaskInput](#ImageSpriteTaskInput) | Input of the image sprite generating task. |
| Output | [MediaImageSpriteItem](#MediaImageSpriteItem) | Output of the image sprite generating task. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaProcessTaskInput
Type of the video processing task
Referenced by: CreateProcedureTemplate, DescribeProcedureTemplates, ProcessMedia, ResetProcedureTemplate.
| Name | Type | Required | Description |
|------|------|----------|------|
| TranscodeTaskSet | Array of [TranscodeTaskInput](#TranscodeTaskInput) | No | List of transcoding tasks. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| AnimatedGraphicTaskSet | Array of [AnimatedGraphicTaskInput](#AnimatedGraphicTaskInput) | No | List of animated image generating tasks. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| SnapshotByTimeOffsetTaskSet | Array of [SnapshotByTimeOffsetTaskInput](#SnapshotByTimeOffsetTaskInput) | No | List of time point-based screencapturing tasks. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| SampleSnapshotTaskSet | Array of [SampleSnapshotTaskInput](#SampleSnapshotTaskInput) | No | List of sampling-based screencapturing tasks. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| ImageSpriteTaskSet | Array of [ImageSpriteTaskInput](#ImageSpriteTaskInput) | No | List of image sprite generating tasks. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| CoverBySnapshotTaskSet | Array of [CoverBySnapshotTaskInput](#CoverBySnapshotTaskInput) | No | List of cover generating tasks. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| AdaptiveDynamicStreamingTaskSet | Array of [AdaptiveDynamicStreamingTaskInput](#AdaptiveDynamicStreamingTaskInput) | No | List of conversion to adaptive bitrate tasks. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaProcessTaskResult
Result type of the querying task
Referenced by: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Type | String | Task type; value range: <br/><li>Transcode: Transcoding </li><li>AnimatedGraphics: Animated image generating </li><li>SnapshotByTimeOffset: Time point-based screencapturing </li><li>SampleSnapshot: Sampling-based screencapturing </li><li>ImageSprites: Image sprite generating </li><li>CoverBySnapshot: Cover generating </li><li>AdaptiveDynamicStreaming: Conversion to adaptive bitrate</li> |
| TranscodeTask | [MediaProcessTaskTranscodeResult](#MediaProcessTaskTranscodeResult) | Query result of the transcoding task, which is valid if task type is Transcode. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| AnimatedGraphicTask | [MediaProcessTaskAnimatedGraphicResult](#MediaProcessTaskAnimatedGraphicResult) | Query result of the animated image generating task, which is valid if task type is AnimatedGraphics. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| SnapshotByTimeOffsetTask | [MediaProcessTaskSnapshotByTimeOffsetResult](#MediaProcessTaskSnapshotByTimeOffsetResult) | Query result of the time point-based screencapturing task, which is valid if task type is SnapshotByTimeOffset. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| SampleSnapshotTask | [MediaProcessTaskSampleSnapshotResult](#MediaProcessTaskSampleSnapshotResult) | Query result of the sampling-based screencapturing task, which is valid if task type is SampleSnapshot. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| ImageSpriteTask | [MediaProcessTaskImageSpriteResult](#MediaProcessTaskImageSpriteResult) | Query result of the image sprite generating task, which is valid if task type is ImageSprite. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| CoverBySnapshotTask | [MediaProcessTaskCoverBySnapshotResult](#MediaProcessTaskCoverBySnapshotResult) | Query result of the cover generating task, which is valid if task type is CoverBySnapshot. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| AdaptiveDynamicStreamingTask | [MediaProcessTaskAdaptiveDynamicStreamingResult](#MediaProcessTaskAdaptiveDynamicStreamingResult) | Query result of the conversion to adaptive bitrate task, which is valid if task type is AdaptiveDynamicStreaming. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaProcessTaskSampleSnapshotResult
Type of the sampling-based screencapturing task result  
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Status | String | Task status; value range: PROCESSING, SUCCESS, and FAIL. |
| ErrCode | Integer | Error code; 0 - success, other values - failure. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Input | [SampleSnapshotTaskInput](#SampleSnapshotTaskInput) | Input of the sampling-based screencapturing task. |
| Output | [MediaSampleSnapshotItem](#MediaSampleSnapshotItem) | Output of the sampling-based screencapturing task. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaProcessTaskSnapshotByTimeOffsetResult
Type of the time point-based screencapturing task result  
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Status | String | Task status; value range: PROCESSING, SUCCESS, and FAIL. |
| ErrCode | Integer | Error code; 0 - success, other values - failure. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Input | [SnapshotByTimeOffsetTaskInput](#SnapshotByTimeOffsetTaskInput) | Input of the time point-based screencapturing task. |
| Output | [MediaSnapshotByTimeOffsetItem](#MediaSnapshotByTimeOffsetItem) | Output of the time point-based screencapturing task. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaProcessTaskTranscodeResult
Type of the transcoding task result  
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Status | String | Task status; value range: PROCESSING, SUCCESS, and FAIL. |
| ErrCode | Integer | Error code; 0 - success, other values - failure. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Input | [TranscodeTaskInput](#TranscodeTaskInput) | Input of the transcoding task. |
| Output | [MediaTranscodeItem](#MediaTranscodeItem) | Output of the transcoding task. |
## MediaSampleSnapshotInfo
Information of the sampled screenshot of the VOD file  
Used for calling the following APIs: DescribeMediaInfos, SearchMedia.
| Name | Type | Description |
|------|------|-------|
| SampleSnapshotSet | Array of [MediaSampleSnapshotItem](#MediaSampleSnapshotItem) | Information set of the sampled screenshots of the specified types. Each element represents a set of sampled screenshots of the same type. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaSampleSnapshotItem
Information of the sampled screenshots  
Used for calling the following APIs: DescribeMediaInfos, DescribeTaskDetail, PullEvents, SearchMedia.
| Name | Type | Description |
|------|------|-------|
| Definition | Integer | Type ID of the screenshot type. For more information, see [Sampling-based Screencapturing Parameter Template](https://cloud.tencent.com/document/product/266/11702#.E9.87.87.E6.A0.B7.E6.88.AA.E5.9B.BE.E6.A8.A1.E6.9D.BF). <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| SampleType | String | Sampling method; value range:<br/><li>Percent: Sample at the specified percentage interval. </li><li>Time: Sample at the specified time interval. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Interval | Integer | Sampling interval <br/><li>If SampleType is Percent, this value means to take a screenshot at an interval of the specified percentage. </li><li>If SampleType is Time, this value means to take a screenshot at an interval of the specified time. The first screenshot is always the first frame of the video. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| ImageUrlSet | Array of String | List of URLs of the generated screenshots. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| WaterMarkDefinition | Array of Integer | List of the watermarking template IDs if the screenshots are watermarked. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaSnapshotByTimeOffsetInfo
Information of the time point-based screenshots of the VOD file  
Used for calling the following APIs: DescribeMediaInfos, SearchMedia.
| Name | Type | Description |
|------|------|-------|
| SnapshotByTimeOffsetSet | Array of [MediaSnapshotByTimeOffsetItem](#MediaSnapshotByTimeOffsetItem) | Information of the time point screenshots of the specified type. Currently, there can be only one set of screenshots of each type. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaSnapshotByTimeOffsetItem
Information of the time point-based screenshots of the VOD file  
Used for calling the following APIs: DescribeMediaInfos, DescribeTaskDetail, PullEvents, SearchMedia.
| Name | Type | Description |
|------|------|-------|
| Definition | Integer | Type of the time point screenshot. For more information, see [Parameter Template for Time Point-based Screencapturing](https://cloud.tencent.com/document/product/266/11702#.E6.8C.87.E5.AE.9A.E6.97.B6.E9.97.B4.E7.82.B9.E6.88.AA.E5.9B.BE.E6.A8.A1.E6.9D.BF). <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| PicInfoSet | Array of [MediaSnapshotByTimePicInfoItem](#MediaSnapshotByTimePicInfoItem) | Information set of the screenshots of the same type. Each element represents a screenshot. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaSnapshotByTimePicInfoItem
Information of the time point screenshots  
Used for calling the following APIs: DescribeMediaInfos, DescribeTaskDetail, PullEvents, SearchMedia.
| Name | Type | Description |
|------|------|-------|
| TimeOffset | Float | Time offset corresponding to the screenshot in seconds. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Url | String | URL of the screenshot. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| WaterMarkDefinition | Array of Integer | List of the watermarking template IDs if the screenshots are watermarked. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaSourceData
Information of the source file  
Used for calling the following APIs: DescribeMediaInfos, PullEvents, SearchMedia.
| Name | Type | Description |
|------|------|-------|
| SourceType | String | Source type of the media file: <br/><li>Record: Recording, such as LVB recording and LVB offset recording. </li><li>Upload: Upload, such as pull upload, upload from the server, and UCG upload from the client. </li><li>VideoProcessing: Video processing, such as video stitching and video clipping. </li><li>Unknown: Unknown source. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| SourceContext | String | Field passed through when the file is created. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaTranscodeInfo
Transcoding information of the VOD file  
Used for calling the following APIs: DescribeMediaInfos, SearchMedia.
| Name | Type | Description |
|------|------|-------|
| TranscodeSet | Array of [MediaTranscodeItem](#MediaTranscodeItem) | Information set of the transcoding of each type. Each element represents the result of transcoding of a type. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaTranscodeItem
Transcoding information  
Used for calling the following APIs: DescribeMediaInfos, DescribeTaskDetail, PullEvents, SearchMedia.
| Name | Type | Description |
|------|------|-------|
| Url | String | Address of the transcoded video file. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Definition | Integer | Transcoding type ID. For more information, see [Transcoding Parameter Template](https://cloud.tencent.com/document/product/266/11701#.E8.BD.AC.E7.A0.81.E6.A8.A1.E6.9D.BF). <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Bitrate | Integer | Sum of the average bitrate of the video stream and that of the audio stream in bps. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Height | Integer | Maximum value of the video stream height in px. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Width | Integer | Maximum value of the video stream width in px. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Size | Integer | Total size of the media file in bytes (which is the sum of the size of the m3u8 file and that of the ts file if the video is HLS). <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Duration | Float | Video duration in seconds. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Container | String | Container, such as m4a and mp4. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Md5 | String | MD5 value of the video. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| AudioStreamSet | Array of [MediaAudioStreamItem](#MediaAudioStreamItem) | Information of the audio stream. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| VideoStreamSet | Array of [MediaVideoStreamItem](#MediaVideoStreamItem) | Information of the video stream. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## MediaVideoStreamItem
Information of the video stream in the VOD file  
Used for calling the following APIs: DescribeMediaInfos, DescribeTaskDetail, LiveRealTimeClip, PullEvents, SearchMedia, SimpleHlsClip.
| Name | Type | Description |
|------|------|-------|
| Bitrate | Integer | Bit rate of the video stream in bps. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Height | Integer | Height of the video stream in px. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Width | Integer | Width of the video stream in px. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Codec | String | Codec of the video stream, such as h264. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Fps | Integer | Frame rate in Hz. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## ProcedureTask
Information of the video processing task  
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| TaskId | String | ID of the video processing task. |
| Status | String | Task flow status; value range: <br/><li>PROCESSING: Processing; </li><li>FINISH: Finished. </li> |
| ErrCode | Integer | Error code <br/><li>0: Success; </li><li>Other values: Failure. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| FileId | String | Media file ID. <br/><li>If the process is initiated by [ProcessMedia](https://cloud.tencent.com/document/product/266/33427), this field means the FileId in [MediaInfo](https://cloud.tencent.com/document/product/266/31773#MediaInfo); </li><li>If the process is initiated by [ProcessMediaByUrl](https://cloud.tencent.com/document/product/266/33426), this field means the Id in [MediaInputInfo](https://cloud.tencent.com/document/product/266/31773#MediaInputInfo). </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| FileName | String | Media file name. <br/><li>If the process is initiated by [ProcessMedia](https://cloud.tencent.com/document/product/266/33427), this field means the BasicInfo.Name in [MediaInfo](https://cloud.tencent.com/document/product/266/31773#MediaInfo); </li><li>If the process is initiated by [ProcessMediaByUrl](https://cloud.tencent.com/document/product/266/33426), this field means the Name in [MediaInputInfo](https://cloud.tencent.com/document/product/266/31773#MediaInputInfo). </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| FileUrl | String | Media file address. <br/><li>If the process is initiated by [ProcessMedia](https://cloud.tencent.com/document/product/266/33427), this field means the BasicInfo.MediaUrl in [MediaInfo](https://cloud.tencent.com/document/product/266/31773#MediaInfo); </li><li>If the process is initiated by [ProcessMediaByUrl](https://cloud.tencent.com/document/product/266/33426), this field means the Url in [MediaInputInfo](https://cloud.tencent.com/document/product/266/31773#MediaInputInfo). </li> |
| MetaData | [MediaMetaData](#MediaMetaData) | Metadata of the original video. |
| MediaProcessResultSet | Array of [MediaProcessTaskResult](#MediaProcessTaskResult) | Execution status and result of the video processing task. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| AiContentReviewResultSet | Array of [AiContentReviewResult](#AiContentReviewResult) | Execution status and result of the video content review task. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| AiAnalysisResultSet | Array of [AiAnalysisResult](#AiAnalysisResult) | Execution status and result of the video content analysis task. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| TasksPriority | Integer | Priority of the task flow; value range: [-10, 10]. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| TasksNotifyMode | String | Notification mode for the change in task flow status. <br/><li>Finish: An event notification is initiated only after the task flow is completely executed; </li><li>Change: An event notification is initiated as soon as the status of a sub-task in the task flow changes; </li><li>None: The callback for the task flow is not accepted. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| SessionContext | String | The source context which is used to pass through the user request information. The task flow status change callback returns the value of this field. Up to 250 characters. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| SessionId | String | The ID used for deduplication. If there was a request with the same ID in the past seven days, the current request will return an error. Up to 50 characters. If missing or with a blank string, no deduplication is performed. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## ProcedureTemplate
Details of task flow template  
Used for calling the following APIs: DescribeProcedureTemplates.
| Name | Type | Description |
|------|------|-------|
| Name | String | Task flow name. |
| MediaProcessTask | [MediaProcessTaskInput](#MediaProcessTaskInput) | Parameter of the video processing task. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| AiContentReviewTask | [AiContentReviewTaskInput](#AiContentReviewTaskInput) | Parameter of the AI-based content review task. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| AiAnalysisTask | [AiAnalysisTaskInput](#AiAnalysisTaskInput) | Parameter of the AI-based content analysis task. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| AiRecognitionTask | [AiRecognitionTaskInput](#AiRecognitionTaskInput) | Parameter of the AI-based content recognition task. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| CreateTime | String | Creation time of the template in [ISO date format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). |
| UpdateTime | String | Last modified time of the template in [ISO date format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). |
## PullFileTask
Information of the video upstream task
Used for calling the following APIs: PullEvents.
| Name | Type | Description |
|------|------|-------|
| TaskId | String | ID of the pull and upload task. |
| ErrCode | Integer | Error code <br/><li>0: Success; </li><li>Other values: Failure. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| FileId | String | ID of the video generated after pull and upload. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| FileUrl | String | Playback address generated after pull and upload. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| ProcedureTaskId | String | If a video processing flow is specified when the video is pulled and uploaded, this parameter is the ID of the task flow. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## SampleSnapshotTaskInput
Type of the input parameters of the sampling-based screencapturing task  
Used for calling the following APIs: CreateProcedureTemplate, DescribeProcedureTemplates, DescribeTaskDetail, ProcessMedia, PullEvents, ResetProcedureTemplate.
| Name | Type | Required | Description |
|------|------|----------|------|
| Definition | Integer | Yes | ID of the sampled screencapturing template. |
| WatermarkSet | Array of [WatermarkInput](#WatermarkInput) | No | List of up to 10 image or text watermarks. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## SnapshotByTimeOffset2017
 (v2017)
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| ErrCode | Integer | Error code <br/><li>0: Success; </li><li>Other values: Failure. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| TimeOffset | Integer | Specific time point of the screenshot in milliseconds. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Url | String | Address of the screencapturing output file. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## SnapshotByTimeOffsetTask2017
Information of the time point-based screencapturing task. This structure is only used for tasks initiated by the [time point-based screencapturing](https://cloud.tencent.com/document/product/266/8102) API in v2017.  
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| TaskId | String | Screencapturing task ID. |
| FileId | String | Screenshot file ID. |
| Definition | Integer | Screenshot type. For more information, see [Parameter Template for Time Point-based Screencapturing](https://cloud.tencent.com/document/product/266/11702#.E6.8C.87.E5.AE.9A.E6.97.B6.E9.97.B4.E7.82.B9.E6.88.AA.E5.9B.BE.E6.A8.A1.E6.9D.BF). |
| SnapshotInfoSet | Array of [SnapshotByTimeOffset2017](#SnapshotByTimeOffset2017) | Screencapturing result information. |
## SnapshotByTimeOffsetTaskInput
Input parameter type of the time point-based screencapturing task  
Used for calling the following APIs: CreateProcedureTemplate, DescribeProcedureTemplates, DescribeTaskDetail, ProcessMedia, PullEvents, ResetProcedureTemplate.
| Name | Type | Required | Description |
|------|------|----------|------|
| Definition | Integer | Yes | ID of the time point-based screencapturing template. |
| TimeOffsetSet | Array of Float | Yes | List of the time points of screenshots in milliseconds. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| WatermarkSet | Array of [WatermarkInput](#WatermarkInput) | No | List of up to 10 image or text watermarks. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## SortBy
Sort by criterion  
Used for calling the following APIs: SearchMedia.
| Name | Type | Description |
|------|------|-------|
| Field | String | Sorted field |
| Order | String | Sorting order; value range: Asc (ascending) and Desc (descending) |
## SvgWatermarkInput
Input parameter of the SVG watermarking template  
Used for calling the following APIs: CreateWatermarkTemplate.
| Name | Type | Required | Description |
|------|------|----------|------|
| Width | String | No | Watermark width, which supports six formats of px, %, W%, H%, S%, and L%: <br/><li>If the string ends in px, the watermark width is in px, for example, 100px means that Width is 100 px; if 0px is entered and Height is not 0px, the watermark width is proportionally scaled based on the original SVG image; if 0px is entered for both Width and Height, the watermark width is the width of the original SVG image; </li><li>If the string ends in W%, the watermark width is the specified percentage of the video width, for example, 10W% means that Width is 10% of the video width; </li><li>If the string ends in H%, the watermark width is the specified percentage of the video height, for example, 10H% means that Width is 10% of the video height; </li><li>If the string ends in S%, the watermark width is the specified percentage of the short side of the video, for example, 10S% means that Width is 10% of the short side of the video; </li><li>If the string ends in L%, the watermark width is the specified percentage of the long side of the video, for example, 10L% means that Width is 10% of the long side of the video;</li><li>If the string ends in %, the meaning is the same as W%. </li><br/>Default value: 10W%. |
| Height | String | No | Watermark height, which supports six formats of px, %, W%, H%, S%, and L%: <br/><li>If the string ends in px, the watermark height is in px, for example, 100px means that Height is 100 px; if 0px is entered and Width is not 0px, the watermark height is proportionally scaled based on the original SVG image; if 0px is entered for both Width and Height, the watermark height is the height of the original SVG image; </li><li>If the string ends in W%, the watermark height is the specified percentage of the video width, for example, 10W% means that Height is 10% of the video width; </li><li>If the string ends in H%, the watermark height is the specified percentage of the video height, for example, 10H% means that Height is 10% of the video height; </li><li>If the string ends in S%, the watermark height is the specified percentage of the short side of the video, for example, 10S% means that Height is 10% of the short side of the video; </li><li>If the string ends in L%, the watermark height is the specified percentage of the long side of the video, for example, 10L% means that Height is 10% of the long side of the video;</li><li>If the string ends in %, the meaning is the same as H%. </li><br/>Default value: 0px. |
## SvgWatermarkInputForUpdate
Input parameter of the SVG watermarking template  
Used for calling the following APIs: ModifyWatermarkTemplate.
| Name | Type | Required | Description |
|------|------|----------|------|
| Width | String | No | Watermark width, which supports six formats of px, %, W%, H%, S%, and L%: <br/><li>If the string ends in px, the watermark width is in px, for example, 100px means that Width is 100 px; if 0px is entered and Height is not 0px, the watermark width is proportionally scaled based on the original SVG image; if 0px is entered for both Width and Height, the watermark width is the width of the original SVG image; </li><li>If the string ends in W%, the watermark width is the specified percentage of the video width, for example, 10W% means that Width is 10% of the video width; </li><li>If the string ends in H%, the watermark width is the specified percentage of the video height, for example, 10H% means that Width is 10% of the video height; </li><li>If the string ends in S%, the watermark width is the specified percentage of the short side of the video, for example, 10S% means that Width is 10% of the short side of the video; </li><li>If the string ends in L%, the watermark width is the specified percentage of the long side of the video, for example, 10L% means that Width is 10% of the long side of the video;</li><li>If the string ends in %, the meaning is the same as W%. </li><br/>Default value: 10W%. |
| Height | String | No | Watermark height, which supports six formats of px, %, W%, H%, S%, and L%: <br/><li>If the string ends in px, the watermark height is in px, for example, 100px means that Height is 100 px; if 0px is entered and Width is not 0px, the watermark height is proportionally scaled based on the original SVG image; if 0px is entered for both Width and Height, the watermark height is the height of the original SVG image; </li><li>If the string ends in W%, the watermark height is the specified percentage of the video width, for example, 10W% means that Height is 10% of the video width; </li><li>If the string ends in H%, the watermark height is the specified percentage of the video height, for example, 10H% means that Height is 10% of the video height; </li><li>If the string ends in S%, the watermark height is the specified percentage of the short side of the video, for example, 10S% means that Height is 10% of the short side of the video; </li><li>If the string ends in L%, the watermark height is the specified percentage of the long side of the video, for example, 10L% means that Height is 10% of the long side of the video;</li><li>If the string ends in %, the meaning is the same as H%. <br/>Default value: 0px. |
## TaskSimpleInfo
Summary of the task   
Used for calling the following APIs: DescribeTasks.
| Name | Type | Description |
|------|------|-------|
| TaskId | String | Task ID. |
| TaskType | String | Task type; value range: <br/><li>Procedure: Video processing task; </li><li>EditMedia: Video editing task; </li><li>WechatDistribute: Publishing on WeChat task. </li><br/>Task types compatible with v2017: <br/><li>Transcode: Video transcoding task; </li><li>SnapshotByTimeOffset: Screencapturing task: </li><li>Concat: Video stitching task; </li><li>Clip: Video clipping task; </li><li>ImageSprites: Image sprite creating task. </li> |
| CreatTime | String | Creation time of the task in [ISO date format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). |
| BeginProcessTime | String | Start time of task execution in [ISO date format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). If the task has not been started yet, this field is blank. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| FinishTime | String | End time of the task in [ISO date format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). If the task has not been completed yet, this field is blank. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## TempCertificate
Temporary credentials  
Used for calling the following APIs: ApplyUpload.
| Name | Type | Description |
|------|------|-------|
| SecretId | String | ID of the temporary security certificate. |
| SecretKey | String | Key of the temporary security certificate. |
| Token | String | Token value. |
| ExpiredTime | Integer | Expiry time of the certificate. A Unix timestamp is returned which is accurate down to the second. |
## TextWatermarkTemplateInput
Text watermarking template  
Used for calling the following APIs: CreateWatermarkTemplate, DescribeWatermarkTemplates.
| Name | Type | Required | Description |
|------|------|----------|------|
| FontType | String | Yes | Font type; currently, only arial.ttf is supported. |
| FontSize | String | Yes | Font size in Npx format where N is a numeric value. |
| FontColor | String | Yes | Font color in 0xRRGGBB format; default value: 0xFFFFFF (black). |
| FontAlpha | Float | Yes | Text transparency; value range: (0, 1] <br/><li>0: Completely transparent </li><li>1: Completely opaque </li><br/>Default Value: 1. |
## TextWatermarkTemplateInputForUpdate
Text watermarking template  
Used for calling the following APIs: ModifyWatermarkTemplate.
| Name | Type | Required | Description |
|------|------|----------|------|
| FontType | String | No | Font type; currently, only arial.ttf is supported. |
| FontSize | String | No | Font size in Npx format where N is a numeric value. |
| FontColor | String | No | Font color in 0xRRGGBB format; default value: 0xFFFFFF (black). |
| FontAlpha | Float | No | Text transparency; value range: (0, 1] <br/><li>0: Completely transparent </li><li>1: Completely opaque </li> |
## TranscodePlayInfo2017
Information of video transcoding playback (v2017)  
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| Url | String | Playback address. |
| Definition | Integer | Transcoding type ID. For more information, see [Transcoding Parameter Template](https://cloud.tencent.com/document/product/266/11701#.E8.BD.AC.E7.A0.81.E6.A8.A1.E6.9D.BF). |
| Bitrate | Integer | Sum of the average bitrate of the video stream and that of the audio stream in bps. |
| Height | Integer | Maximum value of the video stream height in px. |
| Width | Integer | Maximum value of the video stream width in px. |
## TranscodeTask2017
Information of the video transcoding task. This structure is only used for tasks initiated by the [video transcoding](https://cloud.tencent.com/document/product/266/7822) API in v2017.
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| TaskId | String | Transcoding task ID. |
| ErrCode | Integer | Error code <br/><li>0: Success; </li><li>Other values: Failure. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| FileId | String | ID of the transcoded file. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| FileName | String | Name of the transcoded file. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Duration | Integer | Video duration in seconds. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| CoverUrl | String | Cover address. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| PlayInfoSet | Array of [TranscodePlayInfo2017](#TranscodePlayInfo2017) | Playback information generated after video transcoding. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## TranscodeTaskInput
Types of the transcoding task parameters
Used for calling the following APIs: CreateProcedureTemplate, DescribeProcedureTemplates, DescribeTaskDetail, ProcessMedia, PullEvents, ResetProcedureTemplate.
| Name | Type | Required | Description |
|------|------|----------|------|
| Definition | Integer | Yes | ID of the video transcoding template. |
| WatermarkSet | Array of [WatermarkInput](#WatermarkInput) | No | List of up to 10 image or text watermarks. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## TranscodeTemplate
Details of the transcoding template  
Used for calling the following APIs: DescribeTranscodeTemplates.
| Name | Type | Description |
|------|------|-------|
| Definition | String | Unique ID of the transcoding template. |
| Container | String | Container; value range: mp4, flv, hls, mp3, flac, and ogg. |
| Name | String | Name of the transcoding template. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Comment | String | Template description. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Type | String | Template type; value range: <br/><li>Preset: Preset template; </li><li>Custom: Custom template. </li> |
| RemoveVideo | Integer | Whether to remove the video data; value range: <br/><li>0: No; </li><li>1: Yes. </li> |
| RemoveAudio | Integer | Whether to remove the audio data; value range: <br/><li>0: No; </li><li>1: Yes. </li> |
| VideoTemplate | [VideoTemplateInfo](#VideoTemplateInfo) | Video stream configuration parameter. This field is valid only when RemoveVideo is 0. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| AudioTemplate | [AudioTemplateInfo](#AudioTemplateInfo) | Audio stream configuration parameter. This field is valid only when RemoveAudio is 0. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| ContainerType | String | Filter of container; value range: <br/><li>Video: Video container that can contain both video stream and audio stream; </li><li>PureAudio: Audio container that can contain only audio stream. </li> |
| CreateTime | String | Creation time of the template in [ISO date format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). |
| UpdateTime | String | Last modified time of the template in [ISO date format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). |
## VideoTemplateInfo
Video stream configuration parameters
Used for calling the following APIs: CreateTranscodeTemplate, DescribeTranscodeTemplates.
| Name | Type | Required | Description |
|------|------|----------|------|
| Codec | String | Yes | Codec of the video stream; value range: <br/><li>libx264: H.264 encoding </li><li>libx265: H.265 encoding </li><br/>Currently, a resolution within 640\*480 must be specified for H.265 encoding |
| Fps | Integer | Yes | Video frame rate in Hz; value range: [0, 60]. <br/>If the value is 0, the frame rate is the same as that of the original video. |
| Bitrate | Integer | Yes | Bit rate of the video stream; value range: 0 or [128, 35000] in Kbps. <br/>If the value is 0, the bitrate of the video is the same as that of the original video. |
| ResolutionAdaptive | String | No | Adaptive resolution; value range: <br/><li>open: Enabled. In this case, Width represents the width of the video, and Height the height; </li><li>close: Disabled. In this case, Width represents the long side of the video, and Height the short side. </li><br/>Default value: open. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Width | Integer | No | Maximum value of the width (or long side) video stream in px; value range: 0 and [128, 4096]. <br/><li>If both Width and Height are 0, the resolution is the same as that of the source video; </li><li>If Width is 0 but Height is not 0, Width is proportionally scaled; </li><li>If Width is not 0 but Height is 0, Height is proportionally scaled; </li><li>If both Width and Height are not 0, the resolution is specified by the user. </li><br/>Default value: 0. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Height | Integer | No | Maximum value of the width (or short side) video stream in px; value range: 0 and [128, 4096]. <br/><li>If both Width and Height are 0, the resolution is the same as that of the source video; </li><li>If Width is 0 but Height is not 0, Width is proportionally scaled; </li><li>If Width is not 0 but Height is 0, Height is proportionally scaled; </li><li>If both Width and Height are not 0, the resolution is specified by the user. </li><br/>Default value: 0. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## VideoTemplateInfoForUpdate
Video stream configuration parameter  
Used for calling the following APIs: ModifyTranscodeTemplate.
| Name | Type | Required | Description |
|------|------|----------|------|
| Codec | String | No | Codec of the video stream; value range: <br/><li>libx264: H.264 encoding </li><li>libx265: H.265 encoding </li><br/>Currently, a resolution within 640\*480 must be specified for H.265 encoding |
| Fps | Integer | No | Video frame rate in Hz; value range: [0, 60]. <br/>If the value is 0, the frame rate is the same as that of the original video. |
| Bitrate | Integer | No | Bit rate of the video stream; value range: 0 or [128, 35000] in Kbps. <br/>If the value is 0, the bitrate of the video is the same as that of the original video. |
| ResolutionAdaptive | String | No | Adaptive resolution; value range: <br/><li>open: Enabled. In this case, Width represents the width of the video, and Height the height; </li><li>close: Disabled. In this case, Width represents the long side of the video, and Height the short side. </li> |
| Width | Integer | No | Maximum value of the width (or long side) video stream in px; value range: 0 and [128, 4096]. <br/><li>If both Width and Height are 0, the resolution is the same as that of the source video; </li><li>If Width is 0 but Height is not 0, Width is proportionally scaled; </li><li>If Width is not 0 but Height is 0, Height is proportionally scaled; </li><li>If both Width and Height are not 0, the resolution is specified by the user. </li> |
| Height | Integer | No | Maximum value of the width (or short side) video stream in px; value range: 0 and [128, 4096]. |
## WatermarkInput
Watermark parameter type of the video processing task  
Used for calling the following APIs: CreateProcedureTemplate, DescribeProcedureTemplates, DescribeTaskDetail, ProcessMedia, PullEvents, ResetProcedureTemplate.
| Name | Type | Required | Description |
|------|------|----------|------|
| Definition | Integer | Yes | ID of the watermarking template. |
| TextContent | String | No | Text content of up to 100 characters. This is to be entered only when the watermark type is text. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| SvgContent | String | No | SVG content. Up to 2,000,000 characters. This is to be entered only when the watermark type is SVG. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
## WatermarkTemplate
Watermarking template details
Used for calling the following APIs: DescribeWatermarkTemplates.
| Name | Type | Description |
|------|------|-------|
| Definition | Integer | Unique ID of the watermarking template. |
| Type | String | Watermark type; value range: <br/><li>image: Image watermark; </li><li>text: Text watermark. </li> |
| Name | String | Name of the watermarking template. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Comment | String | Template description. |
| XPos | String | The horizontal position of the origin of the watermark image relative to the origin of the video. <br/><li>If the string ends in %, the left edge of the watermark is at the position of the specified percentage of the video width, for example, 10% means that the left edge is at 10% of the video width; </li><li>if the string ends in px, the left edge of the watermark is at the position of the specified px of the video width, for example, 100px means that the left edge is at the position of 100px. </li> |
| YPos | String | The vertical position of the origin of the watermark image relative to the origin of the video. <br/><li>If the string ends in %, the top edge of the watermark is at the position of the specified percentage of the video height, for example, 10% means that the top edge is at 10% of the video height; </li><li>if the string ends in px, the top edge of the watermark is at the position of the specified px of the video height, for example, 100px means that the top edge is at the position of 100px. </li> |
| ImageTemplate | [ImageWatermarkTemplate](#ImageWatermarkTemplate) | Image watermarking template. This field has a value only when Type is image. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| TextTemplate | [TextWatermarkTemplateInput](#TextWatermarkTemplateInput) | Text watermarking template. This field has a value only when Type is text. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| CreateTime | String | Creation time of the template in [ISO date format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). |
| UpdateTime | String | Last modified time of the template in [ISO date format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). |
| CoordinateOrigin | No | String | Origin position; value range: <br/><li>topLeft: The origin of coordinates is in the top-left corner of the video, and the origin of the watermark is in the top-left corner of the image or text; </li><li>topRight: The origin of coordinates is in the top-right corner of the video, and the origin of the watermark is in the top-right corner of the image or text; </li><li>bottomLeft: The origin of coordinates is in the bottom-left corner of the video, and the origin of the watermark is in the bottom-left corner of the image or text; </li><li>bottomRight: The origin of coordinates is in the bottom-right corner of the video, and the origin of the watermark is in the bottom-right corner of the image or text. </li> |
## WechatPublishTask
Information of the publishing on WeChat task  
Used for calling the following APIs: DescribeTaskDetail, PullEvents.
| Name | Type | Description |
|------|------|-------|
| TaskId | String | Task ID. |
| Status | String | Task status; value range: <br/>WAITING: Waiting; <br/>PROCESSING: Processing; <br/>FINISH: Finished. |
| ErrCode | Integer | Error code <br/><li>0: Success; </li><li>Other values: Failure. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Message | String | Error message. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| FileId | String | ID of the published video file. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Definition | Integer | ID of the publishing on WeChat template. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| SourceDefinition | Integer | ID of the transcoding template corresponding to the published video; 0 represents the original video. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| WechatStatus | String | Publishing on WeChat status; value range: <br/><li>FAIL: Failed; </li><li>SUCCESS: Succeeded; </li><li>AUDITNOTPASS: Disapproved; </li><li>NOTTRIGGERED: Publishing on WeChat not initiated yet. </li><br/>Note: This field may return null, indicating that no effective values can be obtained. |
| WechatVid | String | WeChat Vid. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| WechatUrl | String | WeChat address. <br/>Note: This field may return null, indicating that no effective values can be obtained. |

