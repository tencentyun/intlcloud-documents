## Error Code Description
When an API call fails, an *Error* is returned in the result. For example:
```
 {
    "Response": {
        "Error": {
            "Code": "AuthFailure.SignatureFailure",
            "Message": "The provided credentials could not be validated. Please check your signature is correct."
        },
        "RequestId": "ed93f3cb-f35e-473f-b9f3-0d451b8b79c6"
    }
}
```
In *Error*, *Code* indicates the error code, and *Message* specifies the detailed information of the error.

## Error Code List
### Common Error Codes

| Error code | Description |
|--------|------|
| AuthFailure.InvalidSecretId | Invalid key (not TencentCloud API key type). |
| AuthFailure.MFAFailure | MFA error. |
| AuthFailure.SecretIdNotFound | Key does not exist. Please check whether the key has been deleted or disabled in the console. If the status is normal, please check whether the key is entered correctly. Please note that there must be no leading or trailing spaces. |
| AuthFailure.SignatureExpire | Signature expired. Timestamp and server time must not differ by more than five minutes. Please check whether the local time matches the standard time. |
| AuthFailure.SignatureFailure | Signature error. Signature calculation error. Please check the signature calculation process against the API authentication document in Calling Methods. |
| AuthFailure.TokenFailure | Token error. |
| AuthFailure.UnauthorizedOperation | Request not authorized through CAM. |
| DryRunOperation | DryRun operation, which means the request will succeed, but an unnecessary DryRun parameter is passed in. |
| FailedOperation | Operation failed. |
| InternalError | Internal error |
| InvalidAction | API does not exist. |
| InvalidParameter | Parameter error |
| InvalidParameterValue | Incorrect parameter value. |
| LimitExceeded | Quota limit is exceeded. |
| MissingParameter | Parameter missing. |
| NoSuchVersion | API version does not exist. |
| RequestLimitExceeded | The number of requests exceeds the rate limit. |
| ResourceInUse | Resource is in use. |
| ResourceInsufficient | Insufficient resource. |
| ResourceNotFound | Resource does not exist. |
| ResourceUnavailable | Resource not available. |
| UnauthorizedOperation | Unauthorized operation. |
| UnknownParameter | Unknown parameter error. |
| UnsupportedOperation | Unsupported operation. |
| UnsupportedProtocol | HTTP(S) request protocol error; only GET and POST requests are supported. |
| UnsupportedRegion | API does not support the passing region. |
### Business Error Codes
| Error code | Description |
|:-------|:-----|
| FailedOperation | Operation failed. |
| FailedOperation.ClassLevelLimitExceeded | Operation failed: The number of category levels exceeds the limit. |
| FailedOperation.ClassNameDuplicate | Operation failed: The category name already exists. |
| FailedOperation.ClassNoFound | Operation failed: The category does not exist. |
| FailedOperation.ParentIdNoFound | Operation failed: The parent category ID does not exist. |
| FailedOperation.SubclassLimitExceeded | Operation failed: The number of subcategories exceeds the limit. |
| FailedOperation.TaskDuplicate | Operation failed: The task already exists. |
| InternalError | Internal error |
| InternalError.GetFileInfoError | Internal error: Error getting media file information. |
| InternalError.GetMediaListError | Internal error: Error getting media list. |
| InternalError.UpdateMediaError | Internal error: Error updating media file information. |
| InternalError.UploadCoverImageError | Internal error: Error uploading cover image. |
| InternalError.UploadWatermarkError | Internal error: Watermark image upload failed. |
| InvalidParameter | Parameter error |
| InvalidParameter.ExistedProcedureName | The task flow template name already exists. |
| InvalidParameter.ExpireTime | Incorrect parameter value: Expiry time. |
| InvalidParameter.ProcedureNameNotExist | The task flow template name does not exist |
| InvalidParameterValue | Incorrect parameter value. |
| InvalidParameterValue.AddKeyFrameDescsAndClearKeyFrameDescsConflict | Incorrect parameter value: AddKeyFrameDescs conflicts with ClearKeyFrameDescs. |
| InvalidParameterValue.AddKeyFrameDescsAndDeleteKeyFrameDescsConflict | Incorrect parameter value: AddKeyFrameDescs conflicts with DeleteKeyFrameDescs. |
| InvalidParameterValue.AddTagsAndClearTagsConflict | Incorrect parameter value: AddTags conflicts with ClearTags. |
| InvalidParameterValue.AddTagsAndDeleteTagsConflict | Incorrect parameter value: AddTags conflicts with DeleteTags. |
| InvalidParameterValue.AiAnalysisTaskDefinition | Incorrect parameter value: AI-based analysis definition. |
| InvalidParameterValue.AiContentReviewTaskDefinition | Incorrect parameter value: AI-based content review definition. |
| InvalidParameterValue.AudioBitrate | Parameter error: Audio stream bitrate. |
| InvalidParameterValue.AudioChannel | Incorrect parameter value: AudioChannel. |
| InvalidParameterValue.AudioCodec | Parameter error: Audio stream codec. |
| InvalidParameterValue.AudioSampleRate | Parameter error: Audio stream sample rate. |
| InvalidParameterValue.ClassId | Incorrect parameter value: Category ID. |
| InvalidParameterValue.ClassIds | Incorrect parameter value: ClassIds is invalid. |
| InvalidParameterValue.ClassName | Incorrect parameter value: ClassName is invalid. |
| InvalidParameterValue.ClipDuration | Incorrect parameter value: Clipping duration is too long. |
| InvalidParameterValue.Comment | Parameter error: Template description. |
| InvalidParameterValue.Container | Parameter error: Container. |
| InvalidParameterValue.ContainerType | Incorrect parameter value: ContainerType. |
| InvalidParameterValue.CoordinateOrigin | Parameter error: CoordinateOrigin. |
| InvalidParameterValue.CoverType | Incorrect parameter value: Cover type. |
| InvalidParameterValue.Definition | Incorrect parameter value: Definition. |
| InvalidParameterValue.Definitions | Incorrect parameter value: Definitions. |
| InvalidParameterValue.Description | Incorrect parameter value: Description exceeds the length limit. |
| InvalidParameterValue.EndTime | Incorrect parameter value: EndTime is invalid. |
| InvalidParameterValue.ExpireTime | Incorrect parameter value: ExpireTime is in wrong format. |
| InvalidParameterValue.FileId | FileId does not exist. |
| InvalidParameterValue.Fps | Parameter error: Frame rate. |
| InvalidParameterValue.Height | Parameter error: Height. |
| InvalidParameterValue.ImageTemplate | Parameter error: Image watermarking template. |
| InvalidParameterValue.KeyFrameDescContentTooLong | Incorrect parameter value: Timestamp content is too long. |
| InvalidParameterValue.Limit | Parameter error: Limit. |
| InvalidParameterValue.MediaType | Incorrect parameter value: Media type. |
| InvalidParameterValue.Name | Parameter error: Name exceeds the length limit. |
| InvalidParameterValue.Names | Too many elements in the Names array. |
| InvalidParameterValue.Offset | Incorrect parameter value: Offset is invalid. |
| InvalidParameterValue.ParentId | Incorrect parameter value: ParentId is invalid. |
| InvalidParameterValue.RemoveAudio | Incorrect parameter value: RemoveAudio. |
| InvalidParameterValue.RemoveVideo | Incorrect parameter value: RemoveVideo. |
| InvalidParameterValue.RepeatType | Incorrect parameter value: RepeatType is invalid. |
| InvalidParameterValue.Resolution | Parameter error: Resolution. |
| InvalidParameterValue.SessionContextTooLong | SessionContext is too long. |
| InvalidParameterValue.SessionId | The deduplication ID already exists. The request is removed due to duplication. |
| InvalidParameterValue.SessionIdTooLong | SessionId is too long. |
| InvalidParameterValue.Sort | Incorrect parameter value: Sort is invalid. |
| InvalidParameterValue.SourceType | Incorrect parameter value: SourceType is invalid. |
| InvalidParameterValue.StartTime | Incorrect parameter value: StartTime is invalid. |
| InvalidParameterValue.Status | Incorrect parameter value: The value of human confirmation result is invalid. |
| InvalidParameterValue.StreamIdInvalid | Incorrect parameter value: StreamId is invalid. |
| InvalidParameterValue.SubAppId | Incorrect parameter value: Sub-application ID |
| InvalidParameterValue.TagTooLong | Incorrect parameter value: Tag too long. |
| InvalidParameterValue.Tags | Incorrect parameter value: Tags is invalid. |
| InvalidParameterValue.TaskId | The task ID does not exist. |
| InvalidParameterValue.Text | Incorrect parameter value: Search text. |
| InvalidParameterValue.TextAlpha | Parameter error: Text transparency. |
| InvalidParameterValue.TextTemplate | Parameter error: Text template. |
| InvalidParameterValue.Type | Incorrect Type parameter value. |
| InvalidParameterValue.VideoBitrate | Parameter error: Video stream bitrate. |
| InvalidParameterValue.VideoCodec | Parameter error: Video stream codec. |
| InvalidParameterValue.VodSessionKey | Incorrect parameter value: VOD session. |
| InvalidParameterValue.Width | Parameter error: Width. |
| InvalidParameterValue.XPos | The horizontal position of the origin of the watermark relative to the origin of coordinates of the video. % and px formats are supported. |
| InvalidParameterValue.YPos | The vertical position of the origin of the watermark relative to the origin of coordinates of the video. % and px formats are supported. |
| LimitExceeded | Quota limit is exceeded. |
| LimitExceeded.KeyFrameDescCountReachMax | Limit exceeded: The total number of new and old timestamps exceeds the limit. |
| LimitExceeded.TagCountReachMax | The total number of new and old tags exceeds the limit. |
| LimitExceeded.TooMuchTemplate | Limit exceeded: The number of templates exceeds the limit. |
| ResourceNotFound | Resource does not exist. |
| ResourceNotFound.FileNotExist | Resource does not exist: The file does not exist. |
| ResourceNotFound.TemplateNotExist | Resource does not exist: The template does not exist. |
| UnsupportedOperation.ClassNotEmpty | Non-empty categories cannot be deleted. |

