## Error Codes
### Video processing

| Error Code | Description |
| -- | -- |
| InvalidInput | Invalid input parameter. Please check. |
| InvalidInput.InvalidTimeOffset | Invalid input parameter: the specified time point is invalid. |
| InvalidInput.DefinitionNotExist | Invalid input parameter: the specified template ID doesn't exist. |
| InvalidInput.ConfigurationUnsupported | Invalid input parameters. Reasons include but are not limited to: <li>the user has not registered.</li><li>The input parameter value is invalid (due to errors in the format, value range or others).</li><li>The parameter template configuration is invalid.</li><li>No video processing task is specified.</li>|
|InvalidInput.TaskDuplicated|Invalid input parameter: duplicate task |
|InvalidInput.PermissionDenied|Invalid input parameter: you do not have permission to use this feature. Please apply for the permission first.|
|InvalidInput.ResultFileSizeTooLarge|Invalid input parameter: the spliced file is too large after inputting multiple files. |
| SourceFileError | Invalid source file: for example, video data is corrupted. Please check whether the source file is normal. |
| SourceFileError.NoVideoMedia | Invalid source file: there is no video image. |
| SourceFileError.NoVideoResolution | Invalid source file: the resolution of the source file cannot be obtained. |
|SourceFileError.ContentMalformed|Invalid source file: errors occur in the input content. For example, the file does not exist, the file is corrupted, or the media file cannot be decoded. |
|SourceFileError.ContentUnsupported|Invalid source file: the input file is invalid due to unsupported file format, size, duration, or other reasons.|
|SourceFileError.DownloadNotAccessible|Invalid source files: the files are not accessible during download. Check the availability of the source files.|
|InternalError | Internal service error. Please try again. |
