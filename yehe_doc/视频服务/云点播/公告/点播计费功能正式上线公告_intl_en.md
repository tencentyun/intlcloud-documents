# Video on Demand (VOD) Billing Feature Is Coming Soon
Dear Tencent Cloud user,
VOD billing feature will be available on November 13, 2020.
VOD Billable Items：Video Storage, Video Transcoding, Video Acceleration. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/266/2838)
##  Video Storage
Fees for VOD video storage are charged differently in Chinese Mainland and outside Chinese Mainland.

|Regions|Unit Price（USD）|
|----|----|
|Chinese mainland|0.0006 USD/GB/Day|
|Outside Chinese mainland|0.0009 USD/GB/Day|


## Video Transcoding
### Basic Transcoding
Charges are made according to the duration of output files and the resolution range of video short side.

|Codec|Resolution|Unit Price (USD/min)|
|----|----|----|
|H.264|4K (Short side ≤ 2160 px）|0.0521|
|H.264|	2K (Short side ≤ 1440 px）|	0.0242|
|H.264|	FHD (Short side ≤ 1080 px|	0.0121|
|H.264|	HD (short side ≤ 720 px)	|0.0061|
|H.264|	SD (short side ≤ 480 px)|0.003|
|H.265|	4K (Short side ≤ 2160 px）	|0.2521|
|H.265|	2K (Short side ≤ 1440 px）	|0.126|
|H.265|	FHD (Short side ≤ 1080 px）|	0.063|
|H.265|	HD (Short side ≤ 720 px)	|0.0315|
|H.265|	SD (Short side ≤ 480 px)	|0.0158|
|Remuxing|	-|	0.0028|
|Audio transcoding	|-	|0.002|

### TESHD
Charges are based on the output file duration and the resolution range of the video short side.

|Codec|	Resolution	|Unit Price (USD/min)|
|----|----|----|
|H.264|	4K (short side ≤ 2160 px)	|0.1721|
|H.264|	2K (short side ≤ 1440 px)|	0.08|
|H.264|	FHD(short side ≤ 1080 px)	|0.04|
|H.264|	HD(Short side ≤ 720 px)|	0.02|
|H.264|	HD(Short side ≤ 480 px)	|0.01|
|H.265|	4K (short side ≤ 2160 px)|	0.8319|
|H.265|	2K (short side ≤ 1440 px)|	0.416|
|H.265|	FHD(short side ≤ 1080 px)|	0.208|
|H.265|	HD(short side ≤ 720 px)|	0.104|
|H.265|	SD(short side ≤ 480 px)|	0.052|

### Video Editing
Charges are based on the codec, duration and resolution of the output file.The unit prices as per resolution is the same as those of the Video Transcoding.

## Video Acceleration
Charges of VOD video acceleration differ in Chinese mainland and outside Chinese mainland.

In Chinese mainland, fees are charged uniformly without discrimination for all regions. Outside Chinese mainland, there are eight billing regions determined according to locations of Tencent Cloud CDN node servers. The eight regions are Asia Pacific Region 1, Asia Pacific Region 2, Asia Pacific Region 3, Middle East, Europe, North America, South America, and Africa.

|Regions|	Countries and Places|
|----|----|
|Asia Pacific Region 1|	Hong Kong (China), Macau (China), Vietnam, Singapore, Thailand|
|Asia Pacific Region 2	|Taiwan (China), Japan, South Korea, Malaysia, Indonesia|
|Asia Pacific Region 3	|Philippines, India, Australia, other Asia-Pacific countries and regions|
|Middle East|	Saudi Arabia, United Arab Emirates, Turkey|
|Europe|	United Kingdom, Russia, Germany, Italy, Ireland, France, Netherlands, Spain|
|North America	|United States, Canada|
|South America|	Brazil|
|Africa|	South Africa|

Tencent VOD traffic is billed on a daily basis with a tiered pricing. The more traffic you use on each day, the lower the billing tier. Detailed tiered unit prices are as follows:

|Traffic Tier (USD/GB)|	Chinese Mainland|	Asia Pacific Zone 1|	Asia Pacific Zone 2	|Asia Pacific Zone 3|	Middle East|	Europe|	North America|	South America	|Africa|
|----|----|----|----|----|----|----|----|----|----|
|0 GB - 500 GB (inclusive)	|0.039	|0.113|	0.125|	0.125	|0.163	|0.071	|0.071|	0.169|	0.169|
|500 GB - 2 TB (inclusive)|	0.038|	0.038	|0.105|	0.105|	0.159	|0.064|	0.064	|0.161|	0.161|
|2 TB - 50 TB (inclusive)|	0.036|	0.097|	0.099|	0.099	|0.154	|0.051|	0.051|	0.156	|0.156
|50 TB - 100 TB (inclusive)	|0.033|	0.084	|0.092|	0.092	|0.145|	0.033	|0.033|	0.15|	0.15|
|100 TB |	0.025|	0.071|	0.085	|0.085|	0.135	|0.026|	0.026	|0.14|	0.14|

If your business volume is so large ( with storage capacity greater than 1 PB or daily traffic consumption over 10 TB) that daily billing cycle cannot meet your needs. You can contact sales to negotiate the billing modes and prices.

Please pay attention to the changes in billing rules and your balance, and adjust your business in time.

If you have any questions,please [contact us](https://intl.cloud.tencent.com/document/product/266/19905).

2020-09-28
Tencent Cloud
