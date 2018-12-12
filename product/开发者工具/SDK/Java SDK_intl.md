## Overview
Welcome to Tencent Cloud Software Development Kit (SDK) 3.0, a companion tool for the TencentCloud API 3.0 platform. Currently, it supports products such as CVM, VPC and CBS. All cloud services and products will be integrated here for access in the future. The new version of SDK is unified and features the same SDK usage, API call methods, error codes and return packet formats for different languages.
To make it easier for Java developers to debug and access the APIs of Tencent Cloud products, this document describes the Tencent Cloud SDK for Java and provides a simple example of using the SDK for the first time, helping you quickly get the SDK and start calling.

## List of Products Supporting SDK 3.0

<table>
  <tr>
    <td><a href="https://cloud.tencent.com/document/api/213/15689">CVM</a></td>
    <td><a href="https://cloud.tencent.com/document/api/362/15634">CBS</a></td>
    <td><a href="https://cloud.tencent.com/document/api/583/17235">SCF</a></td>
    <td><a href="https://cloud.tencent.com/document/api/236/15830 ">TencentDB for MySQL</a></td>
  </tr>
  <tr>
    <td><a href="https://cloud.tencent.com/document/api/571/18122">DTS</a></td>
	<td></td>
	<td></td>
	<td></td>
  </tr>
</table>


## Dependent Environment
1. Dependent environment: JDK version 7 or higher.
2. Activate the corresponding product in the [Tencent Cloud Console](https://console.cloud.tencent.com/).
3. Get the SecretID, SecretKey and call address (endpoint). The general format of endpoint is *.tencentcloudapi.com. For example, the call address of CVM is cvm.tencentcloudapi.com. For details, see the documentation of the specific product.

## Installation
Obtain the security credentials before installing the SDK for Java. Before using the TencentCloud API for the first time, you need to first apply for security credentials in the Tencent Cloud Console, including SecretID and SecretKey. SecretID is used to identify the API caller, while SecretKey is used to encrypt the signature string and verify it on the server. You must keep the SecretKey private and avoid disclosure.
### Installing via Maven (Recommended)
Installing via Maven is the recommended way to use the SDK for Java. Maven is a dependency management tool for Java that supports the dependencies your project requires and installs them into your project. For more information on Maven, see Maven's official website.
1. Go to [Maven's official website](https://maven.apache.org/) to download the corresponding Maven installation package for your system and install.
2. Add Maven dependencies to your project by adding the following dependencies in Maven's pom.xml:
```xml
<dependency>
        <groupId>com.tencentcloudapi</groupId>
        <!-- Note: Please see the latest version number in the GitHub or Maven repository for the version number here. -->
        <artifactId>tencentcloud-sdk-java</artifactId>
        <version>3.0.8</version>
</dependency>
```
3. For reference methods, see the example.

### Installing via Source Package
Go to the [Github code hosting page](https://github.com/tencentcloud/tencentcloud-sdk-java) or [quick download page](https://tencentcloud-sdk-1253896243.file.myqcloud.com/tencentcloud-sdk-java/tencentcloud-sdk-java.zip) to download the source code package.
2. Decompress the package to an appropriate location for your project.
3. You need to put the jar package under the vendor directory in a path that can be found by Java.
4. For reference methods, see the example.

## Example
Take the API for querying available zones as an example:
```java
import com.tencentcloudapi.common.Credential;
import com.tencentcloudapi.common.exception.TencentCloudSDKException;
// Import the client of the corresponding product module.
import com.tencentcloudapi.cvm.v20170312.CvmClient;
// Import the request response class corresponding to the request API.
import com.tencentcloudapi.cvm.v20170312.models.DescribeZonesRequest;
import com.tencentcloudapi.cvm.v20170312.models.DescribeZonesResponse;

public class DescribeZones
{
    public static void main(String [] args) {
        try{
            // Instantiate an authentication object. The Tencent Cloud account secretId and secretKey need to be passed in as the input parameters.
            Credential cred = new Credential("secretId", "secretKey");

            // Instantiate the client object to request the product (with CVM as an example).
            CvmClient client = new CvmClient(cred, "ap-guangzhou");

            // Instantiate a request object.
            DescribeZonesRequest req = new DescribeZonesRequest();

            // Call the API you want to access through the client object; you need to pass in the request object.
            DescribeZonesResponse resp = client.DescribeZones(req);

            // A string return packet in json format is output.
            System.out.println(DescribeZonesRequest.toJsonString(resp));
        } catch (TencentCloudSDKException e) {
                System.out.println(e.toString());
        }

    }

}
```

## More Examples

You can find more detailed examples in the examples directory of the GitHub repository.

## Older SDK
We recommend that you use the new version of SDK. If you need an older version, add the following dependencies to your Maven's pom.xml:
```xml
<dependency>
<groupId>com.qcloud</groupId>
<artifactId>qcloud-java-sdk</artifactId>
<version>2.0.6</version>
</dependency>
```
