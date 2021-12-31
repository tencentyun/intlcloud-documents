
## User Generated Short Video (UGSV) SDK License

UGSV SDK license overview:
- You can apply for the basic edition UGSV license for free to get a 28-day trial.
- UGSV SDK resource consumption such as acceleration, storage, traffic, etc. is billed according to VOD billing rules.
- If you need enterprise edition and Enterprise Pro licenses, please contact sales.
- The license fee cannot be refunded once UGSV is activated.


#### Pricing
|Edition|Validity Period|Unit Price (USD)|
|--|--|--|
|Trial edition|28 days|0|
|Lite edition license|1 year|269|
|Basic edition license|1 year|1,499|
|Enterprise edition license|1 year|25,999|
|Enterprise Pro edition license|1 year|71,999|

For details, please see [SDK Download](https://intl.cloud.tencent.com/document/product/1069/37914)

## AI-Based Video Analysis Feature
AI-based video analysis feature is billed on a postpaid monthly basis. The billing unit is USD/min and this service is billed based on service types and corresponding durations.

- Payment method: postpaid monthly billing cycle
- A duration of less than 1 minute in the source video is counted as 1 minute.

#### Pricing
AI-based video analysis feature has the following billable items:

- Intelligent highlights generation and video segmentation: intelligent video segmentation partitions videos into shots or scenes. This feature can be further optimized according to user requirements. **Highlights generation and video segmentation use different APIs and are billed separately**.
- Intelligent video tagging and video classification: intelligently identify figures, scenarios, voices, text and other information in videos and then automatically generate video tags, categories, summaries among others. **Video tagging and video classification use different APIs and are billed separately**.
- Intelligent video thumbnail recommendation: selects one or more screenshots of a video as the recommended thumbnails.

The billing details are as follows:

|Billable Items|Billing Mode|Unit Price (USD/minute)|
|--------|-------------|-------|
|Intelligent highlights generation|Billing by the original video duration|0.0572|
|Intelligent video segmentation|Billing by the original video duration|0.0572|
|Intelligent video tagging|Billing by the original video duration|0.0572|
|Intelligent video classification|Billing by the original video duration|0.0572| 
|Intelligent video thumbnail recommendation|Billing by the original video duration|0.0572|


#### Billing example

**User A wants to process video B. The APIs of intelligent video tagging and intelligent video classification will be called at the same time, and the original duration of video B is 100 minutes.
Service fee = 100 x 0.0572 + 100 x 0.0572 = 11.4 USD**

## AI-Based Video Auditing

The billing mode for AI-based video auditing is postpaid. The billing unit is USD/min and this service is billed based on service types and corresponding video durations.
Billing rules:

Payment method: postpaid.
- Payment method: Pay-as-you-go
- A duration of less than 1 minute in the source video is counted as 1 minute.

#### Pricing
AI-based video auditing feature intelligently reviews images, audios, and texts in videos to detect inappropirate content and outputs audit results as requested.
The billing details are as follows:

|Billable Items|Billing Mode|Unit Price (USD/min)|
|----------|----------|-------|
|Video auditing|Billing by the original video duration|0.016 |

#### Billing example
Suppose a user uses this feature to audit the 30-minute video A
Service fee = 30 x 0.016 = 0.48 USD.


