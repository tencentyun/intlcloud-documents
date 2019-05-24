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
| AuthFailure.InvalidSecretId | The provided SecretId could not be validated (the type of the SecretId may not be authorized by TencentCloud API). |
| AuthFailure.MFAFailure | Multi-factor authentication (MFA) error. |
| AuthFailure.SecretIdNotFound | The provided SecretId could not be found. The key may have been deleted or disabled in the console, or you may have entered the SecretId correctly, where no leading or trailing spaces are allowed.|
| AuthFailure.SignatureExpire | The Signature has expired. The difference between Timestamp and server time needs to be no larger than five minutes. Please ensure your local time matches the standard time. |
| AuthFailure.SignatureFailure | The Signature was not calculated. Please follow the  API authentication documentation to calculate the signature. |
| AuthFailure.TokenFailure | Token error. |
| AuthFailure.UnauthorizedOperation | CAM did not authorize this request. |
| DryRunOperation | DryRun operation. It means that the request would have succeeded, but the DryRun parameter was used. |
| FailedOperation | The operation failed. |
| InternalError | The error is caused internally. |
| InvalidAction | The API or action requested is not valid. |
| InvalidParameter | A parameter is not valid or cannot be used for the request.  |
| InvalidParameterValue | A value specified in a parameter is not valid or cannot be used for this request. |
| LimitExceeded | The upper limit of the quota limit is exceeded. |
| MissingParameter | A required parameter is missing for the request. |
| NoSuchVersion | The specified API version does not exist or is not found. |
| RequestLimitExceeded | The number of requests exceeds the rate limit. |
| ResourceInUse | The specified resource is occupied. |
| ResourceInsufficient | The specified resource is insufficient for the request. |
| ResourceNotFound | The specified resource does not exist or is not found. |
| ResourceUnavailable | The specified resource is not available. |
| UnauthorizedOperation | The operation is unauthorized. |
| UnknownParameter | An unknown parameter was specified in the request. |
| UnsupportedOperation | The operation is unsupported. |
| UnsupportedMethod| The HTTP(S) method used for the request is not supported; only GET and POST  are supported. Only GET and POST method are supported in HTTP protocol. |
| UnsupportedRegion | The API does not recognize or support the region where the request was sent. |

