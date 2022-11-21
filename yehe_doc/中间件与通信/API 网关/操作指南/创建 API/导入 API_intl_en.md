## Overview
This document describes how to create an API by importing an OpenAPI file in the API Gateway console.

## Prerequisites
- You have [created a service](https://intl.cloud.tencent.com/document/product/628/11787).
- You have an OpenAPI 3.0.0 API description file in YAML or JSON format.

## Directions
1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway) and click **Service** on the left sidebar.
2. In the service list, click the name of the target service.
3. In the service details, click the **Manage API** tab to view the API list of the service.
4. Click **Import API** above the API list to enter the API importing page.
5. Select the **Text format** (YAML or JSON), click **Upload File**, and select API description files, or directly enter the API descriptions in the code editor.
6. Click **Save**, and API Gateway will create APIs based on the descriptions and then return a list of successfully created APIs.
![](https://main.qcloudimg.com/raw/8df8dba737b5479e6678f45fdf616d5d.png)

## Notes

- OpenAPI 3.0.0 API description files in YAML or JSON format are supported.
- You can import up to ten APIs at a time.
- The uploaded API description files must be suffixed with ".yml" or ".json", and each file can be up to 100 KB in size. The uploaded description files will overwrite the content in the code editor.
- An API created successfully will not be published automatically and needs to be published manually to take effect.
- To import an API from an OpenAPI 3.0.0 description file, you need to manually add the `servers` field to define the backend address to be accessed by the API, for example:
  <dx-codeblock>
  ::: YAML
  servers:
  - url: 'http://localhost:8080'
    description: Generated server url
    :::
    </dx-codeblock>



>?
>- For more information on the mapping between OpenAPI specifications and API Gateway, see [Defining APIs](https://intl.cloud.tencent.com/document/product/628/37874).
>- For detailed directions, see [Importing APIs](https://intl.cloud.tencent.com/document/product/628/37873).
