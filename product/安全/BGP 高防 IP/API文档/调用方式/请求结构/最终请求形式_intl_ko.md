[//]: # (chinagitpath:XXXXX)

### 합치기 규칙
Tencent Cloud API 요청 URL 합치기 규칙은 다음과 같습니다.
> **https:// + 요청 도메인 이름 +요청 경로 + ? +최종 요청 매개변수 문자열**

구성 부분 설명:
-  **요청 도메인 이름:** 요청 도메인 이름은 API 소속 제품 또는 소속 제품의 모듈에 따라 달라집니다. 예를 들어 Tencent Cloud CVM의 인스턴스 리스트 조회(DescribeInstances)의 요청 도메인 이름은 `cvm.api.qcloud.com`입니다. 구체적인 제품 요청 도메인 이름은 각 API의 설명을 참조하십시오.
-  **요청 경로:** Tencent Cloud API에 대응하는 제품의 요청 경로입니다. 일반적으로 하나의 제품이 하나의 고정 경로와 대응합니다. 예를 들어 Tencent Cloud CVM 요청 경로는 항상 `/v2/index.php`입니다.
- **최종 요청 매개변수 문자열:** API의 요청 매개변수 문자열은 공용 요청 매개변수와 API 요청 매개변수를 포함합니다.

### 사용 사례
Tencent Cloud API 최종 요청의 URL 구조는 다음과 같습니다.
Tencent Cloud CVM [인스턴스 리스트 조회](https://cloud.tencent.com/document/api/213/15728) API(DescribeInstances)를 예로, 앞부분 6개의 매개변수가 공용 요청 매개변수, 뒷부분 6개의 매개변수가 API 요청 매개변수입니다.

```
https://cvm.api.qcloud.com/v2/index.php?
Action=DescribeInstances
&SecretId=xxxxxxx
&Region=gz
&Timestamp=1465055529
&Nonce=59485
&Signature=mysignature       //공용 요청 매개변수
&instanceIds.0=ins-0hm4gvho
&instanceIds.1=ins-8oby8q00
&offset=0
&limit=20
&status=2
&zoneId=100003      //API 요청 매개변수
```

