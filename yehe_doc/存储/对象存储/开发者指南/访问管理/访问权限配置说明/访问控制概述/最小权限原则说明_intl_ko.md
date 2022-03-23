## 개요

Cloud Object Storage(COS)를 사용 시 임시 키를 사용해 사용자에게 해당 리소스의 작업 권한을 부여하거나 서브 계정 또는 협업 파트너에게 적합한 사용자 정책을 부여해, 그들이 COS의 리소스를 작업할 수 있도록 허용해야 할 수 있습니다. 또한 버킷에 관련 버킷 정책을 추가해 지정된 사용자가 버킷에서 지정된 작업을 하거나 지정된 리소스를 작업하도록 해야 할 수 있습니다. 이와 같은 권한 설정 시, 반드시 **최소 권한 원칙**을 준수해 데이터 자산 보안을 확보하십시오.

**최소 권한 원칙**이란, 권한을 부여할 때 권한 범위를 명확히 하여 **지정 사용자**에게 **어떤 조건**에서 **어떤 작업**을 수행하고 **어떤 리소스**에 액세스할지에 대해 권한을 명확하게 부여하는 것을 의미합니다.

## 주의 사항
권한 부여 시 최소 권한 원칙을 엄격히 따라, 한정된 사용자가 제한된 작업(예: `action:GetObject` 권한 부여)을 수행하고 제한된 리소스에 액세스(예: `resource:examplebucket-1250000000/exampleobject.txt` 권한 부여)하도록 할 것을 권장합니다. 
과도한 권한 부여로 인한 예상 밖의 월권 작업과 데이터 보안 리스크를 피하기 위해, 모든 리소스(예: `resource:*`)에 액세스할 수 있거나 모든 작업(예: `action:*`)이 가능한 권한을 사용자에게 부여하지 않을 것을 강력히 권장합니다.

잠재된 데이터 보안 리스크 예시는 다음과 같습니다.
- 데이터 유출: 사용자에게 `examplebucket-1250000000/data/config.json`과 `examplebucket-1250000000/video/` 다운로드 같은 지정 리소스에 대한 다운로드 권한을 부여합니다. 그러나 권한 정책 중 `examplebucket-1250000000/*`이 설정되어 있을 경우, 이 버킷에 속한 모든 객체의 다운로드가 허용되어 월권 작업 행위로 인해 예상 밖의 데이터 유출이 발생할 수 있습니다.
- 데이터 덮어쓰기: 사용자에게 `examplebucket-1250000000/data/config.json`과 `examplebucket-1250000000/video/`와 같은 리소스에 대한 업로드 권한을 부여합니다. 그러나 권한 정책 중 `examplebucket-1250000000/*`이 설정되어 있을 경우, 해당 버킷에 속한 모든 객체의 업로드가 허용되고, 월권 작업 행위로 인해 예상 밖의 객체 덮어쓰기가 발생할 수 있습니다. 리스크를 예방하려면 최소 권한 원칙을 준수해야 할 뿐만 아니라, [버전 관리](https://intl.cloud.tencent.com/document/product/436/19883)를 통해 데이터의 이전 버전을 모두 보관하여 추적을 용이하게 할 수도 있습니다.
- 데이터 유출: 사용자에게 버킷의 객체 리스트 `cos:GetBucket`을 나열할 수 있는 권한을 부여합니다. 그러나 권한 정책 중 `cos:*`이 설정되어 있을 경우, 버킷 권한 재부여, 객체 삭제 및 버킷 삭제를 포함한 버킷의 모든 작업이 허용되어 데이터 보안에 큰 리스크가 발생할 수 있습니다.


## 사용 가이드

최소 권한 원칙에 따라 정책에서 다음 정보를 명확히 지정해야 합니다.

- 위탁자(principal): 어떤 서브 계정(사용자 ID 작성 필요), 협업 파트너(사용자 ID 작성 필요), 익명 사용자 또는 사용자 그룹에게 권한 부여가 필요한지 명확히 지정할 필요가 있습니다. 임시 키로 액세스를 시도한다면 이 항목을 지정할 필요가 없습니다.
- 명령(statement): 다음 매개변수 중에 적합한 매개변수를 작성합니다.
	- 효력(effect): 해당 정책에 대해 '허용'하는지 '명시적 거부'하는지 명확히 기술해야 합니다. allow와 deny 두 가지 상황이 포함됩니다.
	- 작업(action): 해당 정책에 대해 허용 또는 거부 작업을 명확히 기술해야 합니다. 단일 API 작업이나 여러 API 작업의 결합 작업일 수 있습니다.
	- 리소스(resource): 해당 정책이 권한을 부여한 구체적인 리소스를 명확히 기술해야 합니다. 리소스는 6단식 기술을 사용하며, 리소스 범위를 지정된 파일로 제한할 수 있습니다. 예를 들어 `exampleobject.jpg` 또는 `examplePrefix/*`와 같은 지정 디렉터리가 있습니다. 업무상 필요 외에는 모든 리소스에 액세스할 수 있는 권한 즉, 와일드카드`*`를 임의로 부여하지 마십시오.
	- 조건(condition): 정책의 효력이 발생하는 규제 조건을 기술합니다. 조건에는 오퍼레이터, 작업 키와 작업 값 구성이 포함됩니다. 조건 값은 시간, IP 주소 등의 정보를 포함합니다.

### 임시 키 최소 권한 가이드

임시 키 신청 과정에서 권한 정책 Policy 필드 설정을 통해 작업 및 리소스를 제한하고, 권한을 지정된 범위로 제한할 수 있습니다. 임시 키 생성 관련 자세한 설명은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048) 문서를 참고하십시오.

