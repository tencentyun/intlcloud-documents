# PaaS error codes

| Error Code                                 | Description                     | Billable |
| -------------------------------------- | ------------------------------ | -------- |
| Success                                | Detection succeeded.                 | Yes       |
| FailedOperation.CompareLowSimilarity | The similarity did not reach the passing standard. | Yes       |
| InvalidParameter                       | Invalid parameter.                       | No       |
| InvalidParameterValue                  | Invalid parameter value.                     | No       |
| FailedOperation.DownLoadError          | Download error.                       | No       |
| FailedOperation.UnKnown                | Unknown error.                      | No       |
| FailedOperation.IdPhotoPoorQuality     | The identity photo was in a too low resolution. Please upload a new one.  | No       |
| FailedOperation.LifePhotoDetectFaces   | Several faces were detected.                 | No       |
| FailedOperation.LifePhotoDetectFake    | Real person comparison failed.               | No      |
| FailedOperation.LifePhotoDetectNoFaces | No full face was detected.              | No       |
| FailedOperation.CompareFail            | Comparison failed.                       | No       |
| FailedOperation.LivessSystemError      | An error occurred while calling the liveness detection engine API.              | No       |


# SaaS error codes

| Error Code | Description |
| ------- | ------- |
|0 |Succeeded. |
|1 |Invalid request. Some parameters are missing. |
|2 |Invalid request. Parameters are incorrect. |
|3 |Invalid service request. |
|4 |System error. |
|8 |Failed to store the file. Please try again later. |
|9 |Invalid file format. Please try again later. |
|10 |File system error. Please try again later. |
|11 | File system timeout. Please try again later. |
|14 |The verification was finished. |
|15 |The token expired. Please try again. |
|16 |Too many attempts. |
|17 |The process wasn't finished. |
|202 |Failed to obtain the video. |
|1001 |An error occurred while calling the liveness detection engine API. |
|1002 |Suspected spoofed recording. |
|1003 |Video-based real person detection failed. |
|1004 |Face detection failed. It was unable to extract the photo for comparison. |
|1005 |Liveness detection failed. |
|1101 |No voice was detected. |
|1102 |The face was not fully exposed. |
|1103 |Voice recognition failed. |
|1104 |Invalid video format. |
|1105 |Failed to pull the video. Please try again. |
|1106 |The volume of the video is too low. |
|1107 |The video is empty or its size is inappropriate. The video duration should be about 6s. |
|1108 |The video resolution is too low. |
|1109 |The lip movement range is too small. |
|1201 |The lighting is too dim. |
|1202 |The lighting is too strong. |
|1203 |The face is too close to the screen. |
|1204 |The face is too far right from the screen. |
|1205 | The face is too far from the screen. |
|1206 |The face is too far left from the screen. |
|1207 |No eye closing motions were detected. |
|1208 |The first motion was not detected. |
|1209 |No mouth opening motions were detected. |
|1210 |No full face was detected. |
|1301 |Real person detection failed. |
|1302 |Real person detection did not reach the passing standard. |
|1303 |The video is too short. Please capture a video longer than 2s. |
|1401 |Reflection-based liveness detection failed. |
|2001 |An error occurred while calling the comparison engine API. |
|2004 |The image passed in is too large or too small. |
|2009 |The image passed in is in a too low resolution. Please upload a new one. |
|2010 |Face detection failed. It was unable to extract the photo for comparison. |
|2011 |Real person comparison failed. |
|2012 |Several faces were detected. |
|2013 |No full face was detected. |
|2014 |The image passed in is in a too low resolution. Please upload a new one. |
|2015 |Comparison failed. |
|2016 |The similarity did not reach the passing standard. |