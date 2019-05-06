## 소개
C# SDK는 객체 URL 획득, 서명 계산 및 사전 서명 URL 획득에 사용되는 API를 제공합니다.

### 객체 URL 획득
```C#
string GetAccessURL(CosRequest request);
```
## 서명 계산
```C#
string GenerateSign(string method, string path, Dictionary<string, string> queryParameters, Dictionary<string, string> headers, long signDurationSecond)；
```
## 요청 사전 서명 URL 획득
```C#
string GenerateSignURL(PreSignatureStruct preSignatureStruct);
```
### 매개변수 설명
|매개변수 이름|유형|설명|
|-----|-----|----|
|request|CosRequest|요청 객체|
|preSignatureStruct|PreSignatureStruct|사전 서명 URL 예시|
|method|string|HTTP 요청 방식|
|path|string|HTTP 요청 경로, 즉 객체 키|
|headers|`Dictionary<string, string>`| 서명의 검증 헤더 유무 |
|queryParameters|`Dictionary<string, string>`|서명에 대해 요청 url 중 조회 매개변수 인증 여부|
|signDurationSecond|long|서명 유효 시간, 단위는 초|

### PreSignatureStruct 아키텍처 설명
PreSignatureStruct를 통해 객체가 해당하는 사전 서명 요청 URL을 획득하고, 요청을 발송하는 데 사용합니다.

|매개변수 이름|유형|설명|
|-----|-----|----|
|appid|string|Tencent Cloud 계정 APPID|
|bucket|string|버킷|
|region|string|버킷 소재 지역|
|method|string|HTTP 요청 방식|
|isHttps|bool|true: HTTPS 요청, false: HTTP 요청|
|key|string|객체 키|
|headers|`Dictionary<string, string>`| 서명의 검증 헤더 유무 |
|queryParameters|`Dictionary<string, string>`|서명에 대해 요청 url 중 조회 매개변수 인증 여부|
|signDurationSecond|long|서명 유효 시간, 단위는 초|

## 영구 키로 사전 서명 요청 예시

### 업로드 요청 예시
```C#
try
{
	//영구 키를 사용하여 CosXml 초기화
	CosXmlConfig config = new CosXmlConfig.Builder()
	.SetConnectionTimeoutMs(60000)  //연결 타임아웃 시간 설정, 단위 ms, 기본값 45000ms
	.SetReadWriteTimeoutMs(40000)  //읽기/쓰기 타임아웃 시간 설정, 단위 ms, 기본값 45000ms
	.IsHttps(true)  //기본 https 요청 설정
	.SetAppid("1250000000")  //Tencent Cloud 계정 ID인 APPID 설정
	.SetRegion("ap-beijing")  //기본 버킷 지역 설정
	.SetDebugLog(true)  //로그 표시
	.Build();  //CosXmlConfig 객체 생성
	string secretId = "COS_SECRETID"; //"클라우드 API 키 SecretId".
	string secretKey = "COS_SECRETKEY"; //"클라우드 API 키 SecretKey".
	long durationSecond = 600;  //secretKey 유효 시간, 단위는 초
	QCloudCredentialProvider cosCredentialProvider  =  new DefaultQCloudCredentialProvider(secretId, secretKey, durationSecond);
	CosXmlServer cosXml = new CosXmlServer(config, cosCredentialProvider);

	PreSignatureStruct preSignatureStruct = new PreSignatureStruct();
	preSignatureStruct.appid = "1250000000";//Tencent Cloud 계정 appid
	preSignatureStruct.region = "ap-beijing"; //버킷 지역
	preSignatureStruct.bucket = "examplebucket-1250000000"; //버킷
	preSignatureStruct.key = "exampleobject"; //객체 키
	preSignatureStruct.httpMethod = "PUT"; //http 요청 방식
	preSignatureStruct.isHttps = true; //https 요청 URL 생성
	preSignatureStruct.signDurationSecond = 600; //요청 서명 유효 시간은 600s
	preSignatureStruct.headers = null；//인증해야 하는 서명의 헤더
	preSignatureStruct.queryParameters = null; //인증해야 하는 서명의 URL 요청 매개변수

	string requestSignURL = cosXml.GenerateSignURL(preSignatureStruct); //업로드 사전 서명 URL(영구 키 방식을 사용하여 계산한 서명 URL)

	string srcPath = @"F:\exampleobject"；//로컬 파일 절대 경로
	PutObjectRequest request = new PutObjectRequest(null, null, srcPath);
	//업로드 요청 사전 서명 URL 설정
	request.RequestURLWithSign = requestSignURL;
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
```

