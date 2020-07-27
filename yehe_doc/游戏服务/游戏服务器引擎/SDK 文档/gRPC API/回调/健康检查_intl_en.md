<span id="OnHealthCheck"></span>
## API Name

 OnHealthCheck

## API Description
This API is used for GSE to get the health status of the current game process every minute, and for the current game process to return its health status.

## Request Message

```
message HealthCheckRequest {
}
```

## Response Message

```
message HealthCheckResponse {
    bool healthStatus = 1;
}
```

## Field Description

**HealthCheckResponse**

| Field Name | Type | Description |
| ------------ | ---- | --------------------------------- |
| healthStatus | bool | `true` will be returned if the process is healthy; otherwise, `false` will be returned |


## Sample

```
func (s *rpcService) OnHealthCheck(ctx context.Context, req *grpcsdk.HealthCheckRequest) (*grpcsdk.HealthCheckResponse, error) {
	resp := &grpcsdk.HealthCheckResponse{
		HealthStatus: s.healthStatus,  // Identify the health status of the current process
	}

	return resp, nil
}
```

