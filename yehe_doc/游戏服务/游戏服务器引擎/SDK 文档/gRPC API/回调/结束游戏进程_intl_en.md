
## API Name
OnProcessTerminate
<span id="OnProcessTerminate"></span>

## API Description

This API is used for GSE to tell the game process to end itself during reduction or if health check keeps failing. After the game process receives the request, it needs to end the `GameServerSession` which it sustains on [OnStartGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37423) and call the two GSE APIs [TerminateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37423) and [ProcessEnding](https://intl.cloud.tencent.com/document/product/1055/37434) to tell GSE to end the game server session and the process.

## Request Message

```
// End the game process
message ProcessTerminateRequest {
    int64 terminationTime = 1;
}
```

## Response Message

```
message GseResponse
```

## Field Description

##### ProcessTerminateRequest

| Field Name | Type | Description |
| --------------- | ----- | ------------------------------------------------------------ |
| terminationTime | int64 | Time (timestamp) after which GSE will end the process<li>If the server fleet is under full protection, the time will be ignored<li>If the server fleet is under time-period protection, the time will be the protection period<li>If the server fleet is under no protection, the time will be 5 minutes by default |

## Sample

```
func (s *rpcService) OnProcessTerminates(ctx context.Context, req *grpcsdk.ProcessTerminateRequest) (*grpcsdk.GseResponse, error) {
   s.TerminationTime = req.TerminationTime  
   conn, _ := grpc.DialContext(context.Background(), LOCAL_ADDRESS, grpc.WithInsecure())
   defer conn.Close()
   cli := grpcsdk.NewGseGrpcSdkServiceClient(conn)

   request := &grpcsdk.ProcessEndingRequest{  // Inform GSE that the process is being ended
   }

   return cli.ProcessEnding(getContext(), request)
}
```
