## Overview
This document describes how to create APIs by importing OpenAPI definitions in the API Gateway console.

## Prerequisites
- You have [created a service](https://intl.cloud.tencent.com/document/product/628/11787).
- An API description file compliant with the OpenAPI Specification 3.0.0 is available, and the text format is YAML or JSON.

## Directions
1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway) and click **Service** in the left sidebar.
2. In the service list, click the name of the target service to view it.
3. On the service information page, click the **Manage API** tab to view the API list of the service.
4. Click **Import API** at the top of the API list to access the API importing page.
5. Select a text format (YAML or JSON). Click **Upload File** and select an API description file to upload, or directly enter the API description information in the code editor.
6. Click **Save**. The API Gateway then creates APIs based on your input and returns a list of successfully created APIs.
![](https://main.qcloudimg.com/raw/8df8dba737b5479e6678f45fdf616d5d.png)

## Notes
- Only APIs whose backend is Mock can be imported currently. You can modify the backend configurations of the APIs after importing them successfully.
- An API description file to be imported must comply with the OpenAPI Specification 3.0.0 and be in the YAML or JSON format.
- A maximum of 10 APIs can be imported at a time.
- When you upload an API description file, ensure that the file name extension is .yaml or .json and that the file size is less than or equal to 100 KB. After being uploaded successfully, the API description file will replace the content in the code editor.
- Successfully created APIs cannot be published automatically. Instead, you must manually publish them so that they can take effect.

>?
>- For the mappings between the OpenAPI Specification and the API Gateway, see [Defining APIs](https://intl.cloud.tencent.com/document/product/628/37874).
>- For complete examples of importing APIs, see [Examples of Importing APIs](https://intl.cloud.tencent.com/document/product/628/37873).
