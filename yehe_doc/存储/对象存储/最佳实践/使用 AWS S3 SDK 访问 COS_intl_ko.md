## 소개

Cloud Object Storage(COS)는 AWS S3 호환 API를 제공합니다. 데이터를 S3에서 COS로 마이그레이션한 후에 간단한 설정 수정만으로 클라이언트 애플리케이션을 손쉽게 COS 서비스와 호환 사용할 수 있습니다. 본 문서는 다양한 개발 플랫폼의 S3 SDK 적용 절차를 소개합니다. 이 추가 적용 절차가 끝나면 S3 SDK 인터페이스를 사용해 COS 파일에 액세스할 수 있습니다.

#### 준비 작업

1. [Signing Up](https://intl.cloud.tencent.com/document/product/378/17985)하고 [CAM 콘솔](https://console.cloud.tencent.com/cam/capi)에서 Tencent Cloud 키 SecretID와 SecretKey를 얻습니다.
2. 이제 S3 SDK를 통합해 정상 실행할 수 있는 클라이언트 애플리케이션이 준비되었습니다.

## Android

다음은 AWS Android SDK 2.14.2 버전을 예시로 COS 서비스에 액세스하기 위한 방법을 소개합니다. 디바이스가 COS에 액세스하는 경우 영구 키를 클라이언트 코드에 두면 노출 위험이 커지므로 STS 서비스에 연결해 임시 키를 사용하십시오. 자세한 내용은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참조하십시오. 

#### 초기화

인스턴스를 초기화할 때 임시 키 제공자와 Endpoint 설정이 필요합니다. 버킷이 위치한 리전이 `ap-guangzhou`인 경우를 예로 들어봅니다.

```
AmazonS3Client s3 = new AmazonS3Client(new AWSCredentialsProvider() {
    @Override
    public AWSCredentials getCredentials() {
    	 // 이 백그라운드에서 STS로 임시 키 정보를 요청합니다.
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

AWS iOS SDK 2.10.2 버전을 예시로 COS 서비스에 액세스하기 위한 방법을 소개합니다. 디바이스가 COS에 액세스하는 경우 영구 키를 클라이언트 코드에 두면 노출 위험이 커지므로 STS 서비스에 연결해 임시 키를 사용하십시오. 자세한 내용은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참조하십시오. 

#### 1. AWSCredentialsProvider 프로토콜 실행

```
-(AWSTask<AWSCredentials *> *)credentials{
	// 이 백그라운드에서 STS로 임시 키 정보를 요청합니다.
    AWSCredentials *credential = [[AWSCredentials alloc]initWithAccessKey:@"<TempSecretID>" secretKey:@"<TempSecretKey>" sessionKey:@"<STSSessionToken>" expiration:[NSDate dateWithTimeIntervalSince1970:1565770577]];
    
    return [AWSTask taskWithResult:credential];
    
}

- (void)invalidateCachedTemporaryCredentials{
    
}
```

#### 2. 임시 키 제공자와 Endpoint 제공

버킷이 위치한 리전이 `ap-guangzhou`인 경우

```
NSURL* bucketURL = [NSURL URLWithString:@"http://cos.ap-guangzhou.myqcloud.com"];
    
AWSEndpoint* endpoint = [[AWSEndpoint alloc] initWithRegion:AWSRegionUnknown service:AWSServiceS3 URL:bucketURL];
AWSServiceConfiguration* configuration = [[AWSServiceConfiguration alloc] 
	initWithRegion:AWSRegionUSEast2 endpoint:endpoint 
	credentialsProvider:[MyCredentialProvider new]]; // MyCredentialProvider가 AWSCredentialsProvider 프로토콜 실행
   
[[AWSServiceManager defaultServiceManager] setDefaultServiceConfiguration:configuration];
```

## Node.js

AWS JS SDK 2.509.0 버전을 예시로 COS 서비스에 액세스하기 위한 방법을 소개합니다.

#### 초기화

인스턴스를 초기화할 때 Tencent Cloud 키와 Endpoint를 설정합니다. 버킷이 위치한 리전이 `ap-guangzhou`라고 가정했을 경우 코드는 아래와 같이 표시됩니다.

```
var AWS = require('aws-sdk');

AWS.config.update({
    accessKeyId: "COS_SECRETID",
    secretAccessKey: "COS_SECRETKEY",
    region: "ap-guangzhou",
    endpoint: 'https://cos.ap-guangzhou.myqcloud.com',
});

s3 = new AWS.S3({apiVersion: '2006-03-01'});
```

## Java

다음은 AWS Java SDK 1.11.609 버전을 예시로 COS 서비스에 액세스하기 위한 방법을 소개합니다.

#### 1. AWS 구성 및 인증서 파일 수정하기

> ?다음은 Linux를 예시로 AWS 구성 및 인증서 파일을 수정합니다.

AWS SDK 기본 구성 파일은 사용자 디렉터리에서 [구성 및 인증서 파일](https://docs.aws.amazon.com/zh_cn/cli/latest/userguide/cli-configure-files.html)을 참고하십시오.

- 설정파일(파일 위치는 `~/.aws/config`)에서 다음 설정을 추가합니다.- 구성 파일(파일 위치는 `~/.aws/config`)에서 다음 설정 정보를 추가합니다.
```
[default]  
s3 =  
addressing_style = virtual 
```
- 인증서 파일(파일 위치는 `~/.aws/credentials`)에서 Tencent Cloud 키를 설정합니다.  
```
[default]  
aws_access_key_id = [COS_SECRETID]  
aws_secret_access_key = [COS_SECRETKEY] 
```

#### 2. 코드에서 Endpoint 설정하기

버킷이 위치한 리전이 `ap-guangzhou`라고 가정했을 때 코드는 다음과 같습니다.
```
AmazonS3 s3Client = AmazonS3ClientBuilder.standard()
    .withEndpointConfiguration(new AwsClientBuilder.EndpointConfiguration(
    		"http://cos.ap-guangzhou.myqcloud.com", 
    		"ap-guangzhou"))
    .build();
```

## Python

다음은 AWS Python SDK 1.9.205 버전을 예시로 COS 서비스에 액세스하기 위한 방법을 소개합니다.

#### 1. AWS 구성 및 인증서 파일 수정하기

> ?다음은 Linux를 예시로 AWS 구성 및 인증서 파일을 수정합니다.

AWS SDK 기본 구성 파일은 사용자 디렉터리에서 [구성 및 인증서 파일](https://docs.aws.amazon.com/zh_cn/cli/latest/userguide/cli-configure-files.html)을 참고하십시오.

- 구성 파일(파일 위치는 `~/.aws/config`)에서 다음 설정을 추가합니다.
```
[default]  
s3 =   
	signature_version = s3
	addressing_style = virtual
```
- 인증서 파일(파일 위치는 `~/.aws/credentials`)에서 Tencent Cloud 키를 설정합니다.  
```
[default]  
aws_access_key_id = [COS_SECRETID]  
aws_secret_access_key = [COS_SECRETKEY] 
```

#### 2. 코드에서 Endpoint 설정하기

버킷이 위치한 리전이 `ap-guangzhou`인 경우

```
client = boto3.client('s3', endpoint_url='https://cos.ap-guangzhou.myqcloud.com')
```

## PHP

다음은 AWS PHP SDK 3.109.3 버전을 예시로 COS 서비스에 액세스하기 위한 방법을 소개합니다.

#### 1. AWS 구성 및 인증서 파일 수정하기

> ?다음은 Linux를 예시로 AWS 구성 및 인증서 파일을 수정합니다.

AWS SDK 기본 구성 파일은 사용자 디렉터리에서 [구성 및 인증서 파일](https://docs.aws.amazon.com/zh_cn/cli/latest/userguide/cli-configure-files.html)을 참고하십시오.

- 구성 파일(파일 위치는 `~/.aws/config`)에서 다음 설정을 추가합니다.
```
[default]  
s3 =  
addressing_style = virtual 
```
- 인증서 파일(파일 위치는 `~/.aws/credentials`)에서 Tencent Cloud 키를 설정합니다.  
```
[default]  
aws_access_key_id = [COS_SECRETID]  
aws_secret_access_key = [COS_SECRETKEY] 
```

#### 2. 코드에서 Endpoint 설정하기

버킷이 위치한 리전이 `ap-guangzhou`인 경우
```
$S3Client = new S3Client([
  "Region": "ap-guangzhou",
  'version'         => '2006-03-01',
  'endpoint'        => 'https://cos.ap-guangzhou.myqcloud.com'
]);

```

## .NET

다음은 AWS .NET SDK 3.3.104.12 버전을 예시로 COS 서비스에 액세스하기 위한 방법을 소개합니다.

#### 초기화
인스턴스를 초기화할 때 Tencent Cloud 키와 Endpoint를 설정합니다. 버킷이 속한 리전이 `ap-guangzhou`라고 가정했을 경우

```
string sAccessKeyId = "COS_SECRETID";
string sAccessKeySecret = "COS_SECRETKEY";
string region = "ap-guangzhou";
  
var config = new AmazonS3Config() { ServiceURL = "https://cos." + region + ".myqcloud.com" };
var client = new AmazonS3Client(sAccessKeyId, sAccessKeySecret, config);

```

## Go

다음은 AWS Go SDK 1.21.9 버전을 예시로 COS 서비스에 액세스하기 위한 방법을 소개합니다.

#### 1. 키에 따라 session 생성하기

버킷이 위치한 리전이 `ap-guangzhou`인 경우
```golang
func newSession() (*session.Session, error) {
	creds := credentials.NewStaticCredentials("COS_SECRETID", "COS_SECRETKEY", "")
	"Region": "ap-guangzhou",
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

#### 2. session에 따라 server 생성 요청 발송하기
```golang
sess, _ := newSession()
service := s3.New(sess)

// 파일 업로드의 경우
fp, _ := os.Open("yourLocalFilePath")
defer fp.Close()

ctx, cancel := context.WithTimeout(context.Background(), time.Duration(30)*time.Second)
defer cancel()

service.PutObjectWithContext(ctx, &s3.PutObjectInput{
	Bucket: aws.String("examplebucket-1250000000"),
	Key:    aws.String("exampleobject"),
	Body:   fp,
})
```

## C++

다음은 AWS C++ SDK 1.7.68 버전을 예시로 COS 서비스에 액세스하기 쉽게 적용하는 방법을 소개합니다.

#### 1. AWS 구성 및 인증서 파일 수정하기

> ?다음은 Linux를 예시로 AWS 구성 및 인증서 파일을 수정합니다.

AWS SDK 기본 구성 파일은 사용자 디렉터리에서 [구성 및 인증서 파일](https://docs.aws.amazon.com/zh_cn/cli/latest/userguide/cli-configure-files.html)을 참고하십시오.

- 구성 파일(파일 위치는 `~/.aws/config`)에서 다음 설정을 추가합니다.
```
[default]  
s3 =  
addressing_style = virtual 
```
- 인증서 파일(파일 위치는 `~/.aws/credentials`)에서 Tencent Cloud 키를 설정합니다.  
```
[default]  
aws_access_key_id = [COS_SECRETID]  
aws_secret_access_key = [COS_SECRETKEY] 
```

#### 2. 코드에서 Endpoint 설정하기

버킷이 위치한 리전이 `ap-guangzhou`라고 가정했을 때 코드는 다음과 같습니다.

```cpp
Aws::Client::ClientConfiguration awsCC;
awsCC.scheme = Aws::Http::Scheme::HTTP;
awsCC.region = "ap-guangzhou";
awsCC.endpointOverride = "cos.ap-guangzhou.myqcloud.com"; 
Aws::S3::S3Client s3_client(awsCC);
```
