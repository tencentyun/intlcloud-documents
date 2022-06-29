## Overview

CI monitoring data, such as image processing usage, media job quantity, and content recognition request quantity, is collected and displayed by [CM](https://intl.cloud.tencent.com/document/product/248). Therefore, you can go to the CI or [CM](https://console.cloud.tencent.com/monitor) console to view CI monitoring data in detail.

This document describes how to get CI monitoring metrics. You can call CM APIs to get more detailed data. For more information, see the [CM documentation](https://intl.cloud.tencent.com/document/product/248).

## Basic Features

CM provides the following modules for CI to implement monitoring and alarming.

| Module | Capability | Main Feature |
| ---------- | ---------------------------- | ------------------------------------------------------------ |
| Monitoring overview | Displays the current status of the product | Provides general overview, alarm overview, and overall monitoring information |
| Alarm management | Supports alarm management and configuration | Supports creating new CI alarm policies, custom messages, and trigger templates |
| Monitoring platform | Displays the data of user-defined monitoring metrics | Allows you to customize the monitoring metrics and data to be reported |
| Cloud product monitoring | Displays the bucket monitoring view | Allows you to query the current monitoring views and data for each bucket, such as image processing usage, media job quantity, and content recognition request quantity |


## Use Cases

- **Daily management**: You can log in to the CM console to view the running status of CI in real time.
- **Troubleshooting**: You can receive alarm notifications when the data of a monitoring metric reaches the threshold. It allows you to quickly notify the exceptions, find out the causes, and fix the issues.


## Setting and Querying via Console

You can create an alarm policy for CI in the [CM console](https://console.cloud.tencent.com/monitor). If the data of a monitoring metric reaches the specified threshold, you will receive an alarm notification. For detailed directions, see Setting Monitoring Alarms.



## Querying Monitoring Data via APIs

You can view the monitoring data of CI by calling APIs.

## Monitoring Metrics

>?
>- CI monitoring data resides in Guangzhou region. Therefore, select "Guangzhou" for `Region` when you pull CI monitoring metric data, regardless of where the bucket resides.
> - When pulling data by using [API Explorer](https://console.cloud.tencent.com/api/explorer?Product=monitor&Version=2018-07-24&Action=GetMonitorData&SignVersion=), select "ap-guangzhou" for the `Region` field.
>- When pulling data by using an SDK, enter "ap-guangzhou" for the `Region` field.
>


### Image processing

| Metric | Meaning | Description | Unit | Dimension |
| ----------------------- | ----------------------- | ------------------------------------------------------------ | ---- | ------------- |
| image_requests          | Total image processing requests        | Total number of image processing requests, including basic processing, Guetzli image compression, image advanced compression, and blind watermarking | -    | appid, bucket |
| image_basics_requests   | Image basic processing requests    | Total number of image basic processing requests | -    | appid, bucket |
| image_guetzil_requests  | Guetzil image compression requests | Number of Guetzil image compression requests                                  | -   | appid, bucket |
| image_compress_requests | Image advanced compression requests   | Number of image advanced compression request counts                                     | -    | appid, bucket |
| image_imprint_requests  | Blind watermarking requests          | Number of blind watermarking requests                                       | -    | appid, bucket |
| image_basics_bytes      | Total image basic processing usage      | Total usage of image basic processing requests of all types               | B    | appid, bucket |
| image_basics_bytes_down | Image download usage    | Usage of image basic processing requests of the GET type                              | B    | appid, bucket |
| image_basics_bytes_up   | Image upload usage    | Usage of image basic processing requests of the PUT type                              | B    | appid, bucket |
| image_put_2xx_response  | 2xx status codes for image upload   | Number of PUT requests with a 2xx return code                                   | -    | appid, bucket |
| image_put_3xx_response  | 3xx status codes for image upload   | Number of PUT requests with a 3xx return code                                   | -    | appid, bucket |
| image_put_4xx_response  | 4xx status codes for image upload   | Number of PUT requests with a 4xx return code                                   | -    | appid, bucket |
| image_put_5xx_response  | 5xx status codes for image upload   | Number of PUT requests with a 5xx return code                                   | -    | appid, bucket |
| image_get_2xx_response  | 2xx status codes for image download   | Number of GET requests with a 2xx return code                                   | -    | appid, bucket |
| image_get_3xx_response  | 3xx status codes for image download   | Number of GET requests with a 3xx return code                                   | -    | appid, bucket |
| image_get_4xx_response  | 4xx status codes for image download   | Number of GET requests with a 4xx return code                                   | -    | appid, bucket |
| image_get_5xx_response  | 5xx status codes for image download   | Number of GET requests with a 5xx return code                                   | -    | appid, bucket |

>?
>1. For more information on 2xx, 3xx, 4xx, and 5xx status codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700).
>2. The statistical granularity (`period`) may vary by metric. You can call the [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API to obtain the `period` supported by each metric.
>

### Media processing

| Metric | Meaning | Description | Unit | Dimension |
| -------------------------- | ------------------ | ---------------------------------------- | ---- | ------------- |
| media_tasks                | Media processing jobs     | Total number of media processing jobs of all types                   | -    | appid, bucket |
| media_success_tasks        | Successful media processing jobs | Number of successful media processing jobs of all types         | -    | appid, bucket |
| media_requset_success_rate | Media processing request success rate | Percentage of successful media processing jobs to all jobs | %   | appid, bucket |
| video_transcoding_times   | Standard transcoding duration     | Duration of standard transcoding                 | min   | appid, bucket |
| format_conversion_times   | Audio/Video remuxing duration  | Duration of audio/video remuxing         | min   | appid, bucket |
| audio_transcoding_times   | Audio transcoding duration     | Duration of audio transcoding                 | min   | appid, bucket |
| HD_transcoding_times   | TESHD transcoding duration  | Duration of TESHD transcoding         | min   | appid, bucket |

 

### Content recognition

| Metric | Meaning | Description | Unit | Dimension |
| ------------------------------------ | ------------------------ | ---------------------------- | ---- | ------------- |
| QR_code_recognition_requests         | QR code recognition requests         | Number of QR code recognition requests       | -    | appid, bucket |
| QR_code_recognition_success_requests | Successful QR code recognition requests     | Number of successful QR code recognition requests       | -    | appid, bucket |
| QR_code_recognition_fail_requests    | Failed QR code recognition requests     | Number of failed QR code recognition requests       | -    | appid, bucket |
| image_tag_requests                   | Image tagging requests           | Number of image tagging requests         | -    | appid, bucket |
| image_tag_success_requests           | Successful image tagging requests           | Number of successful image tagging requests         | -    | appid, bucket |
| image_tag_fail_requests              | Failed image tagging requests           | Number of failed image tagging requests         | -    | appid, bucket |
| image_quality_requests               | Image quality assessment requests    | Number of image quality assessment requests     | -    | appid, bucket |
| image_quality_success_requests       | Successful image quality assessment requests    | Number of successful image quality assessment requests     | -    | appid, bucket |
| image_quality_fail_requests          | Failed image quality assessment requests    | Number of failed image quality assessment requests     | -    | appid, bucket |
| audio_recognition_requests           | Speech recognition requests           | Number of speech recognition requests         | -    | appid, bucket |
| audio_recognition_success_requests   | Successful speech recognition requests           | Number of successful speech recognition requests         | -    | appid, bucket |
| audio_recognition_fail_requests      | Failed speech recognition requests           | Number of failed speech recognition requests         | -    | appid, bucket |
| face_check_requests                  | Face detection requests         | Number of face detection requests         | -    | appid, bucket |
| face_check_success_requests          | Successful face detection requests         | Number of successful face detection requests         | -    | appid, bucket |
| face_check_fail_requests             | Failed face detection requests         | Number of failed face detection requests         | -    | appid, bucket |
| face_effects_requests                | Face filter requests           | Number of face filter requests         | -    | appid, bucket |
| face_effects__success_requests       | Successful face filter requests           | Number of successful face filter requests         | -    | appid, bucket |
| face_effects__fail_requests          | Failed face filter requests           | Number of failed face filter requests         | -    | appid, bucket |
| face_identity_check_requests         | Face recognition requests            | Number of face recognition requests         | -    | appid, bucket |
| face_identity_check_success_requests | Successful face recognition requests            | Number of successful face recognition requests         | -    | appid, bucket |
| face_identity_check_fail_requests    | Failed face recognition requests            | Number of failed face recognition requests         | -    | appid, bucket |
| car_recognition_requests             | Vehicle recognition requests           | Number of vehicle recognition requests         | -    | appid, bucket |
| car_recognition_success_requests     | Successful vehicle recognition requests           | Number of successful vehicle recognition requests         | -    | appid, bucket |
| car_recognition_fail_requests        | Failed vehicle recognition requests           | Number of failed vehicle recognition requests         | -    | appid, bucket |
| OCR_recognition_requests             | Image text recognition requests     | Number of image text recognition requests     | -    | appid, bucket |
| OCR_recognition_success_requests     | Successful image text recognition requests     | Number of successful image text recognition requests     | -    | appid, bucket |
| OCR_recognition_fail_requests        | Failed image text recognition requests     | Number of failed image text recognition requests     | -    | appid, bucket |


### File processing

| Metric | Meaning | Description | Unit | Dimension |
| ----------------------------------- | -------------------- | -------------------------- | ---- | ------------- |
| document_transcode_requests         | File transcoding requests       | Number of file transcoding requests       | -    | appid, bucket |
| document_transcode_success_requests | Successful file transcoding requests       | Number of successful file transcoding requests       | -    | appid, bucket |
| document_transcode_fail_requests    | Failed file transcoding requests       | Number of failed file transcoding requests       | -    | appid, bucket |
| document_html_requests              | File-to-HTML requests     | Number of file-to-HTML requests     | -    | appid, bucket |
| document_html_success_requests      | Successful file-to-HTML requests     | Number of successful file-to-HTML requests     | -    | appid, bucket |
| document_html_fail_requests         | Failed file-to-HTML requests     | Number of failed file-to-HTML requests     | -    | appid, bucket |


### Content moderation

| Metric | Meaning | Description | Unit | Dimension |
| :--------------------------------------- | ------------------------ | ------------------------------ | ---- | ------------- |
| document_auditing_tasks                  | Total file moderation jobs         | Total number of submitted file moderation jobs         | -    | appid, bucket |
| document_auditing_success_tasks          | Successful file moderation jobs         | Number of successful file moderation jobs         | -    | appid, bucket |
| document_auditing_fail_tasks             | Failed file moderation jobs         | Number of failed file moderation jobs         | -    | appid, bucket |
| document_auditing_callback_times         | Total file moderation result callbacks   | Total number of file moderation result callbacks   | -    | appid, bucket |
| document_auditing_callback_success_times | Successful file moderation result callbacks   | Number of successful file moderation result callbacks   | -    | appid, bucket |
| document_auditing_callback_fail_times    | Failed file moderation result callbacks   | Number of failed file moderation result callbacks   | -    | appid, bucket |
| text_auditing_tasks                      | Text moderation jobs           | Number of submitted text moderation jobs         | -    | appid, bucket |
| text_auditing_success_tasks              | Successful text moderation jobs           | Number of successful text moderation jobs         | -    | appid, bucket |
| text_auditing_fail_tasks                 | Failed text moderation jobs           | Number of failed text moderation jobs         | -    | appid, bucket |
| text_auditing_callback_times             | Total text moderation result callbacks   | Total number of text moderation result callbacks   | -    | appid, bucket |
| text_auditing_callback_success_times     | Successful text moderation result callbacks   | Number of successful text moderation result callbacks   | -    | appid, bucket |
| text_auditing_callback_fail_times    | Failed text moderation result callbacks   | Number of failed text moderation result callbacks   | -    | appid, bucket |
| images_auditing_tasks                    | Image moderation jobs           | Number of submitted image moderation jobs         | -    | appid, bucket |
| images_auditing_success_tasks            | Successful image moderation jobs           | Number of successful image moderation jobs         | -    | appid, bucket |
| images_auditing_fail_tasks               | Failed image moderation jobs           | Number of failed image moderation jobs         | -    | appid, bucket |
| images_auditing_callback_times             | Total image moderation result callbacks   | Total number of image moderation result callbacks   | -    | appid, bucket |
| images_auditing_callback_success_times     | Successful image moderation result callbacks   | Number of successful image moderation result callbacks   | -    | appid, bucket |
| images_auditing_callback_fail_times    | Failed image moderation result callbacks   | Number of failed image moderation result callbacks   | -    | appid, bucket |
| audio_auditing_tasks                      | Audio moderation jobs           | Number of submitted audio moderation jobs         | -    | appid, bucket |
| audio_auditing_success_tasks              | Successful audio moderation jobs           | Number of successful audio moderation jobs         | -    | appid, bucket |
| audio_auditing_fail_tasks                | Failed audio moderation jobs           | Number of failed audio moderation jobs         | -    | appid, bucket |
| audio_auditing_callback_times             | Total audio moderation result callbacks   | Total number of audio moderation result callbacks   | -    | appid, bucket |
| audio_auditing_callback_success_times     | Successful audio moderation result callbacks   | Number of successful audio moderation result callbacks   | -    | appid, bucket |
| audio_auditing_callback_fail_times    | Failed audio moderation result callbacks   | Number of failed audio moderation result callbacks   | -    | appid, bucket |
| video_auditing_tasks                     | Video moderation jobs           | Number of submitted video moderation jobs         | -    | appid, bucket |
| video_auditing_success_tasks             | Successful video moderation jobs           | Number of successful video moderation jobs         | -    | appid, bucket |
| video_auditing_fail_tasks                | Failed video moderation jobs           | Number of failed video moderation jobs         | -    | appid, bucket |
| video_auditing_callback_times             | Total video moderation result callbacks   | Total number of video moderation result callbacks   | -    | appid, bucket |
| video_auditing_callback_success_times     | Successful video moderation result callbacks   | Number of successful video moderation result callbacks   | -    | appid, bucket |
| video_auditing_callback_fail_times    | Failed video moderation result callbacks   | Number of failed video moderation result callbacks   | -    | appid, bucket |


### Traffic

| Metric | Meaning | Description | Unit | Dimension |
| ------------------------------ | ------------------ | ---------------------------------------- | ---- | ------------- |
| cdn_origin_traffic               | CDN origin-pull traffic    | Traffic generated by CI data transfer from the bucket to the CDN edge node | B | appid, bucket |
| internet_trafficUp              | Public network outbound traffic |  Traffic generated by CI data download from the bucket to the client over the internet | B | appid, bucket |


## Input Parameter Description

**To query the monitoring data of CI, use the following input parameters:**

```txt
 &Namespace=QCE/CI
 &Instances.N.Dimensions.0.Name=appid
 &Instances.N.Dimensions.0.Value=root account APPID
 &Instances.N.Dimensions.1.Name=bucket
 &Instances.N.Dimensions.1.Value=bucket name
```

#### Monitoring description

- **Monitoring interval**: CM supports multiple monitoring intervals, including real time, last 24 hours, last 7 days, and user-specified period, with time granularities of 1 minute, 5 minutes, 1 hour, and 1 day.
- **Data storage**: 1-minute monitoring data can be stored for 15 days, 5-minute data for 31 days, 1-hour data for 93 days, and 1-day data for 186 days.
- **Alarm display**: CM integrates the monitoring data of CI and displays the data in graphs. Alarm notifications can be sent to you according to the predefined alarm metrics of your product. In this way, you can stay informed of the overall running status.
- **Alarm settings**: You can set the threshold for the monitoring metrics. When the monitoring data meets the alarm condition that is set, CM will send the alarm notifications to the specified users.
