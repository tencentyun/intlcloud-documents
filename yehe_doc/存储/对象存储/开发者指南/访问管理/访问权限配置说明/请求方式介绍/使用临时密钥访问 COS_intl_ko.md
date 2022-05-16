## 임시 키 소개

임시 키는 STS(Security Token Service)에서 제공하는 임시 액세스 자격 증명입니다. 임시 키는 TmpSecretId, TmpSecretKey 및 Token의 세 부분으로 구성되며 영구 키와 비교하여 임시 키는 다음과 같은 특징이 있습니다.
- 짧은 유효 시간(30min - 36h), 영구 키를 노출할 필요가 없으므로 계정 유출 리스크가 줄어듭니다.
- 임시 키를 얻을 때 policy 매개변수에 임시 권한을 설정하여 사용자의 권한 범위를 더욱 제한할 수 있습니다.

따라서 임시 키는 프런트 엔드 다이렉트 업로드 등 임시 인증 시나리오에 적합하며 영구 키에 비해 신뢰할 수 없는 사용자에게 임시 키를 배포하는 것이 더 안전합니다.

## 임시 키 획득

임시 키는 당사에서 제공하는 COS STS SDK 또는 STS 클라우드 API를 통해 직접 얻을 수 있습니다.
자세한 내용은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참고하십시오.

## 임시 키의 권한

임시 키를 신청하기 전에 CAM(Cloud Access Management) 사용자(Tencent Cloud 루트 계정 또는 서브 계정)가 있어야 하며, Policy 매개변수를 설정하여 임시 키에 임시 정책을 추가하여 사용자의 권한을 제한할 수 있습니다..
- policy 매개변수가 설정되지 않은 경우 획득한 임시 키는 CAM 사용자와 동일한 권한을 갖습니다.
- policy 매개변수가 설정되면 획득한 임시 키는 CAM 사용자 권한에서 더 나아가 policy에서 설정 범위 내에서 권한을 추가로 제한합니다.

가령 ‘A’는 CAM 사용자의 원래 권한을 나타내고 ‘B’는 policy 매개변수를 통해 임시 키에 대해 설정된 권한을 나타내며 ‘A’와 ‘B’가 교차하는 것은 임시 키의 최종 유효 권한을 나타냅니다.

