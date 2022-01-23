## Overview

To activate the API Gateway service, you need to use resources in other Tencent Cloud services. Therefore, you must authorize API Gateway to access your Tencent Cloud resources.

## Prerequisites

You have [registered a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

>?After you register a Tencent Cloud account, the system will create a root account for you by default, which is used to quickly access Tencent Cloud resources.

## Directions

1. When you log in to the [API Gateway console](https://cloud.tencent.com/login?s_url=https%3A%2F%2Fcloud.tencent.com%2F) with the **root account** for the first time, you need to click **Activate Now** on the console overview page to activate the API Gateway service.
 ![](https://qcloudimg.tencent-cloud.cn/raw/ddedf3008a7d678b15c94c4146baf868.png)

2. Since API Gateway hasn't been granted a service role, it cannot access the resources of other Tencent Cloud services. You need to click **Authorize** to enter the [CAM console](https://console.cloud.tencent.com/cam/overview) for authorization.
	 ![](https://qcloudimg.tencent-cloud.cn/raw/7728e6bc78926a79db5361d33589c5b8.png)

3. Click **Agree** to authorize the API Gateway service to access your resources.
	 ![](https://qcloudimg.tencent-cloud.cn/raw/41d6567188329bf509462a39a71bb71c.png)

>?For more information on how to use API Gateway with a sub-account or collaborator, see [Permission Management](https://intl.cloud.tencent.com/document/product/628/34064).

