## Overview
This document describes how to view monitoring charts by environment, API, and key, respectively, in the API Gateway console.


## Directions
### Viewing monitoring charts by environment
1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1) and click **Service** in the left sidebar to access the service list page.
2. In the service list, click a service name to access the service details page.
3. At the top of the service details page, click the **Monitoring** tab to access the page for viewing monitoring charts.
4. Select an environment from the **Environment** drop-down list box and select **All** from the **API** drop-down list box. Then you can view the statistical monitoring information of all APIs in the corresponding environment, including the number of calls, traffic, response durations, and errors.
![](https://main.qcloudimg.com/raw/8ff65654c33da5b1c7cfd1e61f2a7fc8.png)

### Viewing monitoring charts by API
1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1) and click **Service** in the left sidebar to access the service list page.
2. In the service list, click a service name to access the service details page.
3. At the top of the service details page, click the **Monitoring** tab to access the page for viewing monitoring charts.
4. Select an environment from the **Environment** drop-down list box and select an API from the **API** drop-down list box. Then you can view the statistical monitoring information of the API in the environment, including the number of calls, traffic, response durations, and errors.


### Viewing monitoring charts by key
#### Prerequisites
A key pair authentication API has been configured by referring to [Key Pair Authentication](https://intl.cloud.tencent.com/document/product/628/11819), and the API or the service where the API resides has been bound to a usage plan.

#### Directions
1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1) and click **Service** in the left sidebar to access the service list page.
2. In the service list, click a service name to access the service details page.
3. At the top of the service details page, click the **Manage Environment** tab to access the environment management page.
4. On the environment management page, select an environment and click **Enable Key Monitoring**.
5. At the top of the service details page, click the **Monitoring** tab to access the page for viewing monitoring charts.
6. Select the environment for which key monitoring is enabled, select the key pair authentication API, and select a key pair. Then you can view the key monitoring information of the API in the environment to obtain the API call information.
