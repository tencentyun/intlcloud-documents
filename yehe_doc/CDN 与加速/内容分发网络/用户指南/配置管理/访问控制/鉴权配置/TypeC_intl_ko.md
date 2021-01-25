## 알고리즘 설명
**액세스 URL 형식**
`http://DomainName/md5hash/timestamp/FileName`

**알고리즘 설명**
- timestamp: 16진법(UNIX 타임스탬프).
- md5hash: MD5(사용자 지정 키 + 파일 경로 + timestamp).

**요청 예시**
`http://cloud.tencent.com/8fe9b5597c809d7ace147468c7c7eadb/5e577978/test/test.jpg`

>요청 경로가 `http://cloud.tencent.com/test.jpg`이면 MD5 계산 시의 경로는 `/test.jpg`입니다.

## 설정 가이드
### 매개변수 설명
TypeC 설정 시 필요한 내용은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/d7b8d589f8690f1e4c33985d6bcd3f09.png)
**사용자 지정 인증키: **6 - 32자리의 대소문자, 숫자로 구성됩니다. 키는 사용자와 서버만 알도록 보안을 엄격히 준수해야 합니다.
**사용자 지정 유효시간: **요청 경로 내의 timestamp 값을 통해 설정된 유효시간을 추가한 후 현재 시간과 대조하여 요청의 만료 여부를 판단합니다. 만료 시 바로 403을 리턴합니다.

### 적용 객체
키, 매개변수 명, 만료 시간을 설정한 후 필요에 따라 인증 객체를 아래의 3가지 모드 중 하나로 지정할 수 있습니다.
![](https://main.qcloudimg.com/raw/34d27c8908808cacddfde94c8a3f1d81.png)
+ 지정한 도메인 아래 모든 파일을 인증하도록 설정합니다.
+ 지정 유형의 파일은 인증하지 않고, 나머지는 모두 인증하도록 설정합니다.
+ 지정 유형의 파일만 인증하도록 설정합니다.

## 주의 사항
**캐시 히트율**
TypeC 인증 모드를 활성화한 도메인은 URL에 액세스할 때 인증 매개변수를 포함하므로 CDN 노드에서 리소스를 캐싱할 때 해당하는 인증 경로를 자동으로 무시하기 때문에, 도메인 캐시 히트율에 영향을 미치지 않습니다.
**원본 요청 정책**
TypeC 인증 모드를 활성화한 도메인의 액세스 형식은 다음과 같습니다.
`http://DomainName/md5hash/timestamp/FileName`

인증 확인 통과 후 CDN 노드에 히트하지 못하면 노드가 요청을 보내 **원본 요청 시 경로 중의 md5hash 및 timestamp 경로를 제거하므로**, 원본 서버가 특별히 처리할 필요가 없습니다.
