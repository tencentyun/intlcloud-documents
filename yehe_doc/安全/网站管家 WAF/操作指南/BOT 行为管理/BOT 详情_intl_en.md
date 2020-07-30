## Feature Overview
In bot details page, you can view the access trends in normal requests and bot requests to your domain names, details of bot behaviors in unknown, public, and custom types, and details of bot sessions detected by WAF.
## Instructions
### Viewing overview
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/bot2/record/overview) and select **Bot Behavior Management** > **Bot Details** on the left sidebar to enter the bot details page.
2. In the top-left corner, click the domain name filter box to select or search for the desired domain name.
![](https://main.qcloudimg.com/raw/a0c84369c61a1817d3a76a79ed53dff6.png)
3. Select the bot source distribution by clicking **Global** or **Mainland China** to switch between maps. In the **Global** map, the statistics are accurate to the country/region level, while in the **Mainland China** map, they are accurate to the province level.
![](https://main.qcloudimg.com/raw/3975071a825caee55c3f780d8bd95161.png)
You can view all, unknown, public, or custom bots.
![](https://main.qcloudimg.com/raw/deae845acfd2df71fb11385ad876f7dd.png)
**Statistics item description:**
- **Number of Requests**: the trends in total number of requests and bot requests are displayed.
- **Bot Action**: the quantities and proportions of actions in different types (CAPTCHA verification, redirect, blocking, and monitoring) detected for the domain name are displayed.
- **Bot Type**: the quantities and proportions of bots in different types (unknown, public, and custom) detected for the domain name are displayed.
- **Bot Source Distribution**: the locations (Chinese province or country/region) of source IPs of bots in different types are displayed.

### Type details
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/bot2/record/overview) and select **Bot Behavior Management** > **Bot Details** on the left sidebar to enter the bot details page, where you can view **Unknown Type**, **Custom Type**, and **Public Type** of bots. In the top-left corner, click the domain name filter box to select or search for the desired domain name.
![](https://main.qcloudimg.com/raw/c4a02a53f2ecf19fca7d2b63156e6eca.png)
2. Unknown bots are bot behaviors that WAF detects by tracing the target session and combining of detection capabilities of the session behavior characteristics model and AI testing model.
![](https://main.qcloudimg.com/raw/8f6b4bf8a0e7166ecdd56ca557e35139.png)
**Item description of the unknown bot list:**
- **Access Source IP**: IP of the bot request.
- **Prediction Tag**: suspicious behaviors automatically predicated by the algorithm, which are classified into 12 categories, such as suspicious malicious registration, suspicious regular crawlers, and suspicious unauthorized use of SMS APIs. Filtering is supported.
- **Exceptional Characteristics**: exceptional characteristics detected by the bot engine.
- **Action**: processing action for unknown bots, which is "Monitor" by default.
- **Bot Score**: bot score of the session given by the intelligent bot analysis engine. The higher the score, the more likely the session is initiated by a bot. Sorting is supported.
- **Total Number of Sessions**: total number of bot session requests. Sorting is supported.
- **Session Duration**: duration of the bot session. Sorting is supported.
- **Average Rate**: total number of session requests/session duration in requests/minute. Sorting is supported.
- **Last Detection Time**: time when the bot session request is last detected. Sorting is supported.
- **Operation**: **Blocklist** and **View Details** are supported. Click an unknown bot to view its details, or click **Blocklist** in the "Operation" column on the right to add its IP to the blocklist in the **IP Management** > **[IP Blocklist/Allowlist](https://console.cloud.tencent.com/guanjia/ip/list)** module.
3. Custom bots are bot behaviors detected by WAF based on your custom session policies.
![](https://main.qcloudimg.com/raw/e2626bd53699cc23adfa8a1dfcea1b86.png)
**Item description of the custom bot list:**
- **Access Source IP**: IP of the bot request.
- **Policy Name**: custom or preset policy name set in bot protection configuration.
- **Exceptional Characteristics**: exceptional characteristics detected by the bot engine.
- **Action**: action set in bot protection configuration. Filtering is supported.
- **Bot Score**: bot score of the session given by the intelligent bot analysis engine. The higher the score, the more likely the session is initiated by a bot. Sorting is supported.
- **Total Number of Sessions**: total number of bot session requests. Sorting is supported.
- **Session Duration**: duration of the bot session. Sorting is supported.
- **Average Rate**: total number of session requests/session duration in requests/minute. Sorting is supported.
- **Last Detection Time**: time when the bot session request is last detected. Sorting is supported.
- **Operation**: you can click **View Details** to view the bot details.
4. Public bots are bot behaviors detected by WAF based on Tencent Cloud's bot intelligence library and accumulated public bot data.
![](https://main.qcloudimg.com/raw/219c3327c1af9026d56f3a73fe1b3477.png)
**Item description of the public bot list:**
- **Access Source IP**: IP of the bot request.
- **Bot Category**: WAF provides protection against 12 public categories of bots with over 1,000 subcategories, such as search engine, speed tester, content aggregator, scanner, and website crawler. Filtering is supported.
- **Name**: name of the detected public bot.
- **Exceptional Characteristics**: exceptional characteristics detected by the bot engine.
- **Action**: action set in bot protection configuration. Filtering is supported.
- **Bot Score**: bot score of the session given by the intelligent bot analysis engine. The higher the score, the more likely the session is initiated by a bot. Sorting is supported.
- **Total Number of Sessions**: total number of bot session requests. Sorting is supported.
- **Session Duration**: duration of the bot session. Sorting is supported.
- **Average Rate**: total number of session requests/session duration in requests/minute. Sorting is supported.
- **Last Detection Time**: time when the bot session request is last detected. Sorting is supported.
- **Operation**: you can click **View Details** to view the bot details.
5. You can view **Unknown**, **Custom**, or **Public** bots as needed. Select the desired bot and click **View Details** in the "Operation" column on the right to enter the basic information and access details pages where you can view exceptional characteristics information of the bot.
![](https://main.qcloudimg.com/raw/35dcb4b4b526071be37c0371e5c88cc2.png)
- Click **Basic Info** to view the detailed statistics.
![](https://main.qcloudimg.com/raw/f2d1a270aa310dc7a159e4b4b41b540f.png)
**Basic information item description:**
- **Access Trend**: trend in requests from the current source IP of the bot. Statistics within the last 3 days can be provided.
- **Proportions of Returned Response Codes**: proportions of response codes returned by WAF for the bot session. The first 600 requests of the session are recorded.
- **Proportions of Request Methods**: proportions of request methods used in the bot session. The first 600 requests of the session are recorded.
- **Proportions of HTTP Protocol Versions**: proportions of HTTP protocol versions in the bot session. The first 600 requests of the session are recorded.
- **Basic Session Information**: detected information such as number of sessions, session duration, and index for exceptional time-series behaviors.
- **Basic Bot Information**: detected basic information of bot behavior characteristics, which varies by bot type.
- **Basic IP Information**: detected IP information such as geographical location, latitude and longitude, type, and ISP.
- **UA Information**: detected UA information such as number of UA categories, UA proportion, and proportion of repeated UAs.
- **Other HTTP Header Information**: information on whether `Accept`, `Accept-Language`, `Accept-Encoding`, or `Connectiton` exists.
- **Request Parameter Information**: information such as URL proportion, proportion of repeated URLs, and the most frequently requested URL.
- **Cookie Information**: information such as cookie proportion, number of cookie categories, and most frequent cookie.
- **Referer Information**: information such as referer proportion, number of referer categories, and whether referer is abused.
- **Operation Description**: on the right of the access source IP under the basic information configuration item, click **Blocklist/Allowlist** to add this IP to the **IP Management** > **[IP Blocklist/Allowlist](https://console.cloud.tencent.com/guanjia/ip/list)** module.
![](https://main.qcloudimg.com/raw/8a039ae6f14708c815666a40cf6ec814.png)
>For more information on each field, please see [Bot Protection Configuration Match Condition Description](https://intl.cloud.tencent.com/document/product/627/35642).
- Click **Access Details** to enter the bot session access details page, which provides detailed statistics of the first 600 requests in the bot session.
![](https://main.qcloudimg.com/raw/575ff62dcfa402c451344fd8663a255c.png)
**Access details field description:**
- **Query**: access details can be queried. You can combine the provided conditions to query requests.
- **Request Time**: time when the request is initiated in the bot session.
- **HTTP Protocol Version**: version number of the HTTP protocol used by the request in the bot session.
- **Request Method:** method used by the request in the bot session.
- **UA**: `UA` parameter carried in the HTTP header in the bot session.
- **GET Parameter**: `query` parameter information of the request in the bot session.
- **Status Code**: status code returned by WAF.
