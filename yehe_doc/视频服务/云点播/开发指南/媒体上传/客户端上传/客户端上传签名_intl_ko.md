
클라이언트 업로드 시작 전, App의 서명 배포 서버에 업로드 서명을 신청해야 합니다. 클라이언트 업로드 작업 실행 시, 이 서명이 있어야 VOD가 업로드 승인 여부를 확인할 수 있습니다.


## 서명 생성 단계

1. **Tencent Cloud API 키 가져오기**
SecretId, SecretKey와 같은 서버 API 호출에 필요한 보안 자격 증명을 가져옵니다. 자세한 방법은 다음과 같습니다.
	1. 콘솔에 로그인하고 [클라우드 서비스]>[CAM]>[[API 키 관리]](https://console.cloud.tencent.com/cam/capi)를 선택해 ‘API 키 관리’ 페이지로 이동합니다.
	2. Tencent Cloud API 키를 받습니다. 아직 키를 생성하지 않은 경우, [키 생성]을 클릭하면 한 쌍의 SecretId와 SecretKey가 생성됩니다.
2. **일반 텍스트 문자열 스플라이스 original**
아래와 같이 URL QueryString의 형식 요구 사항에 따라 일반 텍스트 서명 문자열 original을 연결합니다.
```
secretId=[secretId]&currentTimeStamp=[currentTimeStamp]&expireTime=[expireTime]&random=[random]
```
>
	- 상기 original의 `[secretId]`, `[currentTimeStamp]`, `[expireTime]` 및 `[random]`은 실제 매개변수 값으로 대체되어야 합니다.
	- original은 4개의 필수 매개변수 `secretId`, `currentTimeStamp`, `expireTime` 및 `random`을 포함해야 하고 여러 임의의 매개변수 옵션을 포함할 수 있습니다. 자세한 내용은 [서명 매개변수](#p2)를 참고하십시오.
	- 매개변수 값은 UrlEncode되어야 하며 그렇지 않으면 QueryString 구문 분석이 실패할 수 있습니다.
3. **일반 텍스트 문자열을 서명으로 변환**(예: Java 코드 사용).
	1. SecretKey를 사용하여 [HMAC-SHA1](https://www.ietf.org/rfc/rfc2104.txt) 알고리즘으로 original 일반 텍스트 문자열을 암호화하여 signatureTmp를 가져옵니다.
	```java
	 Mac mac = Mac.getInstance("HmacSHA1");
   SecretKeySpec secretKey = new SecretKeySpec(this.secretKey.getBytes("UTF-8"), mac.getAlgorithm());
   mac.init(secretKey);
	 byte[] signatureTmp = mac.doFinal(original.getBytes("UTF-8"));
	```
	>! **signatureTmp는 UTF-8로 인코딩되고 HMAC-SHA1로 암호화된 바이트 배열입니다**.
	
	2. UTF-8을 사용하여 일반 텍스트 문자열 original을 바이트 배열로 인코딩하고, 배열을 signatureTmp와 병합한 다음 이 조합을 [Base64](https://tools.ietf.org/html/rfc4648)로 인코딩하여 signature를 가져옵니다.
```java
String signature = base64Encode(byteMerger(signatureTmp, original.getBytes("utf8")));
```
>**byteMerger와 base64Encode는 각각 배열 병합과 Base64 인코딩 방식으로, 자세한 내용은 [Java의 서명 코드 예시](https://intl.cloud.tencent.com/document/product/266/33923#java-.E7.AD.BE.E5.90.8D.E7.A4.BA.E4.BE.8B)를 참고하십시오**.

## 서명 생성 예시
VOD는 또한 **서명 생성을 위한 코드 예시**와 참고 및 확인을 위한 서명 생성 툴을 제공합니다.
- [클라이언트에서 업로드 - 서명 생성 코드 예시](https://intl.cloud.tencent.com/document/product/266/33923)
- [클라이언트에서 업로드 - 서명 생성 툴](https://video.qcloud.com/signature/ugcgenerate.html)
- [클라이언트에서 업로드 - 서명 검사 툴](https://video.qcloud.com/signature/ugcdecode.html)
		

<span id ="p2"></span>
## 서명 매개변수에 대한 설명

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
| --- | --- | --- | --- |
| secretId | Yes | String | Tencent Cloud API 키의 SecretId. 가져오는 방법은 [클라이언트에서 업로드 가이드 - Tencent Cloud API 키 가져오기](https://intl.cloud.tencent.com/document/product/266/33921#p3)를 참고하십시오. |
| currentTimeStamp | Yes | Integer | 현재의 Unix 타임스탬프. |
| expireTime | Yes | Integer| 서명 만료에 대한 Unix 타임스탬프.<br/>```expireTime = currentTimeStamp + 서명 유효 기간```<br/>서명 유효 기간의 최대값은 7,776,000(즉, 90일)입니다. |
| random | Yes | Integer | 일반 텍스트 서명 문자열을 구성하는 데 사용되는 매개변수(십진수). 최대값은 `xxxxx`(32비트 부호 없는 이진수의 최대값)입니다. |
| classId | No | Integer | 비디오 파일 카테고리. 기본값: 0. |
|<span id ="p3"></span> procedure | No | String | 비디오에 대한 후속 작업 작업. 즉 비디오 파일이 업로드된 후 태스크 플로우 작업이 자동으로 시작됩니다. 이 매개변수 값은 태스크 플로우 템플릿 이름입니다. VOD는 [태스크 플로우 템플릿 생성](https://intl.cloud.tencent.com/document/product/266/14058) 및 템플릿 이름 지정을 지원합니다. |
| taskPriority | No | Integer | 후속 비디오 작업의 우선 순위(procedure가 지정된 경우에만 유효). 값 범위: [-10, 10] 기본값: 0.|
| taskNotifyMode | No | String | 태스크 플로우 상태 변경에 대한 알림 모드(procedure가 지정된 경우에만 유효).<li>Finish: 이벤트 알림은 태스크 플로우가 완전히 실행된 후에만 시작됩니다.</li><li>Change: 태스크 플로우의 서브 작업 상태가 변경되는 즉시 이벤트 알림이 시작됩니다.</li><li>None: 태스크 플로우에 대한 콜백은 허용되지 않습니다. </li>기본값: Finish.|
| sourceContext | No | String | 사용자 요청 정보를 전달하는 데 사용되는 소스 컨텍스트입니다. [업로드 완료 콜백](https://intl.cloud.tencent.com/document/product/266/33950) API는 이 필드의 값을 반환합니다. 최대 250자를 포함할 수 있습니다. |
| oneTimeValid | No | Integer | 서명의 일회성 여부. 자세한 내용은 [클라이언트 업로드 가이드 - 일회성 서명](https://intl.cloud.tencent.com/document/product/266/33921#p4)을 참고하십시오.<br>0(기본값): 활성화되지 않음. 1: 활성화됨.<br>관련 오류 코드는 [일회성 서명 설명](#p1)을 참고하십시오. |
| vodSubAppId | No | Integer | [서브 애플리케이션](https://intl.cloud.tencent.com/document/product/266/33987) ID, 이 매개변수가 공란, 0 또는 Tencent Cloud AppId면, 작업된 서브 애플리케이션이 ‘메인 애플리케이션’이 됩니다. |
| sessionContext | No | String | 사용자 요청 정보를 전달하는 데 사용되는 세션 컨텍스트. 프로시저 매개변수가 지정되면 [태스크 플로우 상태 변경 콜백](https://intl.cloud.tencent.com/document/product/266/33953) API가 이 필드의 값을 반환합니다. 최대 1,000자를 포함할 수 있습니다.|
| storageRegion | No | String | 스토리지 리전 지정. 콘솔에서 직접 스토리지 리전을 추가할 수 있습니다. 자세한 내용은 [스토리지 설정 업로드](https://intl.cloud.tencent.com/document/product/266/18874)를 참고하십시오. 이 필드는 리전 [영어 약칭](https://intl.cloud.tencent.com/document/product/266/33910)을 입력해야 합니다.|

<span id ="p1"></span>
#### 일회성 서명 설명

- 일회성 서명 기능이 활성화된 후 서명 서버는 사용자에게 배포되는 서명이 매번 다른지 확인해야 합니다(예: 동시에 배포되는 서명의 `random` 매개변수가 고유해야 함). 그렇지 않으면 중복 서명 오류가 발생합니다.
- 서명 오류로 인해 업로드가 실패하면 재시도를 위해 새 서명을 받아야 합니다.
- Android 및 Java용 SDK로 인한 서명 오류의 오류 코드는 1001입니다.



