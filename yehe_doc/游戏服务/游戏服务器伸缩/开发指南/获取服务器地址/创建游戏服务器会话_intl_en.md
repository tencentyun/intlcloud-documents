
## Overview
- You can use a client TencentCloud API to create a game server session in the following two ways:
  - Create in a server fleet to implement auto scaling and health check.
  - Create through an alias to implement zero downtime update.
- One game server session is placed in one server process, but the client API calling process varies by supporting mode of the game server session.

## Client API Calling Process
### One game server session supports one game
If one game server session supports only one game, you can call a client API in the following steps:
<span id="CreateGameServerSession"></span>
1. Create a game server session through a server fleet or alias. For detailed directions, please see the API document [CreateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37139).
>?The following sample code is based on Java:

  ```
  public class CreateGameServerSession
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
                CreateGameServerSessionRequest req = CreateGameServerSessionRequest.fromJsonString(params, CreateGameServerSessionRequest.class);

                CreateGameServerSessionResponse resp = client.CreateGameServerSession(req);
 
                System.out.println(CreateGameServerSessionRequest.toJsonString(resp));
            } catch (TencentCloudSDKException e) {
                System.out.println(e.toString());
            }
        }
}
```

<span id="JoinGameServerSession"></span>
2. Join the created game server session. For detailed directions, please see the API document [JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37132).

 ```
public class JoinGameServerSession
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
                JoinGameServerSessionRequest req = JoinGameServerSessionRequest.fromJsonString(params, JoinGameServerSessionRequest.class);

                JoinGameServerSessionResponse resp = client.JoinGameServerSession(req);

                System.out.println(JoinGameServerSessionRequest.toJsonString(resp));
            } catch (TencentCloudSDKException e) {
                    System.out.println(e.toString());
            }
        }
    }
```

### One game server session supports multiple games or one service
If one game server session supports multiple games or one service (such as login), you can all a client API in the following steps:
1. Query the game server session list to check whether there is any game server session. For detailed directions, please see the API document [DescribeGameServerSessions](https://intl.cloud.tencent.com/document/product/1055/37136).

 ```
public class DescribeGameServerSessions
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
                DescribeGameServerSessionsRequest req = DescribeGameServerSessionsRequest.fromJsonString(params, DescribeGameServerSessionsRequest.class);

                DescribeGameServerSessionsResponse resp = client.DescribeGameServerSessions(req);

                System.out.println(DescribeGameServerSessionsRequest.toJsonString(resp));
            } catch (TencentCloudSDKException e) {
                System.out.println(e.toString());
            }
        }
    }
```

  You can also search for existing sessions in the game server session list. For detailed directions, please see the API document [SearchGameServerSessions](https://intl.cloud.tencent.com/document/product/1055/37131).

 ```
public class SearchGameServerSessions
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
                SearchGameServerSessionsRequest req = SearchGameServerSessionsRequest.fromJsonString(params, SearchGameServerSessionsRequest.class);

                SearchGameServerSessionsResponse resp = client.SearchGameServerSessions(req);

                System.out.println(SearchGameServerSessionsRequest.toJsonString(resp));
            } catch (TencentCloudSDKException e) {
                System.out.println(e.toString());
            }
        }
}
```

2. If a game server session exists, you can directly join it. For detailed directions, please see the API document [JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37132) or the [sample code](#JoinGameServerSession) in this document.
3. If no game server sessions exist, you need to create one first. For detailed directions, please see the API document [CreateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37139) or the [sample code](#CreateGameServerSession) in this document. Then, join the created session. For detailed directions, please see the API document [JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37132) or the [sample code](#JoinGameServerSession) in this document.

>?You can use [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gse&Version=2019-11-12&Action=CreateGameServerSession&SignVersion=) for online debugging. You can select TencentCloud APIs under "Game Server Engine" > "Service Management APIs" on the left sidebar and perform operations such as "Code Generation" and "Online Call".
