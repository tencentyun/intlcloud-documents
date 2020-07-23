## API Name
ProcessReady
<span id="ProcessReady"></span>
## API Description

This API is used to notify GSE that a launched game process is ready to sustain a `GameServerSession`. Then, GSE can call the [OnStartGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37423) API to assign a `GameServerSession` to the process.

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
| logPathsToUpload | string array | The paths of logs to upload for the game process. GSE will upload logs in the specified paths to Tencent Cloud for game developers to download |
| clientPort       | int32       | Port to be connected to by game client                           |
| grpcPort         | int32       | Port used by the game process to implement the service defined by `GameServerGrpcSdkService.proto`; connected to by GSE |

## Sample

```
func (r *rpcClient) ProcessReady(logPath []string, clientPort int32, grpcPort int32) (*grpcsdk.GseResponse, error) {
	conn, _ := grpc.DialContext(context.Background(), LOCAL_ADDRESS, grpc.WithInsecure())
	defer conn.Close()
	req := &grpcsdk.ProcessReadyRequest{
		LogPathsToUpload: logPath,
		ClientPort:       clientPort,
		GrpcPort:         grpcPort,
	}

	client := grpcsdk.NewGseGrpcSdkServiceClient(conn)
	return client.ProcessReady(getContext(), req)
}
```
