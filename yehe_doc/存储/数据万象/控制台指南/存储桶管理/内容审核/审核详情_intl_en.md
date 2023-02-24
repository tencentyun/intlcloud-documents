## Overview

After enabling sensitive content moderation, you can view the moderation results by condition and manually process them on the **Moderation Details** page.

## Directions

<span id="ResultScreening"></span>
### Filtering results

1. Log in to the [CI console](https://console.cloud.tencent.com/ci).
2. On the left sidebar, select **Bucket Management** to enter the **Bucket Management** page.
3. Click the name of the target bucket to go to the configuration page.
4. On the left sidebar, select **Sensitive Content Moderation** > **Moderation Details** to enter the **Moderation Details** page.
5. Select the conditions as needed.

 - Scope: You can view the results of moderation through API calls, automatic moderation, and historical data moderation.
 - File type: You can view the moderation results of images, videos, audios, and text.
 - Detection Scenario: You can view the moderation results for pornographic, illegal or non-compliant, or advertising content detection or all scenarios of the selected file type.
 - Moderation Result: Moderated files are categorized into three types: sensitive, suspected, and normal files. You can view a type of file or all files.
    - Sensitive: Images whose score falls within the range of [91,100].
    - Suspected: Images that are suspected to be sensitive and whose score falls within the range of [61,90]. For such images, the system cannot determine whether they are sensitive, so we recommend you determine it through human moderation.
    - Normal: Images whose score falls within the range of [0,60].
 - Block Status: You can view the moderation results of blocked, normal, or all files.
 - Moderation time: You can view the moderation results in the specified time period.
>! If you rename a file or modify its metadata, the file will be considered a newly uploaded file and have a new moderation result.
 - Image Score: If you select **All** for **Moderation Result**, you can filter files by customizing the file moderation score interval.
 - Object Name: You can enter a filename to view the moderation result of the specified file.
6. Click **Query** to view the moderation results.
>? The **Moderation Details** page only displays the details of moderations called in the console but not those called through an API or SDK.
>


### Exporting results

After [filtering results](#ResultScreening), click **Export** to export the results as a .csv or .xlsx file.

The fields in the moderation result file are as detailed below:

| Field | Name | Description |
| :----------- | :------- | :----------------------------------------------------------- |
| recordID     | Record ID  | Unique record ID of the moderation result.                                        |
| fileName     | Filename   | Name of the moderated file.                                               |
| size         | Size     | Size of the moderated file.                                               |
| scene        | Moderation type | You can select **Porn**, **Ad**, **Illegal**, or **Abuse**.                     |
| state        | Moderation result | <ul  style="margin: 0;"><li>`Normal`: Normal file.</li><li>`Possible`: Suspiciously sensitive file.</li><li>`Convince`: Sensitive file.</li></ul> |
| freeze       | Whether the file is blocked | <ul  style="margin: 0;"><li>`Yes`: Blocked.</li><li>`No`: Not blocked.</li></ul> |
| score        | Moderation score | The confidence the moderation result hits the moderation scene. Value range: 0–100. The higher the value, the more likely the content hits the currently returned moderation scene. <br>For example, `Porn 99` means that the content is very likely to be pornographic. |
| createTime   | Creation time | Creation time of the moderated file.                                           |
| resourcePath | Resource path | Storage path of the moderated file.                                           |
| sourceUrl    | Source URL   | URL of the moderated file.                                               |


### Manually moderating results

After you [filter results](#ResultScreening), the **Moderation Details** page will show filtered results, and you can perform the following operations on the filtered results:
 - Block an image or set its status to **Normal**.

 - Click a moderated image to view its details.

