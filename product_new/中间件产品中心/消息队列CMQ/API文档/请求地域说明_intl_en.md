> Fees will be incurred whenever public network downstream traffic is generated from using a public network domain name, including beta testing. We strongly recommend that users with services on Tencent Cloud use private network domain names because doing so will not incur traffic fees.

## Request Domain Name
### Queue Model
**Please refer to the notes below to replace {$region} in the domain name with the corresponding region name: **
- Domain name for public network API request: `https://cmq-queue-{$region}.api.qcloud.com`
- Domain name for private network API request: `http://cmq-queue-{$region}.api.tencentyun.com`

### Topic Model
**Please refer to the notes below to replace {$region} in the domain name with the corresponding region name: **
- Domain name for public network API request: `https://cmq-topic-{$region}.api.qcloud.com`
- Domain name for private network API request: `http://cmq-topic-{$region}.api.tencentyun.com`

#### Notes
- {$region} must be replaced with a specific region, such as gz (Guangzhou), sh (Shanghai), bj (Beijing), hk (Hong Kong), cd (Chengdu), ca (North America), usw (West US), use (East US), in (India), th (Thailand), and sg (Singapore). The value of "region" in the common parameters should be consistent with that in the domain name. If there is any inconsistency, the request will be sent to the region specified in the domain name.
- The domain name for public network request only supports HTTPS, and the domain name for private network request only supports HTTP.
- Some of the input parameters are optional. Default value is used for those not specified.
- All the output parameters are returned to the user when the request is successful; otherwise, at least code, message, and requestId are returned.



## Region
The "region" in the API request domain name must be replaced with a specific region. The region is subject to the "region" value of the domain name instead of that in the common parameters. Currently, the regions launched in CMQ are shown in the following table:
### Queue Model

| Region | Replacement Value | Domain Name for Public Network Request | Domain Name for Private Network Request |
|---------|---------|---------|---------|
| Beijing | bj | `https://cmq-queue-bj.api.qcloud.com`|`http://cmq-queue-bj.api.tencentyun.com` |
| Shanghai | sh | `https://cmq-queue-sh.api.qcloud.com`|`http://cmq-queue-sh.api.tencentyun.com` |
| Guangzhou | gz | `https://cmq-queue-gz.api.qcloud.com`|`http://cmq-queue-gz.api.tencentyun.com` |
| Hong Kong | hk | `https://cmq-queue-hk.api.qcloud.com`|`http://cmq-queue-hk.api.tencentyun.com` |
| Chengdu | cd | `https://cmq-queue-cd.api.qcloud.com`|`http://cmq-queue-cd.api.tencentyun.com` |
| North America | ca | `https://cmq-queue-ca.api.qcloud.com`|`http://cmq-queue-ca.api.tencentyun.com` |
| West US | usw | `https://cmq-queue-usw.api.qcloud.com`|`http://cmq-queue-usw.api.tencentyun.com` |
| East US | use | `https://cmq-queue-use.api.qcloud.com`|`http://cmq-queue-use.api.tencentyun.com` |
| Thailand | th | `https://cmq-queue-th.api.qcloud.com`|`http://cmq-queue-th.api.tencentyun.com` |
| India | in | `https://cmq-queue-in.api.qcloud.com`|`http://cmq-queue-in.api.tencentyun.com` |
| Singapore | sg | `https://cmq-queue-sg.api.qcloud.com`|`http://cmq-queue-sg.api.tencentyun.com` |


### Topic Model 

| Region | Replacement Value | Domain Name for Public Network Request | Domain Name for Private Network Request |
|---------|---------|---------|---------|
| Beijing | bj | `https://cmq-topic-bj.api.qcloud.com`|`http://cmq-topic-bj.api.tencentyun.com` |
| Shanghai | sh | `https://cmq-topic-sh.api.qcloud.com`|`http://cmq-topic-sh.api.tencentyun.com` |
| Guangzhou | gz | `cmq-topic-gz.api.qcloud.com` | `cmq-topic-gz.api.tencentyun.com` |
| Hong Kong | hk | `https://cmq-topic-hk.api.qcloud.com`|`http://cmq-topic-hk.api.tencentyun.com` |
| North America | ca | `https://cmq-topic-ca.api.qcloud.com`|`http://cmq-topic-ca.api.tencentyun.com` |
| Chengdu  |cd | `https://cmq-topic-cd.api.qcloud.com`|`http://cmq-topic-cd.api.tencentyun.com` |
| West US | usw | `https://cmq-topic-usw.api.qcloud.com`|`http://cmq-topic-usw.api.tencentyun.com` |
| East US | use | `https://cmq-topic-use.api.qcloud.com`|`http://cmq-topic-use.api.tencentyun.com` |
| Thailand | th | `https://cmq-topic-th.api.qcloud.com`|`http://cmq-topic-th.api.tencentyun.com` |
| India | in | `https://cmq-topic-in.api.qcloud.com`|`http://cmq-topic-in.api.tencentyun.com` |
| Singapore | sg | `https://cmq-topic-sg.api.qcloud.com`|`http://cmq-topic-sg.api.tencentyun.com` |

