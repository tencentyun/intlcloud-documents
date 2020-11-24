## Overview
The API Gateway signature tool is a web tool provided by Tencent Cloud API Gateway to generate request signatures for key pair authentication APIs. You can set parameters on the signature tool page in the API Gateway console to generate a request signature.


## Prerequisites
Postman has been downloaded and installed ([download address](https://www.postman.com/downloads/)).

## Directions

### Step 1: enter the basic information for a signature
1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway)
2. In the left sidebar, choose **Tools** -> **Signature Tool** to go to the API Gateway signature tool page.
3. In the **Basic Info** module, click **Obtain**. The system will automatically fill in the start time and end time of the signature validity period.
4. Enter any value as the signature watermark value.
![](https://main.qcloudimg.com/raw/5e6e18dbb642e507b1f22251e7811300.png)

### Step 2: enter an API key pair
In the **Secret Key** module, set the API key pair information using either of the following methods:
- Method 1: click **Select** to select a key pair that has been created under your account.
- Method 2: enter a key pair.

Make sure you enter the correct information. If the information is incorrect, your signature will be invalid.
![](https://main.qcloudimg.com/raw/30ab6f97d0ca79b1987d86125e72e8fc.png)

### Step 3: generate a signature
Click **Generate Signature**. The request signature result will be displayed in the module on the right. The main parameters are as follows:
- **Source**: signature watermark value.
- **X-Date**: HTTP request construction time in GMT format. The difference between **X-Date** and the current time cannot exceed 15 minutes.
- **Authorization**: signing information.

![](https://main.qcloudimg.com/raw/5c69a16414f6a4d04dd447f0f87fd7da.png)

### Step 4: initiate a call in Postman
Open Postman, enter the `Source`, `X-Date`, and `Authorization` parameters in `Headers`, enter the API request address, API request parameters, and other information, and click **Send** to call the key pair authentication API.
![](https://main.qcloudimg.com/raw/9eab8698a99139b7f9fa6d11cf41e39c.png)

## Notes

- Because the server will verify the time, you must initiate a call within the validity period of the signature. Otherwise, the call will fail.
- The signature tool only verifies the validity of the parameters, but does not identify or inform you of the specific incorrect parameters.
- For more information about key pair authentication, see [Key Pair Authentication](https://intl.cloud.tencent.com/document/product/628/11819).
