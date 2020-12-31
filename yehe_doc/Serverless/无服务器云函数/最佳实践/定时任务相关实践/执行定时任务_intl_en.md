
## Overview
This document uses an SCF function and Puppeteer to perform scheduled tasks on webpage content such as data collection and storage. You can also perform complicated scheduled web tasks like data crawling, scheduled sign-in, and webpage inspection.


## Directions
### Creating function
1. Log in to the SCF Console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. At the top of the "Function Service" page, select the **Beijing** region and click **Create** to enter the function creating page.
Set the following parameter information and click **Next** as shown below:
 - **Function name**: enter "Timertask".
 - **Runtime environment**: select "Nodejs 8.9".
 - **Creation method**: select **Function Template**.
 - **Fuzzy search**: enter "TimerTask" and search.
Click **Learn More** in the template to view relevant information in the "Template Details" pop-up window, which can be downloaded. 
![](https://main.qcloudimg.com/raw/8e6f2b0518ec40132c2868d025fed01e.png)
3. Keep the default configuration and click **Complete** to complete the function creation. If you need to modify the configuration, please see [Modifying function template](#puppeteer).



### Testing function
1. At the bottom of the function code page, click **Test** to view the execution log of the function.
2. After the test is passed, you can configure the scheduled trigger in the **Trigger Method** tab according to the actual situation and check the related Base64 value.




## Relevant Operations
### Modifying function template<span id="puppeteer"></span>
The current template function references Puppeteer to screencapture the webpage content and convert it to a Base64 value for printout in the function log. You can modify the template according to your own scheduled task needs.
For example, run the following command to get the page title:
```
// Sample page title
const title = await page.title();
console.log(title);
```

Add the following code to set the page click attribute.
```
// Sample page click attribute
await page.click('a');
```

For more information on how to use Puppeteer, please see [here](https://github.com/puppeteer/puppeteer). With this tool, you can access page content at scheduled times and perform task operations on the page, such as data crawling and sign-in.
