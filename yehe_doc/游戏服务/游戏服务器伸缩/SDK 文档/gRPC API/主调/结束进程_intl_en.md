## API Name
ProcessEnding 
<span id="ProcessEnding"></span>


## API Description

This API is used to notify GSE that the game process is ending.

## Request Structure

```
message ProcessEndingRequest {
}
```

## Response Message

```
message GseResponse
```

## Field Description

N/A

## Sample

```
func (r *rpcClient) ProcessEnding() (*grpcsdk.GseResponse, error) {
   conn, _ := grpc.DialContext(context.Background(), LOCAL_ADDRESS, grpc.WithInsecure())
   defer conn.Close()
   req := &grpcsdk.ProcessEndingRequest{
   }
   client := grpcsdk.NewGseGrpcSdkServiceClient(conn)
   return client.ProcessEnding(g.getContext(), req)
}
```
