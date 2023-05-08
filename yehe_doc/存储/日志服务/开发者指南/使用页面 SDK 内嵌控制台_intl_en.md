## Overview

CLS allows you to embed an independent search and dashboard page SDK into the console. Compared with the iframe-embedded console, the page SDK-embedded console is more independent, avoids login state conflicts, and supports custom resource permission control (which is not the case for the former, as the permission strictly follows the role). The page SDK-embedded console is recommended if your business is sensitive to permissions and stringent on page interaction.

| Embedment Method      | Application Scenario                                         |
| ------------- | ------------------------------------------------ |
| [Embedded console](https://intl.cloud.tencent.com/document/product/614/36997)    | Login-free implementation, without resource permission control and demanding interactive experience |
| Embedded SDK | Login-free implementation, with resource permission control and demanding interactive experience         |


## Example

A unified Ops and operations portal requires one-stop problem solving and therefore integrates CLS into the specified menu. To ensure a good experience and permission management, the embedded SDK is required.
<img src="https://qcloudimg.tencent-cloud.cn/raw/17480a26edf6cbafbcb9a40543d16e1e.png" style="width: 48%;" />

## Case Analysis

The Ops platform requires embedding the CLS log search page into the visual menu and implementing the display of the target log topic upon a click at a service on the left service list. The Ops platform can control users' log topic permissions by controlling their service permissions.



To implement permission control and page integration for the business, you need to develop the frontend page embedment and backend access-layer forwarding logic as instructed [here](https://github.com/TencentCloud/cls-console-sdk/blob/main/sdk-modules/定制化开发.md).

<img src="https://qcloudimg.tencent-cloud.cn/raw/ebd24648ac6eee89866b2355e352f0d3.png" style="width: 50%;" />

## Directions

### Step 1. Get the page SDK

Download the source code from [cls-console-sdk](https://github.com/TencentCloud/cls-console-sdk) on GitHub.

This project is a demo of an **independent runtime environment** implemented based on the `sdk-modules` folder. You can integrate the CLS console into your page to use the search and analysis page and dashboard capabilities.


### Step 2. Deploy the page SDK

1. Create the `./capi-forward/.env` file in the source code and enter the [key information](https://console.cloud.tencent.com/cam/capi) and environment password.
```
# Environment variables are case-sensitive. `secretId` contains 36 characters and `secretKey` 32 characters.
secretId=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
secretKey=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
# Password authentication is supported after the configuration; otherwise, no authentication will be performed.
demoPassword=123456
```
2. Deploy the project as needed.
<dx-tabs>
::: Containerized deployment
1. Run the following command to build the latest image:
```
docker build . --tag=cls_web
```
2. Run the following command to run the container:
```
docker run --env-file ./capi-forward/.env -p 3001:3001 cls_web
```
:::
::: Node.js deployment
1. Install pnpm as instructed in [Installation](https://pnpm.io/zh/installation).
>? Skip this step if you have installed pnpm.
>
2. Run the following command in the root directory of the project to install dependencies:
```
pnpm recursive install --frozen-lockfile=true
```
>? In case of an installation error, run the `find . -name "node_modules" -type d -exec rm -rf '{}' +` command in the root directory of the project and perform the reinstallation.
>
3. Run the following command in the root directory of the project to complete the project build:
```
npm run build
```
4. Run the following command in the root directory of the project to start the project:
```
npm run serve
```
>! You need to rebuild the project after modifying the code.
>

:::
</dx-tabs>

### Step 3. Use the page SDK

<dx-tabs>
::: Access in a browser
After the project is run, you can open the corresponding page in a browser.
```
# Search and analysis page: Replace the `${Region}` and `${TopicId}` in the following URL with the target region and log topic ID to enable the access. `${Query}` is the search statement and can be left empty.
http://localhost:3001/cls/search?region=${Region}&topic_id=${TopicId}&query=${Query}&time=now-h,now

# Search and analysis page: Replace the `${Region}`, `${logset_name}`, and `${topic_name}` in the following URL with the target region, logset name, and log topic name to enable the access.
http://localhost:3001/cls/search?region=${Region}&topic_name=${TopicName}&logset_name=${LogsetName}

# Dashboard page: Replace the `${dashboardId}` in the following URL with the dashboard ID to enable the access.
http://localhost:3001/cls/dashboard/d?id=${dashboardId}&time=now-7d,now
```
The region parameter is in the format of `ap-shanghai`. For more information on parameter settings on the search page, see Parameter Settings on Search Page.
:::
::: Iframe-embedded use
In the internal business system, directly embed the SDK console page as an iframe and integrate it with other pages through the routing parameter.
```
// A sample for quickly checking the effect. You can adjust it as needed.
function prepareSdkFrame(url) {
   var ifrm = document.createElement("iframe");
   ifrm.setAttribute("src", url);
   ifrm.style.width = "1280px";
   ifrm.style.height = "960px";
   document.body.appendChild(ifrm);
}
const url = 'http://localhost:3001/cls/search?region=${Region}&topic_id=${TopicId}&query=${Query}&time=now-h,now'

prepareSdkFrame(url)
```

:::
</dx-tabs>

