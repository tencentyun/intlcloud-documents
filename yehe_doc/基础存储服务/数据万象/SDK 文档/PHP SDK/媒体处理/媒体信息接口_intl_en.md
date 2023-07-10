## Overview

This document provides code samples for getting media file information.
>! COS PHP SDK v2.3.2 or later is required. Earlier versions may contain bugs and need to be upgraded to the [latest version](https://github.com/tencentyun/cos-php-sdk-v5/releases/) when used.
>

| API | Operation |  Description |
| ------------------------------------------------------------ | --------------------------|---------------------------- |
|  [GetMediaInfo](https://intl.cloud.tencent.com/document/product/436/46915)    |   Querying file information | Queries media file information      |

## Querying File Information

#### Feature description

This API is used to query the information of a media file.
>! Before using this API, make sure that the media processing feature has been enabled in the data processing section in the console; otherwise, the error `media bucket unbinded, bucket's host is unavailable` will be reported.

#### Sample code

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; // Replace it with your real `secretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; // Replace it with your real `secretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with your real region information, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is `http` by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
            
try {
    $result = $cosClient->GetMediaInfo(
        array(
            'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
            'Key' => 'exampleobject', // Media file object path, such as `folder/movie.mp4`
            'ci-process' => 'videoinfo' // Operation type, which is fixed at `videoinfo`
        )
    );
    // Request successful
    echo($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID`. | String  | Yes   |
| Key     | Object key (object name), which is the unique identifier of the object (a media file here) in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| ci-process |  Operation type, which is fixed at `videoinfo`. | String | Yes   |


#### Sample response

```php
GuzzleHttp\Command\Result Object
(
    [RequestId] => NjE0NTkxMWNfYTkyZTJjMGJfNTgyZF84ZDY2NWY=
    [ContentType] => application/xml
    [ContentLength] => 1787
    [MediaInfo] => Array
        (
            [Stream] => Array
                (
                    [Audio] => Array
                        (
                            [Bitrate] => 383.727000
                            [Channel] => 6
                            [ChannelLayout] => 5.1
                            [CodecLongName] => AAC (Advanced Audio Coding)
                            [CodecName] => aac
                            [CodecTag] => 0x6134706d
                            [CodecTagString] => mp4a
                            [CodecTimeBase] => 1/48000
                            [Duration] => 62.314667
                            [Index] => 1
                            [Language] => und
                            [SampleFmt] => fltp
                            [SampleRate] => 48000
                            [StartTime] => 0.000000
                            [Timebase] => 1/48000
                        )

                    [Subtitle] => Array
                        (
                        )

                    [Video] => Array
                        (
                            [CodecTagString] => avc1
                            [Rotation] => 0.000000
                            [Index] => 0
                            [CodecName] => h264
                            [CodecLongName] => H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10
                            [CodecTimeBase] => 1/12800
                            [CodecTag] => 0x31637661
                            [Profile] => Main
                            [Height] => 720
                            [Width] => 1280
                            [HasBFrame] => 0
                            [RefFrames] => 1
                            [Sar] => 1:1
                            [Dar] => 16:9
                            [PixFormat] => yuv420p
                            [Level] => 31
                            [Fps] => 25.500000
                            [AvgFps] => 25/1
                            [Timebase] => 1/12800
                            [StartTime] => 0.000000
                            [Duration] => 62.280000
                            [Bitrate] => 959.963000
                            [NumFrames] => 1557
                            [Language] => und
                        )

                )

            [Format] => Array
                (
                    [NumStream] => 2
                    [NumProgram] => 0
                    [FormatName] => mov,mp4,m4a,3gp,3g2,mj2
                    [FormatLongName] => QuickTime / MOV
                    [StartTime] => 0.000000
                    [Duration] => 62.315000
                    [Bitrate] => 1347.820000
                    [Size] => 10498677
                )

        )

    [Key] => exampleobject
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject
)
```
