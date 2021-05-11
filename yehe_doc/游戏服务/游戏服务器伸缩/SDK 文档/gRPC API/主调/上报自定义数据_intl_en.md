## API Name
ReportCustomData 
<span id="ReportCustomData"></span>


## API Description

This API is used for the game process to inform GSE of custom data.

## Request Message

```
message ReportCustomDataRequest {
    int32 currentCustomCount = 1 ;
    int32 maxCustomCount = 2;
}
```

## Response Message

```
message GseResponse
```

## Field Description

##### ReportCustomDataRequest

| Field Name | Type | Description |
| ------------------ | ----- | ------------ |
| currentCustomCount | int32 | Current custom value |
| maxCustomCount     | int32 | Maximum custom value |

## Sample

```
func (r *rpcClient) ReportCustomData(currentCustomCount, maxCustomCount int32) (*grpcsdk.GseResponse, error) {
   conn, _ := grpc.DialContext(context.Background(), LOCAL_ADDRESS, grpc.WithInsecure())
   defer conn.Close()
   req := &grpcsdk.ReportCustomDataRequest{
      CurrentCustomCount:   currentCustomCount,
      MaxCustomCount:       maxCustomCount,
   }

   client := grpcsdk.NewGseGrpcSdkServiceClient(conn)
   return client.ReportCustomData(getContext(), req)
}
```
