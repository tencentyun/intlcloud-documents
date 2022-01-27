## 소개

본 문서는 객체 메타데이터 작업 조회에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명         | 작업 설명                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | 객체 메타데이터 조회 | 객체의 메타데이터 정보 조회                  |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 객체 메타데이터 조회

#### 기능 설명

사용자 정의 헤더, Etag 및 객체 메타 정보를 포함한 Object Meta 정보를 쿼리합니다.

#### 예시 코드

[//]: # (.cssg-snippet-head-object)
```cs
using COSXML.Model.Object;
using COSXML.Auth;
using System;
using COSXML;

namespace COSSnippet
{
    public class HeadObjectModel {

      private CosXml cosXml;

      HeadObjectModel() {
        CosXmlConfig config = new CosXmlConfig.Builder()
          .SetRegion("COS_REGION") // 기본 리전을 설정합니다. COS 리전의 약칭은 https://cloud.tencent.com/document/product/436/6224를 참고하십시오.
          .Build();
        
        string secretId = "SECRET_ID";   // Tencent Cloud API 키 SecretId. API 키를 얻으려면 https://console.cloud.tencent.com/cam/capi를 참고하십시오.
        string secretKey = "SECRET_KEY"; // Tencent Cloud API 키 SecretKey. API 키를 얻으려면 https://console.cloud.tencent.com/cam/capi를 참고하십시오.
        long durationSecond = 600;           //각 서명 요청의 유효 시간. 단위: 초.
        QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
          secretKey, durationSecond);
        
        this.cosXml = new CosXmlServer(config, qCloudCredentialProvider);
      }

      /// 객체 정보 가져오기
      public void HeadObject()
      {
        //.cssg-snippet-body-start:[head-object]
        try
        {
          // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
          string bucket = "examplebucket-1250000000";
          string key = "exampleobject"; //객체 키
          HeadObjectRequest request = new HeadObjectRequest(bucket, key);
          //실행 요청
          HeadObjectResult result = cosXml.HeadObject(request);
          //요청 완료
          Console.WriteLine(result.GetResultInfo());
          // 객체 crc64 출력
          Console.WriteLine(result.crc64ecma);
          // 객체의 eTag 출력
          Console.WriteLine(result.eTag);
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
        
        //.cssg-snippet-body-end
      }
      // .cssg-methods-pragma

      static void Main(string[] args)
      {
        HeadObjectModel m = new HeadObjectModel();

        /// 객체 정보 가져오기
        m.HeadObject();
        // .cssg-methods-pragma
      }
    }
}
```
>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/HeadObject.cs)를 참고하십시오.

