## 임시 키

임시 키는 CAM이 제공하는 API를 통해, 권한이 제한된 키를 얻습니다.<br>
 COS API는 임시 키를 사용해 서명을 컴퓨팅할수 있으며, COS API 요청을 시작하는 데 사용됩니다.<br>
 COS API 요청은 임시 키를 사용해 서명 컴퓨팅할 경우, 임시 키 API에서 반환하는 정보 중 3가지 필드를 얻어 사용해야 할 필요가 있습니다. 사용법은 각각 다음과 같습니다.
- `tmpSecretId`
- `tmpSecretKey`
- `sessionToken`

## 임시 키의 장점

Web, iOS, Android에서 COS의 시나리오를 사용할 경우, 고정 키 서명 컴퓨팅 방식은 권한을 효과적으로 제어할 수 없을 뿐 아니라 영구 키를 클라이언트 코드에 두면 유출 위험이 매우 큽니다. 임시 키 방식을 통해 편리하고, 효과적으로 권한 제어 문제를 해결할 수 있습니다.
예: 임시 키 신청 과정에서, 권한 정책 [policy](https://cloud.tencent.com/document/product/436/31923#policy) 필드를 설정함으로 작업과 리소스를 제한하여 권한을 지정된 범위 내에서 제한합니다.

COS API 권한 부여 정책에 관한 사항:
- [COS API 임시 키 권한 부여 정책 가이드](https://cloud.tencent.com/document/product/436/31923)
- [일반 시나리오의 임시 키 권한 정책 예시](https://cloud.tencent.com/document/product/436/31923#.E5.B8.B8.E8.A7.81.E5.9C.BA.E6.99.AF.E6.8E.88.E6.9D.83.E7.AD.96.E7.95.A5)

## 임시 키 획득

임시 키를 획득하려면, 제공된 [COS STS SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk) 방식으로 획득할 수 있고, 직접 STS 클라우드 API에 요청하여 획득할 수도 있습니다.

### COS STS SDK

COS는 STS에 SDK와 예시를 제공하며, 현재 이미 Java, Nodejs, PHP, Python 등 다양한 언어 예시가 있습니다.
구체적인 내용은 [COS STS SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk)를 참조하십시오. 각 SDK의 사용 설명은 Github에 있는 README와 예시를 참조하십시오.

COS STS SDK가 제공하는 [Java SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/java)를 예로 들면, 임시 키 획득은 다음과 같습니다.

```java
import com.qcloud.Utilities.Json.JSONObject;

public class Demo {
    public static void main(String[] args) {
        TreeMap<String, Object> config = new TreeMap<String, Object>();

		try {
		    // 고정 키
		    config.put("SecretId", "AKIDXXXXXXXXXXXXXXXXX");
		    // 고정 키
		    config.put("SecretKey", "XXXXXXXXXXXXXXXXX");

		    // 임시 키의 유효 시간(초)
		    config.put("durationSeconds", 1800);

		    // 사용자의 버킷으로 대체
		    config.put("bucket", "examplebucket-appid");
		    // 버킷 소재 지역으로 대체
		    config.put("region", "ap-guangzhou");

		    // 여기서 허용된 경로 접두사로 대체하며, 자신의 웹사이트 사용자 로그인 상태에 따라 업로드 허용 디렉터리를 판단할 수 있습니다. 예: * 또는 a/* 또는 a.jpg
		    config.put("allowPrefix", "*");

		    // 키의 권한 리스트입니다. 간편 업로드와 멀티파트 업로드는 다음과 같은 권한이 필요합니다. 다른 권한 리스트는 https://cloud.tencent.com/document/product/436/31923 참조하십시오.
		    String[] allowActions = new String[] {
		            // 간편 업로드
		            "name/cos:PutObject",
		            // 멀티파트 업로드
		            "name/cos:InitiateMultipartUpload",
		            "name/cos:ListMultipartUploads",
		            "name/cos:ListParts",
		            "name/cos:UploadPart",
		            "name/cos:CompleteMultipartUpload"
		    };
		    config.put("allowActions", allowActions);

		    JSONObject credential = CosStsClient.getCredential(config);
		    System.out.println(credential);
		} catch (Exception e) {
		    throw new IllegalArgumentException("no valid secret !");
		}
    }
}
```

### 임시 키로 COS에 액세스

 COS API에서 임시 키를 사용해 COS 서비스에 접근할 경우, `x-cos-security-token` 필드를 통해 임시 `sessionToken`을 전달합니다. 임시 `SecretId`와 `SecretKey`로 서명을 컴퓨팅합니다.

COS Java SDK를 예로 들면, 임시 키를 사용해 COS에 접근하는 예시는 다음과 같습니다.
> [여기](https://github.com/tencentyun/cos-java-sdk-v5)를 클릭하여 Github에서 Java SDK 설치 패키지를 다운로드합니다.

```java
public class Demo {
    public static void main(String[] args) throws Exception {

        // 사용자 기본 정보
        String tmpSecretId = "AKIDxxxxxx";
        String tmpSecretKey = "xxxxxx";
        String sessionToken = "xxxxxx";

        // 1 사용자 인증 정보(secretId, secretKey)를 초기화합니다.
        COSCredentials cred = new BasicCOSCredentials(tmpSecretId, tmpSecretKey);
        // 2 버킷 지역을 설정합니다. COS 지역의 약칭: https://cloud.tencent.com/document/product/436/6224
        ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
        // 3 COS 클라이언트를 생성합니다.
        COSClient cosclient = new COSClient(cred, clientConfig);
        // 버킷 이름에는 appid가 포함되어야 합니다.
        String bucketName = "mybucket-1251668577";

        String key = "aaa/bbb.txt";
        //객체를 업로드할 경우, 20M이하의 파일은 이 API에서 사용하기를 권장합니다.
        File localFile = new File("src/test/resources/test.txt");
        PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

        // x-cos-security-token header 필드를 설정합니다.
        ObjectMetadata objectMetadata = new ObjectMetadata();
        objectMetadata.setSecurityToken(sessionToken);
        putObjectRequest.setMetadata(objectMetadata);

        try {
            PutObjectResult putObjectResult = cosclient.putObject(putObjectRequest);
            // putobjectResult는 파일의 etag를 반환합니다.
            String etag = putObjectResult.getETag();
        } catch (CosServiceException e) {
            e.printStackTrace();
        } catch (CosClientException e) {
            e.printStackTrace();
        }

        // 클라이언트를 종료합니다.
        cosclient.shutdown();

    }
}
```

### STS API
#### API 요청 주소
```shell
https://sts.api.qcloud.com/v2/index.php
```
## API 요청 방법
클라우드 API의 매개변수는 GET 매개변수와 POST 매개변수 두 형식을 지원합니다. 다음은 GET 매개변수의 형식에 대한 소개입니다.
#### API 요청 매개변수 설명

>? 요청 매개변수 리스트에서, 임시 키 API 특유의 매개변수는 name, policy, durationSeconds가 있습니다. 다른 필드에는 클라우드 API의 [공용 요청 매개변수](https://cloud.tencent.com/document/api/213/6976)가 있습니다.

| 필드 | 설명 | 필수 항목 여부 | 유형 |
| ------------ | ------------ | ------------ | ------------ |
| name | 페더레이션 ID를 가진 사용자의 별명. <br>주석 필드에 사용자 uin을 기입할 수 있습니다. | 예 | String |
| policy | 정책 구문. 실제 요청의 URL은 아래 예에서 URL이 두 번 인코딩된 문자열입니다.| 예 | String |
| durationSeconds |  임시 인증서 유효 기간, 단위: 초 <br>기본 설정: 1800초, 최장 유효 기간: 2시간(7200초) | 아니요 | Int |
| Action | 클라우드 API의 Action 매개변수입니다. GetFederationToken을 지정해야 합니다 | 예 | String |
| Timestamp | 현재 UNIX 타임스탬프 | 예 | Int |
| Nonce | 랜덤 양의 정수. 타임스탬프와 결합하여 재전송 공격 방지에 사용됩니다.| 예 | Int|
| Region | 클라우드 API 지역 매개변수, 빈 문자열이 가능하여,기본적으로 가장 가까운 지역을 액세스합니다. 작성 가능한 지역은 [공용 요청 매개변수](https://cloud.tencent.com/document/api/213/6976)를 참조하십시오. | 예 | String |
| SecretId | 클라우드 API 키에서 신청한 ID 식별의 SecretId입니다. 하나의 SecretId는 유일한 SecretKey와 해당하며, SecretKey는 요청 서명 Signature를 생성하는 데 사용됩니다. | 예 | String |
| Signature | 요청 서명입니다. 요청의 유효성을 검증하는 데 사용하며, 사용자가 실제 입력한 매개변수에 따라 계산해야 합니다. <br>계산 방법은 [서명 방법](https://cloud.tencent.com/document/api/213/6984#.E7.94.9F.E6.88.90.E7.AD.BE.E5.90.8D.E4.B8.B2 "서명 방법")을 참조하십시오.|예|String|

#### 반환 결과 설명

| 필드     | 유형  | 설명  |
| ------------ | ------------ | ------------ |
| expiredTime | Int | 임시 키가 무효되는 타임스탬프. |
| credentials | Object | 객체에는 Token, tmpSecretId, tmpSecretKey의 트리플 포함. |
| --tmpSecretId | String| tmpSecretId 서명 걔산 시 사용. |
| --tmpSecretKey |String| tmpSecretKey 서명 계산 시 사용. |
| --sessionToken | String | sessionToken 인증 요청 시 사용, COS API는 Header의 x-cos-security-token 필드 안에 배치됨. |

#### 접근 요청 예시

```shell
https://sts.api.qcloud.com/v2/index.php?
policy=%7B%0D%0A++%22version%22%3A+%222.0%22%2C%0D%0A++%22statement%22%3A+%5B%0D%0A++++%7B%0D%0A++++++%22action%22%3A+%5B%0D%0A++++++++%22name%2Fcos%3AHead*%22%2C%0D%0A++++++++%22name%2Fcos%3AGet*%22%2C%0D%0A++++++++%22name%2Fcos%3AList*%22%2C%0D%0A++++++++%22name%2Fcos%3AOptionsObject%22%0D%0A++++++%5D%2C%0D%0A++++++%22effect%22%3A+%22allow%22%2C%0D%0A++++++%22resource%22%3A+%5B%0D%0A++++++++%22*%22%0D%0A++++++%5D%0D%0A++++%7D%0D%0A++%5D%0D%0A%7D&name=brady&Action=GetFederationToken&SecretId=AKIDPiqmW3qcgXVSKN8jngPzRhvxzYyDL5qP&Nonce=665530507&Timestamp=1545889218&RequestClient=net-sdk-v5&durationSeconds=7200&Signature=S5LPn2GNbi1mLR3EnAcVAW3iYe8%3D
```

#### 성공한 반환 내용 예시

```shell
{
  "code": 0,
  "message": "",
  "codeDesc": "Success",
  "data": {
    "credentials": {
      "sessionToken":"xxxxxx",
      "tmpSecretId":"AKIDxxxxx",
      "tmpSecretKey":"xxxxx"
    },
    "expiredTime":1545896418
  }
}
```

## 문제 해결

반환 결과의 오류 코드는 오류의 주요 원인을 나타냅니다.

- 코드는 모든 모듈의 API에 적용될 수 있는 공통 오류 코드입니다. 코드가 0이면 호출이 성공하고 그렇지 않으면 호출 실패함을 나타납니다. 호출이 실패하면 사용자는 공통 오류 코드 리스트에 따라 오류 원인을 확인하고 해당 조치를 취할 수 있습니다.

- codeDesc는 모듈과 관련된 오류를 나타내는 모듈 오류 코드입니다. 호출이 실패하면 사용자는 모듈 오류 코드 리스트에 따라 오류 원인을 확인하고 해당 조치를 취할 수 있습니다.

구체적인 오류 코드 설명은 [오류 코드](https://intl.cloud.tencent.com/document/product/598/13884)를 참조하십시오.