### Application Errors
| Error code | Description |
|:-------|:-----|
| FailedOperation | The operation is failed. |
| FailedOperation.ClassLevelLimitExceeded | The operation is failed: The number of category levels exceeds the limit. |
| FailedOperation.ClassNameDuplicate | The operation is failed: The category name already exists. |
| FailedOperation.ClassNoFound | The operation is failed: The category does not exist. |
| FFailedOperation.ParentIdNoFound | The operation is failed: The parent category ID does not exist. |
| FailedOperation.SubclassLimitExceeded | The operation is failed: The number of subcategories exceeds the limit. |
| FailedOperation.TaskDuplicate | The operation is failed: The task already exists. |
| InternalError | The error is caused internally. |
| InternalError.GetFileInfoError | Internal error: Failed to get media file information. |
| InternalError.GetMediaListError | Internal error: Failed to get a list of media. |
| InternalError.UpdateMediaError |  Failed to update media file information. |
| InternalError.UploadCoverImageError | Failed to upload cover image. |
| InternalError.UploadWatermarkError | Internal error: Failed to add a watermark. |
| InvalidParameter | A parameter is not valid or cannot be used for the request. |
| InvalidParameter.ExistedProcedureName | The name of the task flow template already exists. |
| InvalidParameter.ExpireTime | Invalid value specified in the parameter: The time typed is passed |
| InvalidParameter.ProcedureNameNotExist | The name of the task flow template does not exist.|
| InvalidParameterValue | A value specified in a parameter is not valid or cannot be used for this request. |
| InvalidParameterValue.AddKeyFrameDescsAndClearKeyFrameDescsConflict | Invalid parameter value: The value of *AddKeyFrameDescs* conflicts with that of *ClearKeyFrameDescs*. |
| InvalidParameterValue.AddKeyFrameDescsAndDeleteKeyFrameDescsConflict | Invalid parameter value: The value of *AddKeyFrameDescs* conflicts with that of *DeleteKeyFrameDescsConflict*. |
| InvalidParameterValue.AddTagsAndClearTagsConflict | The input value of *AddTags* conflicts with that of *ClearTags*. |
| InvalidParameterValue.AddTagsAndDeleteTagsConflict | Invalid parameter value: The value of *AddTags* conflicts with that of *DeleteTags*. |
| InvalidParameterValue.AiAnalysisTaskDefinition |The input value of AI-analyzed *Definition* is invalid. |
| InvalidParameterValue.AiContentReviewTaskDefinition | The value of *Definition* of AI-reviewed content is invalid. |
| InvalidParameterValue.AudioBitrate | The specified audio stream bitrate is invalid.|
| InvalidParameterValue.AudioChannel | The specified audio channel is invalid. |
| InvalidParameterValue.AudioCodec | The specified audio stream codec is invalid. |
| InvalidParameterValue.AudioSampleRate |The  audio stream sample rate is invalid. |
| InvalidParameterValue.ClassId | The category ID provided is invalid. |
| InvalidParameterValue.ClassIds | The class IDs provided are invalid. |
| InvalidParameterValue.ClassName | The name specified for the class is invalid. |
| InvalidParameterValue.ClipDuration | The clip duration is too long. |
| InvalidParameterValue.Comment | The description of the template is invalid. |
| InvalidParameterValue.Container | The container format is unsupported. |
| InvalidParameterValue.ContainerType | The container type is unsupported |
| InvalidParameterValue.CoordinateOrigin | The coordinates of the origin are invalid. |
| InvalidParameterValue.CoverType | The cover type is unsupported . |
| InvalidParameterValue.Definition | The value of *Definition* is invalid. |
| InvalidParameterValue.Definitions | The value of *Definitions* is invalid. |
| InvalidParameterValue.Description | The length of description exceeds the limit. |
| InvalidParameterValue.EndTime | The end time is invalid. |
| InvalidParameterValue.ExpireTime | The format of the expiration time is unsupported |
| InvalidParameterValue.FileId | The specified file ID  does not exist. |
| InvalidParameterValue.Fps | The the value of the frame rate is invalid. |
| InvalidParameterValue.Height | The value of the video height is invalid. |
| InvalidParameterValue.ImageTemplate | The watermark template is unsupported |
| InvalidParameterValue.KeyFrameDescContentTooLong | The length of timestamp content exceeds the limit. |
| InvalidParameterValue.Limit | The value of *Limit* is invalid. |
| InvalidParameterValue.MediaType | The media type is unsupported. |
| InvalidParameterValue.Name | The length of the name exceeds the limit. |
| InvalidParameterValue.Names | The number of elements allowed in array *Names* is exceeded. |
| InvalidParameterValue.Offset | The offset value is invalid. |
| InvalidParameterValue.ParentId | The value of *ParentId* is invalid. |
| InvalidParameterValue.RemoveAudio | The value of *RemoveAudio* is invalid. |
| InvalidParameterValue.RemoveVideo | The value of **RemoveVideo** is invalid. |
| InvalidParameterValue.RepeatType | The repeat type is invalid. |
| InvalidParameterValue.Resolution | The value of resolution is unsupported. |
| InvalidParameterValue.SessionContextTooLong | The length of session context exceeds the limit. |
| InvalidParameterValue.SessionId | The session ID already exists. The request is removed due to duplication. |
| InvalidParameterValue.SessionIdTooLong | The length of the session ID is too long. |
| InvalidParameterValue.Sort | The sort is unsupported. |
| InvalidParameterValue.SourceType | The source type is invalid. |
| InvalidParameterValue.StartTime | The start time is invalid. |
| InvalidParameterValue.Status | Incorrect parameter value: The value of human confirmation result is invalid. |
| InvalidParameterValue.StreamIdInvalid | The Stream ID is invalid or unfoundeded. |
| InvalidParameterValue.SubAppId | I The sub-application ID is invalid or unfoundeded. |
| InvalidParameterValue.TagTooLong | The tag contains too many characters |
| InvalidParameterValue.Tags | The tags provided are invalid |
| InvalidParameterValue.TaskId | The task ID does not exist in our records. |
| InvalidParameterValue.Text | The text searched is invalid. |
| InvalidParameterValue.TextAlpha | The input value of the text transparency is incorrect or invalid. |
| InvalidParameterValue.TextTemplate | The text template used is invalid. |
| InvalidParameterValue.Type | The input value of the type is invalid. |
| InvalidParameterValue.VideoBitrate | The video stream bitrate specified is invalid |
| InvalidParameterValue.VideoCodec | The video stream codec specified is invalid|
| InvalidParameterValue.VodSessionKey | The VOD session is invalid. |
| InvalidParameterValue.Width | The width specified is invalid |
| InvalidParameterValue.XPos | The input value of Xpos is invalid. XPos is the horizontal coordinate of the watermark origin relative to the video origin coordinates. % and px are supported. |
| InvalidParameterValue.YPos | The input value of Xpos is invalid. YPos is the vertical coordinate of the watermark origin relative to the video origin coordinates. % and px are supported. |
| LimitExceeded | The usage exceeds the quota limit |
| LimitExceeded.KeyFrameDescCountReachMax | The total number of new and old timestamps exceeds the limit |
| LimitExceeded.TagCountReachMax | The total number of new and old tags exceeds the limit |
| LimitExceeded.TooMuchTemplate | The number of templates exceeds the limit. |
| ResourceNotFound | The specified resource does not exist or is not found. |
| ResourceNotFound.FileNotExist | The specified file does not exist or is not found |
| ResourceNotFound.TemplateNotExist | The specified template does not exist or is not found. |
| UnsupportedOperation.ClassNotEmpty | You cannot delete a non-empty category|
