## Supported Environments

- JDK 7 or above.

- Endpoint: tms.tencentcloudapi.com

>! The API supports access from either a nearby region (at `tms.tencentcloudapi.com`) or a specified region (at `tms.ap-guangzhou.tencentcloudapi.com` for Guangzhou, for example). 

## Installing SDK

### Method 1. Install through Maven (recommended)

Maven is a dependency management tool for Java that supports the dependencies your project requires and installs them into your project.

1. Go to [Maven official website](https://maven.apache.org/) to download the corresponding Maven installation package for your system and install it.

2. Add Maven dependencies for your project by adding the following dependencies under the `<dependencies>` tag in Maven's `pom.xml`:

   ```
   <dependency>
        <groupId>com.tencentcloudapi</groupId>
        <artifactId>tencentcloud-sdk-java</artifactId>
        <!-- go to https://search.maven.org/search?q=tencentcloud-sdk-java and get the latest version. -->
        <!-- Query the latest version at https://search.maven.org/search?q=tencentcloud-sdk-java, which is as follows -->
        <version>3.1.322</version>
   </dependency>
   ```

   >!
   >- The version number here is just an example, and you can view the latest version number in the [Maven repository](https://search.maven.org/search?q=tencentcloud-sdk-java).
   >- v4.0.11 shown in the Maven repository was disused but has not been completely deleted due to the Maven index update issue.
   >- The above import method downloads the SDKs of all Tencent Cloud services to your local system. You can replace the `artifactId` with `tencentcloud-sdk-java-cvm/cbs/vpc` to import the SDK of the specific product. The code can be used in the same way, and the major packages are the same. For more information, see the samples.

3. Set the mirror source to speed up the download. To do so, edit the `settings.xml` configuration file of Maven and add the mirror configuration in the `mirrors` section:

   ```
       <mirror>
         <id>tencent</id>
         <name>tencent maven mirror</name>
         <url>https://mirrors.tencent.com/nexus/repository/maven-public/</url>
         <mirrorOf>*</mirrorOf>
       </mirror>
   ```

### Method 2. Install through source package

1. Go to the [GitHub code hosting page](https://github.com/tencentcloud/tencentcloud-sdk-java) to download the source code package.
2. Decompress the source package to an appropriate location in your project.
3. You need to put the jar package under the `vendor` directory in a path that can be found by Java.
4. For importing methods, see [Using SDK](https://intl.cloud.tencent.com/document/product/1121/43766#SDK).

## Using SDK

See the sample code below, which calls the `TextModeration` API. The `region` is configured as `Guangzhou` as an example and should be configured as needed.

```
import com.tencentcloudapi.common.Credential;
import com.tencentcloudapi.common.profile.ClientProfile;
import com.tencentcloudapi.common.profile.HttpProfile;
import com.tencentcloudapi.common.exception.TencentCloudSDKException;
import com.tencentcloudapi.tms.v20201229.TmsClient;
import com.tencentcloudapi.tms.v20201229.models.*;
public class TextModeration {
    public static void main(String[] args) {
        try {
            // Instantiate an authentication object. Pass in `secretId` and `secretKey` of your Tencent Cloud account as the input parameters and keep them confidential 
            // You can get them by visiting https://console.cloud.tencent.com/cam/capi 
            Credential cred = new Credential("SecretId", "SecretKey");
            // (Optional) Instantiate an HTTP option 
            HttpProfile httpProfile = new HttpProfile();
            httpProfile.setEndpoint("tms.tencentcloudapi.com");
            // Instantiate a client option (optional; skip if no special requirements are present) 
            ClientProfile clientProfile = new ClientProfile();
            clientProfile.setHttpProfile(httpProfile);
            // Instantiate the client object of the requested product. `clientProfile` is optional 
            TmsClient client = new TmsClient(cred, "ap-guangzhou", clientProfile);
            // Instantiate a request object. Each API corresponds to a request object 
            TextModerationRequest req = new TextModerationRequest();
            // The returned `resp` is an instance of `TextModerationResponse` which corresponds to the request object 
            TextModerationResponse resp = client.TextModeration(req);
            // A string return packet in JSON format is output 
            System.out.println(TextModerationResponse.toJsonString(resp));
        } catch (TencentCloudSDKException e) {
            System.out.println(e.toString());
        }
    }
}
```



