
## Overview
You can use a client TencentCloud API to place a game server session, that is, you can implement nearby resource scheduling and cross-region disaster recovery through a game server queue.

## Client API Calling Process
1. First, check whether a game server session has been placed in a process. For detailed directions, please see the API document [DescribeGameServerSessionPlacement](https://intl.cloud.tencent.com/document/product/1055/37137).
  >? The following sample code is based on Java:

 ```
public class DescribeGameServerSessionPlacement
{
        public static void main(String [] args) {
            try{

                Credential cred = new Credential("", "");

                HttpProfile httpProfile = new HttpProfile();
                httpProfile.setEndpoint("gse.tencentcloudapi.com");

                ClientProfile clientProfile = new ClientProfile();
                clientProfile.setHttpProfile(httpProfile);

                GseClient client = new GseClient(cred, "", clientProfile);

                String params = "{}";
                DescribeGameServerSessionPlacementRequest req = DescribeGameServerSessionPlacementRequest.fromJsonString(params, DescribeGameServerSessionPlacementRequest.class);
 
                DescribeGameServerSessionPlacementResponse resp = client.DescribeGameServerSessionPlacement(req);

                System.out.println(DescribeGameServerSessionPlacementRequest.toJsonString(resp));
            } catch (TencentCloudSDKException e) {
                System.out.println(e.toString());
            }
        }
 }
 ```
  
2. Start placing the game server session. For detailed directions, please see the API document [StartGameServerSessionPlacement](https://intl.cloud.tencent.com/document/product/1055/37130).

 ```
public class StartGameServerSessionPlacement
{
        public static void main(String [] args) {
            try{

                Credential cred = new Credential("", "");

                HttpProfile httpProfile = new HttpProfile();
                httpProfile.setEndpoint("gse.tencentcloudapi.com");

                ClientProfile clientProfile = new ClientProfile();
                clientProfile.setHttpProfile(httpProfile);

                GseClient client = new GseClient(cred, "", clientProfile);

                String params = "{}";
                StartGameServerSessionPlacementRequest req = StartGameServerSessionPlacementRequest.fromJsonString(params, StartGameServerSessionPlacementRequest.class);
 
                StartGameServerSessionPlacementResponse resp = client.StartGameServerSessionPlacement(req);

                System.out.println(StartGameServerSessionPlacementRequest.toJsonString(resp));
            } catch (TencentCloudSDKException e) {
                System.out.println(e.toString());
            }
        }
}
```

3. Stop placing the game server session. For detailed directions, please see the API document [StopGameServerSessionPlacement](https://intl.cloud.tencent.com/document/product/1055/37129).

 ```
public class StopGameServerSessionPlacement
{
        public static void main(String [] args) {
            try{

                Credential cred = new Credential("", "");

                HttpProfile httpProfile = new HttpProfile();
                httpProfile.setEndpoint("gse.tencentcloudapi.com");

                ClientProfile clientProfile = new ClientProfile();
                clientProfile.setHttpProfile(httpProfile);

                GseClient client = new GseClient(cred, "", clientProfile);
 
                String params = "{}";
                StopGameServerSessionPlacementRequest req = StopGameServerSessionPlacementRequest.fromJsonString(params, StopGameServerSessionPlacementRequest.class);

                StopGameServerSessionPlacementResponse resp = client.StopGameServerSessionPlacement(req);

                System.out.println(StopGameServerSessionPlacementRequest.toJsonString(resp));
            } catch (TencentCloudSDKException e) {
                System.out.println(e.toString());
            }
        }
}
```
>?You can use [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gse&Version=2019-11-12&Action=DescribeGameServerSessionPlacement&SignVersion=) for online debugging. You can select TencentCloud APIs under "Game Server Engine" > "Service Management APIs" on the left sidebar, and perform operations such as "Code Generation" and "Online Call".
