## Overview

This document describes how to use the audio moderation feature in the console to check audio content for **pornographic**, **illegal**, and **advertising** information.

After you configure automatic audio moderation, new audios uploaded to a bucket will be automatically moderated, and the identified non-compliant content can be automatically blocked (by denying public read access to the content).

You can also moderate existing audios stored in COS. For more information, see Setting Historical Data Moderation Job .

>?
>- Audio moderation is a paid feature.
>- Supported audio formats: MP3, WAV, AAC, FLAC, AMR, 3GP, M4A, WMA, OGG, APE.
>- Supported audio bitrate: 128–256 Kbps.
>- Supported audio size: < 600 MB.
>- Maximum duration: 3 hours.
>- Audio moderation can recognize Mandarin and English.
>

## Operation Process
<img style="width:418px; max-width: inherit;" src="https://staticintl.cloudcachetci.com/yehe/backend-news/3YaP402_PRELIM__%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-1.png" />


## Directions

1. Log in to the [CI console](https://console.cloud.tencent.com/ci). On the **Bucket Management** page, select the target bucket to enter the bucket management page.
2. On the left sidebar, select **Sensitive Content Moderation** > **Automatic Moderation Configuration** and click **Audio Moderation**.
3. Click **Add Automatic Audio Moderation Configuration** and set the following configuration items:
   - **Moderation Scope**: Select the scope of audio files to be moderated, which can be the entire bucket, a specific directory, or a specific file prefix.
   - **Moderation Suffix**: The following audio formats can be moderated: MP3, WAV, AAC, FLAC, AMR, 3GP, M4A, WMA, OGG, and APE. You can select multiple formats.
   - **Moderation Policy**: Select a moderation policy. You can create different policies for refined moderation. If no policies have been configured, the default policy will be used. Moderation scene options include **Pornographic**, **Illegal**, and **Advertisement**, and you can select one or multiple options. For detailed directions on how to configure a moderation policy, see Setting Moderation Policy.
   - **Moderation Scene**: It displays the scene that you configure in the moderation policy. You can select the target scene as needed.
   - **Restricted File Block**: You can enable this service to authorize CI to perform automatic or manual moderation and block the identified non-compliant files by denying public read access to them. After enabling this service, you need to select the block type and score range of audios to be blocked.
   - **Block Type**: You can select a block type and mechanism. **Machine moderation and block** is selected by default. If you select **Manual review freeze**, TenDI's professional team will review suspiciously sensitive audios identified during machine moderation. You can select the audio score range for blocking (by specifying an integer between 60 and 100; the greater the score, the more sensitive the audio).
   - **Callback**: After callback is enabled, you will receive moderation results. You need to select the moderation type and callback content and set the callback URL. For more information, see [Callback Content](#1).
4. After completing the configuration, click **Save**. Audio files uploaded subsequently will be moderated. To moderate historical data, see Setting Historical Data Moderation Task.

<span id=1></span>
## Callback Content

If you enable callback, after audio moderation is completed, the system will send the following callback message to the callback URL:

```plaintext
{
    "code":0,
    "message":"success",
    "data":{
        "url":"",
        "result":1,
        "forbidden_status":1,
        "trace_id":"",
        "porn_info":{
            "hit_flag":1,
            "score":91,
            "label":""
        },
        "ads_info":{
            "hit_flag":0,
            "score":0,
            "label":""
        }
    }
}
```

| Parameter | Description | Type | Required |
| :--------------- | :------------------------------------------------------ | :----- | :------- |
| forbidden_status | Block status. Valid values: `0` (normal); `1` (blocked).                  | Int    | Yes       |
| porn_info        | Porn detection information, including moderation result, score, and detailed tags.            | json   | Yes       |
| ads_info         | Ad detection information, including moderation result, score, and detailed tags.        | json   | Yes       |
| result           | Recognition result for reference. Valid values: `0` (normal), `1` (sensitive), `2` (suspiciously sensitive). | Int    | Yes       |
| trace_id         | `jobid` of the submitted moderation job.                                       | String | Yes       |
| url              | The URL of the uploaded resource, including the domain name.                             | String | Yes       |

The moderation information (`porn_info` and `ads_info`) has the following sub-nodes:

| Parameter | Description | Type | Required |
| :------- | :----------------------------------------------------------- | :----- | :------- |
| hit_flag | Whether the moderation type is hit. Valid values: `0` (miss), `1` (hit), and `2` (suspected). | Int    | Yes       |
| label    | Recognized audio tag.                                             | String | Yes       |
| score    | Moderation score. Valid value ranges: 0–60 (normal); 60–90 (suspiciously sensitive); 90–100 (sensitive). | Int    | Yes       |


## Notes

1. Audio moderation adopts a scoring mechanism, with a score between 0 and 100 returned for each audio.
2. The **confirmed part** refers to the audios that are confirmed to be normal or sensitive (with a score in the range of [0,60] or (90,100]). For such audios, no manual intervention is required.
3. The **uncertain part** refers to the audios that are suspected to be sensitive (with a score in the range of (60,90]). For such audios, manual moderation is recommended.
