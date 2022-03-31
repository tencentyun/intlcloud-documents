## Overview

COS offers AWS S3-compatible APIs. Therefore, after your data is migrated from S3 to COS, you can make your client application conveniently compatible with the COS service by simply modifying the configurations. This document describes how to adapt the S3 SDK to different development platforms. After adding adaptation, you can use the APIs of S3 SDK to access files in COS.

### Preparations

1. You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and obtained the Tencent Cloud SecretID and SecretKey from the [CAM Console](https://console.cloud.tencent.com/cam/capi).
2. You have a client application that has been integrated with the S3 SDK and runs properly.

## Android

The following describes how to adapt the AWS SDK 2.14.2 for Android to COS. If COS is accessed from a device, a permanent key placed into the client code is at great risk of being leaked; therefore, you are recommended to connect to the STS service to obtain a temporary key. For more information, see [Temporary Key Generation and Usage Guide](https://intl.cloud.tencent.com/document/product/436/14048). 

### Initialization

When initiating an instance, you need to set the temporary key provider and `Endpoint`. Suppose that the bucket region is `ap-guangzhou`:

```
AmazonS3Client s3 = new AmazonS3Client(new AWSCredentialsProvider() {
    @Override
    public AWSCredentials getCredentials() {
    	 // Here, the backend requests for a temporary key from STS
        return new BasicSessionCredentials(
        		"<TempSecretID>", "<TempSecretKey>", "<STSSessionToken>"
        );
    }

    @Override
    public void refresh() {
        //
    }
});

s3.setEndpoint("cos.ap-guangzhou.myqcloud.com"); 
```

## iOS

The following describes how to adapt the AWS SDK 2.10.2 for iOS to COS. If COS is accessed from a device, a permanent key placed into the client code is at great risk of being leaked; therefore, you are recommended to connect to the STS service to obtain a temporary key. For more information, see [Temporary Key Generation and Usage Guide](https://intl.cloud.tencent.com/document/product/436/14048). 

#### 1. Implement the `AWSCredentialsProvider` protocol

```
-(AWSTask<AWSCredentials *> *)credentials{
	// Here, the backend requests for a temporary key from STS
    AWSCredentials *credential = [[AWSCredentials alloc]initWithAccessKey:@"<TempSecretID>" secretKey:@"<TempSecretKey>" sessionKey:@"<STSSessionToken>" expiration:[NSDate dateWithTimeIntervalSince1970:1565770577]];
    
    return [AWSTask taskWithResult:credential];
    
}

- (void)invalidateCachedTemporaryCredentials{
    
}
```

#### 2. Provide a temporary key provider and `Endpoint`

Suppose that the bucket region is `ap-guangzhou`:

```
NSURL* bucketURL = [NSURL URLWithString:@"http://cos.ap-guangzhou.myqcloud.com"];
    
AWSEndpoint* endpoint = [[AWSEndpoint alloc] initWithRegion:AWSRegionUnknown service:AWSServiceS3 URL:bucketURL];
AWSServiceConfiguration* configuration = [[AWSServiceConfiguration alloc] 
	initWithRegion:AWSRegionUSEast2 endpoint:endpoint 
	credentialsProvider:[MyCredentialProvider new]]; // `MyCredentialProvider` implements the `AWSCredentialsProvider` protocol
   
[[AWSServiceManager defaultServiceManager] setDefaultServiceConfiguration:configuration];
```

## Node.js

The following describes how to adapt the AWS SDK 2.509.0 for JS to COS.

### Initialization

When initiating an instance, set the Tencent Cloud key and `Endpoint`. Supposing that the bucket region is `ap-guangzhou`, the sample code is as follows:

```
var AWS = require('aws-sdk');

AWS.config.update({
    accessKeyId: "<Tencent Cloud SecretID>",
    secretAccessKey: "<Tencent Cloud SecretKey>",
    region: "ap-guangzhou",
    endpoint: 'https://cos.ap-guangzhou.myqcloud.com',
});

s3 = new AWS.S3({apiVersion: '2006-03-01'});
```

## Java

The following describes how to adapt the AWS SDK 1.11.609 for Java to COS.

#### 1. Modify the configuration and certificate files of AWS

> Below is an example of modifying the configuration and certificate files of AWS on Linux.

The default configuration file of the AWS SDK is typically located under the user directory. For more information, see [Configuration and Certificate Files](https://docs.aws.amazon.com/en_us/cli/latest/userguide/cli-configure-files.html).

- Add the following configuration information to the configuration file (located in `~/.aws/config`):
```
[default]  
s3 =  
addressing_style = virtual 
```
- Configure the Tencent Cloud key in the certificate file (located in `~/.aws/credentials`):  
```
[default]  
aws_access_key_id = [Tencent Cloud SecretID]  
aws_secret_access_key = [Tencent Cloud SecretKey] 
```

#### 2. Set the `Endpoint` in the code

Supposing that the bucket region is `ap-guangzhou`, the sample code is as follows:
```
AmazonS3 s3Client = AmazonS3ClientBuilder.standard()
    .withEndpointConfiguration(new AwsClientBuilder.EndpointConfiguration(
    		"http://cos.ap-guangzhou.myqcloud.com", 
    		"ap-guangzhou"))
    .build();
```

## Python

The following describes how to adapt the AWS SDK 1.9.205 for Python to COS.

#### 1. Modify the configuration and certificate files of AWS

> Below is an example of modifying the configuration and certificate files of AWS on Linux.

The default configuration file of the AWS SDK is typically located under the user directory. For more information, see [Configuration and Certificate Files](https://docs.aws.amazon.com/en_us/cli/latest/userguide/cli-configure-files.html).

- Add the following configuration information to the configuration file (located in `~/.aws/config`):
```
[default]  
s3 =  
	signature_version = s3
addressing_style = virtual 
```
- Configure the Tencent Cloud key in the certificate file (located in `~/.aws/credentials`):  
```
[default]  
aws_access_key_id = [Tencent Cloud SecretID]  
aws_secret_access_key = [Tencent Cloud SecretKey] 
```

#### 2. Set the `Endpoint` in the code

Suppose that the bucket region is `ap-guangzhou`:

```
client = boto3.client('s3', endpoint_url='"https://cos.ap-guangzhou.myqcloud.com"')
```

## PHP

The following describes how to adapt the AWS SDK 3.109.3 for PHP to COS.

#### 1. Modify the configuration and certificate files of AWS

> Below is an example of modifying the configuration and certificate files of AWS on Linux.

The default configuration file of the AWS SDK is typically located under the user directory. For more information, see [Configuration and Certificate Files](https://docs.aws.amazon.com/en_us/cli/latest/userguide/cli-configure-files.html).

- Add the following configuration information to the configuration file (located in `~/.aws/config`):
```
[default]  
s3 =  
addressing_style = virtual 
```
- Configure the Tencent Cloud key in the certificate file (located in `~/.aws/credentials`):  
```
[default]  
aws_access_key_id = [Tencent Cloud SecretID]  
aws_secret_access_key = [Tencent Cloud SecretKey] 
```

#### 2. Set the `Endpoint` in the code

Suppose that the bucket region is `ap-guangzhou`:
```
$S3Client = new S3Client([
  'region'          => 'ap-guangzhou',
  'version'         => '2006-03-01',
  'endpoint'        => 'https://cos.ap-guangzhou.myqcloud.com'
]);

```

## .NET

The following describes how to adapt the AWS SDK 3.3.104.12 for .NET to COS.

### Initialization
When initiating an instance, set the Tencent Cloud key and `Endpoint`. Suppose that the bucket region is `ap-guangzhou`:

```
string sAccessKeyId = "<Tencent Cloud SecretID>";
string sAccessKeySecret = "<Tencent Cloud SecretKey>";
string region = "ap-guangzhou";
  
var config = new AmazonS3Config() { ServiceURL = "https://cos." + region + ".myqcloud.com" };
var client = new AmazonS3Client(sAccessKeyId, sAccessKeySecret, config);

```

## Go

The following describes how to adapt the AWS SDK 1.21.9 for Go to COS.

#### 1. Create a session based on the key

Suppose that the bucket region is `ap-guangzhou`:
```golang
func newSession() (*session.Session, error) {
	creds := credentials.NewStaticCredentials("<Tencent Cloud SecretID>", "<Tencent Cloud SecretKey>", "")
	region := "ap-guangzhou"
	endpoint := "http://cos.ap-guangzhou.myqcloud.com"
	config := &aws.Config{
		Region:           aws.String(region),
		Endpoint:         &endpoint,
		S3ForcePathStyle: aws.Bool(true),
		Credentials:      creds,
		// DisableSSL:       &disableSSL,
	}
	return session.NewSession(config)
}
```

#### 2. Create a server initiation request based on the session
```golang
sess, _ := newSession()
service := s3.New(sess)

// Take uploading a file as an example
fp, _ := os.Open("s3_test.go")
defer fp.Close()

ctx, cancel := context.WithTimeout(context.Background(), time.Duration(30)*time.Second)
defer cancel()

service.PutObjectWithContext(ctx, &s3.PutObjectInput{
	Bucket: aws.String("alangz-1250000000"),
	Key:    aws.String("test/s3_test.go"),
	Body:   fp,
})
```

## C++

The following describes how to adapt the AWS SDK 1.7.68 for C++ to COS.

#### 1. Modify the configuration and certificate files of AWS

> Below is an example of modifying the configuration and certificate files of AWS on Linux.

The default configuration file of the AWS SDK is typically located under the user directory. For more information, see [Configuration and Certificate Files](https://docs.aws.amazon.com/en_us/cli/latest/userguide/cli-configure-files.html).

- Add the following configuration information to the configuration file (located in `~/.aws/config`):
```
[default]  
s3 =  
addressing_style = virtual 
```
- Configure the Tencent Cloud key in the certificate file (located in `~/.aws/credentials`):  
```
[default]  
aws_access_key_id = [Tencent Cloud SecretID]  
aws_secret_access_key = [Tencent Cloud SecretKey] 
```

#### 2. Set the `Endpoint` in the code

Supposing that the bucket region is `ap-guangzhou`, the sample code is as follows:

```cpp
Aws::Client::ClientConfiguration awsCC;
awsCC.scheme = Aws::Http::Scheme::HTTP;
awsCC.region = "ap-guangzhou";
awsCC.endpointOverride = "cos.ap-guangzhou.myqcloud.com"; 
Aws::S3::S3Client s3_client(awsCC);
```
