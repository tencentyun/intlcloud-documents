## UGSV SDK License

Overview:

- You can apply for a 28-day trial license for UGSV Basic for free.
- The acceleration, storage, and traffic resources you use with the UGSV SDK are billed according to the billing rules of VOD.
- To use UGSV Enterprise or Enterprise Pro, please contact sales.
- Licenses are not refundable once activated.


#### Pricing

| Edition               | Validity Period | Price (USD) |
| ------------------ | ------ | ------------ |
| Trial     | 28 days   | 0            |
| Lite     | 1 year    | 269          |
| Basic     | 1 year    | 1499         |
| Enterprise     | 1 year    | 25999        |
| Enterprise Pro | 1 year    | 71999        |

To learn about the features of different editions, see [SDK Download](https://intl.cloud.tencent.com/document/product/1069/37914).

## AI-Based Video Analysis

The AI-based video analysis feature is billed monthly in the postpaid mode. We calculate the fee by multiplying the number of minutes used for a service by the unit price of the service.

- Payment method: Postpaid on a monthly basis
- A duration of less than 1 minute of the source video is counted as 1 minute.

#### Pricing

The billable items of AI-based video analysis are as follows:

- Intelligent highlights generation and video segmentation: Intelligent video segmentation splits videos into shots or scenes. This feature can be further optimized based on your requirements. **Highlights generation and video segmentation uses different APIs and are billed separately**.
- Intelligent video labeling and classification: Intelligent face, speech, and optical character recognition and generation of labels, categories, and summaries. **Video labeling and classification uses different APIs and are billed separately**.
- Intelligent thumbnail generation: Capturing one or more frames from a video to use as the thumbnail.

The items are billed as follows:

| Item       | Billed By                 | Price (USD/Min) |
| ------------ | ------------------------ | ----------------- |
| Highlights generation | Duration of the source video for which highlights are generated | 0.0572            |
| Video segmentation | Duration of the source video segmented | 0.0572            |
| Video labeling | Duration of the source video labeled | 0.0572            |
| Video classification | Duration of the source video classified | 0.0572            |
| Thumbnail generation | Duration of the source video for which thumbnails are generated | 0.0572            |


#### Billing example

**User A called the video labeling and classification APIs to analyze video B, whose length is 100 minutes.
Service fee = 100 x 0.0572 + 100 x 0.0572 = 11.4 USD**

## AI-Based Video Moderation

AI-based video moderation is billed monthly in the postpaid mode. We calculate the fee by multiplying the number of minutes moderated by the unit price.
Billing rules:

- Payment method: Postpaid
- A duration of less than 1 minute of the source video is counted as 1 minute.

#### Pricing

AI-based video moderation reviews the images, audios, and texts in videos to detect inappropriate content and generates moderation results as required.

The billing details are as follows:

| Item       | Billed By                 | Price (USD/Min) |
| -------- | ------------------------ | ----------------- |
| Video moderation | Duration of the source video moderated | 0.016             |

#### Billing example

 Suppose a user moderated a 30-minute video.
Service fee = 30 x 0.016 = 0.48 USD.



## DRM

VOD uses commercial DRM solutions to encrypt videos during transcoding. If you enable DRM, the corresponding cost will be included in your transcoding fee. We also bill you by the number of requests to play encrypted videos.

#### Pricing

| Billed By                        | Billing Mode     | Unit Price          |
| :---------------------------- | :----------- | :------------ |
| Number of requests to play encrypted videos | Postpaid | 0.0012 USD/request |



#### Details

- We bill you by the number of requests received to play DRM-encrypted videos.
- You will also be charged a transcoding fee for video encryption.
- DRM fees = DRM transcoding fee + DRM video playback fee (calculated by the number of playback requests)



#### Billing example

Assume that you used a commercial DRM solution to encrypt video A (length: 10 minutes; resolution: 2560 x 1440) on January 1 and generated video B (length: 10 minutes; resolution: 1280 x 640). There were 50 requests to play the encrypted video.
On January 2, you would be charged the following DRM fee:
0.0061 (USD/min) x 10 (minutes) + 50 (requests) x 0.0012 (USD/request) = 0.121 USD

>? DRM transcoding is billed in the same way as general transcoding. You are charged DRM transcoding fees each time you encrypt a video.