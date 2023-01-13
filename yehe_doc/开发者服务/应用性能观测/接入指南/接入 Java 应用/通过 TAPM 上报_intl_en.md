This document describes how to automatically install the proprietary probe in the following two ways:

- [Installing by modifying the configuration file](#conf)
- [Installing by adding JVM parameters without modifying the configuration file](#addjvm)

## Prerequisites

- Before installing the probe, make sure that your local browser and all the servers have the same time zone and time; otherwise, the data accuracy may be affected, such as incorrect topology.
- Download the [SDK](https://apm-agent-java-1251763868.cos.ap-guangzhou.myqcloud.com/tapm-agent-java-3.6.4.1.zip).

## Directions

### Installing by modifying the configuration file[](id:conf)


<dx-tabs>
::: Linux/Mac

1. Run the following command to decompress the Agent installation package to the root directory of your application server. Below is a sample:
   <dx-codeblock>
   :::  plaintext
   unzip tapm-agent-java-x.x.x.zip -d /path/to/appserver/
   :::
   </dx-codeblock><dx-alert infotype="explain" title="">
   `/path/to/appserver` is a sample path. Replace it with the correct directory based on your environment.
   For example, if the root directory of the application server is `/path/to/tomcat`, then the directory where `tapm` is located after decompression should be `/path/to/tomcat`.
   </dx-alert>
2. Modify the `tapm.properties` file in the extracted `tapm` directory.
   The configuration items `license_key`, `app_name`, and `collector.addresses` in the file should be modified; otherwise, the probe cannot start or collect data. Other configuration items can be set as needed.
   - **license_key**: Enter the token obtained when accessing the application in the [APM console](https://console.cloud.tencent.com/apm), which is associated with your APM account. The data collected by the probe will be uploaded to the account bound to the `license_key`.
   - **app_name**: Enter a custom application name, which can be the business name of the application preferably.
   - **collector.addresses**: Enter the endpoint obtained when accessing the application in the [APM console](https://console.cloud.tencent.com/apm), such as `tapm.ap-guangzhou.api.tencentyun.com:80`.
3. Run the following command in the `tapm` directory to automatically install the probe.

```plaintext
cd /path/to/appserver/tapm
java -jar tapm-agent-java.jar install

```

4. Start or restart the application server.
5. Log in to the APM console to view the performance data.
   Five minutes after the restart, when your Java application service receives an HTTP request, the performance data will be sent to APM.

:::
::: Windows

1. Open `tapm-agent-java-x.x.x.zip`.
2. Copy the `tapm` directory to the root directory of your application server.
    <dx-alert infotype="explain" title="">
    For example, if the root directory of the application server is `/path/to/tomcat`, then the directory where `tapm` is located after decompression should be `/path/to/tomcat`.
    </dx-alert>
3. Modify the `tapm.properties` file in the extracted `tapm` directory on the server.
    The configuration items `license_key`, `app_name`, and `collector.addresses` in the file should be modified as follows; otherwise, the probe cannot start or collect data. Other configuration items can be set as needed.
    - **license_key**: Enter the token obtained when accessing the application in the [APM console](https://console.cloud.tencent.com/apm), which is associated with your APM account. The data collected by the probe will be uploaded to the account bound to the `license_key`.
    - **app_name**: Enter a custom application name, which can be the business name of the application preferably.
    - **collector.addresses**: Enter the endpoint obtained when accessing the application in the [APM console](https://console.cloud.tencent.com/apm), such as `tapm.ap-guangzhou.api.tencentyun.com:80`.
4. Run the following command in the command line window by pressing the Windows logo key + **R** and entering **cmd**.
    <dx-codeblock>
    :::  plaintext
    cd tapm
    java -jar tapm-agent-java.jar install

:::
</dx-codeblock>

5. Start or restart the application server.
6. Log in to the APM console to view the performance data.
7. Five minutes after the restart, when your Java application service receives an HTTP request, the performance data will be sent to APM.
   :::
   </dx-tabs>

>?If there is no application performance data received within a few minutes, check the following:
>
>- Follow the above steps to check whether the installation, directory, and startup script are correct.
>- Check whether `license_key` in `tapm.properties` is the same as the token in the APM console.



### Installing by adding JVM parameters without modifying the configuration file[](id:addjvm)

If your application is deployed as a `Jar`, you can install the probe in the following way:

1. Decompress `tapm-agent-java-x.x.x.zip`.
2. Run the following command in the command line window by pressing the Windows logo key + R and entering "cmd".


**Use case:**

```
java -javaagent:/path/to/appserver/tapm/tapm-java-agent.jar  -Dtapm.app_name={APP_NAME} -Dtapm.collector.addresses={COLLECTOR_ADDRESSES} -Dtapm.license_key={LICENSE_KEY} -jar application.jar
```

>?Here, `application.jar` is the application to be monitored.

Run the above statement to start the probe.

To configure JAVA_OPTS, add the following three parameters after `-javaagent` and separate them by space:

```
	-Dtapm.app_name=${APP_NAME}
	-Dtapm.license_key=${LICENSE_KEY}
	-Dtapm.collector.addresses=${COLLECTOR_ADDRESSES}
```

The parameters are as detailed below:

- **-Dtapm.app_name**: Enter a custom application name, which can be the business name of the application preferably.
- **-Dtapm.license_key**: Enter the token obtained when accessing the application in the [APM console](https://console.cloud.tencent.com/apm), which is associated with your APM account. The data collected by the probe will be uploaded to the account bound to the `license_key`.
- **-Dtapm.collector.addresses**: Enter the endpoint obtained when accessing the application in the [APM console](https://console.cloud.tencent.com/apm), such as `tapm.ap-guangzhou.api.tencentyun.com:80`. Agent collector refers to the address and port number of the server. In the high-availability deployment mode, be sure to configure all the agent collector server addresses and port numbers in the same data center and separate them by comma.


The above parameters are optional. If they are configured at startup, the corresponding parameters in the configuration file `tapm.properties` will be replaced by them; if they are not configured, the system will automatically obtain the corresponding parameters from the configuration file.

### View monitoring data
Log in to the [APM console](https://console.cloud.tencent.com/apm) to view the performance data.