아래 이미지와 같이 CAM 사용자 권한과 policy 임시 권한의 교집합이 유효 권한입니다.
![](https://qcloudimg.tencent-cloud.cn/raw/60982ace7d24b98f97210e674fd373a9.png)

아래 이미지와 같이 policy는 CAM 사용자 권한 내에 있으며 policy는 유효 권한입니다.
![](https://qcloudimg.tencent-cloud.cn/raw/03b30ed344faa1a9e28a6210810866d1.png)

## 임시 키를 사용한 COS 액세스

![](https://qcloudimg.tencent-cloud.cn/raw/0127017176d6014ec8957f47d4858666.png)
임시 키는 SecretId, SecretKey 및 Token이 있으며, 각 루트 계정과 서브 계정은 여러 개의 임시 키를 생성할 수 있습니다. 영구 키에 비해 임시 키는 30분 - 36시간 동안만 유효합니다. 임시 키는 프런트 엔드 다이렉트 업로드와 같은 임시 인증 시나리오에 적합하며 영구 키에 비해 신뢰할 수 없는 사용자에게 임시 키를 배포하는 것이 더 안전합니다. 자세한 내용은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048) 및 [프런트 엔드 다이렉트 업로드를 위한 임시 키 사용 가이드](https://intl.cloud.tencent.com/document/product/436/35265)를 참고하십시오.

- API 요청 발송
영구 키와 마찬가지로 임시 키를 통해 서명을 생성하고 요청 헤더에 Authorization을 입력하여 서명된 요청을 형성할 수도 있습니다. COS는 요청을 수신한 후 서명이 유효한지, 임시 키가 만료되었는지 확인합니다.
서명 알고리즘에 대한 소개는 [서명 요청](https://intl.cloud.tencent.com/document/product/436/7778)을 참고하십시오. COS는 서명 생성 툴을 제공하며, SDK를 통해서도 서명을 생성할 수 있습니다. [SDK 서명 구현](https://intl.cloud.tencent.com/document/product/436/7778#sdk-.E7.AD.BE.E5.90.8D.E5.AE.9E.E7.8E.B0)을 참고하십시오.
- SDK 툴 사용
SDK 툴을 설치한 후 임시 키를 사용하여 사용자 신분 정보를 초기화하는 것 외에도 임시 키(SecretId, SecretKey, Token)를 사용하여 COSClient를 초기화하고 서명을 생성하지 않고 SDK를 직접 사용하여 업로드, 다운로드 등을 수행합니다. 임시 키 생성은 임시 키 생성 및 사용 지침을 참고하십시오.

Java SDK 참고 예시는 다음과 같으며 더 많은 언어 demo는 [SDK 개요](https://intl.cloud.tencent.com/document/product/436/6474)를 참고하십시오.

```
// 1 획득한 임시 키(tmpSecretId, tmpSecretKey, sessionToken) 전송
String tmpSecretId = "SECRETID";
String tmpSecretKey = "SECRETKEY";
String sessionToken = "TOKEN";
BasicSessionCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);
// 2 bucket의 리전 설정. COS 리전의 약칭은 https://cloud.tencent.com/document/product/436/6224 참고하십시오.
// clientConfig에 region, https(기본값: http), 타임아웃, 프록시 등을 설정하는 set 메소드가 포함되어 있습니다. 사용 시 소스 코드 또는 FAQ의 Java SDK 부분을 참고하십시오.
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// 3 cos 클라이언트 생성
COSClient cosClient = new COSClient(cred, clientConfig);
```

## 임시 키 사용 시나리오

임시 키는 주로 3rd party가 COS에 임시로 액세스할 수 있는 권한을 부여하는 데 사용됩니다. 예를 들어 사용자가 클라이언트 App을 개발하여 COS 버킷에 데이터를 저장하는 경우 이때 영구 키를 App 클라이언트에 직접 저장하는 것은 안전하지 않지만 클라이언트에게 업로드 및 다운로드 권한을 부여해야 하는 이런 시나리오에서 임시 키를 사용할 수 있습니다. 
![](https://qcloudimg.tencent-cloud.cn/raw/0b37dd8a160a065efe68c0fbeea09c3b.png)

상기 이미지와 같이 사용자가 App 클라이언트를 개발하고 사용자의 서버에 영구 키를 저장합니다. 프론트 엔드 다이렉트 업로드를 위해 임시 키를 사용하려면 다음 단계가 필요합니다.
1. App 클라이언트는 데이터 업로드 및 다운로드를 위해 사용자 서버에 임시 키를 요청합니다.
2. 사용자 서버는 영구 키 신분을 사용하여 STS 서버에서 임시 키를 신청합니다.
3. STS 서비스는 임시 키를 사용자 서버에 반환합니다.
4. 사용자 서버는 임시 키를 App 클라이언트로 전달합니다.
5. App 클라이언트는 임시 키를 사용하여 서명 요청을 생성하고 COS에 데이터 업로드 및 다운로드를 요청합니다.

임시 키는 직접 프런트 엔드 데이터 다이렉트 업로드에 적합하며 다음 모범 사례를 참고하여 임시 키를 사용할 수 있습니다.
- [Web의 다이렉트 업로드 사례](https://intl.cloud.tencent.com/document/product/436/9067)
- [미니프로그램 다이렉트 업로드 사례](https://intl.cloud.tencent.com/document/product/436/30934)
- [모바일 애플리케이션 다이렉트 업로드 사례](https://intl.cloud.tencent.com/document/product/436/30618)

