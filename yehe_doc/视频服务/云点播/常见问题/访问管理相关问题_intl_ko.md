### 파일을 업로드하려면 어떤 권한이 필요합니까?

VOD는 [서버에서 업로드](https://intl.cloud.tencent.com/document/product/266/33912), [클라이언트에서 업로드](https://intl.cloud.tencent.com/document/product/266/33921), [풀링 업로드](https://intl.cloud.tencent.com/document/product/266/34118) 등 다양한 업로드 방법을 제공합니다. 각 방법에 필요한 권한은 다음과 같습니다.


| 업로드 방법   | 리소스 권한     | 작업 권한                                                     | 비고               |
| ---------- | ------------ | ------------------------------------------------------------ | ------------------ |
| 서버에서 업로드 | 지정된 서브 애플리케이션 | [업로드 신청](https://intl.cloud.tencent.com/document/product/266/34120)<br/>[업로드 확인](https://intl.cloud.tencent.com/document/product/266/34119) | -                  |
| 클라이언트에서 업로드 | 지정된 서브 애플리케이션 | [업로드 신청](https://intl.cloud.tencent.com/document/product/266/34120)<br/>[업로드 확인](https://intl.cloud.tencent.com/document/product/266/34119) | -                  |
| 풀링 업로드   | 지정된 서브 애플리케이션 | [풀링 업로드](https://intl.cloud.tencent.com/document/product/266/34118)                      | -                  |
| 라이브 방송 녹화   | 모든 서브 애플리케이션   | -                                                            | 라이브 방송 녹화 기능을 활성화해야 합니다. |

>? VOD 콘솔에서 동영상을 [로컬 업로드](https://intl.cloud.tencent.com/document/product/266/33890#.E6.9C.AC.E5.9C.B0.E4.B8.8A.E4.BC.A0.E6.AD.A5.E9.AA.A4)하는 것은 클라이언트에서 업로드 방식입니다.

### 서버에서 업로드할 경우 ‘권한 없음’ 오류가 반환되지만 다른 업로드 방식은 성공하는 이유는 무엇인가요?

이는 서버 SDK가 이전 버전이기 때문일 수 있습니다. [SDK](https://intl.cloud.tencent.com/document/product/266/33912#1.-.E5.8F.91.E8.B5.B7.E4.B8.8A.E4.BC.A0)를 최신 버전으로 업그레이드하십시오.

### 동영상을 시청하려면 어떤 권한이 필요합니까?

동영상 시청은 본질적으로 Tencent Cloud 계정이 아닌 일반 시청자로 VOD CDN에 요청하는 것이므로, 시청자에게 어떤 권한도 부여할 필요가 없습니다([링크 도용 방지](https://intl.cloud.tencent.com/document/product/266/33984) 또는 [비디오 암호화](https://intl.cloud.tencent.com/document/product/266/33968)가 활성화된 경우 관련 문서에 기재된 조건을 충족해야 비디오를 시청할 수 있지만 액세스 관리와 관련이 없습니다).

### 단일 파일에만 권한을 부여할 수 있습니까?

지원하지 않습니다. VOD 액세스 관리 리소스 단위는 서브 애플리케이션입니다.

### 권한 설정이 상호 충돌하면 어떻게 됩니까?

권한 설정 충돌은 다음과 같은 경우가 있을 수 있습니다.

- 사용자 정의 정책에 디스크립션이 상호 충돌하는 여러 선언이 포함되어 있는 경우(예: 한 선언은 리소스 액세스를 허용하지만 다른 선언은 이러한 액세스를 거부).
- 서브 계정에 디스크립션이 상호 충돌하는 여러 정책이 바인딩되어 있는 경우.

VOD 권한 관리는 CAM을 기반으로 하므로 VOD 권한은 CAM의 정책 [판단 로직](https://intl.cloud.tencent.com/document/product/598/10605)에 따라 결정됩니다.

### VOD는 계정 간 리소스 액세스를 지원합니까?

계정 간 리소스 액세스는 루트 계정 A가 루트 계정 B(또는 서브 계정)에 VOD 권한의 전부 또는 일부를 부여하는 것을 말합니다. 즉, 부여자와 피부여자는 두 개의 독립적인 Tencent Cloud 계정입니다. VOD는 계정 간 리소스 액세스를 **지원하지 않습니다**. 즉, Tencent Cloud 계정은 자체 서브 계정에만 VOD 권한을 부여할 수 있습니다.
