## 알고리즘 설명
**액세스 URL 형식**
`http://DomainName/timestamp/md5hash/FileName`

**알고리즘 설명**
- timestamp: 타임스탬프. 형식은 YYYYMMDDHHMM입니다.
- md5hash: MD5(사용자 지정 키 + timestamp + 파일 경로).

**요청 예시**
`http://cloud.tencent.com/202003032017/b91bad39a0f9c885ddebd6b6164de3c4/test.jpg`

> !MD5 계산 시 요청 경로가 `http://cloud.tencent.com/test.jpg`인 경우, MD5 계산 시 경로는 `/test.jpg`입니다.

## 설정 가이드

### 매개변수 설명
TypeB에 필요한 설정은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/d0cd00305ed4911a500995628bd45cfd.png)
**사용자 정의 인증 키：**6 - 40자리 대소문자 알파벳 및 숫자로 구성합니다. 키는 보안 유지되어야 하며 클라이언트와 서버만 알고 있어야 합니다.
**사용자 정의 유효시간：**요청 경로 상의 timestamp 값에 설정된 유효시간을 추가해 현재 시간과 비교하여 요청 유효시간이 만료되었는지 여부를 판단하며 만료된 경우 직접 403이 반환됩니다. 유효시간의 단위는 초입니다.

### 적용 객체
키, 매개변수 이름, 만료 시간을 설정한 후, 지정이 필요한 인증 객체에 따라 다음 세 가지 모드를 지원합니다.
![](https://main.qcloudimg.com/raw/13ccf23f34aaa9963e2ca36ea48b36f0.png)

- 지정 도메인의 모든 파일 인증 필요
- 지정 유형의 파일은 인증하지 않고, 다른 파일들은 모두 인증 필요
- 지정 유형의 파일 인증

## 주의 사항
**캐시 히트율**
TypeB 인증 모델의 도메인을 활성화하면 액세스 URL 경로에 서명 및 타임스탬프가 수반되고, CDN 노드에서 리소스를 캐시할 때 자동으로 경로 상의 필드를 생략해 도메인 캐시 히트율에 영향을 주지 않습니다.
**원본 가져오기 정책**
TypeB 인증 모델의 도메인을 활성화하고 액세스 형식을 다음과 같이 설정합니다.
`http://DomainName/timestamp/md5hash/FileName`

인증 완료 후 CDN 노드가 미스되는 경우, 노드에서 원본 가져오기 요청을 발송하며 **원본 가져오기 요청 시 경로 상의 md5hash와 timestamp를 제거하여** 원본 서버에서 특수 처리를 하지 않아도 됩니다.

