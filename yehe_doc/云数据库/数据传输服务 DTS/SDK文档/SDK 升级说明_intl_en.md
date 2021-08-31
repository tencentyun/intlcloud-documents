The API 2.0 will not be available for the data subscription SDK of Tencent Cloud Data Transmission Service (DTS). Data subscription SDK 2.8.0 and earlier versions use the API 2.0 for authentication, and thus will be affected when the API 2.0 is deprecated.

Please follow the steps below to upgrade the applications you have consumed through the SDK in time to avoid the impact of API 2.0 deprecation.

## Step 1. Check the SDK version
Check the version of the SDK you downloaded from [Data Subscription SDK](https://intl.cloud.tencent.com/document/product/571/8776) and have used.
Check the SDK version as follows:
 - Check the package name of the SDK you have used, which contains the version number, such as `binlogsdk-2.8.0-jar-with-dependencies.jar`.
 - Check the value of `SDK_VERSION`. If the SDK package has been renamed, run the `unzip` command to decompress the package and check the value of `SDK_VERSION` in the `tencentSubscribe.properties` file.

If the version number of your data subscription SDK is 2.8.0 or smaller, go to [Step 2](#Step2).

<span id="Step2"></span>
## Step 2. Upgrade the SDK
1. Download the latest SDK from [Data Subscription SDK](https://intl.cloud.tencent.com/document/product/571/8776#.E6.95.B0.E6.8D.AE.E8.AE.A2.E9.98.85-sdk-.E4.B8.8B.E8.BD.BD) and replace SDK 2.8.0 and earlier versions with it.
2. After the replacement, refer to the following "Code modification starts" to add a line of code to set `region` for subscription channel.

```java
package com.qcloud.biz;
import com.qcloud.dts.context.NetworkEnv;
import com.qcloud.dts.context.SubscribeContext;
import com.qcloud.dts.message.ClusterMessage;
import com.qcloud.dts.message.DataMessage;
import com.qcloud.dts.subscribe.ClusterListener;
import com.qcloud.dts.subscribe.DefaultSubscribeClient;
import com.qcloud.dts.subscribe.SubscribeClient;
import java.util.List;
public class Main {
    public static void main(String[] args) throws Exception {

        SubscribeContext context=new SubscribeContext();

        context.setSecretId("AKID-522dabxxxxxxxxxxxxxxxxxx");
        context.setSecretKey("AKEY-0ff4cxxxxxxxxxxxxxxxxxxxx");
        /*****************Code modification starts****************/
        // If you do not set the `region` parameter, the API 2.0 will still be used for authentication even after it is deprecated.
        // However, the authentication via API 2.0 will fail then, so the SDK will not work properly.
        // Please set `region` for subscription channel.
        context.setRegion("ap-chongqing");
        /*****************Code modification ends******************/


        //Create a client
        SubscribeClient client=new DefaultSubscribeClient(context);
        //Create a subscription listener
        ClusterListener listener= new ClusterListener() {
            @Override
            public void notify(List<ClusterMessage> messages) throws Exception {
                //Consume subscribed data
                for(ClusterMessage m:messages){
                    for(DataMessage.Record.Field f:m.getRecord().getFieldList()){
                        if(f.getFieldname().equals("id")){
                            System.out.println("seq:"+f.getValue());
                        }
                        DataMessage.Record record  = m.getRecord();
                    }
                    //Consumption acknowledgment
                    m.ackAsConsumed();
                }
            }
            @Override
            public void onException(Exception e){
                System.out.println("listen exception"+e);
            }};
        //Add a listener
        client.addClusterListener(listener);
        //Configure subscription channel requested
        client.askForGUID("dts-channel-r0M8kKsSyRZmSxQt");
        //Launch the client
        client.start();
    }
}
```
