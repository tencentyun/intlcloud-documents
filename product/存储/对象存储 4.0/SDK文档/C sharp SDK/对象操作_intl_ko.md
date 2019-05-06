## 소개

본 문서는 객체에 대한 간편 조작, 멀티파트 조작 등 기타 조작과 관련된 API의 개요 및 SDK 예제 코드를 제공합니다.

**간단한 작업**

| API                                                          | 작업 이름         | 작업 설명                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket(List Object)](https://cloud.tencent.com/document/product/436/7734) | 객체 리스트 획득   | 버킷의 객체 리스트를 획득합니다                    |
| [PUT Object](https://cloud.tencent.com/document/product/436/7749) | 객체 업로드       | 객체(파일/객체)를 버킷으로 업로드합니다     |
| [POST Object](https://cloud.tencent.com/document/product/436/14690) | 테이블로 객체 업로드   | 테이블 요청을 사용하여 객체를 업로드합니다                      |
| [HEAD Object](https://cloud.tencent.com/document/product/436/7745) | 객체 메타데이터 획득 | 객체의 메타 정보를 획득합니다                  |
| [GET Object](https://cloud.tencent.com/document/product/436/7753) | 객체 획득       | 객체(파일/객체)를 로컬로 다운로드합니다     |
| [Options Object](https://cloud.tencent.com/document/product/436/8288) | 사전 요청(Preflight)으로 CORS 구성 | 사전 요청을 이용하여 CORS 요청을 발송 가능 여부 확인 |
| [PUT Object - Copy](https://cloud.tencent.com/document/product/436/10881) | 객체 복사 설정   | 파일을 대상 경로에 복사합니다                        |
| [DELETE Object](https://cloud.tencent.com/document/product/436/7743) | 단일 객체 삭제   | 버킷에서 지정된 객체를 삭제합니다 |

**멀티파트 조작**

| API                                                          | 조작 이름         | 조작 설명                             |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://cloud.tencent.com/document/product/436/7736) | 멀티파트 업로드 조회   | 현재 진행 중인 멀티파트 업로드 정보를 조회합니다         |
| [Initiate Multipart Upload](https://cloud.tencent.com/document/product/436/7746) | 멀티파트 업로드 초기화 | 멀티파트 초기화 작업을 초기화합니다     |
| [Upload Part](https://cloud.tencent.com/document/product/436/7750) | 멀티파트 업로드       | 파일에 대해 멀티파트 업로드를 합니다                         |
| [Upload Part - Copy](https://cloud.tencent.com/document/product/436/8287) | 멀티파트 복사       | 기타 기존의 객체를 한 개의 새로운 파트로 복사합니다             |
| [List Parts](https://cloud.tencent.com/document/product/436/7747) | 업로드된 파트 조회   | 특정 멀티파트 업로드 작업에서 이미 업로드된 파트를 조회합니다   |
| [Complete Multipart Upload](https://cloud.tencent.com/document/product/436/7742) | 멀티파트 업로드 완료   | 전체 파일의 멀티파트 업로드를 완료합니다               |
| [Abort Multipart Upload](https://cloud.tencent.com/document/product/436/7740) | 멀티파트 업로드 중지   | 멀티파트 업로드 작업을 중지하고 이미 업로드된 파트를 삭제합니다 |

**기타 작업**

| API                                                          | 작업 이름         | 작업 설명                             |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [POST Object restore](https://cloud.tencent.com/document/product/436/12633) | 보관된 객체 복구 | 보관 유형의 객체를 다시 액세스할 수 있도록 검색합니다                      |
| [PUT Object acl](https://cloud.tencent.com/document/product/436/7748) | 객체 ACL 설정 | 버킷의 임의의 객체(파일/객체)의 ACL을 설정합니다 |
| [GET Object acl](https://cloud.tencent.com/document/product/436/7744) | 객체 ACL 획득 | 객체(파일/객체)의 ACL을 획득합니다                |

## 간단한 작업

### 객체 리스트 획득

#### 기능 설명

지정 버킷의 모든 객체를 획득합니다(Object List)。

#### 방식 프로토타입

```C#
GetBucketResult GetBucket(GetBucketRequest request);

void GetBucket(GetBucketRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

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

/**
//비동기화 방법
string bucket = "examplebucket-1250000000". //형식: BucketName-APPID
GetBucketRequest request = new GetBucketRequest(bucket);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
cosXml.GetBucket(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		GetBucketResult result = cosResult as GetBucketResult;
		Console.WriteLine(result.GetResultInfo());

	},
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		//요청 실패
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	});
*/
```

#### 매개변수 설명

| 매개변수 이름            | 설정 방법 | 설명                               | 유형           |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket              | 구축 방법 | 버킷 이름, 형식: BucketName-APPID | string         |
| signStartTimeSecond | SetSign  | 서명 유효기간 시작 시간                 | long            |
| durationSecond      | SetSign  | 서명 유효 기간                     | long           |
| headerKeys          | SetSign  | 서명에 검증 헤더 유무                | `List<string>` |
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명

GetBucketResult를 통해 요청의 결과를 반환합니다.

| 멤버 변수   | 유형                                                         | 설명                                                      |
| ---------- | ------------------------------------------------------------ | --------------------------------------------------------- |
| httpCode   | int                                                          | HTTP 코드, [200， 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다 |
|listBucket|[ListBucket](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListBucket.cs)| 버킷 객체 리스트 정보를 반환합니다                                  |

> ?작업 실패 시, 시스템은 [CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 또는 [CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 비정상을 throw합니다.

### 간편 업로드

#### 기능 설명

객체를 지정한 버킷에 업로드합니다(Put Object).

#### 방식 프로토타입

```C#
PutObjectResult PutObject(PutObjectRequest request);

void PutObject(PutObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

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

/**
//비동기화 방법
string bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
string key = "exampleobject"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
string srcPath = @"F:\exampleobject";  //로컬 파일 절대 경로
PutObjectRequest request = new PutObjectRequest(bucket, key, srcPath);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//진행률 콜백 설정
request.SetCosProgressCallback(delegate(long completed, long total)
{
	Console.WriteLine(String.Format("progress = {1:##.##}%", completed * 100.0 / total));
});
//요청 실행
cosXml.PutObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		PutObjectResult result = cosResult as PutObjectResult;
		Console.WriteLine(result.GetResultInfo());

	},
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		//요청 실패
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### 매개변수 설명

| 매개변수 이름            | 설정 방법               | 설명                                                         | 유형                        |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket              | 구축 방법               | 버킷 이름, 형식: BucketName-APPID                           | string                      |
| key                 | 구축 방법 또는 SetCosPath | COS에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324) | string                      |
| srcPath             | 구축 방법               | COS에 로컬 파일 업로드에 사용되는 절대 경로                          | string                      |
| data                | 구축 방법               | COS에 업로드에 사용되는 바이트 배열                                  | byte[]                      |
|progressCallback|SetCosProgressCallback|업로드 진행률 콜백 설정                                             | Callback.OnProgressCallback |
| signStartTimeSecond | SetSign                | 서명 유효기간 시작 시간                                           | long                        |
| durationSecond      | SetSign                | 서명 유효 기간                                               | long                        |
| headerKeys               | SetSign  | 서명에 검증 헤더 유무                | `List<string>` |
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명

PutObjectResult를 통해 요청의 결과를 반환합니다.

| 멤버 변수   | 유형   | 설명                                                       |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode   | int    | HTTP 코드, [200， 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다 |
| eTag     | string | 객체의 eTag를 반환합니다                                          |

> ?작업 실패 시, 시스템은 [CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 또는 [CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 비정상을 throw합니다.

### 테이블로 객체 업로드

#### 기능 설명

테이블 형식으로 객체를 업로드합니다(Post Object).

#### 방식 프로토타입

```C#
PostObjectResult PostObject(PostObjectRequest request);

void PostObject(PostObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

```C#
try
{
	string bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
	string key = "exampleobject"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
	string srcPath = @"F:\exampleobject"；//로컬 파일 절대 경로
	PostObjectRequest request = new PostObjectRequest(bucket, key, srcPath);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//진행률 콜백 설정
	request.SetCosProgressCallback(delegate(long completed, long total)
	{
		Console.WriteLine(String.Format("progress = {1:##.##}%", completed * 100.0 / total));
	});
	//요청 실행
	PostObjectResult result = cosXml.PostObject(request);
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

/**
//비동기화 방법
string bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
string key = "exampleobject"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
string srcPath = @"F:\exampleobject";  //로컬 파일 절대 경로
PostObjectRequest request = new PostObjectRequest(bucket, key, srcPath);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//진행률 콜백 설정
request.SetCosProgressCallback(delegate(long completed, long total)
{
	Console.WriteLine(String.Format("progress = {1:##.##}%", completed * 100.0 / total));
});
//요청 실행
cosXml.PostObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		PostObjectResult result = cosResult as PostObjectResult;
		Console.WriteLine(result.GetResultInfo());

	},
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		//요청 실패
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### 매개변수 설명

| 매개변수 이름            | 설정 방법               | 설명                                                         | 유형                        |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket              | 구축 방법               | 버킷 이름, 형식: BucketName-APPID                           | string                      |
| key                 | 구축 방법 또는 SetCosPath | COS에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324) | string                      |
| srcPath             | 구축 방법               | COS에 로컬 파일 업로드에 사용되는 절대 경로                          | string                      |
| data                | 구축 방법               | COS에 업로드에 사용되는 바이트 배열                                  | byte[]                      |
|progressCallback|SetCosProgressCallback|업로드 진행률 콜백 설정                                             | Callback.OnProgressCallback |
| signStartTimeSecond | SetSign                | 서명 유효기간 시작 시간                                           | long                        |
| durationSecond      | SetSign                | 서명 유효 기간                                               | long                        |
| headerKeys               | SetSign                | 서명에 검증 헤더 유무                                          | `List<string>`              |
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명

PostObjectResult를 통해 요청의 결과를 반환합니다.

| 멤버 변수   | 유형   | 설명                                                       |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode   | int    | HTTP 코드, [200， 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다 |
| eTag     | string | 객체의 eTag를 반환합니다                                          |

> ?작업 실패 시, 시스템은 [CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 또는 [CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 비정상을 throw합니다.

### 객체 조회

#### 기능 설명

버킷에 지정한 객체가 있는지 여부를 조회합니다(Head Object).

#### 방식 프로토타입

```C#
HeadObjectResult HeadObject(HeadObjectRequest request);

void HeadObject(HeadObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

```C#
try
{
	string bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
	string key = "exampleobject"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
	HeadObjectRequest request = new HeadObjectRequest(bucket, key);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//요청 실행
	HeadObjectResult result = cosXml.HeadObject(request);
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

/**
//비동기화 방법
string bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
string key = "exampleobject". //객체의 버킷에서의 위치, 즉 객체 키입니다.
HeadObjectRequest request = new HeadObjectRequest(bucket, key);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//요청 실행
cosXml.HeadObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		HeadObjectResult result = cosResult as HeadObjectResult;
		Console.WriteLine(result.GetResultInfo());

	},
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		//요청 실패
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### 매개변수 설명

| 매개변수 이름            | 설정 방법              | 설명                                                         | 유형           |
| ------------------- | --------------------- | ------------------------------------------------------------ | -------------- |
| bucket              | 구축 방법              | 버킷 이름, 형식: BucketName-APPID                           | string         |
| key                 | 구축 방법 또는 SetCosPath | COS에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324) | string                      |
| signStartTimeSecond | SetSign               | 서명 유효기간 시작 시간                                           | long           |
| durationSecond      | SetSign               | 서명 유효 기간                                               | long           |
| headerKeys               | SetSign                | 서명에 검증 헤더 유무                                          | `List<string>`              |
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명

HeadObjectResult를 통해 요청의 결과를 반환합니다.

| 멤버 변수   | 유형   | 설명                                                       |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode   | int    | HTTP 코드, [200， 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다 |
| eTag     | string | 객체의 eTag를 반환합니다                                          |

> ?작업 실패 시, 시스템은 [CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 또는 [CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 비정상을 throw합니다.

### 객체 다운로드

#### 기능 설명

객체를 로컬로 다운로드합니다(Get Object).

#### 방식 프로토타입

```C#
GetObjectResult GetObject(GetObjectRequest request);

void GetObject(GetObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

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

/**
//비동기화 방법
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
cosXml.GetObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		GetObjectResult result = cosResult as GetObjectResult;
		Console.WriteLine(result.GetResultInfo());

	},
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		//요청 실패
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### 매개변수 설명

| 매개변수 이름            | 설정 방법               | 설명                                                         | 유형                        |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket              | 구축 방법               | 버킷 이름, 형식: BucketName-APPID                           | string                      |
| key                 | 구축 방법 또는 SetCosPath | COS에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324) | string                      |
| localDir            | 구축 방법               | 로컬로 다운로드하고 저장할 객체의 절대 폴더 경로                           | string                      |
| localFileName       | 구축 방법               | 로컬로 다운로드하고 저장할 객체 파일명                                   | string                      |
| progressCallback    | SetCosProgressCallback | 다운로드 진행률 콜백 설정                                             | Callback.OnProgressCallback |
| signStartTimeSecond | SetSign                | 서명 유효기간 시작 시간                                           | long                        |
| durationSecond      | SetSign                | 서명 유효 기간                                               | long                        |
| headerKeys               | SetSign  | 서명에 검증 헤더 유무                | `List<string>` |
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명

GetObjectResult를 통해 요청의 결과를 반환합니다.

| 멤버 변수   | 유형   | 설명                                                       |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode   | int    | HTTP 코드, [200， 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다 |
| eTag     | string | 객체의 eTag를 반환합니다                                            |

> ?작업 실패 시, 시스템은 [CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 또는 [CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 비정상을 throw합니다.

##### 간단한 복사

한 개의 객체를 다른 한 개의 객체로 복사합니다(Put Object Copy).

#### 방식 프로토타입

```C#
CopyObjectResult CopyObject(CopyObjectRequest request);

void CopyObject(CopyObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

```C#
try
{
	string sourceAppid = "1253960454"; //계정 appid
	string sourceBucket = "source-1253960454"; //"소스 객체가 있는 버킷
	string sourceRegion = "ap-beijing"; //소스 객체의 버킷이 있는 지역
	string sourceKey = "exampleobject"; //소스 객체 키
	//소스 객체 속성 구축
	COSXML.Model.Tag.CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceKey);

	string bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
	string key = "copy_exampleobject"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
	CopyObjectRequest request =  new CopyObjectRequest(bucket, key);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//복사 소스 설정
	request.SetCopySource(copySource);
	//복사하는가 또는 업데이트하는가를 설정하고, 여기는 복사
	request.SetCopyMetaDataDirective(COSXML.Common.CosMetaDataDirective.COPY);
	//요청 실행
	CopyObjectResult result = cosXml.CopyObject(request);
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

/**
//비동기화 방법
string sourceAppid = "1253960454"; //계정 appid
string sourceBucket = "source-1253960454"; //"소스 객체가 있는 버킷
string sourceRegion = "ap-beijing"; //소스 객체의 버킷이 있는 지역
string sourceKey = "exampleobject". //소스 객체 키
//소스 객체 속성 구축
COSXML.Model.Tag.CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceKey);

string bucket = "examplebucket-1250000000". //버킷, 형식: BucketName-APPID
string key = "copy_exampleobject". //객체의 버킷에서의 위치, 즉 객체 키입니다.
CopyObjectRequest request =  new CopyObjectRequest(bucket, key);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//복사 소스 설정
request.SetCopySource(copySource);
//복사하는가 또는 업데이트하는가를 설정하고, 여기는 복사
request.SetCopyMetaDataDirective(COSXML.Common.CosMetaDataDirective.COPY);
//요청 실행
cosXml.CopyObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		CopyObjectResult result = cosResult as CopyObjectResult;
		Console.WriteLine(result.GetResultInfo());

	},
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		//요청 실패
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	});
*/
```

#### 매개변수 설명

|매개변수 이름            | 설정 방법                 | 설명                                                         | 유형                 |
| ------------------- | ------------------------ | ------------------------------------------------------------ | -------------------- |
| bucket              | 구축 방법                 | 버킷 이름, 형식: BucketName-APPID                           | string               |
|key                 | 구축 방법 또는 SetCosPath   | COS에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324) | string                      |
| copySource          | SetCopySource            | 복사의 데이터 소스 경로 설명                                         | CopySourceStruct     |
| metaDataDirective   | SetCopyMetaDataDirective | 소스 파일의 메타데이터 복사 또는 소스 파일의 메타데이터 업데이트 여부                 | CosMetaDataDirective |
| signStartTimeSecond | SetSign                  | 서명 유효기간 시작 시간                                           | long                 |
| durationSecond      | SetSign                  | 서명 유효 기간                                               | long                 |
| headerKeys               | SetSign                | 서명에 검증 헤더 유무                                          | `List<string>`              |
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명

CopyObjectResult를 통해 요청의 결과를 반환합니다.

| 멤버 변수   | 유형                                                         | 설명                                                       |
| ---------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode   | int                                                          | HTTP 코드, [200， 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다 |
|copyObject|[CopyObject](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/CopyObject.cs)| 복사 성공의 객체 정보 반환                                     |

> ?작업 실패 시, 시스템은 [CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 또는 [CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 비정상을 throw합니다.

### Options 요청

#### 기능 설명

사전 요청 CORS 구성을 획득합니다(Options Object).

#### 방식 프로토타입

```C#
OptionObjectResult OptionObject(OptionObjectRequest request);

void OptionObject(OptionObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

```C#
try
{
	string bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
	string key = "exampleobject"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
	string origin = "http://cloud.tencent.com";
	string accessMthod = "PUT";
	OptionObjectRequest request = new OptionObjectRequest(bucket, key, origin, accessMthod);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//요청 실행
	OptionObjectResult result = cosResult as OptionObjectResult;
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

/**
//비동기화 방법
string bucket = "examplebucket-1250000000". //버킷, 형식: BucketName-APPID
string key = "exampleobject". //객체의 버킷에서의 위치, 즉 객체 키입니다.
string origin = "http://cloud.tencent.com";
string accessMthod = "PUT";
OptionObjectRequest request = new OptionObjectRequest(bucket, key, origin, accessMthod);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//요청 실행
cosXml.DeleteObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		OptionObjectResult result = cosResult as OptionObjectResult;
		Console.WriteLine(result.GetResultInfo());

	},
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		//요청 실패
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### 매개변수 설명

|매개변수 이름            | 설정 방법                           | 설명                                                         | 유형                 |
| ------------------- | ---------------------------------- | ------------------------------------------------------------ | -------------- |
| bucket              | 구축 방법                           | 버킷 이름, 형식: BucketName-APPID                           | string                      |
|key                 | 구축 방법 또는 SetCosPath | COS에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324) | string                      |
| origin              | 구축 방법 또는 SetOrigin              | CORS의 요청 소스 도메인 이름 시뮬레이션                                   | string         |
| accessMthod         | 구축 방법 또는 SetAccessControlMethod | CORS 요청의 HTTP 방식 시뮬레이션                                 | string         |
| signStartTimeSecond | SetSign                  | 서명 유효기간 시작 시간                                           | long           |
| durationSecond      | SetSign                            | 서명 유효 기간                                               | long           |
| headerKeys               | SetSign                | 서명에 검증 헤더 유무                                          | `List<string>`              |
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명

DeleteObjectResult를 통해 요청의 결과를 반환합니다.

| 멤버 변수                        |유형           | 설명                                                       |
| ------------------------------- | -------------- | ---------------------------------------------------------- |
| httpCode                        | int            | HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다 |
| accessControlAllowHeaders       | `List<string>` | CORS의 허용 요청 헤더                                     |
| accessControlAllowMethods       | `List<string>` | CORS의 허용 요청 HTTP 방식                               |
| accessControlAllowExposeHeaders | `List<string>` | CORS의 허용 요청 사용자 지정 헤더                               |
| accessControlMaxAge             | long           | OPTIONS 요청이 획득한 결과의 유효 기간                               |

> ?작업 실패 시, 시스템은 [CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 또는 [CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 비정상을 throw합니다.

### 객체 삭제

#### 기능 설명

지정한 객체를 삭제합니다(Delete Object).

#### 방식 프로토타입

```C#
DeleteObjectResult DeleteObject(DeleteObjectRequest request);

void DeleteObject(DeleteObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

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

/**
//비동기화 방법
string bucket = "examplebucket-1250000000". //버킷, 형식: BucketName-APPID
string key = "exampleobject". //객체의 버킷에서의 위치, 즉 객체 키입니다.
DeleteObjectRequest request = new DeleteObjectRequest(bucket, key);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//요청 실행
cosXml.DeleteObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		DeleteObjectResult getObjectResult = result as DeleteObjectResult;
		Console.WriteLine(result.GetResultInfo());

	},
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		//요청 실패
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### 매개변수 설명

| 매개변수 이름            | 설정 방법               | 설명                                                         | 유형           |
| ------------------- | ---------------------- | ------------------------------------------------------------ | -------------- |
| bucket              | 구축 방법               | 버킷 이름, 형식: BucketName-APPID                           | string         |
| key                 | 구축 방법 또는 SetCosPath | COS에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324) | string         |
| signStartTimeSecond | SetSign                | 서명 유효기간 시작 시간                                           | long           |
| durationSecond      | SetSign                | 서명 유효 기간                                               | long           |
| headerKeys               | SetSign                | 서명에 검증 헤더 유무                                          | `List<string>`              |
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명

DeleteObjectResult를 통해 요청의 결과를 반환합니다.

| 멤버 변수 |유형 | 설명                                                       |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int  | HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다 |

> ?작업 실패 시, 시스템은 [CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 또는 [CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 비정상을 throw합니다.

## 멀티파트 작업

### 멀티파트 업로드 조회

#### 기능 설명

지정 버킷에서 진행 중인 멀티파트 업로드를 조회합니다(List Multipart Uploads).

#### 방식 프로토타입

```C#
ListMultiUploadsResult ListMultiUploads(ListMultiUploadsRequest request);

void ListMultiUploads(ListMultiUploadsRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

```C#
try
{
	string bucket = "examplebucket-1250000000"; //형식: BucketName-APPID
	ListMultiUploadsRequest request = new ListMultiUploadsRequest(bucket);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//요청 실행
	ListMultiUploadsResult result = cosXml.ListMultiUploads(request);
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

/**
//비동기화 방법
string bucket = "examplebucket-1250000000". //형식: BucketName-APPID
ListMultiUploadsRequest request = new ListMultiUploadsRequest(bucket);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//요청 실행
cosXml.ListMultiUploads(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		ListMultiUploadsResult result = cosResult as ListMultiUploadsResult;
		Console.WriteLine(result.GetResultInfo());

	},
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		//요청 실패
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	});
*/
```

#### 매개변수 설명

| 매개변수 이름            | 설정 방법 | 설명                               | 유형           |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket              | 구축 방법 | 버킷 이름, 형식: BucketName-APPID | string         |
| signStartTimeSecond | SetSign  | 서명 유효기간 시작 시간                 | long            |
| durationSecond      | SetSign  | 서명 유효 기간                     | long           |
| headerKeys          | SetSign  | 서명에 검증 헤더 유무                | `List<string>` |
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명

ListMultiUploadsResult를 통해 요청의 결과를 반환합니다.

| 멤버 변수             |유형                                                         | 설명                                                       |
| -------------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode             | int                                                          | HTTP 코드,  [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다 |
| listMultipartUploads | [ListMultipartUploads](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListMultipartUploads.cs) | 버킷 중 진행 중인 모든 멀티파드 업로드 정보 반환                   |

> ?작업 실패 시, 시스템은 [CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 또는 [CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 비정상을 throw합니다.

### 멀티파트 업로드

멀티파트 업로드가 포함할 수 있는 작업:

- 멀티파트 업로드 객체: 멀티파트 업로드 초기화, 파트 업로드, 모든 파트 업로드 완료.
- 멀티파트 업로드 재개: 업로드된 파트 조회, 파트 업로드, 모든 파트 업로드 완료.
- 업로드된 파트 삭제.

### <span id = "INIT_MULIT_UPLOAD"> 멀티파트 업로드 초기화 </span>

#### 기능 설명

멀티파트 업로드를 초기화하고, 대응하는 uploadId를 획득합니다(Initiate Multipart Upload).

#### 방식 프로토타입

```C#
InitMultipartUploadResult InitMultipartUpload(InitMultipartUploadRequest request);

void InitMultipartUpload(InitMultipartUploadRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

```C#
try
{
	string bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
	string key = "exampleobject"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
	InitMultipartUploadRequest request = new InitMultipartUploadRequest(bucket, key);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//요청 실행
	InitMultipartUploadResult result = cosXml.InitMultipartUpload(request);
	//요청 성공
	string uploadId = result.initMultipartUpload.uploadId; //추후의 멀티파트 업로드에 사용되는 uploadId
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

/**
//비동기화 방법
string bucket = "examplebucket-1250000000". //버킷, 형식: BucketName-APPID
string key = "exampleobject". //객체의 버킷에서의 위치, 즉 객체 키입니다.
InitMultipartUploadRequest request = new InitMultipartUploadRequest(bucket, key);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//요청 실행
cosXml.InitMultipartUpload(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		InitMultipartUploadResult result = cosResult as InitMultipartUploadResult;
		string uploadId = result.initMultipartUpload.uploadId; //추후의 멀티파트 업로드에 사용되는 uploadId
		Console.WriteLine(result.GetResultInfo());

	},
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		//요청 실패
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### 매개변수 설명

| 매개변수 이름            | 설정 방법               | 설명                                                         | 유형           |
| ------------------- | ---------------------- | ------------------------------------------------------------ | -------------- |
| bucket              | 구축 방법               | 버킷 이름, 형식: BucketName-APPID                           | string         |
| key                 | 구축 방법 또는 SetCosPath | COS에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324) | string         |
| signStartTimeSecond | SetSign                | 서명 유효기간 시작 시간                                           | long           |
| durationSecond      | SetSign                | 서명 유효 기간                                               | long           |
| headerKeys               | SetSign                | 서명에 검증 헤더 유무                                          | `List<string>`              |
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명

InitMultipartUploadResult를 통해 요청의 결과를 반환합니다.

| 멤버 변수            |유형                                                         | 설명                                                       |
| ------------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode            | int                                                          | HTTP 코드,  [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다 |
| initMultipartUpload | [InitiateMultipartUpload](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/InitiateMultipartUpload.cs) | 초기화된 멀티파트 업로드의 객체 uploadId를 반환합니다                        |

> ?작업 실패 시, 시스템은 [CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 또는 [CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 비정상을 throw합니다.

### <span id = "LIST_MULIT_UPLOAD"> 업로드된 파트 조회 </span>

#### 기능 설명

지정 uploadId의 업로드된 파트를 조회합니다(List Parts).

#### 방식 프로토타입

```C#
ListPartsResult ListParts(ListPartsRequest request);

void ListParts(ListPartsRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

```C#
try
{
	string bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
	string key = "exampleobject"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
	string uploadId ="xxxxxxxx"; //멀티파트 업로드 초기화로 반환된 uploadId
	ListPartsRequest request = new ListPartsRequest(bucket, key, uploadId);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//요청 실행
	ListPartsResult result = cosXml.ListParts(request);
	//요청 성공
	//업로드된 파트 열거
	List<COSXML.Model.Tag.ListParts.Part> alreadyUploadParts = result.listParts.parts;
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

/**
//비동기화 방법
string bucket = "examplebucket-1250000000". //버킷, 형식: BucketName-APPID
string key = "exampleobject". //객체의 버킷에서의 위치, 즉 객체 키입니다.
string uploadId ="xxxxxxxx"; //멀티파트 업로드로 반환된 uploadId 초기화
ListPartsRequest request = new ListPartsRequest(bucket, key, uploadId);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//요청 실행
cosXml.ListParts(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		ListPartsResult result = cosResult as ListPartsResult;
		//업로드된 파트 열거
		List<COSXML.Model.Tag.ListParts.Part> alreadyUploadParts = result.listParts.parts;
		Console.WriteLine(result.GetResultInfo());

	},
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	 {
		//요청 실패
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### 매개변수 설명

|매개변수 이름            | 설정 방법                | 설명                                                         | 유형           |
| ------------------- | ----------------------- | ------------------------------------------------------------ | -------------- |
| bucket              | 구축 방법                | 버킷 이름, 형식: BucketName-APPID                           | string         |
| key                 | 구축 방법 또는 SetCosPath | COS에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324) | string         |
| uploadId            | 구축 방법 또는 SetUploadId | 지정 멀티파트 업로드의 uploadId 표시 | string         |
| signStartTimeSecond | SetSign                 | 서명 유효기간 시작 시간                                           | long           |
| durationSecond      | SetSign                 | 서명 유효 기간                                               | long           |
| headerKeys               | SetSign                | 서명에 검증 헤더 유무                                          | `List<string>`              |
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명

ListPartsResult를 통해 요청의 결과를 반환합니다.

| 멤버 변수  |유형                                                         | 설명                                                       |
| --------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode  | int                                                          | HTTP 코드,  [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다 |
| listParts | [ListParts](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListParts.cs) | 지정 uploadId의 멀티파트 업로드에 이미 업로드된 파트 정보를 반환합니다               |

> ?작업 실패 시, 시스템은 [CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 또는 [CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 비정상을 throw합니다.

### <span id = "MULIT_UPLOAD_PART"> 파트 업로드 </span>

파트를 업로드합니다(Upload Part).

#### 방식 프로토타입

```C#
UploadPartResult UploadPart(UploadPartRequest request);

void UploadPart(UploadPartRequest, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

```C#
try
{
	string bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
	string key = "exampleobject"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
	string uploadId ="xxxxxxxx"; //멀티파트 업로드 초기화로 반환된 uploadId
	int partNumber = 1; //파트 번호, 1에서 시작하는 자연수열이어야 합니다
	string srcPath = @"F:\exampleobject"; //로컬 파일 절대 경로
	UploadPartRequest request = new UploadPartRequest(bucket, key, partNumber, uploadId, srcPath);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//진행률 콜백 설정
	request.SetCosProgressCallback(delegate(long completed, long total)
	{
		Console.WriteLine(String.Format("progress = {0:##.##}%",  completed * 100.0 / total));
	});
	//요청 실행
	UploadPartResult result = cosXml.UploadPart(request);
	//요청 성공
	//반환된 파트의 eTag 획득, 추후의 CompleteMultiUploads에 사용합니다
	string eTag = result.eTag;
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

/**
//비동기화 방법
string bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
string key = "exampleobject"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
string uploadId ="xxxxxxxx"; //멀티파트 업로드 초기화로 반환된 uploadId
int partNumber = 1; //파트 번호, 1에서 시작하는 자연수열이어야 합니다
string srcPath = @"F:\exampleobject"; //로컬 파일 절대 경로
UploadPartRequest request = new UploadPartRequest(bucket, key, partNumber, uploadId, srcPath);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//진행률 콜백 설정
request.SetCosProgressCallback(delegate(long completed, long total)
{
	Console.WriteLine(String.Format("progress = {0:##.##}%",  completed * 100.0 / total));
});
//요청 실행
cosXml.UploadPart(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		UploadPartResult result = cosResult as UploadPartResult;
		//반환된 파트의 eTag 획득, 추후의 CompleteMultiUploads에 사용합니다
		string eTag = result.eTag;
		Console.WriteLine(result.GetResultInfo());

	},
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		//요청 실패
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### 매개변수 설명

| 매개변수 이름            | 설정 방법                  | 설명                                                         | 유형                        |
| ------------------- | ------------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket              | 구축 방법                  | 버킷 이름, 형식: BucketName-APPID                           | string                      |
| key                 | 구축 방법 또는 SetCosPath    | COS에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324) | string                      |
| uploadId            | 구축 방법 또는 SetUploadId | 지정 멀티파트 업로드의 uploadId 표시                                  | string                      |
| partNumber          | 구축 방법 또는 SetPartNumber | 지정 파트의 번호 표시, 반드시 >= 1                                | int                         |
| srcPath             | 구축 방법                  | COS에 업로드된 로컬 파일의 절대 경로                          | string                      |
| data                | 구축 방법               | COS에 업로드된 바이트 배열                                  | byte[]                      |
| progressCallback    | SetCosProgressCallback    | 업로드 진행률 콜백 설정                                             | Callback.OnProgressCallback |
| signStartTimeSecond | SetSign                  | 서명 유효기간 시작 시간                                           | long                        |
| durationSecond      | SetSign                   | 서명 유효 기간                                               | long                        |
| headerKeys               | SetSign                | 서명에 검증 헤더 유무                                          | `List<string>`              |
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명

UploadPartResult를 통해 요청의 결과를 반환합니다.

| 멤버 변수   | 유형   | 설명                                                       |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode   | int    | HTTP 코드, [200， 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다 |
| eTag | string | 객체의 파트 eTag를 반환합니다 |

> ?작업 실패 시, 시스템은 [CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 또는 [CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 비정상을 throw합니다.

### <span id = "COMPLETE_MULIT_UPLOAD"> 모든 파트 업로드 완료 </span>

#### 기능 설명

전체 멀티파트 업로드를 완료합니다(Complete Multipart Upload).

#### 방식 프로토타입

```C#
CompleteMultipartUploadResult CompleteMultiUpload(CompleteMultipartUploadRequest request);

void CompleteMultiUpload(CompleteMultipartUploadRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

```C#
try
{
	string bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
	string key = "exampleobject"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
	string uploadId ="xxxxxxxx"; //멀티파트 업로드 초기화로 반환된 uploadId
	CompleteMultipartUploadRequest request = new CompleteMultipartUploadRequest(bucket, key, uploadId);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//일정 순서로 업로드된 파트 번호를 설정하며, partNumber에 따라 증가
	request.SetPartNumberAndETag(1, "partNumber1 eTag");
	//요청 실행
	CompleteMultipartUploadResult result = cosXml.CompleteMultiUpload(request);
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

/**
//비동기화 방법
string bucket = "examplebucket-1250000000". //버킷, 형식: BucketName-APPID
string key = "exampleobject". //객체의 버킷에서의 위치, 즉 객체 키입니다.
string uploadId ="xxxxxxxx"; //멀티파트 업로드로 반환된 uploadId 초기화
CompleteMultipartUploadRequest request = new CompleteMultipartUploadRequest(bucket, key, uploadId);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//일정 순서로 업로드된 파트 번호를 설정하며, partNumber에 따라 증가
request.SetPartNumberAndETag(1, "partNumber1 eTag");
//요청 실행
cosXml.CompleteMultiUpload(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		CompleteMultipartUploadResult result = result as CompleteMultipartUploadResult;
		Console.WriteLine(result.GetResultInfo());

	},
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
   {
		//요청 실패
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	});
*/
```

#### 매개변수 설명

| 매개변수 이름            | 설정 방법                | 설명                                                         | 유형                       |
| ------------------- | ----------------------- | ------------------------------------------------------------ | -------------------------- |
| bucket              | 구축 방법                | 버킷 이름, 형식: BucketName-APPID                           | string                     |
| key                 | 구축 방법 또는 SetCosPath | COS에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324) | string                     |
| uploadId | 구축 방법 또는 SetUploadId | 지정 멀티파트 업로드의 uploadId 표시 | string |
| partNumber | SetPartNumberAndETag | 지정 파트의 번호 표시, 반드시 >= 1 | int |
| eTag | SetPartNumberAndETag | 지정 파트의 업로드로 반환된 eTag 표시 | string |
| partNumberAndETags | SetPartNumberAndETag | 파트의 번호 및 업로드 반환된 eTag 표시 |`Dictionary<int, string> `|
| signStartTimeSecond | SetSign                 | 서명 유효기간 시작 시간                                           | long                       |
| durationSecond      | SetSign                 | 서명 유효 기간                                               | long                       |
| headerKeys               | SetSign                | 서명에 검증 헤더 유무                                          | `List<string>`              |
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명

CompleteMultipartUploadResult를 통해 요청의 결과를 반환합니다.

| 멤버 변수       |유형                                                         | 설명                                                       |
| -------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode       | int                                                          | HTTP 코드,  [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다 |
| CompleteResult | [CompleteMultipartUploadResult](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/CompleteResult.cs) | 모든 파트 업로드 성공 정보 반환                                 |

> ?작업 실패 시, 시스템은 [CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 또는 [CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 비정상을 throw합니다.

### <span id = "ABORT_MULIT_UPLOAD"> 업로드된 파트 삭제 </span>

#### 기능 설명

하나의 멀티파트 업로드를 취소하고 이미 업로드된 파트를 삭제합니다(Abort Multipart Upload).

#### 방식 프로토타입

```C#
AbortMultipartUploadResult AbortMultiUpload(AbortMultipartUploadRequest request);

void AbortMultiUpload(AbortMultipartUploadRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

```C#
try
{
	string bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
	string key = "exampleobject"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
	string uploadId ="xxxxxxxx"; //멀티파트 업로드 초기화로 반환된 uploadId
	AbortMultipartUploadRequest request = new AbortMultipartUploadRequest(bucket, key, uploadId);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//요청 실행
	AbortMultipartUploadResult result = cosXml.AbortMultiUpload(request);
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

/**
//비동기화 방법
string bucket = "examplebucket-1250000000". //버킷, 형식: BucketName-APPID
string key = "exampleobject". //객체의 버킷에서의 위치, 즉 객체 키입니다.
string uploadId ="xxxxxxxx"; //멀티파트 업로드로 반환된 uploadId 초기화
AbortMultipartUploadRequest request = new AbortMultipartUploadRequest(bucket, key, uploadId);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//요청 실행
cosXml.AbortMultiUpload(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		AbortMultipartUploadResult result = result as AbortMultipartUploadResult;
		Console.WriteLine(result.GetResultInfo());

	},
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		//요청 실패
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### 매개변수 설명

|매개변수 이름            | 설정 방법                | 설명                                                         | 유형           |
| ------------------- | ----------------------- | ------------------------------------------------------------ | -------------- |
| bucket              | 구축 방법                | 버킷 이름, 형식: BucketName-APPID                           | string         |
| key                 | 구축 방법 또는 SetCosPath | COS에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324) | string         |
| uploadId            | 구축 방법 또는 SetUploadId | 지정 멀티파트 업로드의 uploadId 표시 | string         |
| signStartTimeSecond | SetSign                 | 서명 유효기간 시작 시간                                           | long           |
| durationSecond      | SetSign                 | 서명 유효 기간                                               | long           |
| headerKeys               | SetSign                | 서명에 검증 헤더 유무                                          | `List<string>`              |
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명

AbortMultipartUploadResult를 통해 요청의 결과를 반환합니다.

| 멤버 변수 |유형 | 설명                                                       |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int  | HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다 |

> ?작업 실패 시, 시스템은 [CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 또는 [CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 비정상을 throw합니다.

## 기타 작업

### 보관 객체 복구

#### 기능 설명

보관 객체를 복구합니다(POST Object restore).

#### 방식 프로토타입

```C#
RestoreObjectResult RestoreObject(RestoreObjectRequest request);

void RestoreObject(RestoreObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

```C#
try
{
	string bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
	string key = "exampleobject"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
	RestoreObjectRequest request = new RestoreObjectRequest(bucket, key);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//복구 시간
	request.SetExpireDays(3);
	request.SetTier(COSXML.Model.Tag.RestoreConfigure.Tier.Bulk);

	//요청 실행
	RestoreObjectResult result = cosXml.RestoreObject(request);
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

/**
//비동기화 방법
string bucket = "examplebucket-1250000000". //버킷, 형식: BucketName-APPID
string key = "exampleobject". //객체의 버킷에서의 위치, 즉 객체 키입니다.
RestoreObjectRequest request = new RestoreObjectRequest(bucket, key);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//복구 시간
request.SetExpireDays(3);
request.SetTier(COSXML.Model.Tag.RestoreConfigure.Tier.Bulk);
//요청 실행
cosXml.RestoreObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		RestoreObjectResult result = cosResult as RestoreObjectResult;
		Console.WriteLine(result.GetResultInfo());

	},
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		//요청 실패
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### 매개변수 설명

| 매개변수 이름            | 설정 방법               | 설명                                                         | 유형                  |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------- |
| bucket              | 구축 방법               | 버킷 이름, 형식: BucketName-APPID                           | string                |
| key                 | 구축 방법 또는 SetCosPath | COS에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324) | string                |
| days                | SetExpireDays          | 임시 복제본의 만료 시간 설정                                       | int                   |
| tier                | SetTier                | 데이터 복구 시, Tier는 CAS가 지원하는 세 가지 복구 유형으로 지정될 수 있습니다. 즉, Expedited, Standard, Bulk입니다 | RestoreConfigure.Tier |
| signStartTimeSecond | SetSign                | 서명 유효기간 시작 시간                                           | long                  |
| durationSecond      | SetSign                | 서명 유효 기간                                               | long                  |
| headerKeys               | SetSign                | 서명에 검증 헤더 유무                                          | `List<string>`              |
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명

RestoreObjectResult를 통해 요청의 결과를 반환합니다.

| 멤버 변수 |유형 | 설명                                                       |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int  | HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다 |

> ?작업 실패 시, 시스템은 [CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 또는 [CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 비정상을 throw합니다.

### 객체 ACL 설정

#### 기능 설명

객체 액세스 권한 제어 리스트(ACL)를 설정합니다(Put Object ACL).

#### 방식 프로토타입

```C#
PutObjectACLResult PutObjectACL(PutObjectACLRequest request);

void PutObjectACL(PutObjectACLRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

```C#
try
{
	string bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
	string key = "exampleobject"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
	PutObjectACLRequest request = new PutObjectACLRequest(bucket, key);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//비공개 읽기/쓰기 권한 설정
	request.SetCosACL(CosACL.PRIVATE);
	//1131975903 계정 읽기 권한 부여
	COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount();
	readAccount.AddGrantAccount("1131975903", "1131975903");
	request.SetXCosGrantRead(readAccount);
	//요청 실행
	PutObjectACLResult result = cosXml.PutObjectACL(request);
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

/**
//비동기화 방법
string bucket = "examplebucket-1250000000". //버킷, 형식: BucketName-APPID
string key = "exampleobject". //객체의 버킷에서의 위치, 즉 객체 키입니다.
PutObjectACLRequest request = new PutObjectACLRequest(bucket, key);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//비공개 읽기/쓰기 권한 설정
request.SetCosACL(CosACL.PRIVATE);
//1131975903 계정 읽기 권한 부여
COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount();
readAccount.AddGrantAccount("1131975903", "1131975903");
request.SetXCosGrantRead(readAccount);
//요청 실행
cosXml.PutObjectACL(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		PutObjectACLResult result = cosResult as PutObjectACLResult;
		Console.WriteLine(result.GetResultInfo());

	},
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		//요청 실패
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### 매개변수 설명

| 매개변수 이름            | 설정 방법                                                  | 설명                                                         | 유형           |
| ------------------- | --------------------------------------------------------- | ------------------------------------------------------------ | -------------- |
| bucket              | 구축 방법                                                  | 버킷 이름, 형식: BucketName-APPID                           | string         |
| key                 | 구축 방법 또는 SetCosPath | COS에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324) | string         |
| cosAcl | SetCosAcl | 버킷의 acl 권한 설정 | string |
| grandtAccout | SetXCosGrantRead 또는 SetXCosGrantWrite 또는 SetXCosReadWrite | 사용자에게 읽기/쓰기 권한 부여 |GrantAccount|
| signStartTimeSecond | SetSign                                                   | 서명 유효기간 시작 시간                                           | long           |
| durationSecond      | SetSign                                                   | 서명 유효 기간                                               | long           |
| headerKeys               | SetSign                | 서명에 검증 헤더 유무                                          | `List<string>`              |
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명

PutObjectACLResult를 통해 요청의 결과를 반환합니다.

| 멤버 변수 |유형 | 설명                                                       |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int  | HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다 |

> ?작업 실패 시, 시스템은 [CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 또는 [CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 비정상을 throw합니다.

### 객체 ACL 획득

#### 기능 설명

객체 액세스 권한 제어 리스트(ACL)를 획득합니다(Get Object ACL).

#### 방식 프로토타입

```C#
GetObjectACLResult GetObjectACL(GetObjectACLRequest request);

void GetObjectACL(GetObjectACLRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

```C#
try
{
	string bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
	string key = "exampleobject"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
	GetObjectACLRequest request = new GetObjectACLRequest(bucket, key);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//요청 실행
	GetObjectACLResult result = cosXml.GetObjectACL(request);
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

/**
//비동기화 방법
string bucket = "examplebucket-1250000000". //버킷, 형식: BucketName-APPID
string key = "exampleobject". //객체의 버킷에서의 위치, 즉 객체 키입니다.
GetObjectACLRequest request = new GetObjectACLRequest(bucket, key);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//요청 실행
cosXml.GetObjectACL(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		GetObjectACLResult result = cosResult as GetObjectACLResult;
		Console.WriteLine(result.GetResultInfo());

	},
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		//요청 실패
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### 매개변수 설명

| 매개변수 이름            | 설정 방법               | 설명                                                         | 유형           |
| ------------------- | ---------------------- | ------------------------------------------------------------ | -------------- |
| bucket              | 구축 방법               | 버킷 이름, 형식: BucketName-APPID                           | string         |
| key                 | 구축 방법 또는 SetCosPath | COS에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324) | string         |
| signStartTimeSecond | SetSign                | 서명 유효기간 시작 시간                                           | long           |
| durationSecond      | SetSign                | 서명 유효 기간                                               | long           |
| headerKeys               | SetSign                | 서명에 검증 헤더 유무                                          | `List<string>`              |
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명

GetObjectACLResult를 통해 요청의 결과를 반환합니다.

| 멤버 변수            |유형                                                         | 설명                                                       |
| ------------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode            | int                                                          | HTTP 코드,  [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다 |
| accessControlPolicy | [AccessControlPolicy](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/AccessControlPolicy.cs) | 객체의 액세스 권한 리스트 정보 반환 |

> ?작업 실패 시, 시스템은 [CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 또는 [CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 비정상을 throw합니다.