#### 권한 부여 예시

#### Java SDK를 이용해 임의 객체에 액세스할 수 있는 권한을 부여합니다.

Java SDK를 이용해 버킷 `examplebucket-1250000000` 중 객체 `exampleObject.txt`를 다운로드할 수 있는 권한을 부여해야 한다고 가정했을 때, 설정이 필요한 코드는 다음과 같습니다.

```
// github에서 제공하는 maven 통합 방법에 따라 java sts sdk 가져오기 
import java.util.*;
import org.json.JSONObject; 
import com.tencent.cloud.CosStsClient;

public class Demo {
    public static void main(String[] args) {
        TreeMap<String, Object> config = new TreeMap<String, Object>();

        try {
            // 사용자의 SecretId로 변경 
            config.put("SecretId", "AKIDHTVVaVR6e3");
            // 사용자의 SecretKey로 변경
            config.put("SecretKey", "PdkhT9e2rZCfy6");

            // 임시 키의 유효 기간은 초 단위입니다. 기본값은 1800초이며, 최대 유효 기간은 7200초로 설정 가능합니다.
            config.put("durationSeconds", 1800);

            // 사용자의 bucket으로 변경
            config.put("bucket", "examplebucket-1250000000");
            // bucket 소재 리전으로 변경
            config.put("region", "ap-guangzhou");

            // 여기서 허용된 경로의 접두사로 바꾸면 자신의 웹 사이트의 사용자 로그인 상태에 따라 업로드가 허용된 구체적 경로를 판단할 수 있습니다. 예: a.jpg 또는 a/* 또는 *
            // '*'를 입력하면 사용자가 모든 리소스에 액세스하는 것을 허용하게 됩니다. 업무에 필요한 경우가 아니면 최소 권한 원칙에 따라 사용자에게 적합한 액세스 권한 범위를 부여하십시오.
            config.put("allowPrefix", "exampleObject.txt");

            // 키 권한 리스트. 간단한 업로드, 포맷 업로드 및 멀티 파트 업로드에 필요한 권한은 다음과 같습니다. 기타 권한 리스트는 https://cloud.tencent.com/document/product/436/31923을 참고하십시오.
            String[] allowActions = new String[] {
                    // 데이터 다운로드
                    "name/cos:GetObject"
            };
            config.put("allowActions", allowActions);

            JSONObject credential = CosStsClient.getCredential(config);
            //임시 키 정보를 성공적으로 반환하면, 다음과 같은 키 정보가 출력됩니다.
            System.out.println(credential);
        } catch (Exception e) {
            //실패 시 이상 경고가 발생합니다.
            throw new IllegalArgumentException("no valid secret !");
        }
    }
}
```

