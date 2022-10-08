
Your MPS bills contain only the fees incurred for using media processing services such as transcoding and remuxing. **Fees for COS are not included**.
MPS supports daily and monthly billing for the pay-as-you-go mode. The default billing cycle is daily. If you want to switch to monthly billing, please contact your sales rep.

## Daily Billing
 
Each day, MPS calculates your usage in the previous day, sends you the bill, and deducts the fee from your account balance. You can view your usage details in the [console](https://console.cloud.tencent.com/mps). The daily billing cycle is used by default. If you want to change to monthly billing, please contact your sales rep.
 
+ Billing cycle: Daily. The fees incurred each day are billed and deducted from your account balance between 12:00 and 18:00 the following day.
+ Billing mode: Pay-as-you-go.
 
### Billable items 
#### General transcoding

Pricing: Fees are calculated by multiplying the video duration (minutes) after transcoding by the corresponding unit price.

|Codec|Resolution|Chinese Mainland|Mumbai, Seoul, Bangkok, Moscow|Hong Kong (China), Tokyo, Toronto, Frankfurt|Silicon Valley, Virginia|Singapore|
|-|-|-|-|-|-|-|
|H.264|4K (short side ≤ 2160 px)|0.0421|0.0480|0.0441|0.0441|0.0480|
|H.264|2K (short side ≤ 1440 px)|0.0206|0.0355|0.0316|0.0316|0.0355|
|H.264|FHD (short side ≤ 1080 px)|0.0095|0.0230|0.0215|0.0215|0.0230|
|H.264|HD (short side ≤ 720 px)|0.0049|0.0105|0.0109|0.0109|0.0105|
|H.264|SD (short side ≤ 480 px)|0.0024|0.0074|0.0079|0.0079|0.0074|
|H.265|4K (short side ≤ 2160 px)|0.2121|0.2480|0.2128|0.2128|0.2480|
|H.265|2K (short side ≤ 1440 px)|0.1136|0.1855|0.1564|0.1564|0.1855|
|H.265|FHD (short side ≤ 1080 px)|0.0472|0.1230|0.0494|0.0494|0.1230|
|H.265|HD (short side ≤ 720 px)|0.0246|0.0605|0.0248|0.0248|0.0605|
|H.265|SD (short side ≤ 480 px)|0.0145|0.0449|0.0127|0.0127|0.0449|
| AV1    | 4K (short side ≤ 2160 px)         | 0.5780|0.5780|0.5780|0.5780|0.5780|
| AV1    | 2K (short side ≤ 1440 px)         | 0.2890|0.2890|0.2890|0.2890|0.2890|
| AV1    | FHD (short side ≤ 1080 px) | 0.1445|0.1445|0.1445|0.1445|0.1445|
| AV1    | HD (short side ≤ 720 px)     | 0.0722|0.0722|0.0722|0.0722|0.0722|
| AV1    | SD (short side ≤ 480 px)     | 0.0361|0.0361|0.0361|0.0361|0.0361|
|Audio transcoding|-|0.0008|0.0019|0.0017|0.0017|0.0019|
|Remuxing|-|0.0011|0.0028|0.0026|0.0026|0.0028|


#### TSC transcoding
 
Pricing: Fees are calculated by multiplying the video duration (minutes) after transcoding by the corresponding unit price.

|Codec|Resolution|Chinese Mainland|Mumbai, Seoul, Bangkok, Moscow|Hong Kong (China), Tokyo, Toronto, Frankfurt|Silicon Valley, Virginia|Singapore|
|-|-|-|-|-|-|-|
|H.264|4K (short side ≤ 2160 px)|0.1493|0.1533|0.1467|0.1467|0.1533|
|H.264|2K (short side ≤ 1440 px)|0.0747|0.0767|0.0733|0.0733|0.0767|
|H.264|FHD (short side ≤ 1080 px)|0.0347|0.0356|0.0340|0.0340|0.0356|
|H.264|HD (short side ≤ 720 px)|0.0176|0.0181|0.0173|0.0173|0.0181|
|H.264|SD (short side ≤ 480 px)|0.0117|0.0120|0.0115|0.0115|0.0120|
|H.265|4K (short side ≤ 2160 px)|0.7467|0.7667|0.7333|0.7333|0.7667|
|H.265|2K (short side ≤ 1440 px)|0.3733|0.3833|0.3667|0.3667|0.3833|
|H.265|FHD (short side ≤ 1080 px)|0.1739|0.1785|0.1708|0.1708|0.1785|
|H.265|HD (short side ≤ 720 px)|0.0869|0.0893|0.0854|0.0854|0.0893|
|H.265|SD (short side ≤ 480 px)|0.0581|0.0597|0.0571|0.0571|0.0597|
| AV1    | 4K (short side ≤ 2160 px)         | 1.9074|1.9074|1.9074|1.9074|1.9074|
| AV1    | 2K (short side ≤ 1440 px)         | 0.9537|0.9537|0.9537|0.9537|0.9537|
| AV1    | FHD (short side ≤ 1080 px) | 0.4768|0.4768|0.4768|0.4768|0.4768|
| AV1    | HD (short side ≤ 720 px)     | 0.2384|0.2384|0.2384|0.2384|0.2384|
| AV1    | SD (short side ≤ 480 px)     | 0.1100|0.1100|0.1100|0.1100|0.1100|


### Billing details

+ Billing rule: Transcoding services are billed daily based on the codec used and the output resolution and video duration.
+ Billing formula: Video transcoding fees = Output video duration (minutes) x Codec- and resolution-specific unit price (USD/minute)
+ Each transcoding task is billed only once. Video duration is rounded up to the nearest minute.
 
### Example

Suppose you used the transcoding service in the Mumbai region on January 1 and generated two videos. One was 60 minutes long and had a resolution of 2560 x 1440 px. The other was 100 minutes long and had a resolution of 1600 x 980. The codec used was H.264. On January 2, the transcoding fee deducted would be as follows:
0.0355 (USD/minute) x 60 (minutes) + 0.023 (USD/minute) x 100 (minutes) = 4.43 USD


#### Intelligent content recognition
The intelligent content recognition feature uses AI technologies to identify text, speech, and opening and closing credits in videos. Fees are calculated by multiplying the video duration (minutes) by the unit price.

Billing rules:
- Payment method: Pay-as-you-go.
- Video duration is rounded up to the nearest minute.
The unit prices for different regions are as follows:

|Billable Item|Chinese Mainland|Mumbai, Seoul, Bangkok, Moscow|Hong Kong (China), Tokyo, Toronto, Frankfurt|Silicon Valley, Virginia|Singapore|
|-|-|-|-|-|-|
|Intelligent content recognition|0.0511|0.0562|0.0572|0.0572|0.0562|


Billing formula: Intelligent content recognition fees = Source video duration (minute) x Unit price (USD/minute)


#### Intelligent content analysis
The intelligent content analysis feature leverages AI technologies and a large sample library to analyze and process video content. Its capabilities include intelligent labeling, categorization, thumbnail generation, highlights generation, summarization, and video splitting. Fees are calculated by multiplying the video duration (minutes) by the unit price.
Billing rules:
- Payment method: Pay-as-you-go.
- Video duration is rounded up to the nearest minute.
The unit price is as follows:

|Billable Item|Chinese Mainland|Mumbai, Seoul, Bangkok, Moscow|Hong Kong (China), Tokyo, Toronto, Frankfurt|Silicon Valley, Virginia|Singapore|
|-|-|-|-|-|-|
|Intelligent content analysis|0.0511|0.0562|0.0572|0.0572|0.0562|


Billing formula: Intelligent content recognition fees = Source video duration (minute) x Unit price (USD/minute)



#### Video moderation
The video moderation feature reviews images, speech, and text in videos to detect inappropriate content and generates moderation results as required. Fees are calculated by multiplying the duration of videos moderated by the unit price.

Billing rules:
- Payment method: Pay-as-you-go.
- Video duration is rounded up to the nearest minute.

The unit price is as follows:

|Billable Item|Billed By|Price|
|-|-|-|
|Video moderation|Source video duration|0.016|


Billing formula: Video moderation fees = Source video duration (minute) x Unit price (USD/minute)


## Monthly Billing

On the first day of each month, MPS calculates your usage in the previous month, sends you a bill, and deducts the fee from your balance account. You can view your usage details in the [console](https://console.cloud.tencent.com/mps).


- Billing cycle: Monthly. The fees incurred each month are billed and deducted from your account balance on the first day of the following month.
- Payment method: Pay-as-you-go.
- For monthly billing, the unit prices specified in your contract with Tencent Cloud will apply. For more information, please contact your sales rep.



