## Overview

During the running of an application instance, the process may exit due to an exception, or the instance may run abnormally because the running environment disk is too full, and so on. In such cases, you need to restart the application instance.

In addition, the application instance may be temporarily unable to receive new requests due to database and other access exceptions. In that case, you need to remove the exceptional instance from the load balancer and add the instance to the load balancer when the instance recovers.

For the above two types of OPS requirements, TEM provides two types of health checks to meet the requirements of automatic OPS:

- Liveness check: check whether an application instance is running properly. If not, restart the instance.
- Readiness check: check whether an application instance is ready. If not, stop forwarding traffic to the instance.

**Overall process**

TEM provides the HTTP request method for health checks, and the corresponding HTTP APIs need to be provided by the application itself. Therefore, the overall process of using the health check feature consists of two steps:
<dx-steps>
- [Implement health check HTTP APIs in the application.](#step1)
- [Configure the health check feature when deploying the application on the TEM platform.](#step2)
</dx-steps>


## Directions

### Step 1: implement health check HTTP APIs in the application[](id:step1)

The application needs to implement the health check HTTP APIs based on the development language and framework used. The following are some common examples in the industry:
- [Spring Boot](https://docs.spring.io/spring-boot/docs/current/reference/html/actuator.html)
- [ASP.NET Core](https://docs.microsoft.com/zh-cn/aspnet/core/host-and-deploy/health-checks?view=aspnetcore-5.0)
- [Django](https://django-health-check.readthedocs.io/en/latest/readme.html)
- [Nodejs](https://www.npmjs.com/package/nodejs-health-checker)

The application needs to implement two health check HTTP APIs to handle liveness and readiness checks separately (in this example, the request paths for the liveness and readiness checks are set to `/livez` and `/healthz` respectively).



### Step 2: configure the health check feature when deploying the application on the TEM platform[](id:step2)

If no environment is created, [create an environment](https://intl.cloud.tencent.com/document/product/1094/40358).

Create and deploy an application as follows (a JAR package is used in this example):

1. Select the application deployment region at the top of the **[Application Management](https://console.cloud.tencent.com/tem/service)** page in the TEM console.
2. Click **Create** to access the **New application** page and enter the application information.
![](https://main.qcloudimg.com/raw/dedcc34507c6d79bb7baa2d8d23198b3.png)
3. Click **Submit** and click **OK** in the pop-up window to deploy the application.
4. On the **Deploy Application** page, configure the relevant parameters as needed.
	Set **Request Path** and **Port** to the HTTP API path and port number for health check respectively.
![](https://main.qcloudimg.com/raw/67d66ab61be905810246c1053bd78d45.png)
5. Click **Deploy Application**. The platform automatically manages the application according to the health check configuration.
