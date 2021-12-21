Smart cold storage relies on the media asset management capabilities of VOD. To reduce the storage costs incurred when you use VOD, VOD enables media asset lifecycle management, with which you can change the storage class of VOD files from STANDARD to STANDARD_IA, ARCHIVE, or DEEP_ARCHIVE according to certain policies based on your business characteristics. In this way, you can manage your media asset files more flexibly.

## Use Cases
- **Ecommerce live streaming**: as stipulated by [Measures for the Supervision and Administration of Online Trading](http://gkml.samr.gov.cn/nsjg/fgs/202103/t20210315_326936.html) issued by the State Administration for Market Regulation of China, live streaming service providers shall retain live streaming videos of online transactions for at least three years after the live streaming ends. Such videos are generally stored in VOD in STANDARD storage class, some of which will never or seldom be played back and will be only used for audit by applicable authorities. The smart cold storage feature can effectively help you reduce the storage costs of media assets.
- **Cold storage of infrequently accessed media**: for video portals, streaming media platforms, and UGC management platforms, media assets that are infrequently accessed or watched by users cannot be directly removed for certain reasons, which incur high storage costs. The smart cold storage feature of VOD can store media files in a cold storage class according to the number of accesses, which effectively reduces the storage costs of media assets while still allowing infrequent watches.
- **Media asset archive**: in news, media, radio, and TV industries, some media asset files are highly sensitive to time and generally stored for a long period as historical materials and will be searched and watched in the future only when required. In such scenarios, you can change their storage class to ARCHIVE or DEEP_ARCHIVE to reduce the storage costs.

## Prerequisites
1. You have [signed up for](https://intl.cloud.tencent.com/register?&s_url=https%3A%2F%2Fcloud.tencent.com%2F) and [logged in to](https://intl.cloud.tencent.com/login?s_url=https%3A%2F%2Fcloud.tencent.com%2F) your Tencent Cloud account and completed identity verification.
2. You have activated the [VOD](https://console.cloud.tencent.com/vod/overview) service.
3. You have created relevant policies. For more information, see [Media Asset Cold Storage](https://intl.cloud.tencent.com/document/product/266/42092).

## Use Instructions
To use the media asset cold storage feature, you should understand the concepts of [storage class](#type), [data retrieval and retrieval mode](#retake), and [policy management](#strategy).
### Storage class[](id:type)
VOD provides the following storage classes for storing your media asset files: STANDARD, STANDARD_IA, ARCHIVE, and DEEP_ARCHIVE. Their attributes are as detailed below:

| Storage Class   | STANDARD | STANDARD_IA | ARCHIVE  | DEEP_ARCHIVE   |
| ------ | ---- | ---- | ----- | -------- |
| Default in VOD  | Yes    | No    | No     | No        |
| Storage costs   | High    | Medium    | Low     | Very low       |
| Access performance | High | Low | Access not supported | Access not supported |
| Data retrieval fees | No    | No    | Yes | Yes    |
| Supported regions   | All   | All   | All    | Beijing, Shanghai, and Chongqing |

STANDARD is the default storage class in VOD. Live recording files as well as files generated in various upload methods or video processing tasks are stored in STANDARD by default.

| Attribute | Ranking from High to Low |
|---------|---------|
| Storage costs | STANDARD > STANDARD_IA > ARCHIVE > DEEP_ARCHIVE |
| Access performance | STANDARD > STANDARD_IA |
>?
>- ARCHIVE and DEEP_ARCHIVE storage classes don't support direct access, and you should retrieve the data first before you can access it. VOD only allows you to retrieve data to **STANDARD**.
>- Access performance will affect video watch metrics such as **time to first frame (TTFF) and lag rate**; therefore, **we recommend you not change the storage class for frequently accessed businesses in the production environment**.

VOD allows you to change between storage classes as follows:

| Source Storage Class  | Target Storage Class           |
| ------ | ---------------- |
| STANDARD    | STANDARD_IA, ARCHIVE, and DEEP_ARCHIVE |
| STANDARD_IA   | STANDARD, ARCHIVE, and DEEP_ARCHIVE |
| ARCHIVE   | STANDARD             |
| DEEP_ARCHIVE | STANDARD             |
>?
>- To switch ARCHIVE and DEEP_ARCHIVE to another storage class other than STANDARD, you should switch them to STANDARD first and then switch STANDARD to the target storage class.
>- The granularity of storage class change is `FileId`, that is, the storage classes of the original and video processing files are the same, and you cannot specify the storage class for part of the files under the `FileId` separately.

### Data retrieval and retrieval mode[](id:retake)
#### Data retrieval
After the storage class of a media asset is changed to the ARCHIVE or DEEP_ARCHIVE storage class, the file cannot be directly accessed, that is, operations such as video playback and processing initiation cannot be performed. If you want to access it, you can change its storage class as instructed in the previous section. However, sometimes you only want to access a media asset for a short period of time and still retain it in ARCHIVE or DEEP_ARCHIVE after access. In this case, the above method is not applicable. To meet such needs, VOD provides the data retrieval capabilities.

VOD supports two retrieval operations for media in ARCHIVE and DEEP_ARCHIVE: permanent retrieval and retrieval for specified period.

| Operation on ARCHIVE/DEEP_ARCHIVE | Storage Class Change   | Retrieval       |
| ------------------- | -------- | -------- |
| Real-Timeness                 | Async       | Async       |
| Mode                  | Expedited/Standard/Bulk | Expedited/Standard/Bulk |
| Validity period                 | Permanent       | Specified period     |
| Copy generation                | No        | Yes        |

1. After retrieval, VOD will generate a copy for the media asset in STANDARD storage class.
2. A retrieval copy is valid for a specific number of days, within which the media asset can be accessed. Once expired, it will be automatically cleared, and then the media asset will become inaccessible.
3. Within the copy's validity period, additional STANDARD storage fees will be incurred.
4. Within the copy's validity period, the media asset cannot be retrieved again.

#### Retrieval mode
Storage class change and retrieval for ARCHIVE and DEEP_ARCHIVE have multiple modes, which have the same final effect but are different in speed and cost (i.e., retrieval fees).

| Retrieval Mode | Time of Retrieval from ARCHIVE | Time of Retrieval from DEEP_ARCHIVE |
| ---- | -------- | ---------- |
| Expedited mode | 5 minutes      | Not supported        |
| Standard mode | 5 hours      | 24 hours       |
| Bulk mode | 12 hours     | 48 hours       |
>?
>- A media asset (represented as one `FileId`) can contain many files in storage, such as original file, transcoded file, and screenshot file, each of which may have different actual retrieval completion time. VOD doesn't maintain the specific retrieval completion status of each file but takes the media asset as a whole to calculate its retrieval completion time based on the longest possible time uniformly. Before that time arrives, even if all files under the media asset are retrieved, the media asset will still be marked as not retrieved and be inaccessible.
>- As the time point when a media asset is marked as unretrieved will be after the actual retrieval time point, the available duration of the retrieved copy of the media asset will be shorter than the expected period. To ensure that the copy has a sufficient available duration, we recommend you add one more day to the validity period when retrieving a media asset from DEEP_ARCHIVE.

### Policy management[](id:strategy)
To help you uniformly manage the lifecycle of a large number of media assets, VOD combines media asset information and media asset file playback statistics to offer the policy-based smart management system.

The VOD backend executes management tasks every day and changes the storage class of media assets that meet the conditions of the specific policy.
#### Policy capabilities
##### Combined filtering
A policy allows you to specify a series of conditions to change the storage class of media assets that meet all conditions **at the same time**. The specific filter conditions are as detailed below:
- Media asset type, such as video, audio, and image.
- Media asset creation date, which offers the following options:
 - Files created before the specified date.
 - Files created after the specified date.
 - Files created between two specified dates.
 - Files created before a certain number of days (which dynamically changes with the current date).
 - Unlimited (that is, all media assets meet this condition).
- Category ID. You can specify multiple category IDs or none (that is, all media assets meet this condition).
- Media asset source type, including live recording, upload, video editing, and other. You can specify multiple source types or none (that is, all media assets meet this condition).
- Number of recent playbacks. You can filter media assets whose number of playbacks is less than the specified value in the specified number of days. You can also set no limit (that is, all media assets meet this condition).

##### Disabling policy
Once created, a policy will be started automatically, and you can disable it as needed. Once disabled, it will be ignored in management tasks created on the next day and afterwards until it is enabled again.
>?Once disabled, a policy may still take effect or not take effect in the management tasks on the current day.

#### Restrictions
Up to 10 policies can be configured.
You cannot specify the policy priority. If a media asset hits multiple policies at the same time, the policy priorities will be automatically determined by the target storage class as follows: DEEP_ARCHIVE > ARCHIVE > STANDARD_IA.

## Configuring VOD Smart Cold Storage Policy
### Step 1. Create a cold storage policy
Log in to the [VOD console](https://console.cloud.tencent.com/vod/media) (non-admin), click **Media Assets** > **Cold Storage** on the left sidebar, and click **Create Policy**.
![](https://qcloudimg.tencent-cloud.cn/raw/8c2143b18f7b88b715b3881e25062e9b.png)

### Step 2. Configure the cold storage policy
![](https://qcloudimg.tencent-cloud.cn/raw/d0c4864520a38107b5f4c43d3b6ac56c.png)
Configure the cold storage policy as needed.
Example: as shown above, if the number of video playbacks is less than 300 in 30 days for a video, the STANDARD_IA storage policy will be triggered, and VOD will store all media assets meeting the rule in STANDARD_IA.

### Step 3. Confirm the configuration for it to take effect
![](https://qcloudimg.tencent-cloud.cn/raw/098381b8a25eb591445aefc642c5447e.png)
