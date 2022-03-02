This document describes how to store Maven artifacts in CODING-AR, including how to create a repository and push and pull artifacts.

## Open CODING-AR

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click **Use Now** to go to CODING page.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the project.
3. In the menu on the left, click **Artifact Management**.

## Create an Artifact Repository

Click **Create Repository**.

-   Select Maven as the repository type.
-   Enter a repository name.
-   Enter a repository description (optional).
-   Configure the permissions of different roles on the current repository. By default, all project members have the **Pull** and **Push** permissions. 
-   Click **Create**.

![](https://qcloudimg.tencent-cloud.cn/raw/19264a1daba278f8f4d046b9fd9fe8d2.png)

## Configure Authentication Information

Authentication information must be configured before you can pull artifacts from or push artifacts to CODING-AR.

Configure authentication information in either of the following ways:
-   Configure the access token in settings.xml.
-   Configure your CODING account and password in settings.xml.

We recommend you use an **access token** to generate the authentication configuration.

>? For details about the Maven settings.xml, refer to [FAQs](https://intl.cloud.tencent.com/document/product/1136/44816).

### Method 1: generate configuration from access token

1.  On the guide page, click **Generate configuration from access token** and enter the account login password in the pop-up window.
![](https://qcloudimg.tencent-cloud.cn/raw/51b8a1f3490e9414b8926c6beaff7f0f.png)
2.  Copy the configuration generated and add it to settings.xml.
![](https://qcloudimg.tencent-cloud.cn/raw/bb8f1f5c08a3247165a4eb05017d1d37.png)

### Method 2: configure account password manually

On the guide page, copy the following configuration, replace **PASSWORD** with your login password, and then add the configuration to settings.xml.
![](https://qcloudimg.tencent-cloud.cn/raw/b0d8cf4c71c876f84ac23a5edf146c99.png)

## Compile and Upload a Maven Artifact

This section describes how to push a demo Maven package to the repository created above.
![](https://main.qcloudimg.com/raw/0b1e6f151fd89969a79122ff2164a0b9.png)
1.  On the guide page, copy the following configuration to pom.xml.
![](https://qcloudimg.tencent-cloud.cn/raw/94f04bf477a9a50f6ad9ddc58ea37495.png)
Generally, groupId, artifactId, and version configurations already exist for a Maven project. You only need to add `distributionManagement` to it.
![](https://qcloudimg.tencent-cloud.cn/raw/7a55b4f775c46be802548299371c61ac.png)
2.  Run the mvn deploy command.
<dx-codeblock>
:::  java
mvn deploy
:::
</dx-codeblock>
If settings.xml is not found, add `-s` to the end of the command and add the path of the settings file.
<dx-codeblock>
:::  java
 mvn deploy -s "/Users/somebody/software/apache-maven-3.6.2/conf/settings.xml"
:::
</dx-codeblock>
3.  If a build success message is displayed, refresh the repository page to view the latest artifacts.


## Upload a Maven Package Without Source Code

If a third-party Maven package is not officially released to a repository and only a JAR package is provided without source code, you can upload the JAR package to the repository by running the following command:
<dx-codeblock>
:::  java
mvn deploy:deploy-file -Durl=file://C:\m2-repo \
                       -DrepositoryId=some.id \
                       -Dfile=your-artifact-1.0.jar \
                       [-DpomFile=your-pom.xml] \
                       [-DgroupId=org.some.group] \
                       [-DartifactId=your-artifact] \
                       [-Dversion=1.0] \
                       [-Dpackaging=jar] \
                       [-Dclassifier=test] \
                       [-DgeneratePom=true] \
                       [-DgeneratePom.description="My Project Description"] \
                       [-DrepositoryLayout=legacy]
:::
</dx-codeblock>

If `pom.xml` is provided by the third party, you can obtain group, artifact, and version information. For example, use the following command for the **WeChat Cloud Pay Java SDK**:
<dx-codeblock>
:::  ini
mvn deploy:deploy-file --settings ./settings.xml -Durl=https://coding-public-maven.pkg.coding.net/repository/tencent-cloud-pay-sdk-java/tencent/ \
                       -DrepositoryId=coding-public-tencent-cloud-pay-sdk-java-tencent \
                       -Dfile=../cloudpay.jar \
                       -DpomFile=pom.xml
:::
</dx-codeblock>



The following illustrates the JAR package upload page.


## Pull a Maven Artifact

1.  On the guide page, copy the configuration to settings.xml. For example, the configuration for the **WeChat Cloud Pay Java SDK** is as follows:
<dx-codeblock>
:::  xml BRACKET-FILTER
<settings>
    <!--   omitted xml -->
    <profiles>
        <profile>
            <id>Repository Proxy</id>
            <activation>
                <activeByDefault>true</activeByDefault>
            </activation>
            <repositories>
                <repository>
                    <id>coding-public-tencent-cloud-pay-sdk-java-tencent</id>
                    <name>tencent</name>
                    <url>https://coding-public-maven.pkg.coding.net/repository/tencent-cloud-pay-sdk-java/tencent/</url>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                    <snapshots>
                        <enabled>true</enabled>
                    </snapshots>
                </repository>
            </repositories>
        </profile>
    </profiles>
</settings>
:::
</dx-codeblock>
2.  Configure the dependencies in the `pom.xml` file of your Java project. For example, for the **WeChat Cloud Pay Java SDK**, the configuration is as follows:
<dx-codeblock>
:::  xml BRACKET-FILTER
<project>
    <dependencies>
        <dependency>
            <groupId>com.tencent</groupId>
            <artifactId>cloudpay</artifactId>
            <version>1.6</version>
        </dependency>
    </dependencies>
</project>
:::
</dx-codeblock>
3.  Compile the project.
<dx-codeblock>
:::  java
mvn install -s ./settings.xml
:::
</dx-codeblock>

You can view the package is being pulled during the execution. Alternatively, view the pulled package in the local maven cache after the execution is completed.
![](https://main.qcloudimg.com/raw/9cc69e91c1d43c9ff5b2afaa859441b6.png)
