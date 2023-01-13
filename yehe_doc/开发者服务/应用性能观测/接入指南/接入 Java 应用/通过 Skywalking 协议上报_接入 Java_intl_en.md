This document describes how to report the data of a Java application over the SkyWalking protocol.

## Prerequisites[](id:before)

- Download [SkyWalking](https://archive.apache.org/dist/skywalking/8.5.0/) 8.5.0 or later and place the extracted agent folder to a directory accessible to the Java process.
- Plugins are in the `/plugins` directory. Put a new plugin in this directory during the startup phase to enable it, or remove it from this directory to disable it. Log files are output to the `/logs` directory by default.

## Access Steps

### Step 1. Get the endpoint and token
Log in to the [APM console](https://console.cloud.tencent.com/apm), enter the **Application monitoring** > **Application list** page, click **Access application**, and select the Java language and the SkyWalking data collection method.
Then, get the endpoint and token in the step of access method selection.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5rBD100_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A120230112-120043%402x.png)


### Step 2. Download Skywalking
- If you have already used SkyWalking, skip this step.
- Otherwise, download the [latest version](http://skywalking.apache.org/downloads/?spm=a2c4g.11186623.2.12.65355968AbUoDc) as instructed in [Prerequisites](#before).

### Step 3. Configure parameters and names
Open the `agent/config/agent.config` file to configure the endpoint, token, and custom service name.

```
collector.backend_service=<endpoint>
agent.authentication=<Token>
agent.service_name=<reporting service name>
```

>?After modifying `agent.config`, remove the `#` before configuration items; otherwise, the changed information will not take effect.

### Step 4. Specify the plugin path
Select an appropriate method based on the runtime environment of your application to specify the path of the SkyWalking agent.
 - Linux Tomcat 7/Tomcat 8
   Add the following to the first line in `tomcat/bin/catalina.sh`:
	<dx-codeblock>
	:::  sh
	CATALINA_OPTS="$CATALINA_OPTS -javaagent:<skywalking-agent-path>"; export CATALINA_OPTS
	:::
	</dx-codeblock>
	
- JAR file or Spring Boot
  Add the `-javaagent` parameter to the startup command line of the application with the following content:
	<dx-codeblock>
	:::  sh
java -javaagent:<skywalking-agent-path> -jar yourApp.jar
	:::
	</dx-codeblock>

### Step 5. Restart the application
After completing the above deployment steps, restart the application as instructed in [Install javaagent FAQs](https://github.com/apache/skywalking/blob/v8.2.0/docs/en/setup/service-agent/java-agent/README.md#install-javaagent-faqs).

