

## Overview

This document provides an overview of APIs and SDK code samples for Go related to log management.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | Setting log management | Enables logging for the source bucket |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | Querying log management | Queries the logging configuration information of the source bucket |

## Setting Log Management

#### Feature description

This API (PUT Bucket logging) is used to enable logging for the source bucket and store its access logs in a specified destination bucket.

#### Method prototype

```go
func (s *BucketService) PutLogging(ctx context.Context, opt *BucketPutLoggingOptions) (*Response, error)
```

#### Sample request

```go
opt := &cos.BucketPutLoggingOptions{
	LoggingEnabled: &cos.BucketLoggingEnabled{
    	TargetBucket: TargetBucket,
    },  
}   
resp, err := client.Bucket.PutLogging(context.Background(), opt)
```

#### Parameter description

```go
type BucketLoggingEnabled struct {
    TargetBucket string 
    TargetPrefix string 
}

// BucketPutLoggingOptions is the options of PutBucketLogging
type BucketPutLoggingOptions struct {
    XMLName        xml.Name             
    LoggingEnabled *BucketLoggingEnabled 
}
```

| Parameter Name | Description | Type |
| ----------------------- | ------------------------------------------------------------ | ------ |
| BucketPutLoggingOptions | Log management configuration parameter                                             | Struct |
| LoggingEnabled          | Log management configuration                                                 | Struct |
| TargetBucket | The destination bucket for storing logs, which can be the source bucket (not recommended) or a bucket in the same region under the same account | String |
| TargetPrefix | Specified path in the destination bucket for storing logs | String |

## Querying Log Management

#### Feature description

This API (GET Bucket logging) is used to query the log configuration information of a specified bucket.

#### Method prototype

```go
func (s *BucketService) GetLogging(ctx context.Context) (*BucketGetLoggingResult, *Response, error)
```

#### Sample request

```go
v, resp, err := client.Bucket.GetLogging(context.Background())
```

#### Returned result description

```go
type BucketGetLoggingResult BucketPutLoggingOptions
```

| Parameter Name | Description | Type |
| ---------------------- | ------------------------------------------------------------ | ------ |
| BucketGetLoggingResult | Log management configuration parameter                                             | Struct |
| LoggingEnabled          | Log management configuration                                                 | Struct |
| TargetBucket | The destination bucket for storing logs, which can be the source bucket (not recommended) or a bucket in the same region under the same account | String |
| TargetPrefix | Specified path in the destination bucket for storing logs | String |
