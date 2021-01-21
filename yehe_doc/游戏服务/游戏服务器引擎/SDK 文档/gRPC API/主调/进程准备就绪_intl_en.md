## API Name
ProcessReady
<span id="ProcessReady"></span>
## API Description

This API is used to notify GSE that a game process is started and ready to sustain a `GameServerSession`. Then, you can call the corresponding Tencent Cloud APIs such as `CreateGameServerSession` to generate a `GameServerSession`. Finally, GSE can call the [OnStartGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37423) API to assign the `GameServerSession` to the process.

## Request Message

```
message ProcessReadyRequest {
    repeated string logPathsToUpload = 1;
    int32 clientPort = 2;
    int32 grpcPort = 3;
}
```

## Response Message

```
message GseResponse 
```

## Field Description

**ProcessReadyRequest**

| Field Name | Type | Description |
| ---------------- | ----------- | ------------------------------------------------------------ |
| logPathsToUpload | String array | Path of the game process logs to be uploaded to Tencent Cloud. Directory paths and file paths are supported. GSE will upload logs in the specified paths to Tencent Cloud for you to download. |
| clientPort       | Int32       | Port to be connected to by the game client                           |
| grpcPort         | Int32       | Port used by GSE to call the service APIs defined by `GameServerGrpcSdkService.proto` in the game process. |

## Sample

```
func (r *rpcClient) ProcessReady(logPath []string, clientPort int32, grpcPort int32) (*grpcsdk.GseResponse, error) {
			conn, _ := grpc.DialContext(context.Background(), LOCAL_ADDRESS, grpc.WithInsecure())
			defer conn.Close()
			req := &grpcsdk.ProcessReadyRequest{
				LogPathsToUpload: logPath, // E.g., Absolute path to logs: `/local/game/logs`; relative path to logs: `./logs`.
				ClientPort:       clientPort,
				GrpcPort:         grpcPort,
			}

			client := grpcsdk.NewGseGrpcSdkServiceClient(conn)
			return client.ProcessReady(getContext(), req)
}
```
