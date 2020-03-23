All mobile phone vendors have a certain limit on the queries per second (QPS) of their push channels. If the current QPS cannot meet your operational needs, you can apply to the vendor for QPS increase as instructed below. (Only certain vendors allow such application.)
## Huawei Push
### QPS limit
QPS = app's MAU in the Huawei channel * app category weight * 0.00072
#### Glossary
MAU: the value of app's pushes through the Huawei channel on the last calendar day in a month is taken as the MAU of that month.
Categorization rule: the app category in Huawei AppGallery is used.

| Group Name | App Category | Weight |
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

>If your app has not been released on Huawei AppGallery, its category will be "Default".
If your app's QPS calculated by the formula is smaller than 6,000, the QPS of 6,000 will be used by default.
When the traffic across the entire network is high, there may be a system-level traffic throttling. 
In addition, no matter what app category it is, the number of pushes for a single device cannot exceed 100,000 per day; otherwise, push permission will be restricted, and you need to rectify your app and submit your rectification plan to apply for push permission again.

### Applying for QPS increase
If you have any questions and feedback about the product, please send an email in the following format to hwpush@huawei.com:
**Title: [QPS] consultancy and feedback + app name**

| Application Form for Increasing Huawei Message Push QPS for App |   |   
| --- | --- | 
| App name: |   |  
| Company name: |   |  
| App package name: |   | 
| App category on Huawei AppGallery： |   | 
| Question type: | Application for increasing the QPS, consultancy on the specific QPS, etc. |  
| Background of the demand: |   |  
| Specific demand: |   |  
| Contact information (email) |   |  

## Mi Push
### QPS limit
QPS: 600,000/minute.
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
QPS: it is 500 pushes/sec for an app by default. If you need a higher value, please contact Meizu for adjustment.

### Applying for QPS increase
You can contact Meizu for adjustment.
Push service QQ ID: 2442575011.
Push service email: push_support@meizu.com.

