## 概要

Cloud Object Storage（COS）はAWS S3と互換性のあるAPIを提供しているため、データをS3からCOSに移行した後、簡単な設定変更を行うだけで、クライアントアプリケーションに簡単にCOSサービスとの互換性を持たせることができます。ここでは主に、各開発プラットフォームにおけるS3 SDKの適用の手順についてご説明します。適用手順の追加が完了すると、S3 SDKのインターフェースを使用してCOS上のファイルにアクセスできるようになります。

#### 準備作業

1. [Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)が完了しており、なおかつ[CAMコンソール](https://console.cloud.tencent.com/cam/capi)上でTencent CloudキーのSecretIDとSecretKeyを取得済みであることとします。
2. S3 SDKを統合済みで、正常に実行可能なクライアントアプリケーションがすでにあることとします。

## Android

以下ではAWS Android SDK 2.14.2バージョンを例に、COSサービスにアクセスできるように適用する方法についてご説明します。端末からCOSへのアクセスについては、パーマネントキーをクライアントコード内に埋め込むと、開示されるリスクが極めて大きいため、STSサービスにアクセスして一時キーを取得することをお勧めします。詳細については、[一時キーの生成および使用ガイド](https://intl.cloud.tencent.com/document/product/436/14048)をご参照ください。 

#### 初期化

インスタンスを初期化する際、一時キープロバイダおよびEndpointを設定する必要があります。バケットの所在リージョンが`ap-guangzhou`の場合を例にとります。

```
AmazonS3Client s3 = new AmazonS3Client(new AWSCredentialsProvider() {
    @Override
    public AWSCredentials getCredentials() {
    	 // ここではバックエンドがSTSにリクエストし、一時キー情報を取得します
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

AWS iOS SDK 2.10.2バージョンを例に、COSサービスにアクセスできるように適用する方法についてご説明します。端末からCOSへのアクセスについては、パーマネントキーをクライアントコード内に埋め込むと、開示されるリスクが極めて大きいため、STSサービスにアクセスして一時キーを取得することをお勧めします。詳細については、[一時キーの生成および使用ガイド](https://intl.cloud.tencent.com/document/product/436/14048)をご参照ください。 

#### 1. AWSCredentialsProviderプロトコルの実装

```
-(AWSTask<AWSCredentials *> *)credentials{
	// ここではバックエンドがSTSにリクエストし、一時キー情報を取得します
    AWSCredentials *credential = [[AWSCredentials alloc]initWithAccessKey:@"<TempSecretID>" secretKey:@"<TempSecretKey>" sessionKey:@"<STSSessionToken>" expiration:[NSDate dateWithTimeIntervalSince1970:1565770577]];
    
    return [AWSTask taskWithResult:credential];
    
}

- (void)invalidateCachedTemporaryCredentials{
    
}
```

#### 2. 一時キープロバイダおよびEndpointの提供

バケットの所在リージョンが`ap-guangzhou`の場合を例にとります。

```
NSURL* bucketURL = [NSURL URLWithString:@"http://cos.ap-guangzhou.myqcloud.com"];
    
AWSEndpoint* endpoint = [[AWSEndpoint alloc] initWithRegion:AWSRegionUnknown service:AWSServiceS3 URL:bucketURL];
AWSServiceConfiguration* configuration = [[AWSServiceConfiguration alloc] 
	initWithRegion:AWSRegionUSEast2 endpoint:endpoint 
	credentialsProvider:[MyCredentialProvider new]]; // MyCredentialProviderがAWSCredentialsProviderプロトコルを実装しました
   
[[AWSServiceManager defaultServiceManager] setDefaultServiceConfiguration:configuration];
```

## Node.js

以下ではAWS JS SDK 2.509.0バージョンを例に、COSサービスにアクセスできるように適用する方法についてご説明します。

#### 初期化

インスタンスを初期化する際にTencent CloudキーおよびEndpointを設定します。バケットの所在リージョンが`ap-guangzhou`の場合のコードの例は次のようになります。

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

以下ではAWS Java SDK 1.11.609バージョンを例に、COSサービスにアクセスできるように適用する方法についてご説明します。

#### 1. AWSの設定および証明書ファイルを変更する

> ?以下ではLinuxを例に、AWSの設定および証明書ファイルの変更を行います。

AWS SDKのデフォルトの設定ファイルは通常、ユーザーディレクトリ下にあります。[設定および証明書ファイル](https://docs.aws.amazon.com/zh_cn/cli/latest/userguide/cli-configure-files.html)をご参照ください。

- 設定ファイル（ファイルの位置は`~/.aws/config`）に次の設定情報を追加します。
```
[default]  
s3 =  
addressing_style = virtual 
```
- 証明書ファイル（ファイルの位置は`~/.aws/credentials`）にTencent Cloudのキーを設定します。  
```
[default]  
aws_access_key_id = [COS_SECRETID]  
aws_secret_access_key = [COS_SECRETKEY] 
```

#### 2. コードにEndpointを設定する

バケットの所在リージョンが`ap-guangzhou`の場合のコードの例は次のようになります。
```
AmazonS3 s3Client = AmazonS3ClientBuilder.standard()
    .withEndpointConfiguration(new AwsClientBuilder.EndpointConfiguration(
    		"http://cos.ap-guangzhou.myqcloud.com", 
    		"ap-guangzhou"))
    .build();
```

## Python

以下ではAWS Python SDK 1.9.205バージョンを例に、COSサービスにアクセスできるように適用する方法についてご説明します。

#### 1. AWSの設定および証明書ファイルを変更する

> ?以下ではLinuxを例に、AWSの設定および証明書ファイルの変更を行います。

AWS SDKのデフォルトの設定ファイルは通常、ユーザーディレクトリ下にあります。[設定および証明書ファイル](https://docs.aws.amazon.com/zh_cn/cli/latest/userguide/cli-configure-files.html)をご参照ください。

- 設定ファイル（ファイルの位置は`~/.aws/config`）に次の設定を追加します。
```
[default]  
s3 =   
	signature_version = s3
	addressing_style = virtual
```
- 証明書ファイル（ファイルの位置は`~/.aws/credentials`）にTencent Cloudのキーを設定します。  
```
[default]  
aws_access_key_id = [COS_SECRETID]  
aws_secret_access_key = [COS_SECRETKEY] 
```

#### 2. コードにEndpointを設定する

バケットの所在リージョンが`ap-guangzhou`の場合を例にとります。

```
client = boto3.client('s3', endpoint_url='https://cos.ap-guangzhou.myqcloud.com')
```

## PHP

以下ではAWS PHP SDK 3.109.3バージョンを例に、COSサービスにアクセスできるように適用する方法についてご説明します。

#### 1. AWSの設定および証明書ファイルを変更する

> ?以下ではLinuxを例に、AWSの設定および証明書ファイルの変更を行います。

AWS SDKのデフォルトの設定ファイルは通常、ユーザーディレクトリ下にあります。[設定および証明書ファイル](https://docs.aws.amazon.com/zh_cn/cli/latest/userguide/cli-configure-files.html)をご参照ください。

- 設定ファイル（ファイルの位置は`~/.aws/config`）に次の設定を追加します。
```
[default]  
s3 =  
addressing_style = virtual 
```
- 証明書ファイル（ファイルの位置は`~/.aws/credentials`）にTencent Cloudのキーを設定します。  
```
[default]  
aws_access_key_id = [COS_SECRETID]  
aws_secret_access_key = [COS_SECRETKEY] 
```

#### 2. コードにEndpointを設定する

バケットの所在リージョンが`ap-guangzhou`の場合を例にとります。
```
$S3Client = new S3Client([
  'region'          => 'ap-guangzhou',
  'version'         => '2006-03-01',
  'endpoint'        => 'https://cos.ap-guangzhou.myqcloud.com'
]);

```

## .NET

以下ではAWS .NET SDK 3.3.104.12バージョンを例に、COSサービスにアクセスできるように適用する方法についてご説明します。

#### 初期化
インスタンスを初期化する際にTencent CloudキーおよびEndpointを設定します。バケットの所在リージョンが`ap-guangzhou`の場合を例にとります。

```
string sAccessKeyId = "COS_SECRETID";
string sAccessKeySecret = "COS_SECRETKEY";
string region = "ap-guangzhou";
  
var config = new AmazonS3Config() { ServiceURL = "https://cos." + region + ".myqcloud.com" };
var client = new AmazonS3Client(sAccessKeyId, sAccessKeySecret, config);

```

## Go

以下ではAWS Go SDK 1.21.9バージョンを例に、COSサービスにアクセスできるように適用する方法についてご説明します。

#### 1. キーによってsessionを作成する

バケットの所在リージョンが`ap-guangzhou`の場合を例にとります。
```golang
func newSession() (*session.Session, error) {
	creds := credentials.NewStaticCredentials("COS_SECRETID", "COS_SECRETKEY", "")
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

#### 2. sessionによってserverを作成し、リクエストを送信する
```golang
sess, _ := newSession()
service := s3.New(sess)

// ファイルのアップロードの例
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

以下ではAWS C++ SDK 1.7.68バージョンを例に、COSサービスにアクセスできるように適用する方法についてご説明します。

#### 1. AWSの設定および証明書ファイルを変更する

> ?以下ではLinuxを例に、AWSの設定および証明書ファイルの変更を行います。

AWS SDKのデフォルトの設定ファイルは通常、ユーザーディレクトリ下にあります。[設定および証明書ファイル](https://docs.aws.amazon.com/zh_cn/cli/latest/userguide/cli-configure-files.html)をご参照ください。

- 設定ファイル（ファイルの位置は`~/.aws/config`）に次の設定を追加します。
```
[default]  
s3 =  
addressing_style = virtual 
```
- 証明書ファイル（ファイルの位置は`~/.aws/credentials`）にTencent Cloudのキーを設定します。  
```
[default]  
aws_access_key_id = [COS_SECRETID]  
aws_secret_access_key = [COS_SECRETKEY] 
```

#### 2. コードにEndpointを設定する

バケットの所在リージョンが`ap-guangzhou`の場合のコードの例は次のようになります。

```cpp
Aws::Client::ClientConfiguration awsCC;
awsCC.scheme = Aws::Http::Scheme::HTTP;
awsCC.region = "ap-guangzhou";
awsCC.endpointOverride = "cos.ap-guangzhou.myqcloud.com"; 
Aws::S3::S3Client s3_client(awsCC);
```
