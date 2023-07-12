## Overview

The COS content moderation service intelligently moderates the multimedia content of images, videos, audios, documents, and text. It helps you effectively identify non-compliant content such as pornographic, vulgar, illegal, disgusting, and offensive information to avoid operational risks.

After files are moderated successfully, you can view the moderation results by condition and manually process them on the **Moderation Details** page.

## Directions

<span id="ResultScreening"></span>
### Filtering results

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the target bucket to go to the configuration page.
4. On the left sidebar, select **Sensitive Content Moderation** > **Moderation Details** to enter the **Moderation Details** page.
5. Select the conditions as needed.

 - Scope: You can view the results of moderation through API calls, automatic moderation, and historical data moderation.
 - File type: You can view the moderation results of images, videos, audios, and text.
 - Level-1 category of moderation result: It refers to the level-1 label of the moderation result. You can specify it to filter the results.
 - Level-2 category of moderation result: It refers to the level-2 label of the moderation result, which is more specific than the level-1 category. You can specify it to filter the results.
 - Moderation Result: Moderated files are categorized into three types: sensitive, suspected, and normal files. You can view a type of file or all files.
    - Sensitive: Images whose score falls within the range of [91,100].
    - Suspected: Images that are suspected to be sensitive and whose score falls within the range of [61,90]. For such images, the system cannot determine whether they are sensitive, so we recommend you determine it through human moderation.
    - Normal: Images whose score falls within the range of [0,60].
 - Block Status: You can view the moderation results of blocked, normal, or all files.
 - Moderation Status: You can filter the moderation status, including **under review**, **succeeded**, and **rejected**.
 - Moderation Policy: You can filter moderation results by moderation policy (`BizType`).
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

| Field        | Description                             |
| ------------------- | --------------------------------------------------------- |
| Moderation record ID      | Unique ID of the moderation job (also known as job ID), through which you can query the moderation result.  |
| Object name        | Name of the moderated file. <br>Note: This field is empty if you use the API to directly moderate text content.      |
| Moderation result type  | Moderation result type of the file such as **Porn** or **Ad**. If the moderation result is **Normal**, this field will be empty.     |
| Moderation score | The confidence the moderation result hits the moderation scene. Value range: 0–100. The higher the value, the more likely the content hits the currently returned moderation scene. <br>For example, `99` means that the content is very likely to be pornographic. |
| Moderation result subtype | Moderation subtype of the file such as **Sexy**. If the moderation result is **Normal**, this field will be empty. |
| Moderation result        | Moderation results include **Normal**, **Sensitive**, and **Suspected**. The result is determined by the moderation score. <li>Normal: The moderation score is 0–60.<li>Sensitive: The moderation score is 91–100.<li>Suspected: The moderation score is 61–90. |
| Blocked        | Whether the moderated file is blocked. You can configure automatic blocking upon moderation in **Automatic Moderation** and **Historical Data Moderation**.                        |
| File size        | Unit: B.                        |
| Moderation time        | Time when the file is moderated.              |
| File path        | Location of the file in the bucket. <br>Note: This field is empty if you use the API to directly moderate text content or a file not in COS.                                                    |
| Original link  | File URL. <br>Note: This field is empty if you use the API to directly moderate text content.       |
| Moderation method        | File moderation method. Valid values: <li>`Notify`: Automatic moderation. <li>`Task`: Historical data moderation. <li>`API`: Moderation through API call. |
| File type        | Data source of the moderated file. Valid values: <li>`object`: The file is in COS. <li>`objecturl`: The file is specified by URL, which can be an external URL. <li>`API`: The file is moderated through API call.           |
| Moderation status        | <li>`Success`: The moderation succeeded. <li>`Failed`: The moderation failed.      |
| Error code           | If the moderation status is `Failed`, the error cause will be returned through an error code. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).        |
| Error message        | Error message of the moderation failure.        |
| bizType             | Unique ID of the moderation policy, by which you can find the currently configured moderation policy.                                                                                                     |


### Manually moderating results

After you [filter results](#ResultScreening), the **Moderation Details** page will show filtered results, and you can perform the following operations on the filtered results:
 - Block an image or set its status to **Normal**.

 - Click a moderated image to view its details.

