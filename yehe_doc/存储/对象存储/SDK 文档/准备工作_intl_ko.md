SDK 사용 시 다음의 개념과 용어가 언급될 수 있으므로 관련 정보를 미리 숙지하시기 바랍니다.

| 이름             | 설명                                                         |
| :--------------- | :----------------------------------------------------------- |
| APPID            | COS 서비스에 액세스하는 개발자가 보유한 사용자 차원의 고유 리소스 식별자. 리소스 표시에 사용하며, [API 키 관리](https://console.cloud.tencent.com/capi) 페이지에서 획득 가능 |
| SecretId         | 개발자가 보유한 프로젝트 신원 확인 ID. 실명 인증에 사용하며, [API 키 관리](https://console.cloud.tencent.com/capi) 페이지에서 획득 가능 |
| SecretKey        | 개발자가 보유한 프로젝트 신원 확인 키. [API 키 관리](https://console.cloud.tencent.com/capi) 페이지에서 획득 가능 |
| Bucket           | 버킷. COS에서 데이터 저장에 사용되는 컨테이너이며, 버킷과 관련된 자세한 내용은 [버킷 개요](https://intl.cloud.tencent.com/document/product/436/13312) 문서 참고 |
| BucketName-APPID | APPID를 접미사로 하는 전체 버킷 이름(예시: `examplebucket-1250000000`) |
| Object           | 객체. COS에 저장되는 구체적인 파일이며 스토리지의 기본 실체                 |
| ObjectKey        | 객체 키. 버킷에 있는 객체의 고유 식별자로, 객체와 객체 키에 대한 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324) 문서 참고 |
| Region           | 리전 정보. 열거 값은 [가용 리전](https://intl.cloud.tencent.com/document/product/436/6224) 문서 참고. 예시: ap-beijing, ap-hongkong, eu-frankfurt 등 |
| ACL              | 액세스 제어 리스트(Access Control List). 특정 Bucket 또는 Object의 액세스 제어 정보 리스트로, [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583) 문서 참고 |

>? XML 버전 SDK 사용 중 함수 또는 메소드가 존재하지 않는 등의 오류 발생 시, XML 버전 SDK를 최신 버전으로 업그레이드한 후 재시도하십시오.
>
