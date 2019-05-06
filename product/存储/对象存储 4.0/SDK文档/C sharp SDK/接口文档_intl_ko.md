COS 서비스 XML C# SDK 작업이 성공하면 각 API에 해당하는 결과를 반환하며, 실패하면 CosClientException과
 CosServerException을 throw합니다. 그 중 CosClientException은 매개변수가 비어 있거나 네트워크 연결이 실패하는 등의 클라이언트 비정상을 나타냅니다. CosServerException은 존재하지 않는 파일 액세스, 파일 액세스 권한 없음 등 서버 요구에 부합하지 않는 클라이언트 요청을 처리하여 반환되는 오류를 나타냅니다. 자세한 내용은 [SDK 비정상 설명](#COS_EXCEPTION)을 참조하십시오.

SDK에는 API 요청별로 동기화와 비동기 두 가지 요청 방식을 제공하였습니다.

## Service API 설명

### 버킷 리스트 획득

#### 기능 설명

지정한 계정의 모든 버킷 리스트를 획득하는 데 사용합니다.

#### 방식 프로토타입
```C#
GetServiceResult GetService(GetServiceRequest request);

void GetService(GetServiceRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명
GetServiceResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|
|listAllMyBuckets|[ListAllMyBuckets](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListAllMyBuckets.cs)|지정 계정의 버킷 리스트 정보를 반환합니다|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

## Bucket API 설명

### 버킷 생성

#### 기능 설명

버킷을 생성합니다(Put Bucket).

#### 방식 프로토타입
```C#
PutBucketResult PutBucket(PutBucketRequest request);

void PutBucket(PutBucketRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시
```C#
try
{
	string bucket = "test-1253960454"; //형식: bucketname-appid
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
string bucket = "test-1253960454"; //형식: bucketname-appid
PutBucketRequest request = new PutBucketRequest(bucket).
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명
PutBucketResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

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
	string bucket = "test-1253960454"; //형식: bucketname-appid
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
string bucket = "test-1253960454"; //형식: bucketname-appid
DeleteBucketRequest request = new DeleteBucketRequest(bucket).
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명
DeleteBucketResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

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
	string bucket = "test-1253960454"; //형식: bucketname-appid
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
string bucket = "test-1253960454"; //형식: bucketname-appid
HeadBucketRequest request = new HeadBucketRequest(bucket).
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

#### 매개변수 설명
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명
HeadBucketResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

### 객체 리스트 획득

#### 기능 설명

지정 버킷의 모든 객체를 획득합니다(Object List).

#### 방식 프로토타입
```C#
GetBucketResult GetBucket(GetBucketRequest request);

void GetBucket(GetBucketRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시
```C#
try
{
	string bucket = "test-1253960454"; //형식: bucketname-appid
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
string bucket = "test-1253960454"; //형식: bucketname-appid
GetBucketRequest request = new GetBucketRequest(bucket).
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명
GetBucketResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|
|listBucket|[ListBucket](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListBucket.cs)|버킷 객체 리스트 정보 반환|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

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
	string bucket = "test-1253960454"; //형식: bucketname-appid
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
string bucket = "test-1253960454"; //형식: bucketname-appid
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명
GetBucketLocationResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|
|locationConstraint|[LocationConstraint](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/LocationConstraint.cs)|버킷 지역 정보 반환|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다


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
	string bucket = "test-1253960454"; //형식: bucketname-appid
	PutBucketACLRequest request = new PutBucketACLRequest(bucket);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//비공개 읽기/쓰기 권한 설정
	request.SetCosACL(CosACL.PRIVATE);
	//1131975903 계정 읽기 권한 부여
	COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount();
	readAccount.AddGrantAccount("1131975903", "1131975903");
	request.setXCosGrantRead(readAccount);
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
string bucket = "test-1253960454"; //형식: bucketname-appid
PutBucketACLRequest request = new PutBucketACLRequest(bucket);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//비공개 읽기/쓰기 권한 설정
request.SetCosACL(CosACL.PRIVATE);
//1131975903 계정 읽기 권한 부여
COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount();
readAccount.AddGrantAccount("1131975903", "1131975903");
request.setXCosGrantRead(readAccount);
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|cosAcl|SetCosAcl|버킷의 acl 권한 설정|string|
|grandtAccout|SetXCosGrantRead 또는 SetXCosGrantWrite 또는 SetXCosReadWrite|사용자 읽기/쓰기 권한 부여|GrantAccount|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명
PutBucketACLResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

### 버킷 ACL 획득

#### 기능 설명

지정 버킷 액세스 권한 제어 리스트(ACL)를 획득합니다(Get Bucket ACL).

#### 방식 프로토타입
```C#
GetBucketACLResult GetBucketACL(GetBucketACLRequest request);

void GetBucketACL(GetBucketACLRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시
```C#
try
{
	string bucket = "test-1253960454"; //형식: bucketname-appid
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
string bucket = "test-1253960454"; //형식: bucketname-appid
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명
GetBucketACLResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|
|accessControlPolicy|[AccessControlPolicy](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/AccessControlPolicy.cs)|버킷 액세스 권한 리스트 정보 반환|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

### 버킷의 CORS 구성 설정

#### 기능 설명

지정 버킷의 CORS 구성 정보를 설정합니다(Put Bucket CORS).

#### 방식 프로토타입
```C#
PutBucketCORSResult PutBucketCORS(PutBucketCORSRequest request);

void PutBucketCORS(PutBucketCORSRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시
```C#
try
{
	string bucket = "test-1253960454"; //형식: bucketname-appid
	PutBucketCORSRequest request = new PutBucketCORSRequest(bucket);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//크로스 도메인 리소스 공유 CORS 구성 설정
	COSXML.Model.Tag.CORSConfiguration.CORSRule corsRule = new COSXML.Model.Tag.CORSConfiguration.CORSRule();
	corsRule.id = "corsconfigureId";
	corsRule.maxAgeSeconds = 6000;
	corsRule.allowedOrigin = "http://cloud.tencent.com";

	corsRule.allowedMethods = new List<string>();
	corsRule.allowedMethods.Add("PUT");

	corsRule.allowedHeaders = new List<string>();
	corsRule.allowedHeaders.Add("Host");

	corsRule.exposeHeaders = new List<string>();
	corsRule.exposeHeaders.Add("x-cos-meta-x1");

	request.SetCORSRule(corsRule);

	//요청 실행
	PutBucketCORSResult result = cosXml.PutBucketCORS(request);
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
string bucket = "test-1253960454"; //형식: bucketname-appid
PutBucketCORSRequest request = new PutBucketCORSRequest(bucket);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);

//크로스 도메인 리소스 공유 CORS 구성 설정
COSXML.Model.Tag.CORSConfiguration.CORSRule corsRule = new COSXML.Model.Tag.CORSConfiguration.CORSRule();
corsRule.id = "corsconfigureId";
corsRule.maxAgeSeconds = 6000;
corsRule.allowedOrigin = "http://cloud.tencent.com";

corsRule.allowedMethods = new List<string>();
corsRule.allowedMethods.Add("PUT");

corsRule.allowedHeaders = new List<string>();
corsRule.allowedHeaders.Add("Host");

corsRule.exposeHeaders = new List<string>();
corsRule.exposeHeaders.Add("x-cos-meta-x1");

request.SetCORSRule(corsRule);

cosXml.PutBucketCORS(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		PutBucketCORSResult result = cosResult as PutBucketCORSResult;
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|corsRule|SetCORSRule|버킷의 CORS 구성 설정|CORSConfiguration.CORSRule|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명
PutBucketCORSResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

### 버킷 CORS 구성 획득

#### 기능 설명

지정 버킷의 CORS 구성 정보를 획득합니다(Get Bucket CORS).

#### 방식 프로토타입
```C#
GetBucketCORSResult GetBucketCORS(GetBucketCORSRequest request);

void GetBucketCORS(GetBucketCORSRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시
```C#
try
{
	string bucket = "test-1253960454"; //형식: bucketname-appid
	GetBucketCORSRequest request = new GetBucketCORSRequest(bucket);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//요청 실행
	GetBucketCORSResult result = cosXml.GetBucketCORS(request);
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
string bucket = "test-1253960454"; //형식: bucketname-appid
GetBucketCORSRequest request = new GetBucketCORSRequest(bucket);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//요청 실행
cosXml.GetBucketCORS(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		GetBucketCORSResult result = cosResult as GetBucketCORSResult;
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명
GetBucketCORSResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|
|corsConfiguration|[CORSConfiguration](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/CORSConfiguration.cs)|버킷 CORS 구성 정보를 반환합니다|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

### 버킷 CORS 구성 삭제

#### 기능 설명

지정 버킷의 CORS 구성을 삭제합니다(Delete Bucket CORS).

#### 방식 프로토타입
```C#
DeleteBucketCORSResult DeleteBucketCORS(DeleteBucketCORSRequest request);

void DeleteBucketCORS(DeleteBucketCORSRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시
```C#
try
{
	string bucket = "test-1253960454"; //형식: bucketname-appid
	DeleteBucketCORSRequest request = new DeleteBucketCORSRequest(bucket);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//요청 실행
	DeleteBucketCORSResult result = cosXml.DeleteBucketCORS(request);
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
string bucket = "test-1253960454"; //형식: bucketname-appid
DeleteBucketCORSRequest request = new DeleteBucketCORSRequest(bucket);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//요청 실행
cosXml.DeleteBucketCORS(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		DeleteBucketCORSResult result = cosResult as DeleteBucketCORSResult;
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명
DeleteBucketCORSResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다


### 버킷의 수명 주기 설정

#### 기능 설명

지정 버킷의 수명 주기 구성 정보(Lifecycle)를 설정합니다 (Put Bucket LifeCycle).

#### 방식 프로토타입
```C#
PutBucketLifecycleResult PutBucketLifecycle(PutBucketLifecycleRequest request);

void PutBucketLifecycle(PutBucketLifecycleRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시
```C#
try
{
	string bucket = "test-1253960454"; //형식: bucketname-appid
	PutBucketLifecycleRequest request = new PutBucketLifecycleRequest(bucket);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//수명 주기 설정
	COSXML.Model.Tag.LifecycleConfiguration.Rule rule = new COSXML.Model.Tag.LifecycleConfiguration.Rule();
	rule.id = "lfiecycleConfigureId";
	rule.status = "Enabled"; //Enabled，Disabled

	rule.filter = new COSXML.Model.Tag.LifecycleConfiguration.Filter();
	rule.filter.prefix = "2/";

	//파트 만료 삭제 작업 지정
	rule.abortIncompleteMultiUpload = new COSXML.Model.Tag.LifecycleConfiguration.AbortIncompleteMultiUpload();
	rule.abortIncompleteMultiUpload.daysAfterInitiation = 2;

	request.SetRule(rule);

	//요청 실행
	PutBucketLifecycleResult result = cosXml.PutBucketLifecycle(request);
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
string bucket = "test-1253960454"; //형식: bucketname-appid
PutBucketLifecycleRequest request = new PutBucketLifecycleRequest(bucket);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//수명 주기 설정
COSXML.Model.Tag.LifecycleConfiguration.Rule rule = new COSXML.Model.Tag.LifecycleConfiguration.Rule();
rule.id = "lfiecycleConfigureId";
rule.status = "Enabled"; //Enabled，Disabled

rule.filter = new COSXML.Model.Tag.LifecycleConfiguration.Filter();
rule.filter.prefix = "2/";

rule.abortIncompleteMultiUpload = new COSXML.Model.Tag.LifecycleConfiguration.AbortIncompleteMultiUpload();
rule.abortIncompleteMultiUpload.daysAfterInitiation = 2;

request.SetRule(rule);

//요청 실행
cosXml.PutBucketLifecycle(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		PutBucketLifecycleResult result = cosResult as PutBucketLifecycleResult;
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|rule|SetRule|버킷의 수명 주기 구성 설정|LifecycleConfiguration.Rule|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명
PutBucketLifecycleResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

### 버킷의 수명 주기 획득

#### 기능 설명

지정 버킷의 수명 주기(Lifecycle)를 획득합니다(Get Bucket Lifecycle).

#### 방식 프로토타입
```C#
GetBucketLifecycleResult GetBucketLifecycle(GetBucketLifecycleRequest request);

void GetBucketLifecycle(GetBucketLifecycleRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시
```C#
try
{
	string bucket = "test-1253960454"; //형식: bucketname-appid
	GetBucketLifecycleRequest request = new GetBucketLifecycleRequest(bucket);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//요청 실행
	GetBucketLifecycleResult result = cosXml.GetBucketLifecycle(request);
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
string bucket = "test-1253960454"; //형식: bucketname-appid
GetBucketLifecycleRequest request = new GetBucketLifecycleRequest(bucket);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//요청 실행
cosXml.GetBucketLifecycle(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		 GetBucketLifecycleResult result = cosResult as GetBucketLifecycleResult;
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명
GetBucketLifecycleResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|
|lifecycleConfiguration|[LifecycleConfiguration](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/LifecycleConfiguration.cs)|버킷의 수명 주기 구성 정보 반환|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

### 버킷의 수명 주기 삭제

#### 기능 설명

지정 버킷의 수명 주기(Lifecycle)를 삭제합니다(Delete Bucket Lifecycle).

#### 방식 프로토타입
```C#
DeleteBucketLifecycleResult DeleteBucketLifecycle(DeleteBucketLifecycleRequest request);

void DeleteBucketLifecycle(DeleteBucketLifecycleRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시
```C#
try
{
	string bucket = "test-1253960454"; //형식: bucketname-appid
	DeleteBucketLifecycleRequest request = new DeleteBucketLifecycleRequest(bucket);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//요청 실행
	DeleteBucketLifecycleResult result = cosXml.DeleteBucketLifecycle(request);
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
string bucket = "test-1253960454"; //형식: bucketname-appid
DeleteBucketLifecycleRequest request = new DeleteBucketLifecycleRequest(bucket);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//요청 실행
cosXml.DeleteBucketLifecycle(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		DeleteBucketLifecycleResult result = cosResult as DeleteBucketLifecycleResult;
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명
DeleteBucketLifecycleResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

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
	string bucket = "test-1253960454"; //형식: bucketname-appid
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
string bucket = "test-1253960454"; //형식: bucketname-appid
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명
ListMultiUploadsResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|
|listMultipartUploads|[ListMultipartUploads](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListMultipartUploads.cs)|버킷 중 진행 중인 모든 멀티파드 업로드 정보 반환|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

## Object API 설명

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
	string bucket = "test-1253960454"; //버킷, 형식: bucketname-appid
	string key = "test.txt"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
	string srcPath = @"F:\test.txt"；//로컬 파일 경로
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
string bucket = "test-1253960454"; //버킷, 형식: bucketname-appid
string key = "test.txt"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
string srcPath = @"F:\test.txt";  //로컬 파일 경로
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|key|구축 방법 또는 SetCosPath|cos에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324)|string|
|srcPath|구축 방법|cos에 업로드된 로컬 파일의 절대 경로|string|
|data|구축 방법|cos에 업로드된 바이트 배열|byte[]|
|progressCallback|SetCosProgressCallback|업로드 진행률 콜백 설정|Callback.OnProgressCallback|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명
PutObjectResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|
|eTag|string|객체의 eTag를 반환합니다|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

### 멀티파트 업로드

멀티파트 업로드가 포함할 수 있는 작업:

멀티파트 업로드 객체: 멀티파트 업로드 초기화, 파트 업로드, 모든 파트 업로드 완료.

멀티파트 업로드 재개: 업로드된 파트 조회, 파트 업로드, 모든 파트 업로드 완료.

업로드된 파트 삭제.

#### <span id = "INIT_MULIT_UPLOAD"> 멀티파트 업로드 초기화 </span>

##### 기능 설명

멀티파트 업로드를 초기화하고, 해당하는 uploadId를 획득합니다(Initiate Multipart Upload).

##### 방식 프로토타입
```C#
InitMultipartUploadResult InitMultipartUpload(InitMultipartUploadRequest request);

void InitMultipartUpload(InitMultipartUploadRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

##### 요청 예시
```C#
try
{
	string bucket = "test-1253960454"; //버킷, 형식: bucketname-appid
	string key = "test.txt"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
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
string bucket = "test-1253960454". //버킷, 형식: bucketname-appid
string key = "test.txt". //객체의 버킷에서의 위치, 즉 객체 키입니다.
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|key|구축 방법 또는 SetCosPath|cos에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324)|string|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

## 반환 결과 설명
InitMultipartUploadResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|
|initMultipartUpload|[InitiateMultipartUpload](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/InitiateMultipartUpload.cs)|초기화된 멀티파트 업로드의 객체 uploadId를 반환합니다|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

#### <span id = "LIST_MULIT_UPLOAD"> 업로드된 파트 조회 </span>

##### 기능 설명

지정 uploadId에 업로드된 파트를 조회합니다(List Parts).

##### 방식 프로토타입
```C#
ListPartsResult ListParts(ListPartsRequest request);

void ListParts(ListPartsRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

##### 요청 예시
```C#
try
{
	string bucket = "test-1253960454"; //버킷, 형식: bucketname-appid
	string key = "test.txt"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
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
string bucket = "test-1253960454". //버킷, 형식: bucketname-appid
string key = "test.txt". //객체의 버킷에서의 위치, 즉 객체 키입니다.
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|key|구축 방법 또는 SetCosPath|cos에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324)|string|
|uploadId|구축 방법 또는 SetUploadId|지정 멀티파트 업로드의 uploadId 표시|string|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

## 반환 결과 설명
ListPartsResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|
|listParts|[ListParts](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListParts.cs)|지정 uploadId의 멀티파트 업로드에 이미 업로드된 파트 정보를 반환합니다|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

#### <span id = "MULIT_UPLOAD_PART"> 멀티파트 업로드 </span>

파트를 업로드합니다(Upload Part).

##### 방식 프로토타입
```C#
UploadPartResult UploadPart(UploadPartRequest request);

void UploadPart(UploadPartRequest, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

##### 요청 예시
```C#
try
{
	string bucket = "test-1253960454"; //버킷, 형식: bucketname-appid
	string key = "test.txt"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
	string uploadId ="xxxxxxxx"; //멀티파트 업로드 초기화로 반환된 uploadId
	int partNumber = 1; //파트 번호, 1에서 시작하는 자연수열이어야 합니다
	string srcPath = @"F:\test.txt"; //로컬 파일 경로
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
string bucket = "test-1253960454"; //버킷, 형식: bucketname-appid
string key = "test.txt"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
string uploadId ="xxxxxxxx"; //멀티파트 업로드 초기화로 반환된 uploadId
int partNumber = 1; //파트 번호, 1에서 시작하는 자연수열이어야 합니다
string srcPath = @"F:\test.txt"; //로컬 파일 경로
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|key|구축 방법 또는 SetCosPath|cos에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324)|string|
|uploadId|구축 방법 또는 SetUploadId|지정 멀티파트 업로드의 uploadId 표시|string|
|partNumber|구축 방법 또는 SetPartNumber|지정 파트의 번호 표시, 반드시 >= 1|int|
|srcPath|구축 방법|cos에 업로드된 로컬 파일의 절대 경로|string|
|data|구축 방법|cos에 업로드된 바이트 배열|byte[]|
|progressCallback|SetCosProgressCallback|업로드 진행률 콜백 설정|Callback.OnProgressCallback|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

## 반환 결과 설명
UploadPartResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|
|eTag|string|객체의 파트 eTag를 반환합니다|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

#### <span id = "COMPLETE_MULIT_UPLOAD"> 모든 파트 업로드 완료 </span>

##### 기능 설명

전체 멀티파트 업로드를 완료합니다(Complete Multipart Upload).

##### 방식 프로토타입
```C#
CompleteMultiUploadResult CompleteMultiUpload(CompleteMultiUploadRequest request);

void CompleteMultiUpload(CompleteMultiUploadRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

##### 요청 예시
```C#
try
{
	string bucket = "test-1253960454"; //버킷, 형식: bucketname-appid
	string key = "test.txt"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
	string uploadId ="xxxxxxxx"; //멀티파트 업로드 초기화로 반환된 uploadId
	CompleteMultiUploadRequest request = new CompleteMultiUploadRequest(bucket, key, uploadId);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//일정 순서로 업로드된 파트 번호를 설정하며, partNumber에 따라 증가
	request.SetPartNumberAndETag(1, "partNumber1 eTag");
	//요청 실행
	CompleteMultiUploadResult result = cosXml.CompleteMultiUpload(request);
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
string bucket = "test-1253960454". //버킷, 형식: bucketname-appid
string key = "test.txt". //객체의 버킷에서의 위치, 즉 객체 키입니다.
string uploadId ="xxxxxxxx"; //멀티파트 업로드로 반환된 uploadId 초기화
CompleteMultiUploadRequest request = new CompleteMultiUploadRequest(bucket, key, uploadId);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//일정 순서로 업로드된 파트 번호를 설정하며, partNumber에 따라 증가
request.SetPartNumberAndETag(1, "partNumber1 eTag");
//요청 실행
cosXml.CompleteMultiUpload(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		CompleteMultiUploadResult result = result as CompleteMultiUploadResult;
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|key|구축 방법 또는 SetCosPath|cos에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324)|string|
|uploadId|구축 방법 또는 SetUploadId|지정 멀티파트 업로드의 uploadId 표시|string|
|partNumber|SetPartNumberAndETag|지정 파트의 번호 표시, 반드시 >= 1|int|
|eTag|SetPartNumberAndETag|지정 파트의 업로드로 반환된 eTag 표시|string|
|partNumberAndETags|SetPartNumberAndETag|파트의 번호 및 업로드로 반환된 eTag 표시 |`Dictionary<int, string> `|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

## 반환 결과 설명
CompleteMultiUploadResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|
|completeMultipartUpload|[CompleteMultipartUploadResult](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/CompleteMultipartUploadResult.cs)|모든 파트 업로드 성공 정보 반환|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

#### <span id = "ABORT_MULIT_UPLOAD"> 업로드된 파트 삭제 </span>

##### 기능 설명

하나의 멀티파트 업로드를 취소하고 이미 업로드된 파트를 삭제합니다(Abort Multipart Upload).

##### 방식 프로토타입
```C#
AbortMultiUploadResult AbortMultiUpload(AbortMultiUploadRequest request);

void AbortMultiUpload(AbortMultiUploadRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

##### 요청 예시
```C#
try
{
	string bucket = "test-1253960454"; //버킷, 형식: bucketname-appid
	string key = "test.txt"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
	string uploadId ="xxxxxxxx"; //멀티파트 업로드 초기화로 반환된 uploadId
	AbortMultiUploadRequest request = new AbortMultiUploadRequest(bucket, key, uploadId);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//요청 실행
	AbortMultiUploadResult result = cosXml.AbortMultiUpload(request);
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
string bucket = "test-1253960454". //버킷, 형식: bucketname-appid
string key = "test.txt". //객체의 버킷에서의 위치, 즉 객체 키입니다.
string uploadId ="xxxxxxxx"; //멀티파트 업로드로 반환된 uploadId 초기화
AbortMultiUploadRequest request = new AbortMultiUploadRequest(bucket, key, uploadId);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//요청 실행
cosXml.AbortMultiUpload(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		AbortMultiUploadResult result = result as AbortMultiUploadResult;
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|key|구축 방법 또는 SetCosPath|cos에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324)|string|
|uploadId|구축 방법 또는 SetUploadId|지정 멀티파트 업로드의 uploadId 표시|string|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

## 반환 결과 설명
AbortMultiUploadResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

### Post 업로드

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
	string bucket = "test-1253960454"; //버킷, 형식: bucketname-appid
	string key = "test.txt"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
	string srcPath = @"F:\test.txt"；//로컬 파일 경로
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
string bucket = "test-1253960454"; //버킷, 형식: bucketname-appid
string key = "test.txt"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
string srcPath = @"F:\test.txt";  //로컬 파일 경로
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|key|구축 방법 또는 SetCosPath|cos에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324)|string|
|srcPath|구축 방법|cos에 업로드된 로컬 파일의 절대 경로|string|
|data|구축 방법|cos에 업로드된 바이트 배열|byte[]|
|progressCallback|SetCosProgressCallback|업로드 진행률 콜백 설정|Callback.OnProgressCallback|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명
PostObjectResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|
|eTag|string|객체의 eTag를 반환합니다|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

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
	string bucket = "test-1253960454"; //버킷, 형식: bucketname-appid
	string key = "test.txt"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
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
string bucket = "test-1253960454". //버킷, 형식: bucketname-appid
string key = "test.txt". //객체의 버킷에서의 위치, 즉 객체 키입니다.
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|key|구축 방법 또는 SetCosPath|cos에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324)|string|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명
HeadObjectResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|
|eTag|string|객체의 eTag를 반환합니다|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

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
	string bucket = "test-1253960454"; //버킷, 형식: bucketname-appid
	string key = "test.txt"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
	string localDir = @"F:\"；//로컬 지정 폴더로 다운로드
	string localFileName = "test.txt"; //로컬 저장할 파일 이름 지정
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
string bucket = "test-1253960454"; //버킷, 형식: bucketname-appid
string key = "test.txt"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
string localDir = @"F:\"；//로컬 지정 폴더로 다운로드
string localFileName = "test.txt"; //로컬 저장할 파일 이름 지정
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|key|구축 방법 또는 SetCosPath|cos에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324)|string|
|localDir|구축 방법|로컬로 다운로드하고 저장할 객체의 절대 폴더 경로|string|
|localFileName|구축 방법|로컬로 다운로드하고 저장할 객체 파일명|string|
|progressCallback|SetCosProgressCallback|다운로드 진행률 콜백 설정|Callback.OnProgressCallback|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명
GetObjectResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|
|eTag|string|객체의 eTag를 반환합니다 |

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

### 객체 복사

객체 복사는 다음 포함: 간편 복사(1M~5G 적용), 멀티파트 복사(5G 같은 대용량 파일 복사에 사용)

##### 간편 복사

한 개의 객체를 다른 한 개의 객체로 복사합니다(Put Object Copy).

##### 방식 프로토타입
```C#
CopyObjectResult CopyObject(CopyObjectRequest request);

void CopyObject(CopyObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

##### 요청 예시
```C#
try
{
	string sourceAppid = "1253960454"; //계정 appid
	string sourceBucket = "source-1253960454"; //"소스 객체가 있는 버킷
	string sourceRegion = "ap-beijing"; //소스 객체의 버킷이 있는 지역
	string sourceKey = "test.txt"; //소스 객체 키
	//소스 객체 속성 구축
	COSXML.Model.Tag.CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceKey);

	string bucket = "test-1253960454"; //버킷, 형식: bucketname-appid
	string key = "copy_test.txt"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
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
string sourceKey = "test.txt". //소스 객체 키
//소스 객체 속성 구축
COSXML.Model.Tag.CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceKey);

string bucket = "test-1253960454". //버킷, 형식: bucketname-appid
string key = "copy_test.txt"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|key|구축 방법 또는 SetCosPath|cos에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324)|string|
|copySource|SetCopySource|복사의 데이터 소스 경로 설명|CopySourceStruct|
|metaDataDirective|SetCopyMetaDataDirective|소스 파일의 메타데이터 복사 또는 업데이트|CosMetaDataDirective|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

## 반환 결과 설명
CopyObjectResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|
|copyObject|[CopyObject](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/CopyObject.cs)|복사 성공의 객체 정보 반환|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

##### 멀티파트 복사

멀티파트 복사에 포함된 작업:
1, 멀티파트 업로드를 초기화하고, uploadId를 획득합니다. 자세한 내용은 [InitMultipartUpload](#INIT_MULIT_UPLOAD)를 참조하십시오.
2, uploadId에 따라 멀티파트 복사를 진행합니다.
3, 모든 멀티파트 복사를 완료합니다. 자세한 내용은 [CompleteMultiUpload](#COMPLETE_MULIT_UPLOAD)를 참조하십시오.

##### 방식 프로토타입
```C#
UploadPartCopyResult PartCopy(UploadPartCopyRequest request);

void PartCopy(UploadPartCopyRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

##### 요청 예시
```C#
try
{
	string sourceAppid = "1253960454"; //계정 appid
	string sourceBucket = "source-1253960454"; //"소스 객체가 있는 버킷
	string sourceRegion = "ap-beijing"; //소스 객체의 버킷이 있는 지역
	string sourceKey = "test.txt"; //소스 객체 키
	//소스 객체 속성 구축
	COSXML.Model.Tag.CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceKey);

	string bucket = "test-1253960454"; //버킷, 형식: bucketname-appid
	string key = "copy_test.txt"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
	string uploadId = "1505706248ca8373f8a5cd52cb129f4bcf85e11dc8833df34f4f5bcc456c99c42cd1ffa2f9 "； //멀티파트 업로드 초기화의 uploadId
	int partNumber = 1; // partNumber >= 1
	UploadPartCopyRequest request = new UploadPartCopyRequest(bucket, key, partNumber, uploadId);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//복사 소스 설정
	request.SetCopySource(copySource);
	//복사 파트 설정
	request.SetCopyRange(0, 1024 * 1024);
	//요청 실행
	UploadPartCopyResult result = cosXml.PartCopy(request);
	//요청 성공
	//해당 파트의 반환 eTag 획득, CompleteMultiUpload에 사용
	string eTag = result.copyObject.eTag;
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
string sourceKey = "test.txt". //소스 객체 키
//소스 객체 속성 구축
COSXML.Model.Tag.CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceKey);

string bucket = "test-1253960454". //버킷, 형식: bucketname-appid
string key = "copy_test.txt"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
string uploadId = "1505706248ca8373f8a5cd52cb129f4bcf85e11dc8833df34f4f5bcc456c99c42cd1ffa2f9 "； //멀티파트 업로드 초기화의 uploadId
int partNumber = 1; // partNumber >= 1
UploadPartCopyRequest request = new UploadPartCopyRequest(bucket, key, partNumber, uploadId);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//복사 소스 설정
request.SetCopySource(copySource);
//복사하는가 또는 업데이트하는가를 설정하고, 여기는 복사
request.SetCopyMetaDataDirective(COSXML.Common.CosMetaDataDirective.COPY);
//요청 실행
cosXml.PartCopy(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		UploadPartCopyResult getObjectResult = result as UploadPartCopyResult;
		//해당 파트의 반환 eTag 획득, CompleteMultiUpload에 사용
		string eTag = result.copyObject.eTag;
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|key|구축 방법 또는 SetCosPath|cos에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324)|string|
|partNumber|구축 방법|파트 번호, partNumber >= 1|int|
|uploadId|구축 방법|지정 멀티파트 복사의 uploadId 표시|string|
|copySource|SetCopySource|복사의 데이터 소스 경로 설명|CopySourceStruct|
|start|SetCopyRange|복사 내용의 시작 위치|long|
|end|SetCopyRange|복사 내용의 종료 위치|long|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

## 반환 결과 설명
UploadPartCopyResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|
|copyObject|[CopyObject](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/CopyObject.cs)|복사 성공한 객체 파트 정보 반환|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

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
	string bucket = "test-1253960454"; //버킷, 형식: bucketname-appid
	string key = "test.txt"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
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
string bucket = "test-1253960454". //버킷, 형식: bucketname-appid
string key = "test.txt". //객체의 버킷에서의 위치, 즉 객체 키입니다.
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|key|구축 방법 또는 SetCosPath|cos에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324)|string|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명
DeleteObjectResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

### 객체 배치 삭제

#### 기능 설명

지정한 버킷의 여러 개의 객체를 삭제합니다(Delete Multi Objects).

#### 방식 프로토타입
```C#
DeleteMultiObjectResult DeleteMultiObjects(DeleteMultiObjectRequest request);

void DeleteMultiObjects(DeleteMultiObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 요청 예시
```C#
try
{
	string bucket = "test-1253960454"; //버킷, 형식: bucketname-appid
	DeleteMultiObjectRequest request = new DeleteMultiObjectRequest(bucket);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//반환 결과 형식 설정
	request.SetDeleteQuiet(false);
	//여러 객체 삭제
	List<string> keys = new List<string>();
	keys.Add("test1.txt");
	keys.Add("test2.txt");
	request.SetObjectKeys(keys);
	//요청 실행
	DeleteMultiObjectResult result = cosXml.DeleteMultiObjects(request);
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
string bucket = "test-1253960454". //버킷, 형식: bucketname-appid
DeleteMultiObjectRequest request = new DeleteMultiObjectRequest(bucket);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//반환 결과 형식 설정
request.SetDeleteQuiet(false);
//여러 객체 삭제
List<string> keys = new List<string>();
keys.Add("test1.txt");
keys.Add("test2.txt");
request.SetObjectKeys(keys);

//요청 실행
cosXml.DeleteMultiObjects(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//요청 성공
		DeleteMultiObjectResult result = cosResult as DeleteMultiObjectResult;
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|quiet|SetDeleteQuiet|배치 업로드 결과 반환 모드 설정, true: 각 키의 삭제 상황 반환, false: 삭제 실패한 키의 정보만 반환|bool|
|key|SetDeleteKey|삭제할 cos의 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324)|string|
|versionId|SetDeleteKey|삭제할 cos의 객체의 지정 버전|string|
|keys|SetObjectKeys|삭제할 cos의 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324) 집합|`List<string>`|
|versionIdAndKey|SetObjectKeys|삭제할 cos의 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324) 및 지정 버전의 집합|Dictionary<string, string>|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명
DeleteMultiObjectResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|
|deleteResult|[DeleteResult](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/DeleteResult.cs)|배치 삭제 객체의 정보 반환|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

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
	string bucket = "test-1253960454"; //버킷, 형식: bucketname-appid
	string key = "test.txt"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
	PutObjectACLRequest request = new PutObjectACLRequest(bucket, key);
	//서명 유효 기간 설정
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//비공개 읽기/쓰기 권한 설정
	request.SetCosACL(CosACL.PRIVATE);
	//1131975903 계정 읽기 권한 부여
	COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount();
	readAccount.AddGrantAccount("1131975903", "1131975903");
	request.setXCosGrantRead(readAccount);
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
string bucket = "test-1253960454". //버킷, 형식: bucketname-appid
string key = "test.txt". //객체의 버킷에서의 위치, 즉 객체 키입니다.
PutObjectACLRequest request = new PutObjectACLRequest(bucket, key);
//서명 유효 기간 설정
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//비공개 읽기/쓰기 권한 설정
request.SetCosACL(CosACL.PRIVATE);
//1131975903 계정 읽기 권한 부여
COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount();
readAccount.AddGrantAccount("1131975903", "1131975903");
request.setXCosGrantRead(readAccount);
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|key|구축 방법 또는 SetCosPath|cos에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324)|string|
|cosAcl|SetCosAcl|버킷의 acl 권한 설정|string|
|grandtAccout|SetXCosGrantRead 또는 SetXCosGrantWrite 또는 SetXCosReadWrite|사용자 읽기/쓰기 권한 부여|GrantAccount|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명
PutObjectACLResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

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
	string bucket = "test-1253960454"; //버킷, 형식: bucketname-appid
	string key = "test.txt"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
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
string bucket = "test-1253960454". //버킷, 형식: bucketname-appid
string key = "test.txt". //객체의 버킷에서의 위치, 즉 객체 키입니다.
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
|매개변수 이름|설정 방법|설명|유형|
|-----|-----|-----|------|
|bucket|구축 방법|버킷 이름, 형식: bucketname-appid|string|
|key|구축 방법 또는 SetCosPath|cos에 저장된 객체의 [객체 키](https://cloud.tencent.com/document/product/436/13324)|string|
|signStartTimeSecond|SetSign|서명 유효기간 시작 시간|long|
|durationSecond|SetSign|서명 유효 기간|long|
|headerKeys|SetSign|서명에 검증 헤더 유무|`List<string>`|
| queryParameterKeys  | SetSign                | 서명에 대해 요청 url 중 조회 매개변수 인증 여부                                | `List<string>` |

#### 반환 결과 설명
GetObjectACLResult를 통해 요청의 결과를 반환합니다.

|멤버 변수|유형|설명|
|-----|-----|----|
|httpCode|int|HTTP 코드, [200, 300) 사이라면 작업 성공을 나타내며, 그렇지 않으면 작업 실패를 나타냅니다|
|accessControlPolicy|[AccessControlPolicy](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/AccessControlPolicy.cs)|객체의 액세스 권한 리스트 정보 반환|

> 작업 실패는 [CosClientException](#COS_CLIENT_EXCEPTION) 또는 [CosServerException](#COS_SERVER_EXCEPTION) 비정상을 throw합니다

## 고급 API

### 고급 API로 파일 업로드(권장)

**TransferManager**, **COSXMLUploadTask**는 간편 업로드, 멀티파트 업로드 API의 비동기화 요청을 캡슐화했습니다
```go
string bucket = "test-1253960454"; //버킷, 형식: bucketname-appid
string key = "test.txt"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
string srcPath = @"F:\test.txt"; //파일의 로컬 위치
COSXMLUploadTask uploadTask = new COSXMLUploadTask(bucket, null, key)
{
	//진행률 콜백
	successCallback = delegate (CosResult cosResult)
	{
		Console.WriteLine(String.Format("progress ={0:##.##}%",completed * 100.0 / total));
	},
	//콜백 성공
	successCallback = delegate (CosResult cosResult)
	{
		COSXML.Transfer.COSXMLUploadTask.UploadTaskResult result = cosResult as COSXML.Transfer.COSXMLUploadTask.UploadTaskResult;
		Console.WriteLine(result.GetResultInfo());
	},
	//콜백 실패
	failCallback = delegate (CosClientException clientEx, CosServerException serverEx)
	{
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	}
};
//업로드 소스 설정
long offset = 0; //소스 파일 0 위치에서 시작
long  sendContentLength  =  -1; //전체 파일 업로드(또는 부분 내용 업로드, sendContentLength > -1)
uploadTask.SetSrcPath(srcPath, offset, sendContentLength);
//요청 실행
transferManager.Upload(uploadTask);
```

### 고급 API로 파일 다운로드(권장)

**TransferManager**, **COSXMLDownloadTask**는 다운로드 API의 비동기화 요청을 캡슐화했습니다
```go
string bucket = "test-1253960454"; //버킷, 형식: bucketname-appid
string key = "test.txt"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
string localDir = @"F:\"; //로컬로 다운로드된 파일의 저장 폴더 경로
string localFileNmae = "test.txt"; //로컬로 다운로드된 파일의 파일명
COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(bucket, null, key, localDir, localFileName)
{
	//진행률 콜백
	successCallback = delegate (CosResult cosResult)
	{
		Console.WriteLine(String.Format("progress ={0:##.##}%",completed * 100.0 / total));
	},
	//콜백 성공
	successCallback = delegate (CosResult cosResult)
	{
		COSXML.Transfer.COSXMLDownloadTask.DownloadTaskResult result = cosResult as COSXML.Transfer.COSXMLDownloadTask.DownloadTaskResult;
		Console.WriteLine(result.GetResultInfo());
	},
	//콜백 실패
	failCallback = delegate (CosClientException clientEx, CosServerException serverEx)
	{
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	}
};

//요청 실행
transferManager.Download(downloadTask);
```

### 고급 API로 파일 복사(권장)

**TransferManager**, **COSXMLCopyTask**는 간편 복사, 멀티파트 복사 API의 비동기화 요청을 캡슐화했습니다
```go
string sourceAppid = "1253960454"; //계정 appid
string sourceBucket = "source-1253960454"; //"소스 객체가 있는 버킷
string sourceRegion = "ap-beijing"; //소스 객체의 버킷이 있는 지역
string sourceKey = "test.txt"; //소스 객체 키
//소스 객체 속성 구축
COSXML.Model.Tag.CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceKey);
string bucket = "test-1253960454"; //버킷, 형식: bucketname-appid
string key = "copy_test.txt"; //객체의 버킷에서의 위치, 즉 객체 키입니다.
COSXMLCopyTask copyTask = new COSXMLCopyTask(bucket, null, key, copySource)
{
	//콜백 성공
	successCallback = delegate (CosResult cosResult)
	{
		COSXML.Transfer.COSXMLCopyTask.CopyTaskResult result = cosResult as COSXML.Transfer.COSXMLCopyTask.CopyTaskResult;
		Console.WriteLine(result.GetResultInfo());
	},
	//콜백 실패
	failCallback = delegate (CosClientException clientEx, CosServerException serverEx)
	{
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	}
};
//요청 실행
transferManager.Copy(copyTask);
```

## <span id="COS_EXCEPTION"> SDK 비정상 설명 </span>

SDK에서, API를 호출하여 cos 객체 작업에 실패하면, CosXmlClientException 비정상 또는 CosXmlServiceException 비정상을 throw합니다

### <span id="COS_CLIENT_EXCEPTION"> [CosXmlClientException](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/CosException/CosClientException.cs) </span>

클라이언트 비정상이란 클라이언트 원인으로 서버와 정상적인 상호 작용을 완료하지 못해 발생한 실패를 가리킵니다. 예를 들어 클라이언트가 서버에 연결할 수 없거나, 서버에서 반환한 데이터를 해석할 수 없거나, 로컬 파일 읽기에 IO 예외 발생 등과 같습니다.
CosClientException은 System.ApplicationException으로부터 통합되며, 사용 방법은 System.ApplicationException과 같고, 또한 한개의 예외 멤버 errorCode를 추가합니다. 예:

|멤버|설명|유형|
| ---- | ---- | ---- |
|errorCode|클라이언트 오류 코드, 예를 들어 10000은 매개변수 인증 실패를 나타냅니다|int|


### <span id="COS_SERVER_EXCEPTION"> [CosXmlServiceException](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/CosException/CosServerException.cs) </span>

CosServerException 서비스 비정상, 상호 작용이 정상적으로 완료되지만, 작업이 실패하는 시나리오를 가리킵니다. 예를 들어 클라이언트가 존재하지 않는 버킷에 액세스하거나, 존재하지 않는 파일을 삭제하거나, 권한이 없는 조작을 진행하거나, 서버에 고장 발생 등과 같습니다.
CosServerException는 서버가 반환한 상태 코드, requestid, 오류 세부 정보 등을 포함합니다. 비정상을 캡처한 후, 필수 검사 요소를 포함된 전체 비정상에 대해 인쇄를 하는 것이 좋습니다. 다음은 비정상 멤버 변수에 대한 설명입니다.

| 멤버 | 설명 | 유형 |
| ------------ | ---------------------------------------- | --------- |
| requestId    | 요청 ID, 요청을 나타냅니다. 문제 검사에 매우 중요합니다. | string    |
| statusCode   | 응답의 상태 코드, 4xx는 클라이언트로 인해 요청이 실패했음을 의미하고, 5xx는 서버 비정상으로 인한 실패입니다. [COS 오류 정보](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. | string    |
| errorCode      | 요청 실패 시 본문이 반환한 오류 코드입니다. [COS 오류 정보](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. | string |
| errorMessage | 요청 실패 시 본문이 반환한 오류 메시지입니다. [COS 오류 정보](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. | string |
