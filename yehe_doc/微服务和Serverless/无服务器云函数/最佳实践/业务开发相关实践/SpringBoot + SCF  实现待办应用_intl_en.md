
## Overview

 [Spring Boot](https://spring.io/projects/spring-boot) is a framework provided by the Pivotal team to simplify the initial build and development of new Spring applications. It uses specific configuration methods, so you don't need to define template-based configuration items.

This document describes how to use Spring Boot through SCF to build a todo application. SCF provides [event-triggered functions](https://intl.cloud.tencent.com/document/product/583/9210) and [HTTP-triggered functions](https://intl.cloud.tencent.com/document/product/583/40688) (recommended in Spring Boot scenarios).

## Prerequisites

You have prepared the development environment and tools as instructed in [Notes on Java](https://intl.cloud.tencent.com/document/product/583/12214).




## Directions

### Using HTTP-triggered function

SCF provides template functions. You can use an HTTP-triggered function as follows to quickly create a todo application and add, delete, modify, and query todos.

>! This template is for demonstration only. Todo data is actually stored in the instance cache instead of being persistently stored.

#### Creating function[](id:createwebfunc)

1. Log in to the [Serverless console](https://console.cloud.tencent.com/scf).
2. Click **Create** on the **Function Service** page.
3. On the **Create** page, select **Template** and search for `springboot` and `webfunc`. In the search results, select **SpringBootToDoApplication** and click **Next** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/8bc02a327bd4831a11689be32164543e.png)
4. Keep the default configuration and click **Complete** to complete the function creation.


#### Testing function

On the **Function Code** tab, follow the steps below to initiate a simulated request based on the test template. In this way, you can try out the CRUD features of the todo application.

- Query the todo list:
 Select GET as the request method, enter `/todos` for `path`, click **Test**, and you will see the current todos in the response body as shown below:
 ![](https://qcloudimg.tencent-cloud.cn/raw/a194239f8b9361e0b2723039be84965b.png)

- Add a todo:
 Select POST as the request method, enter `/todos` for `path` and `{"key":"3","content":"Third todo","done": false}` for `body`, and click **Test** to add a todo as shown below:
 ![](https://qcloudimg.tencent-cloud.cn/raw/82e24fe9bbdb99cd416ffa0d182da797.png)

- Delete a todo:
 Select DELETE as the request method, enter `/todos/2` for `path` (to delete the todo whose `key` is 2 for example), and click **Test** as shown below:
  ![](https://qcloudimg.tencent-cloud.cn/raw/a674c4c3ebc6a36338488abd40c341de.png)

- Modify a todo:
 Select PUT as the request method, enter `/todos/3` for `path` (to mark the todo whose `key` is 3 as completed for example), enter `{"key":"3","content":"Third todo","done": true}` for `body`, and click **Test** as shown below:
 ![](https://qcloudimg.tencent-cloud.cn/raw/1b0bb7936edd341d94dcf4b70250349f.png)



#### Sample code

In the [Creating function](#createwebfunc) step, you can also modify the function template based on your business needs. On the **Select Template** page, click **Learn More** in the top-right corner of the template card. On the pop-up page, click **Download Template Function** to get the template function source code.

You can migrate a native Spring Boot project to an HTTP-triggered function as follows:

-  Make sure that the Spring listening port is 9000 (specified listening port of the SCF HTTP-triggered function).
 ![](https://qcloudimg.tencent-cloud.cn/raw/d47575ec0139f5eb6f4293e87fd93a4a.png )

- Compile the JAR package.
 Download the code and run the following compilation command in the `Webfunc-Java8-SpringBoot` directory:
  ```shell
  gradle build
  ```
 After the compilation, you can get the JAR package in the `build/libs` directory. Select the JAR package whose suffix is `-all`.

- Prepare the executable file `scf_bootstrap` to start the web server. Below is the sample file content:
  ``` shell
  #!/bin/bash
  /var/lang/java8/bin/java -Dserver.port=9000 -jar scf-springboot-java8-0.0.2-SNAPSHOT-all.jar
  ```
>! Run `chmod 755 scf_bootstrap` in the directory of the `scf_bootstrap` file to ensure that the file has the execution permission.

- Package the `scf_bootstrap` file and the generated JAR package into a ZIP package and deploy it to SCF as follows:
    1. Log in to the [Serverless console](https://console.cloud.tencent.com/scf).
    2. Click **Create** on the **Function Service** page.
    3. On the **Create** page, select **Create from scratch** and configure the following items:
          **Function Type**: HTTP-triggered function.
          **Runtime Environment**: Java 8.
          **Submitting Method**: Local ZIP file.
          **Function Code**: Click to upload the ZIP package.
    4. Keep the default values for other configuration items and click **Complete** to complete the function creation as shown below:
  ![](https://qcloudimg.tencent-cloud.cn/raw/f8bd35f0192934f8003dd9838f09e664.png)



### Using event-triggered function



SCF provides template functions. You can use an event-triggered function as follows to quickly create a todo application and add, delete, modify, and query todos.

>! This template is for demonstration only. Todo data is actually stored in the instance cache instead of being persistently stored.

#### Creating function[](id:createnew)
1. Log in to the [Serverless console](https://console.cloud.tencent.com/scf).
2. Click **Create** on the **Function Service** page.
3. On the **Create** page, select **Template** and search for `springboot`. In the search results, select **SpringBoot** and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/9987e93125cac78d6d528b44155215ec.png)
4. Keep the default configuration and click **Complete** to complete the function creation.

#### Creating trigger

>! If you have created an API Gateway trigger during function creation, simply check whether its configuration is the same as that described below.

1. After creating a function, on the **Trigger Management** tab, click **Create Trigger**.
 ![](https://qcloudimg.tencent-cloud.cn/raw/741a21e45bb8a785c2e77544022846b3.png)
2. Configure the trigger in the pop-up window as shown below, keep the default values for other configuration items, and click **Submit**.
 - Trigger Method: API Gateway trigger
 - Integration Response: Enabled
3. After the creation, you need to adjust the API Gateway trigger parameters. Click **API Name** to enter the API Gateway console for subsequent operations as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/498376cfbcb907e421efafa877dba728.png)
4. In the API Gateway console, find the API used by the function and click **Edit** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/fc7806263bc9b74021e09398a9ba9206.png)
On the frontend configuration page, change the path to `/todos`, click **Complete Now**, and release the service as prompted, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/64475c1f6f9220ace61f6dc8c54ef1aa.png)

#### Testing function

On the **Function Code** tab, follow the steps below to initiate a simulated request based on the test template. In this way, you can try out the CRUD features of the todo application.

- Query the todo list:
 Select GET as the request method, enter `/todos` for `path`, click **Test**, and you will see the current todos in the response body as shown below:
 ![](https://qcloudimg.tencent-cloud.cn/raw/bc4a347a430da76cda9234c719860880.png)

- Add a todo:
 Select POST as the request method, enter `/todos` for `path` and `{"key":"3","content":"Third todo","done": false}` for `body`, and click **Test** to add a todo as shown below:
 ![](https://qcloudimg.tencent-cloud.cn/raw/b69f2d377fee46f11cbeeeda95abef67.png)

- Delete a todo:
 Select DELETE as the request method, enter `/todos/2` for `path` (to delete the todo whose `key` is 2 for example), and click **Test** as shown below:
 ![](https://qcloudimg.tencent-cloud.cn/raw/072371c2e28e0055b145904ea3197ba0.png)

- Modify a todo:
 Select PUT as the request method, enter `/todos/2` for `path` (to mark the todo whose `key` is 2 as completed for example), enter `{"key":"2","content":"Third todo","done": true}` for `body`, and click **Test** as shown below:
 ![](https://qcloudimg.tencent-cloud.cn/raw/14ad1793f370c0b19811ef5f65502baa.png)

#### Sample code
In the [Creating function](#createnew) step, you can also modify the function template based on your business needs. On the **Select Template** page, click **Learn More** in the top-right corner of the template card. On the pop-up page, click **Download Template Function** to get the template function source code.


You can configure as follows:

- Add the `ScfHandler` class, which is used to receive event triggers and forward messages to the Spring service. After receiving the response from the Spring service, the function will return it to the invoker.
  The project structure after the `ScfHandler` class is added is as shown below:
  ```
  .
  ├── src
  |   └── main
  |        |        ├── java
  |        |        |        └── com.tencent.scfspringbootjava8
  |        |        |        |        ├── controller
  |        |        |        |        ├── model
  |        |        |        |        └── repository
  |        |        |        |        |        ├── ScfHandler.java
  |        |        |        |        |        └── ScfSpringbootJava8Application.java
  |        |        └── resources
  ```

- Compile the JAR package
  Download the code and run the following compilation command in the root directory:
  ```shell
  gradle build
  ```
  After the compilation, you can get the JAR package in the `build/libs` directory. Select the JAR package whose suffix is `-all`.

- Deploy the generated JAR package to SCF as follows:
   1. Log in to the [Serverless console](https://console.cloud.tencent.com/scf).
   2. Click **Create** on the **Function Service** page.
   3. On the **Create** page, select **Create from scratch** and configure the following items:
       **Function Type**: Event-triggered function.
       **Runtime Environment**: Java 8.
       **Submitting Method**: Local ZIP file.

		 **Execution**: `com.tencent.scfspringbootjava8.ScfHandler:: mainHandler`.
		 **Function Code**: Click to upload the ZIP package.
	4. Keep the default values for other configuration items and click **Complete** to complete the function creation as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/18882840db917ee900e8ade25daa1d7f.png)



