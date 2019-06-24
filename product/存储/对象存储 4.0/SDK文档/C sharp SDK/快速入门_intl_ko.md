## 다운로드 및 설치

### 관련 리소스
- COS의 XML C# SDK 소스 코드 다운로드 주소: [ XML C# SDK ](https://github.com/tencentyun/qcloud-sdk-dotnet).
- 예시 데모 다운로드 주소: [ COS XML C# SDK 예시](https://github.com/tencentyun/qcloud-sdk-dotnet-demo).
- COS의 XML C# SDK DLL 파일 다운로드 주소: [COS XML DLL 라이브러리](https://github.com/tencentyun/qcloud-sdk-dotnet/tree/master/libs).

### 환경 의존
- COS XML C# SDK 소스 코드는 .NET 4.0을 기반으로 개발하였고, newtonsoft.json 라이브러리에 의존합니다.
- Windows: .NET 2.0 이상 버전, Visual Studio 2010 이상 버전을 설치하십시오. 
- Linux/Mac: Mono 3.12 이상 버전을 설치하십시오.

### SDK 설치
SDK에 포함된 DLL 라이브러리 파일은 COSXML.dll 및 Newtonsoft.Json.dll이며, 다음 방식으로 SDK를 설치할 수 있습니다.

- DLL 참조 방식
	[SDK 개발 키트](https://github.com/tencentyun/qcloud-sdk-dotnet/tree/master/libs)를 획득하고, 그 중의 DLL 파일을 프로젝트로 가져옵니다.
- 프로젝트 가져오기 방식
	 [소스 코드](https://github.com/tencentyun/qcloud-sdk-dotnet/tree/master/QCloudCSharpSDK)를 획득하여 프로젝트로 가져오기 합니다.
- Nuget 참조 방식
	Nuget 키트 매니저에서 Tencent.QCloud.Cos.Sdk를 찾아서 설치를 클릭하십시오.

## 시작하기
다음에서는 COS C# SDK를 사용하여 클라이언트 초기화, 버킷 생성, 버킷 리스트 조회, 객체 업로드, 객체 리스트 조회, 객체 다운로드 및 객체 삭제 등의 기초 작업을 완료하는 방법을 소개합니다.

### 초기화

COS 서비스와 관련된 요청을 하기 전, `CosXmlConfig, QCloudCredentialProvider, CosXmlServer` 3개의 객체를 인스턴스화해야 합니다. 그 중,
- `CosXmlConfig`는 SDK API 구성을 제공합니다.
- `QCloudCredentialProvider`는 키 정보 설정 API를 제공합니다.
- `CosXmlServer`는 다양한 COS 서비스 API를 제공합니다.

```C#
//CosXmlConfig 초기화 
string appid = "1250000000";//Tencent Cloud 계정 ID인 APPID 설정
string region = "ap-beijing"; //기본 버킷 지역 설정
CosXmlConfig config = new CosXmlConfig.Builder()
	.SetConnectionTimeoutMs(60000)  //연결 타임아웃 시간 설정, 단위 ms, 기본값 45000ms
	.SetReadWriteTimeoutMs(40000)  //읽기/쓰기 타임아웃 시간 설정, 단위 ms, 기본값 45000ms
	.IsHttps(true)  //기본 https 요청 설정
	.SetAppid(appid)  //Tencent Cloud 계정 ID인 APPID 설정
	.SetRegion(region)  //기본 버킷 지역 설정
	.SetDebugLog(true)  //로그 표시
	.Build();  //CosXmlConfig 객체 생성

//QCloudCredentialProvider 초기화, SDK에서 영구 키, 임시 키, 사용자 지정 키 3가지 방식을 제공합니다. 
QCloudCredentialProvider cosCredentialProvider  =  null;

//방식 1, 영구 키
string secretId = "COS_SECRETID"; //"클라우드 API 키 SecretId".
string secretKey = "COS_SECRETKEY"; //"클라우드 API 키 SecretKey".
long durationSecond = 600;  //secretKey 유효 시간, 단위는 초
cosCredentialProvider = new DefaultQCloudCredentialProvider(secretId, secretKey, durationSecond);

//방식 2, 임시 키
string tmpSecretId = "COS_SECRETID"; //"임시 키 SecretId".
string tmpSecretKey = "COS_SECRETKEY"; //"임시 키 SecretKey".
string tmpToken = "COS_TOKEN"; //"임시 키 token".
long tmpExpireTime = 1546862502；//임시 키 유효 시간
cosCredentialProvider = new DefaultSessionQCloudCredentialProvider(tmpSecretId,tmpSecretKey,tmpExpireTime,tmpToken);

//방식 3, 사용자 지정 키, 사용자 지정 방식으로 키 정보를 제공합니다다. QCloudCredentialProvider를 계승하고 GetQCloudCredentials() 방식을 덮어쓰기합니다.
public class MyQCloudCredentialProvider : QCloudCredentialProvider
{
	public override QCloudCredentials GetQCloudCredentials()
	{
		string secretId = "COS_SECRETID"; //키 SecretId
		string secretKey = "COS_SECRETKEY"; //키 SecretKey
		string keyTime = "키 유효 기간"; //1546862502;1546863102
		return new QCloudCredentials(secretId, secretKey, keyTime);
	}

	public override void Refresh()
	{
		//키 정보 업데이트
	}
}
cosCredentialProvider = new MyQCloudCredentialProvider();

//CosXmlServer 초기화
CosXmlServer cosXml = new CosXmlServer(config, cosCredentialProvider);

```

### 버킷 생성
```C#
try
{
	string bucket = "examplebucket-1250000000"; //버킷 이름 형식: BucketName-APPID
	PutBucketRequest request = new PutBucketRequest(bucket);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//요청 실행
	PutBucketResult result = cosXml.PutBucket(request);
	//요청 성공
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
	//요청 실패
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//요청 실패
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

```

### 버킷 리스트 조회
```C#
try
{
	GetServiceRequest request = new GetServiceRequest();
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//요청 실행
	GetServiceResult result = cosXml.GetService(request);
	//요청 성공
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
	//요청 실패
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{	
	//요청 실패
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

### 업로드 객체
```C#
try
{
	string bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
	string key = "exampleobject"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
	string srcPath = @"F:\exampleobject"；//로컬 파일 절대 경로
	PutObjectRequest request = new PutObjectRequest(bucket, key, srcPath);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//진행률 콜백 설정
	request.SetCosProgressCallback(delegate(long completed, long total)
	{
		Console.WriteLine(String.Format("progress = {1:##.##}%", completed * 100.0 / total));
	});
	//요청 실행
	PutObjectResult result = cosXml.PutObject(request);
	//요청 성공
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	//요청 실패
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//요청 실패
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

**// 대용량 파일은 멀티파트 업로드를 사용해야 하고(), SDK에 캡슐화된 TransferManager 및 COSXMLUploadTask를 참조할 수 있습니다. 예시는 다음과 같습니다 **
TransferManager transferManager = new TransferManager(cosXml, new TransferConfig());
COSXMLUploadTask uploadTask = new COSXMLUploadTask(bucket, null, key);
uploadTask.SetSrcPath(srcPath);
uploadTask.progressCallback = delegate (long completed, long total)
{
	Console.WriteLine(String.Format("progress = {1:##.##}%", completed * 100.0 / total));
};
uploadTask.successCallback = delegate (CosResult cosResult) 
{
	COSXML.Transfer.COSXMLUploadTask.UploadTaskResult result = cosResult as COSXML.Transfer.COSXMLUploadTask.UploadTaskResult;
	Console.WriteLine(result.GetResultInfo());
};
uploadTask.failCallback = delegate (CosClientException clientEx, CosServerException serverEx) 
{
	if (clientEx != null)
	{
		Console.WriteLine("CosClientException: " + clientEx.Message);
	}
	if (serverEx != null)
	{
		Console.WriteLine("CosServerException: " + serverEx.GetInfo());
	}
};
transferManager.Upload(uploadTask);

```

### 객체 리스트 조회
```C#
try
{
	string bucket = "examplebucket-1250000000"; //형식: BucketName-APPID
	GetBucketRequest request = new GetBucketRequest(bucket);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//요청 실행
	GetBucketResult result = cosXml.GetBucket(request);
	//요청 성공
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
	//요청 실패
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//요청 실패
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

### 객체 다운로드
```C#
try
{
	string bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
	string key = "exampleobject"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
	string localDir = @"F:\"；//로컬 지정 폴더로 다운로드
	string localFileName = "exampleobject"; //로컬 저장할 파일 이름 지정
	GetObjectRequest request = new GetObjectRequest(bucket, key, localDir, localFileName);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//진행률 콜백 설정
	request.SetCosProgressCallback(delegate(long completed, long total)
	{
		Console.WriteLine(String.Format("progress = {1:##.##}%", completed * 100.0 / total));
	});
	//요청 실행
	GetObjectResult result = cosXml.GetObject(request);
	//요청 성공
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	//요청 실패
 	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//요청 실패
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

### 객체 삭제
```C#
try
{
	string bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
	string key = "exampleobject"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
	DeleteObjectRequest request = new DeleteObjectRequest(bucket, key);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//요청 실행
	DeleteObjectResult result = cosXml.DeleteObject(request);
	//요청 성공
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	//요청 실패
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//요청 실패
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