### 다운로드 요청 예시
```C#
try
{
	//영구 키를 사용하여 CosXml 초기화
	CosXmlConfig config = new CosXmlConfig.Builder()
	.SetConnectionTimeoutMs(60000)  //연결 타임아웃 시간 설정, 단위 ms, 기본값 45000ms
	.SetReadWriteTimeoutMs(40000)  //읽기/쓰기 타임아웃 시간 설정, 단위 ms, 기본값 45000ms
	.IsHttps(true)  //기본 https 요청 설정
	.SetAppid("1250000000")  //Tencent Cloud 계정 ID인 APPID 설정
	.SetRegion("ap-beijing")  //기본 버킷 지역 설정
	.SetDebugLog(true)  //로그 표시
	.Build();  //CosXmlConfig 객체 생성
	string secretId = "COS_SECRETID"; //"클라우드 API 키 SecretId".
	string secretKey = "COS_SECRETKEY"; //"클라우드 API 키 SecretKey".
	long durationSecond = 600;  //secretKey 유효 시간, 단위는 초
	QCloudCredentialProvider cosCredentialProvider  =  new DefaultQCloudCredentialProvider(secretId, secretKey, 600);
	CosXmlServer cosXml = new CosXmlServer(config, cosCredentialProvider);

	PreSignatureStruct preSignatureStruct = new PreSignatureStruct();
	preSignatureStruct.appid = "1250000000";//Tencent Cloud 계정 appid
	preSignatureStruct.region = "ap-beijing"; //버킷 지역
	preSignatureStruct.bucket = "examplebucket-1250000000"; //버킷
	preSignatureStruct.key = "exampleobject"; //객체 키
	preSignatureStruct.httpMethod = "GET"; //http 요청 방식
	preSignatureStruct.isHttps = true; //https 요청 URL 생성
	preSignatureStruct.signDurationSecond = 600; //요청 서명 유효 시간은 600s
	preSignatureStruct.headers = null；//인증해야 하는 서명의 헤더
	preSignatureStruct.queryParameters = null; //인증해야 하는 서명의 URL 요청 매개변수

	string requestSignURL = cosXml.GenerateSignURL(preSignatureStruct); //요청 사전 서명 URL(영구 키 방식을 사용하여 계산한 서명 URL)

	string localDir = @"F:\"；//로컬 지정 폴더로 다운로드
	string localFileName = "exampleobject"; //로컬 저장할 파일 이름 지정
	GetObjectRequest request = new GetObjectRequest(null, null, localDir, localFileName);
	//다운로드 요청 사전 서명 URL 설정
	request.RequestURLWithSign = requestSignURL;
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


## 임시 키 사전 서명 요청 예시

### 업로드 요청 예시
```C#
try
{
	//임시 키를 사용하여 CosXml 초기화
	CosXmlConfig config = new CosXmlConfig.Builder()
	.SetConnectionTimeoutMs(60000)  //연결 타임아웃 시간 설정, 단위 ms, 기본값 45000ms
	.SetReadWriteTimeoutMs(40000)  //읽기/쓰기 타임아웃 시간 설정, 단위 ms, 기본값 45000ms
	.IsHttps(true)  //기본 https 요청 설정
	.SetAppid("1250000000")  //Tencent Cloud 계정 ID인 APPID 설정
	.SetRegion("ap-beijing")  //기본 버킷 지역 설정
	.SetDebugLog(true)  //로그 표시
	.Build();  //CosXmlConfig 객체 생성
	string tmpSecretId = "COS_SECRETID"; //"임시 키 SecretId".
	string tmpSecretKey = "COS_SECRETKEY"; //"임시 키 SecretKey".
	string tmpToken = "COS_TOKEN"; //"임시 키 token".
	long tmpExpireTime = 1546862502；//임시 키 유효 시간
	QCloudCredentialProvider cosCredentialProvider = new DefaultSessionQCloudCredentialProvider(tmpSecretId,tmpSecretKey,tmpExpireTime,tmpToken);
	CosXmlServer cosXml = new CosXmlServer(config, cosCredentialProvider);

	PreSignatureStruct preSignatureStruct = new PreSignatureStruct();
	preSignatureStruct.appid = "1250000000";//Tencent Cloud 계정 appid
	preSignatureStruct.region = "ap-beijing"; //버킷 지역
	preSignatureStruct.bucket = "examplebucket-1250000000"; //버킷
	preSignatureStruct.key = "exampleobject"; //객체 키
	preSignatureStruct.httpMethod = "PUT"; //http 요청 방식
	preSignatureStruct.isHttps = true; //https 요청 URL 생성
	preSignatureStruct.signDurationSecond = 600; //요청 서명 유효 시간은 600s
	preSignatureStruct.headers = null；//인증해야 하는 서명의 헤더
	preSignatureStruct.queryParameters = null; //인증해야 하는 서명의 URL 요청 매개변수

	string requestSignURL = cosXml.GenerateSignURL(preSignatureStruct); //업로드 사전 서명 URL(임시 키 방식을 사용하여 계산한 서명 URL)

	string srcPath = @"F:\exampleobject"；//로컬 파일 절대 경로
	PutObjectRequest request = new PutObjectRequest(null, null, srcPath);
	//업로드 요청 사전 서명 URL 설정
	request.RequestURLWithSign = requestSignURL;
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
```

### 다운로드 요청 예시
```C#
try
{
	//임시 키를 사용하여 CosXml 초기화
	CosXmlConfig config = new CosXmlConfig.Builder()
	.SetConnectionTimeoutMs(60000)  //연결 타임아웃 시간 설정, 단위 ms, 기본값 45000ms
	.SetReadWriteTimeoutMs(40000)  //읽기/쓰기 타임아웃 시간 설정, 단위 ms, 기본값 45000ms
	.IsHttps(true)  //기본 https 요청 설정
	.SetAppid("1250000000")  //Tencent Cloud 계정 ID인 APPID 설정
	.SetRegion("ap-beijing")  //기본 버킷 지역 설정
	.SetDebugLog(true)  //로그 표시
	.Build();  //CosXmlConfig 객체 생성
	string tmpSecretId = "COS_SECRETID"; //"임시 키 SecretId".
	string tmpSecretKey = "COS_SECRETKEY"; //"임시 키 SecretKey".
	string tmpToken = "COS_TOKEN"; //"임시 키 token".
	long tmpExpireTime = 1546862502；//임시 키 유효 시간
	QCloudCredentialProvider cosCredentialProvider = new DefaultSessionQCloudCredentialProvider(tmpSecretId,tmpSecretKey,tmpExpireTime,tmpToken);
	CosXmlServer cosXml = new CosXmlServer(config, cosCredentialProvider);

	PreSignatureStruct preSignatureStruct = new PreSignatureStruct();
	preSignatureStruct.appid = "1250000000";//Tencent Cloud 계정 appid
	preSignatureStruct.region = "ap-beijing"; //버킷 지역
	preSignatureStruct.bucket = "examplebucket-1250000000"; //버킷
	preSignatureStruct.key = "exampleobject"; //객체 키
	preSignatureStruct.httpMethod = "GET"; //http 요청 방식
	preSignatureStruct.isHttps = true; //https 요청 URL 생성
	preSignatureStruct.signDurationSecond = 600; //요청 서명 유효 시간은 600s
	preSignatureStruct.headers = null；//인증해야 하는 서명의 헤더
	preSignatureStruct.queryParameters = null; //인증해야 하는 서명의 URL 요청 매개변수

	string requestSignURL = cosXml.GenerateSignURL(preSignatureStruct); //요청 사전 서명 URL(임시 키 방식을 사용하여 계산한 서명 URL)

	string localDir = @"F:\"；//로컬 지정 폴더로 다운로드
	string localFileName = "exampleobject"; //로컬 저장할 파일 이름 지정
	GetObjectRequest request = new GetObjectRequest(null, null, localDir, localFileName);
	//다운로드 요청 사전 서명 URL 설정
	request.RequestURLWithSign = requestSignURL;
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
