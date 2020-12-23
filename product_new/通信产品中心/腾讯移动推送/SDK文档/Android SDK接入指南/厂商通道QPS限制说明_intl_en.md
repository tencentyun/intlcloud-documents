All mobile phone vendors have a certain limit on the queries per second (QPS) of their push channels. If the current QPS cannot meet your operational needs, you can apply to the vendor for QPS increase as instructed below. (Only certain vendors allow such application.)
## Huawei Push
### QPS limit
QPS = application's MAU in the Huawei channel * application category weight * 0.00072
#### Glossary
MAU: the value of application's pushes through the Huawei channel on the last calendar day in a month is taken as the MAU of that month.
Categorization rule: the application category in Huawei AppGallery is used.

| Group Name | Application Category | Weight |
|-----|-----|-----|
| IM | Communication | 5 |
| Finance | Finance | 5 |
| News | News and information | 4 |
| Content | Books and references; media and entertainment; photography | 3 |
| Ecommerce | Shopping | 3 |
| Basic life necessities | Lifestyle and convenience; travel and navigation; food and drink; travel and accommodation | 3 |
| Business | Business | 3 |
| Gaming | Online games; puzzles games; simulation games; board games | 2 |
| Tools | Tools | 1 |
| Sports and health | Medicine and health; sports and health | 1 |
| Others | Kids; education; personalized themes; cars | 1 |
| Default | Default | 1 |

>?If your application has not been released on Huawei AppGallery, its category will be "Default".
If your application's QPS calculated by the formula is smaller than 6,000, the QPS of 6,000 will be used by default.
When the traffic across the entire network is high, there may be a system-level traffic throttling. 
In addition, no matter what application category it is, the number of pushes for a single device cannot exceed 100,000 per day; otherwise, push permission will be restricted, and you need to rectify your application and submit your rectification plan to apply for push permission again.

### Applying for QPS increase
If you have any questions and feedback about the product, please send an email in the following format to hwpush@huawei.com:
**Title: [QPS] consultancy and feedback + application name**

| Application Form for Increasing Huawei Message Push QPS for Application |   |   
| --- | --- | 
| Application name: |   |  
| Company name: |   |  
| Application package name: |   | 
| Application category on Huawei AppGallery: |   | 
| Question type: | Application for increasing the QPS, consultancy on the specific QPS, etc. |  
| Demand background: |   |  
| Specific demand: |   |  
| Contact information (email) |   |  

## Mi Push
### QPS limit
The assignment of push rate (QPS) by Mi Push is mainly based on the number of daily online MIUI devices of the application.
QPS indicates the number of requests that can be called in one second. Up to 1,000 target devices can be included in one request. For example, if the QPS is 3,000, a message can be pushed to up to 3 million devices in one second.
>?You can query the number of daily online MIUI devices in [Push Operation Platform](https://admin.xmpush.xiaomi.com/zh_CN/app/unauth) > Push Statistics > User Data > Detailed Data.

Different numbers of daily online MIUI devices are assigned with different QPS:

| Daily online MIUI devices |QPS|
| ---------|----------|
|≥10 million|3000|
|≥5 million and <10 million|2500|
|≥1 million and <5 million|2000|
|≥100,000 and <1 million|1000|
|< 100,000|500|


### Applying for QPS increase
Currently, no application is allowed.
## OPPO Push
### QPS limit
QPS: currently, the QPS limit of OPPO is not made public.

### Applying for QPS increase
Currently, no application is allowed.
## Vivo Push
### QPS limit
QPS: it is automatically adjusted based on the SDK subscription quantity, and the default minimum value is 500 pushes/sec.
### Applying for QPS increase
Currently, no application is allowed.

## Meizu Push
### QPS limit
QPS: it is 500 pushes/sec for an application by default. If you need a higher value, please contact Meizu for adjustment.

### Applying for QPS increase
You can contact Meizu for adjustment.
Push service QQ ID: 2442575011.
Push service email: push_support@meizu.com.

