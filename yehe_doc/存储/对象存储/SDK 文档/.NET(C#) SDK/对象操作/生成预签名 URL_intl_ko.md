## 소개

본 문서는 객체 사전 서명된 링크 생성에 대한 예시 코드를 제공합니다.

>?
> - 사용자는 임시 키를 사용하여 사전 서명을 생성하고, 임시 승인을 통해 사전 서명 업로드 및 다운로드 요청의 보안성을 강화할 것을 권장합니다. 임시 키 신청 시, [최소 권한의 원칙 관련 가이드](https://intl.cloud.tencent.com/document/product/436/32972)를 준수하여 타깃 버킷이나 객체 이외의 리소스가 유출되지 않도록 하시기 바랍니다.
> - 사전 서명 생성을 위해 영구 키를 사용해야 하는 경우, 리스크 방지를 위해 영구 키 권한을 업로드 또는 다운로드 작업으로 제한할 것을 권장합니다.
> 


## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 서명되지 않은 링크 생성

객체의 ACL 속성을 ‘공개 읽기’로 설정하면 다음 SDK 인터페이스로 생성된 URL을 통해 객체에 직접 액세스할 수 있습니다.

```C#
 string GetObjectUrl(string bucket, string key);
 ```

## 객체 사전 서명된 링크 생성

#### 예시 코드1: 사전 서명된 업로드 링크 생성

[//]: # (.cssg-snippet-get-presign-upload-url)
```cs
try
{
  PreSignatureStruct preSignatureStruct = new PreSignatureStruct();
  preSignatureStruct.appid = "1250000000";//Tencent Cloud 계정의 APPID
  preSignatureStruct.region = "COS_REGION"; //버킷 리전
  preSignatureStruct.bucket = "examplebucket-1250000000"; //버킷
  preSignatureStruct.key = "exampleobject"; //객체 키
  preSignatureStruct.httpMethod = "PUT"; //HTTP 요청 메소드
  preSignatureStruct.isHttps = true; //HTTPS 요청 URL 생성
  preSignatureStruct.signDurationSecond = 600; //서명 요청 지속 시간: 600초
  preSignatureStruct.headers = null;//서명에서 검증할 header
  preSignatureStruct.queryParameters = null; //서명에서 검증할 URL 요청 매개변수

  //업로드를 위해 미리 서명된 URL(영구 키로 계산됨)
  string requestSignURL = cosXml.GenerateSignURL(preSignatureStruct);

  string srcPath = @"temp-source-file";//로컬 파일 절대 경로
  PutObjectRequest request = new PutObjectRequest(null, null, srcPath);
  //업로드 요청을 위해 미리 서명된 URL 설정
  request.RequestURLWithSign = requestSignURL;
  //진행률 콜백 설정
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  //실행 요청
  PutObjectResult result = cosXml.PutObject(request);
  //요청 완료
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  //요청 실패
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  //요청 실패
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ObjectPresignUrl.cs)를 참고하십시오.
>

#### 예시 코드2: 사전 서명된 다운로드 링크 생성

[//]: # (.cssg-snippet-get-presign-download-url)
```cs
try
{
  PreSignatureStruct preSignatureStruct = new PreSignatureStruct();
  preSignatureStruct.appid = "1250000000";//Tencent Cloud 계정의 APPID
  preSignatureStruct.region = "COS_REGION"; //버킷 리전
  preSignatureStruct.bucket = "examplebucket-1250000000"; //버킷
  preSignatureStruct.key = "exampleobject"; //객체 키
  preSignatureStruct.httpMethod = "GET"; //HTTP 요청 메소드
  preSignatureStruct.isHttps = true; //HTTPS 요청 URL 생성
  preSignatureStruct.signDurationSecond = 600; //서명 요청 지속 시간: 600초
  preSignatureStruct.headers = null;//서명에서 검증할 header
  preSignatureStruct.queryParameters = null; //서명에서 검증할 URL 요청 매개변수

  string requestSignURL = cosXml.GenerateSignURL(preSignatureStruct); 

  //다운로드 요청을 위해 미리 서명된 URL(영구 키로 계산됨)
  string localDir = System.IO.Path.GetTempPath();//로컬 폴더
  string localFileName = "my-local-temp-file"; //로컬 저장 파일 이름 지정
  GetObjectRequest request = new GetObjectRequest(null, null, localDir, localFileName);
  //다운로드 요청을 위해 미리 서명된 URL 설정
  request.RequestURLWithSign = requestSignURL;
  //진행률 콜백 설정
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  //실행 요청
  GetObjectResult result = cosXml.GetObject(request);
  //요청 완료
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  //요청 실패
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  //요청 실패
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ObjectPresignUrl.cs)를 참고하십시오.
>

