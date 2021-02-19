
## Overview
This document uses SCF, [MTA](https://mta.qq.com/), and WeCom bot to perform tasks such as report content collection and data display.

## Directions
### Creating function
1. Log in to the SCF console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. At the top of the **Function Service** page, select the **Beijing** region and click **Create** to enter the function creating page.
Set the following parameter information and click **Next** as shown below:
 - **Function name**: enter "ReportMTA".
 - **Runtime environment**: select "Php7".
 - **Creation method**: select **Function Template**.
 - **Fuzzy search**: enter "TimerReport" and search.
Click **Learn More** in the template to view relevant information in the **Template Details** pop-up window, which can be downloaded. 
![](https://main.qcloudimg.com/raw/e749130ec4ac72c78ae95e921e5728ea.png)
3. Keep the default configuration and click **Complete** to complete the function creation.

### Testing function
1. At the bottom of the function code page, click **Test** to view the execution log of the function and go to the WeCom group for confirmation.
2. After the test is passed, you can configure the scheduled trigger in the **Trigger Method** tab according to the actual situation. To modify the configuration, please see [Modifying function template](#puppeteer).


## Relevant Operations 
<span id="puppeteer"></span>
### Modifying function template

The current template function only supports pulling MTA site reports. For more information, please see [here](https://mta.qq.com/docs/h5_api.html).
Add the following code to modify the MTA parameters:
```
$app_id ="xxxxxx"; // MTA APPID 
$secret_key = 'xxxxx'; // MTA SECRET KEY
```

Run the following command to access the WeChat bot. For more information, please see [here](https://work.weixin.qq.com/help?person_id=1&doc_id=13376).
```
  CURLOPT_URL => "https://qyapi.weixin.qq.com/cgi-bin/webhook/send?key=xxxxx", // WeCom bot API
```
