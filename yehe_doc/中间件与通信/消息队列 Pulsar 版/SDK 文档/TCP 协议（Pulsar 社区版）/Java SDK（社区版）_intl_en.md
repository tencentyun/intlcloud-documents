## Overview
TDMQ for Pulsar already supports Apache Pulsar SDK for Java. This document describes how to access the SDK.

## Directions
The steps to access the Pulsar SDK for Java are as follows:
1. Add Maven dependencies as instructed in [Pulsar Java client](http://pulsar.apache.org/docs/en/client-libraries-java/).
<dx-codeblock>
:::  xml
``` xml
<!-- in your <properties> block -->
<pulsar.version>2.7.1</pulsar.version>

<!-- in your <dependencies> block -->
<dependency>
	<groupId>org.apache.pulsar</groupId>
	<artifactId>pulsar-client</artifactId>
	<version>${pulsar.version}</version>
</dependency>
```
:::
</dx-codeblock>
2. Run `mvn clean package` in the directory where `pom.xml` is located to download the Apache Pulsar SDK for Java.
3. Go to the **[Role Management](https://console.cloud.tencent.com/tdmq/role)** page in the TDMQ for Pulsar console to copy the token.
4. Add the copied token to the code that creates the client (and add the `listenerName` parameter if the cluster version is 2.6.1).
>?You can click the following tabs to view the access samples for different cluster versions.
<dx-tabs>
::: Access\ssample\sfor\scluster\son\sv2.7.1\sor\sabove
<dx-codeblock>
:::  java
PulsarClient client = PulsarClient.builder()
		.serviceUrl("http://***")// Replace with the access point address copied in the console
		.authentication(AuthenticationFactory.token("eyJh****"))
		.build();
:::
</dx-codeblock>
:::
::: Access\ssample\sfor\scluster\son\sv2.6.1
<dx-codeblock>
:::  java
PulsarClient client = PulsarClient.builder()
		.serviceUrl("pulsar://*.*.*.*:6000/")// Access address, which can be copied from the access point list in the access point list in **Cluster Management**
		.listenerName("custom:********/vpc-******/subnet-********")// custom:+ route ID, which can be copied from the access point list in **Cluster Management**
		.authentication(AuthenticationFactory.token("eyJh****"))
		.build();
:::
</dx-codeblock>
:::
</dx-tabs>

For how to use various features of the Apache Pulsar SDK for Java, see [Pulsar Java client](http://pulsar.apache.org/docs/en/client-libraries-java/).

