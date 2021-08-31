## Overview

You can use the API document feature to generate exquisite API documents for APIs hosted in API Gateway and provide them to third-party callers of your APIs.
>?The API document feature is completely free of charge with technical support provided by CODING DevOps. Click [here](https://coding.net/) to learn more about the capabilities of CODING.

## Prerequisites

You have created a service and an API in API Gateway (as instructed in [Creating Services](https://intl.cloud.tencent.com/document/product/628/11787) and [API Creation Overview](https://intl.cloud.tencent.com/document/product/628/11795)) and published the service to any environment (as instructed in [Service Release and Deactivation](https://intl.cloud.tencent.com/document/product/628/11809)).

## Directions
### Creating document

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1) and click **Tool** > **API Document** on the left sidebar.

2. On the **API Document** page, click **Create Now**, enter the document name in the pop-up window, select the environment, service, and API, and click **Submit**.

3. Wait patiently for the API document creation to complete.

### Viewing document details



The parameters are described as follows:

| Parameter | Description |
| ---- | ---- |
| API document address | The access address of the current API document. |  
| API document password | The password of the current API document. API documents are encrypted by default and can be viewed only with the correct password. |  
| Shared link | You can copy the link and share it with a third party. |  
| Update time | Last time when the API document was updated. |  
| Service | The service of the API for which the document is generated. |  
| Environment | The environment where the service is published, which can be used to generate the API call address. |  
| API | The API contained in the current API document. |  

### Accessing document

1. Copy the API document address and paste it in a browser to open the document login page.

2. Enter the API document password on the document login page to view the content of the document.


### Updating document

After editing the API for which an API document is generated, the document will not be updated synchronously. Using the "document update" feature can ensure that the API document is consistent with the API information. The steps are as follows:
1. Click **Update** in the top-right corner of the document details page.
2. Click **Confirm** in the pop-up window and wait for the document construction to complete.


### Resetting password

After you reset the API document password, a new password will be generated. Users can only use the new password to access the document, while the old password will not work. The steps are as follows:
1. Click **Reset** after the API document password.
2. Click **Confirm** in the pop-up window to generate a new API document password.


### Deleting document

1. Click **Delete** in the top-right corner of the document details page.
2. Click **Confirm** in the pop-up window to delete the API document.
