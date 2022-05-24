## Overview
Serverless is a popular architecture in recent years. Through the Serverless function computing platform, you can focus on the core logic and run your code without purchasing and managing servers. In the Serverless mode, using the API Gateway can make the service available to external users, and realize advanced features such as security protection, traffic throttling, log monitoring, releasing in the cloud market, and automatic generation of SDK and documents.

Tencent Cloud API Gateway is highly integrated with Tencent Cloud SCF. This document describes how to build a website quickly by using the API Gateway as the entry to configure dynamic APIs through [SCF](https://intl.cloud.tencent.com/document/product/583) and store static resources through [COS](https://intl.cloud.tencent.com/document/product/436).

With this method, you can use the API Gateway to make the Serverless service available quickly in the cloud.

## Prerequisites

Before building a website, you need to go to the [API Gateway official repository](https://github.com/TencentCloud/apigateway-demo/tree/master/hello-website) to download the website source code, which contains a skeleton HTML file and static resources such as pictures, CSS files and JS files.

The directory structure of the downloaded file is as follows:
```
├── client                                      // Root directory of the project
│   ├── static                                  // Static resource
│   │   ├── background.jpg                      // Underground picture of the website
│   │   ├── favicon.ico                         // Website icon
│   │   ├── index.js                            // Script file
│   │   ├── style.css                           // Style file
│   ├── index.html                              // Website homepage
```

## Directions

### Step 1. Create a COS bucket to store static resources

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5/bucket). Create a bucket based on the following figure. For more information, see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).
![](https://main.qcloudimg.com/raw/88b9a367ee03acace0169ec846e294d1.png)
2. Upload the website source code in the bucket. The directory structure must be consistent with the original file. For more information, see [Uploading Objects](https://intl.cloud.tencent.com/document/product/436/13321).
![](https://main.qcloudimg.com/raw/f86586fffc201da9169ce5f055555d06.png)

### Step 2. Create a SCF

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/list). Create a SCF using the "hello world" template. For more information, see [Create and Update a Function](https://intl.cloud.tencent.com/document/product/583/19806).
![](https://main.qcloudimg.com/raw/70813ce761854292233b92fc70873be3.png)
2. Modify the SCF code and return simple JSON data.
![](https://main.qcloudimg.com/raw/bda30bde9cc024b9b2b6fe2ef5ee3660.png)

The SCF code used is as follows:
```JavaScript
'use strict';
exports.main_handler = async(event, context, callback) => {
	return {
		data: 'hello world' // hello world can be replaced with any content
	}
};
```

### Step 3. Create an API Gateway service

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway). Create an API Gateway service based on the following figure. For more information, see [Creating Services](https://intl.cloud.tencent.com/document/product/628/11787).
![](https://main.qcloudimg.com/raw/dd9c3047e63809163dba36f26d98755f.png)
2. Click the name of the service in the service list.
3. Click **Manage API** to go to the API management page. In the next step, you need to create three APIs on this page, with each API points to the corresponding backend resource.

### Step 4. Configure three APIs

1. Click **Create** to create the first API. It is used to obtain the HTML page of the website. The frontend path is configured as "/". For more information, see [API Creation Overview](https://intl.cloud.tencent.com/document/product/628/11795).
![](https://main.qcloudimg.com/raw/d797a68003a6e01277fd36f2f0cbab28.png)
The "index.html" that points to the COS bucket is configured for the backend.
![](https://main.qcloudimg.com/raw/601fa75d0c7bcc6898cdd711ad2c403b.png)
2. Click **Create** again to create the second API. It is used to obtain static resources. The frontend path is configured as "^~/static".
![](https://main.qcloudimg.com/raw/b3911b2ffd827765118b75c874395046.png)
The "/static" path that points to the COS bucket is configured for the backend.
![](https://main.qcloudimg.com/raw/6ecc5aa906c3379e648999b591b7e5fc.png)
3. Click **Create** again to create the third API. It is used to obtain dynamic data. The frontend path is configured as "/fetchData".
![](https://main.qcloudimg.com/raw/f8d2dc6e0acf2a640a3716b6598d8cfa.png)
Enter the corresponding SCF name in the backend configuration.
![](https://main.qcloudimg.com/raw/eb5bab8b734149e5f54e49dfd8571191.png)

### Step 5. Release the service and access the website
1. On the **Service information** tab of the service details page, click **Release** in the upper-right corner to release the service to the "Release" environment.
![](https://main.qcloudimg.com/raw/d18ae93f6a8e24aab4c59048d3b44d05.png)
2. On the **Service information** tab of the service details page, view the "public network access address". Click the "Copy" icon to copy the address.
![](https://main.qcloudimg.com/raw/5ea3316d9acaed82104cacb9ea2feaca.png)
3. Paste the "public network access address" in the address bar of a browser. Press "Enter" to access the deployed website.
![](https://main.qcloudimg.com/raw/ffffd8d4c16b080003a103473ae14b25.png)
4. Click **Obtain data** to initiate a XHR call. The website will return the pre-defined JSON data string through the SCF.


## Notes
In addition to access the website you build through the default domain name provided by the API Gateway, you can also bind an custom domain name to the service. After binding, you can access the website through the custom domain name. For more information, see [Configuring a Custom Domain Name](https://intl.cloud.tencent.com/document/product/628/11791).