#### API를 이용해 임의 객체에 대한 액세스 권한을 부여합니다.

API를 이용해 버킷 `examplebucket-1250000000` 중 객체 `exampleObject.txt` 및 디렉터리 `examplePrefix`에 속한 모든 객체를 다운로드할 수 있는 권한을 부여해야 한다고 가정했을 때, 입력이 필요한 정책은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/exampleObject.txt",
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/examplePrefix/*"
      ]
    }
  ]
}
```

### 사전 서명 최소 권한 가이드

사전 서명된 URL을 통해 임시 업로드 및 다운로드 작업을 구현할 수 있습니다. 또한 사전 서명된 URL을 누구에게나 전달할 수 있으며 유효한 사전 서명된 URL을 받는 사람은 누구나 객체를 업로드하거나 다운로드할 수 있습니다.

>! 임시 키와 영구 키를 모두 사용하여 사전 서명된 URL을 생성할 수 있지만, 최소 권한 가이드 [임시 키 생성](https://intl.cloud.tencent.com/document/product/436/14048)을 준수하여, 임시 키를 사용하여 사전 서명을 계산합니다. 보안 리스크를 피하기 위해 과도한 권한을 가진 영구 키를 사용하지 마십시오.

#### 권한 부여 예시

#### 사용자에게 사전에 서명된 URL을 사용하여 객체를 다운로드할 수 있는 권한을 부여합니다.

임시 키를 사용해 서명이 있는 다운로드 링크를 생성하고, 반환할 일부 공용 헤더(예: content-type, content-language)를 덮어쓰도록 설정합니다. 다음은 Java 예시 코드입니다.

```java
// 획득한 임시 키(tmpSecretId, tmpSecretKey, sessionToken) 전송
String tmpSecretId = "SECRETID";
String tmpSecretKey = "SECRETKEY";
String sessionToken = "TOKEN";
COSCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);
// bucket 리전 설정. COS 리전의 약칭은 https://cloud.tencent.com/document/product/436/6224 참고
// clientConfig에 region, https(기본값: http), 타임아웃, 프록시 등을 설정하는 set 방법이 포함되어 있습니다. 사용 시 소스 코드 또는 FAQ의 Java SDK 부분을 참고하십시오.
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// https 프로토콜을 사용하는 URL을 생성할 경우, 이 행을 설정하길 권장합니다.
// clientConfig.setHttpProtocol(HttpProtocol.https);
// cos 클라이언트 생성
COSClient cosClient = new COSClient(cred, clientConfig);
// 버킷의 이름 생성 포맷: BucketName-APPID 
String bucketName = "examplebucket-1250000000";
// 여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자입니다.
String key = "exampleobject";
GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// 다운로드 시 반환하는 http 헤더 설정
ResponseHeaderOverrides responseHeaders = new ResponseHeaderOverrides();
String responseContentType = "image/x-icon";
String responseContentLanguage = "zh-CN";
// 반환 헤더에 포함되는 파일명 정보 설정
String responseContentDispositon = "filename=\"exampleobject\"";
String responseCacheControl = "no-cache";
String cacheExpireStr =
        DateUtils.formatRFC822Date(new Date(System.currentTimeMillis() + 24L * 3600L * 1000L));
responseHeaders.setContentType(responseContentType);
responseHeaders.setContentLanguage(responseContentLanguage);
responseHeaders.setContentDisposition(responseContentDispositon);
responseHeaders.setCacheControl(responseCacheControl);
responseHeaders.setExpires(cacheExpireStr);
req.setResponseHeaders(responseHeaders);
// 서명 만료 시간 설정(옵션). 설정하지 않을 경우 기본적으로 ClientConfig의 서명 만료 시간(1시간)을 사용합니다.
// 본 예시에서는 30분 후 만료로 설정합니다.
Date expirationDate = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);
req.setExpiration(expirationDate);
URL url = cosClient.generatePresignedUrl(req);
System.out.println(url.toString());
cosClient.shutdown();
```


### 사용자 정책 최소 권한 가이드

사용자 정책은 [CAM 콘솔](https://console.cloud.tencent.com/cam/policy)에 추가된 사용자 권한 정책으로, 사용자가 COS 리소스에 액세스할 수 있는 권한을 부여하는 데 사용됩니다. 사용자 액세스 정책 개요의 설정에 관한 자세한 설명은 [액세스 정책 언어 개요](https://intl.cloud.tencent.com/document/product/436/18023) 문서를 참고하십시오.

#### 권한 부여 예시

#### 계정에 임의 객체에 액세스할 수 있는 권한을 부여합니다.

계정 UIN을 `100000000001`로 하고 버킷 `examplebucket-1250000000` 중 객체 `exampleObject.txt`를 다운로드할 수 있는 권한을 부여해야 한다고 가정했을 때, 적합한 액세스 정책은 다음과 같습니다.
```shell
{
   "version": "2.0",
   "principal": {
      "qcs": [
         "qcs::cam::uin/100000000001:uin/100000000001"
      ]
   },
    "statement": [
        {
            "action": [
                "name/cos:GetObject"
            ],
            "effect": "allow",
            "resource": [
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000.ap-guangzhou.myqcloud.com/exampleObject.txt"
            ]
        }
    ]
}
```

#### 서브 계정에 임의 디렉터리에 액세스할 수 있는 권한을 부여합니다.

서브 계정 UIN을 `100000000011`(루트 계정 UIN은 `100000000001`)로 하고 버킷 `examplebucket-1250000000` 중 디렉터리 `examplePrefix`에 속한 객체를 다운로드할 수 있는 권한을 부여해야 한다고 가정했을 때, 적합한 액세스 정책은 다음과 같습니다.

```shell
{
   "version": "2.0",
   "principal": {
      "qcs": [
         "qcs::cam::uin/100000000001:uin/100000000011"
      ]
   },
    "statement": [
        {
            "action": [
                "name/cos:GetObject"
            ],
            "effect": "allow",
            "resource": [
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000.ap-guangzhou.myqcloud.com/examplePrefix/*"
            ]
        }
    ]
}
```

### 버킷 정책 최소 권한 가이드

버킷 정책은 버킷에서 설정한 액세스 정책으로, 지정 사용자가 버킷 및 버킷 내 리소스에 대해 지정된 작업을 할 수 있도록 허용합니다. 버킷 정책 설정은 [버킷 정책 추가](https://intl.cloud.tencent.com/document/product/436/30927) 문서를 참고하십시오.

#### 권한 부여 예시

#### 서브 계정에 특정 객체에 액세스할 수 있는 권한을 부여합니다.

서브 계정 UIN을 `100000000011`(루트 계정 UIN은 `100000000001`)로 하고 버킷 `examplebucket-1250000000` 중 객체 `exampleObject.txt` 및 디렉터리 `examplePrefix`에 속한 모든 객체를 다운로드할 수 있는 권한을 부여해야 한다고 가정했을 때, 적합한 액세스 정책은 다음과 같습니다.

```shell
{
  "Statement": [
    {
      "Action": [
        "name/cos:GetObject"
      ],
      "Effect": "allow",
      "Principal": {
        "qcs": [
          "qcs::cam::uin/100000000001:uin/100000000011"
        ]
      },
      "Resource": [
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/exampleObject.txt",
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/examplePrefix/*"
      ]
    }
  ],
  "version": "2.0"
}
```

