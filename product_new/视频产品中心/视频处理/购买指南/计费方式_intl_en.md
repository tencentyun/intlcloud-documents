
MPS bill includes fees only for processing audio/video files, such as transcoding or remuxing, but **not fees incurred by COS**.
MPS is billed in two modes: daily billing or monthly billing. The daily billing mode is used by default. If you want to change it to monthly billing, please contact your Tencent Cloud rep.

## Daily Billing
 
MPS will push and settle the bill for your resource usage generated yesterday on a daily basis. You can view the actual resource usage in the [console](https://console.cloud.tencent.com/mps). The daily billing mode is used by default. If you want to change it to monthly billing, please contact your Tencent Cloud rep.
 
+ Billing cycle: The bill is settled daily. Everyday at a point between 12:00 and 18:00 Beijing time, MPS will calculate, output, and settle the bill for fees incurred yesterday.
+ Billing mode: Pay-as-you-go.
 
### Billable items 
#### General transcoding

Pricing: Fees are charged based on the video length after transcoding in USD/minute.

|Codec|Resolution|Mainland China|(Mumbai, Seoul, Bangkok, Moscow)|(Hong Kong of China, Tokyo, Toronto, Frankfurt)|(Silicon Valley, Virginia)|(Singapore)|
|-|-|-|-|-|-|-|
|H.264|4K (3840 * 2160p) or below|0.0421|0.0480|0.0441|0.0441|0.0480|
|H.264|2K (2560 * 1440p) or below|0.0206|0.0355|0.0316|0.0316|0.0355|
|H.264|FHD (1920 * 1080p) or below|0.0095|0.0230|0.0215|0.0215|0.0230|
|H.264|HD (1280 * 720p) or below|0.0049|0.0105|0.0109|0.0109|0.0105|
|H.264|SD (640 * 480p) or below|0.0024|0.0074|0.0079|0.0079|0.0074|
|H.265|4K (3840 * 2160p) or below|0.2121|0.2480|0.2128|0.2128|0.2480|
|H.265|2K (2560 * 1440p) or below|0.1136|0.1855|0.1564|0.1564|0.1855|
|H.265|FHD (1920 * 1080p) or below|0.0472|0.1230|0.0494|0.0494|0.1230|
|H.265|HD (1280 * 720p) or below|0.0246|0.0605|0.0248|0.0248|0.0605|
|H.265|SD (640 * 480p) or below|0.0145|0.0449|0.0127|0.0127|0.0449|
|Audio transcoding|-|0.0008|0.0019|0.0017|0.0017|0.0019|
|Remuxing|-|0.0011|0.0028|0.0026|0.0026|0.0028|


#### Tencent Extreme Speed High Definition
 
Pricing: Fees are charged based on the source video length in USD/minute.
 
|Codec|Resolution|Mainland China|(Mumbai, Seoul, Bangkok, Moscow)|(Hong Kong of China, Tokyo, Toronto, Frankfurt)|(Silicon Valley, Virginia)|(Singapore)|
|-|-|-|-|-|-|-|
|H.264|4K (3840 * 2160p) or below|0.1493|0.1533|0.1467|0.1467|0.1533|
|H.264|2K (2560 * 1440p) or below|0.0747|0.0767|0.0733|0.0733|0.0767|
|H.264|FHD (1920 * 1080p) or below|0.0347|0.0356|0.0340|0.0340|0.0356|
|H.264|HD (1280 * 720p) or below|0.0176|0.0181|0.0173|0.0173|0.0181|
|H.264|SD (640 * 480p) or below|0.0117|0.0120|0.0115|0.0115|0.0120|
|H.265|4K (3840 * 2160p) or below|0.7467|0.7667|0.7333|0.7333|0.7667|
|H.265|2K (2560 * 1440p) or below|0.3733|0.3833|0.3667|0.3667|0.3833|
|H.265|FHD (1920 * 1080p) or below|0.1739|0.1785|0.1708|0.1708|0.1785|
|H.265|HD (1280 * 720p) or below|0.0869|0.0893|0.0854|0.0854|0.0893|
|H.265|SD (640 * 480p) or below|0.0581|0.0597|0.0571|0.0571|0.0597|



### Billing description

+ Billing rule: The transcoding service is billed daily based on the requested codec, resolution, and output video length.
+ Billing formula: Video transcoding fees = output video length (minute) * transcoding unit price for different codec and resolution options (USD/minute)
+ Each transcoding task is billed only once. If the output video length is less than 1 minute, it will be calculated as 1 minute.
 
### Billing example

For example, if you use the general transcoding service in the Mumbai region on January 1 to transcode two videos with H.264 codec (one to a 60-minute video at 2560 * 1440p resolution and the other to a 100-minute video at 1600 * 980p resolution), then you need to pay transcoding fees on January 2 as calculated below:
Transcoding fees = 0.0355 (USD/minute) * 60 (minutes) + 0.023 (USD/minute) * 100 (minutes) = 4.43 USD


#### Intelligent content recognition
The intelligent content recognition feature of MPS uses AI technology to recognize elements in videos such as human faces, objects, texts, speeches, opening and closing credits, and frame-specific tags. It is priced in USD/minute.

The billing description is as shown below:
- Billing mode: Pay-as-you-go.
- If the source video length is less than 1 minute, it will be calculated as 1 minute.
The billing details are as shown below:

|Billable Item|Mainland China|(Mumbai, Seoul, Bangkok, Moscow)|(Hong Kong of China, Tokyo, Toronto, Frankfurt)|(Silicon Valley, Virginia State)|(Singapore)|
|-|-|-|-|-|-|
|Intelligent content recognition|0.0511|0.0562|0.0572|0.0572|0.0562|


__Billing formula__: Intelligent content recognition fees = source video length (minute) * unit price (USD/minute)


#### Video audit
The audiovisual AI-based video audit feature of MPS intelligently audits images, speeches, and texts in videos to detect pornographic, terrorism, and politically sensitive information and outputs audit results as requested. This feature is billed based on the used service and source video length in USD/minute.

The billing description is as shown below:
- Billing mode: Pay-as-you-go.
- If the source video length is less than 1 minute, it will be calculated as 1 minute.

The billing details are as shown below:

|Billable Item|Billing Mode|Price|
|-|-|-|
|Video audit|By the source video length|0.016|


 __Billing formula__: Video audit fees = source video length (minute) * unit price (USD/minute)


## Monthly Billing

On the first day in each month, MPS will push and settle the bill for your resource usage generated in the last month. You can view the actual resource usage in the [console](https://console.cloud.tencent.com/mps).


- Billing cycle: The bill is settled monthly. On the first day in each month, MPS will calculate, output, and settle the bill for fees incurred in the last month.
- Billing mode: Pay-as-you-go.
- For more information on monthly billing, please contact your Tencent Cloud rep. The prices will be subject to the contract.



