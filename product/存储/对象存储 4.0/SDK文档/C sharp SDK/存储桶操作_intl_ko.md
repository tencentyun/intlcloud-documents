## 소개

본 문서는 버킷의 기본 조작 및 ACL의 관련 API 및 SDK 예제 코드를 소개합니다.

**기본 조작**

| API                                                          | 조작 이름             | 조작 설명                           |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://cloud.tencent.com/document/product/436/8291) | 버킷 리스트 획득     | 지정 계정의 모든 버킷 리스트를 획득합니다     |
| [PUT Bucket](https://cloud.tencent.com/document/product/436/7738) | 버킷 생성         | 지정 계정에 버킷 하나를 생성합니다         |
| [HEAD Bucket](https://cloud.tencent.com/document/product/436/7735) | 버킷 및 그의 권한 조회 | 버킷이 있는지 그리고 액세스 권한이 있는지 여부를 조회합니다 |
| [GET Bucket location](https://cloud.tencent.com/document/product/436/8275) | 버킷 지역 정보 획득 | 버킷 소재 지역 정보를 획득합니다           |
| [DELETE Bucket](https://cloud.tencent.com/document/product/436/7732) | 버킷 삭제         | 지정 계정의 빈 버킷을 삭제합니다           |

**ACL**

| API                                                          | 조작 이름         | 조작 설명              |
| ------------------------------------------------------------ | -------------- | --------------------- |
| [PUT Bucket acl](https://cloud.tencent.com/document/product/436/7737) | 버킷 ACL 설정 | 버킷의 ACL 구성을 설정합니다 |
| [GET Bucket acl](https://cloud.tencent.com/document/product/436/7733) | 버킷 ACL 획득 | 버킷의 ACL 구성을 획득합니다 |

## 기본 조작

### 버킷 리스트 획득

#### 기능 설명

지정한 계정의 모든 버킷 리스트(Bucket list)를 획득하는 데 사용합니다.

#### 방식 프로토타입

```C#
GetServiceResult GetService(GetServiceRequest request);

void GetService(GetServiceRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

```
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

/**
//비동기화 방법
GetServiceRequest request = new GetServiceRequest();
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
cosXml.GetService(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		GetServiceResult result = cosResult as GetServiceResult;
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

| 매개변수 이름            | 설정 방법 | 설명                            | 유형           |
| ------------------- | -------- | ------------------------------- | -------------- |
| signStartTimeSecond | SetSign                  | 서명 유효기간의 시작 시간                                           | long                 |
| durationSecond      | SetSign  | 서명 유효 기간                  | long           |
| headerKeys               | SetSign                | 서명에 대해 헤더 검증 여부                                          | `List<string>`              |
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명

GetServiceResult를 통해 요청 결과를 반환합니다.

| 멤버 변수         | 유형                                                         | 설명                                                     |
| ---------------- | ------------------------------------------------------------ | -------------------------------------------------------- |
| httpCode         | int                                                          | HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다 |
|listAllMyBuckets|[ListAllMyBuckets](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListAllMyBuckets.cs)| 지정 계좌의 버킷 리스트의 정보를 반환합니다                         |

> ?작업 실패 시, 시스템은 [CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 또는 [CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 비정상을 throw합니다.

### 버킷 생성

#### 기능 설명

버킷 하나를 생성합니다(Put Bucket).

#### 방식 프로토타입

```C#
PutBucketResult PutBucket(PutBucketRequest request);

void PutBucket(PutBucketRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

```C#
try
{
	string bucket = "examplebucket-1250000000"; //형식: BucketName-APPID
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

/**
//비동기화 방법
string bucket = "examplebucket-1250000000". //형식: BucketName-APPID
PutBucketRequest request = new PutBucketRequest(bucket);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
cosXml.PutBucket(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		PutBucketResult result = cosResult as PutBucketResult;
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

PutBucketResult를 통해 요청의 결과를 반환합니다.

| 멤버 변수 | 유형 | 설명                                                     |
| -------- | ---- | -------------------------------------------------------- |
| httpCode                        | int            | HTTP 코드, [200, 300) 사이려면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다 |

> ?작업 실패 시, 시스템은 [CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 또는 [CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 비정상을 throw합니다.

### 버킷 조회

#### 기능 설명

지정 버킷이 존재하는지 여부를 조회합니다(Head Bucket).

#### 방식 프로토타입

```C#
HeadBucketResult HeadBucket(HeadBucketRequest request);

void HeadBucket(HeadBucketRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

```C#
try
{
	string bucket = "examplebucket-1250000000"; //형식: BucketName-APPID
	HeadBucketRequest request = new HeadBucketRequest(bucket);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//요청 실행
	HeadBucketResult result = cosXml.HeadBucket(request);
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
HeadBucketRequest request = new HeadBucketRequest(bucket);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
cosXml.HeadBucket(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		HeadBucketResult result = cosResult as HeadBucketResult;
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

### 버킷 지역 획득

#### 기능 설명

지정 버킷이 있는 지역 정보를 획득합니다(Get Bucket Location).

#### 방식 프로토타입

```C#
GetBucketLocationResult GetBucketLocation(GetBucketLocationRequest request);

void GetBucketLocation(GetBucketLocationRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

```C#
try
{
	string bucket = "examplebucket-1250000000"; //형식: BucketName-APPID
	GetBucketLocationRequest request = new GetBucketLocationRequest(bucket);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//요청 실행
	GetBucketLocationResult result = cosXml.GetBucketLocation(request);
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
GetBucketLocationRequest request = new GetBucketLocationRequest(bucket);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
cosXml.GetBucketLocation(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		GetBucketLocationResult result = cosResult as GetBucketLocationResult;
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

GetBucketLocationResult를 통해 요청의 결과를 반환합니다.

| 멤버 변수           |유형                                                         | 설명                                                     |
| ------------------ | ------------------------------------------------------------ | -------------------------------------------------------- |
| httpCode           | int                                                          | HTTP 코드, [200, 300) 사이려면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다 |
|locationConstraint|[LocationConstraint](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/LocationConstraint.cs)| 버킷 지역 정보를 반환합니다                                     |

> ?작업 실패 시, 시스템은 [CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 또는 [CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 비정상을 throw합니다.

### 버킷 삭제

#### 기능 설명

지정된 버킷을 삭제합니다(Delete Bucket).

#### 방식 프로토타입

```C#
DeleteBucketResult DeleteBucket(DeleteBucketRequest request);

void DeleteBucket(DeleteBucketRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

```C#
try
{
	string bucket = "examplebucket-1250000000"; //형식: BucketName-APPID
	DeleteBucketRequest request = new DeleteBucketRequest(bucket);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//요청 실행
	DeleteBucketResult result = cosXml.DeleteBucket(request);
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
DeleteBucketRequest request = new DeleteBucketRequest(bucket);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
cosXml.DeleteBucket(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		DeleteBucketResult result = cosResult as DeleteBucketResult;
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

DeleteBucketResult를 통해 요청의 결과를 반환합니다.

| 멤버 변수 | 유형 | 설명                                                     |
| -------- | ---- | -------------------------------------------------------- |
| httpCode                        | int            | HTTP 코드, [200, 300) 사이려면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다 |

> ?작업 실패 시, 시스템은 [CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 또는 [CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 비정상을 throw합니다.

## ACL

### 버킷 ACL 설정

#### 기능 설명

지정 버킷 액세스 권한 제어 리스트(ACL)를 설정합니다(Put Bucket ACL).

#### 방식 프로토타입

```C#
PutBucketACLResult PutBucketACL(PutBucketACLRequest request);

void PutBucketACL(PutBucketACLRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

```C#
try
{
	string bucket = "examplebucket-1250000000"; //형식: BucketName-APPID
	PutBucketACLRequest request = new PutBucketACLRequest(bucket);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//비공개 읽기/쓰기 권한 설정
	request.SetCosACL(CosACL.PRIVATE);
	//1131975903 계정 읽기 권한 부여
	COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount();
	readAccount.AddGrantAccount("1131975903", "1131975903");
	request.SetXCosGrantRead(readAccount);
	//요청 실행
	PutBucketACLResult result = cosXml.PutBucketACL(request);
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
PutBucketACLRequest request = new PutBucketACLRequest(bucket);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//비공개 읽기/쓰기 권한 설정
request.SetCosACL(CosACL.PRIVATE);
//1131975903 계정 읽기 권한 부여
COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount();
readAccount.AddGrantAccount("1131975903", "1131975903");
request.SetXCosGrantRead(readAccount);
//요청 실행
cosXml.PutBucketACL(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		PutBucketACLResult result = cosResult as PutBucketACLResult;
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

|매개변수 이름            | 설정 방법                                                  | 설명                               | 유형           |
| ------------------- | --------------------------------------------------------- | ---------------------------------- | -------------- |
| bucket              | 구축 방법                                                  | 버킷 이름, 형식: BucketName-APPID | string         |
| cosAcl              | SetCosAcl                                                 | 버킷의 ACL 권한 설정              | string         |
|grandtAccout|SetXCosGrantRead 또는 SetXCosGrantWrite 또는 SetXCosReadWrite | 사용자에게 읽기/쓰기 권한 부여 | GrantAccount   |
| signStartTimeSecond | SetSign                                                   | 서명 유효기간 시작 시간                                           | long                 |
| durationSecond     | SetSign                | 서명 유효 기간                                                   | long           |
| headerKeys               | SetSign                                                   | 서명에 검증 헤더 유무                | `List<string>` |
| queryParameterKeys  | SetSign                                                   | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명

PutBucketACLResult를 통해 요청의 결과를 반환합니다.

| 멤버 변수 | 유형 | 설명                                                     |
| -------- | ---- | -------------------------------------------------------- |
| httpCode                        | int            | HTTP 코드, [200, 300) 사이려면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다 |

> ?작업 실패 시, 시스템은 [CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 또는 [CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 비정상을 throw합니다.

### 버킷 ACL 획득

#### 기능 설명

지정 버킷의 액세스 권한 제어 리스트(ACL)를 획득합니다(Get Bucket ACL).

#### 방식 프로토타입

```C#
GetBucketACLResult GetBucketACL(GetBucketACLRequest request);

void GetBucketACL(GetBucketACLRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시

```C#
try
{
	string bucket = "examplebucket-1250000000"; //형식: BucketName-APPID
	GetBucketACLRequest request = new GetBucketACLRequest(bucket);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//요청 실행
	GetBucketACLResult result = cosXml.GetBucketACL(request);
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
GetBucketACLRequest request = new GetBucketACLRequest(bucket);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
cosXml.GetBucketACL(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		GetBucketACLResult result = cosResult as GetBucketACLResult;
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

GetBucketACLResult를 통해 요청의 결과를 반환합니다.

| 멤버 변수            |유형                                                         | 설명                                                     |
| ------------------- | ------------------------------------------------------------ | -------------------------------------------------------- |
| httpCode            | int                                                          | HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다 |
|accessControlPolicy|[AccessControlPolicy](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/AccessControlPolicy.cs)| 버킷 액세스 권한 리스트 정보를 반환합니다 |

> ?작업 실패 시, 시스템은 [CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 또는 [CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 비정상을 throw합니다.

