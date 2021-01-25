## 알고리즘 설명
**액세스 URL 형식**
`http://DomainName/timestamp/md5hash/FileName`

**알고리즘 설명**
- timestamp: 타임스탬프. 형식은 YYYYMMDDHHMM입니다.
- md5hash: MD5(사용자 지정 키 + timestamp + 파일 경로).

**요청 예시**
`http://cloud.tencent.com/202003032017/b91bad39a0f9c885ddebd6b6164de3c4/test.jpg`

> !MD5 계산 시 요청 경로가 `http://cloud.tencent.com/test.jpg`라면 MD5 계산 경로는 `/test.jpg`입니다.

## 설정 가이드

### 매개변수 설명
TypeB 설정 내용은 아래와 같습니다.
![](https://main.qcloudimg.com/raw/d0cd00305ed4911a500995628bd45cfd.png)
**사용자 정의 인증 키: **6 - 32자리의 알파벳 대소문자, 숫자로 구성, 키 보안은 매우 중요하며 사용자 측과 서버 측만 알고 있습니다.
**사용자 정의 유효 시간: **요청 경로의 timestamp 값을 통해 설정한 유효 시간과 현재 시간을 비교하여, 요청이 만료되었는지 확인하고, 만료된 경우 403을 리턴합니다. 

### 유효 대상
키, 매개변수 명칭 및 만료 시간을 설정한 후 필요에 따라 다음 세 가지 중 하나로 인증 대상을 지정할 수 있습니다.
![](https://main.qcloudimg.com/raw/13ccf23f34aaa9963e2ca36ea48b36f0.png)
- 도메인의 모든 파일을 인증 확인합니다.
- 지정 파일 유형에 대해서만 인증하지 않고, 나머지는 인증 확인합니다.
- 지정 파일 유형에 대해서만 인증 확인합니다.

## 주의 사항
**캐시 히트율**
TypeB 인증 모드를 활성화하면, 액세스 URL 경로에 서명 및 타임스탬프가 포함됩니다. CDN 노드에서 리소스 캐싱 시 경로 내의 필드를 무시하고 캐싱하여, 도메인의 캐시 히트율에 영향을 주지 않습니다.
**Origin-pull 정책**
TypeB 인증 모드를 활성화한 도메인의 액세스 형식은 다음과 같습니다.
`http://DomainName/timestamp/md5hash/FileName`

인증 성공 후 CDN 노드와 히트하지 않는 경우 원본 서버에서 별도의 처리 없이, 노드가 원본 요청을 보내고, **원본 요청이 경로의 md5hash 및 timestamp**를 삭제합니다.

