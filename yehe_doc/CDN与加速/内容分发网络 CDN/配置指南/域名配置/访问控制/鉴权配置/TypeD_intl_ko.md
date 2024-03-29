## 알고리즘 설명
**액세스 URL 형식**
`http://DomainName/FileName?sign=md5hash&t=timestamp`

**알고리즘 설명**
- timestamp: 10진법/16진법(UNIX 타임스탬프) 선택 가능
- md5hash: MD5(사용자 정의 키 + 파일 경로 + timestamp)

**요청 예시**
`http://cloud.tenloud.tencent.com/test.jpg?sign=0f8201d814dfaf64cf54e74c5f7dbcb0&t=1582791032`

> !MD5 계산 시 요청 경로가 `http://cloud.tencent.com/test.jpg`인 경우, MD5 계산 시 경로는 `/test.jpg`입니다.

## 설정 가이드
### 매개변수 설명
TypeD에 필요한 설정은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/6caae33f26a263699003ccb2e4e562c5.png)
**사용자 정의 인증 키：**6 - 40자리 대소문자 알파벳 및 숫자로 구성합니다. 키는 보안 유지되어야 하며 클라이언트와 서버만 알고 있어야 합니다.
**사용자 정의 인증 매개변수 이름 및 타임스탬프 매개변수 이름：**예시 상의 sign을 임의의 1~100자리 대소문자 알파벳, 숫자 또는 언더바로 구성된 매개변수로 대체한 후, CDN이 요청을 받은 뒤 지정한 서명 매개변수에 따라 상응하는 값을 추출하여 MD5 계산을 합니다. 전송되어 온 값이 md5hash 값과 매칭되면 서명 인증이 통과된 것이며, 인증이 통과되지 않은 경우 직접 403이 리턴됩니다.
**사용자 정의 유효시간**: 타임스탬프 매개변수 설정에서 timestamp 값을 취한 후 설정된 유효시간을 추가해 현재 시간과 비교하여 요청 유효시간이 만료되었는지 여부를 판단하며 만료된 경우 직접 403이 리턴됩니다. 유효시간의 단위는 초입니다. 

### 적용 객체
키, 매개변수 이름, 만료 시간을 설정한 후, 지정이 필요한 인증 객체에 따라 다음 세 가지 모드를 지원합니다.
![](https://main.qcloudimg.com/raw/8a9b8c36cfc91a31cf96b31f0e6553c2.png)

+ 지정 도메인의 모든 파일 인증 필요
+ 지정 유형의 파일은 인증하지 않고, 다른 파일들은 모두 인증 필요
+ 지정 유형의 파일 인증

## 주의 사항
** 캐시 히트율**
TypeD 인증 모델의 도메인을 활성화하면 액세스 URL에 인증 매개변수가 수반되고, CDN 노드에서 리소스 캐시할 때 자동으로 상응하는 매개변수를 생략해 도메인 캐시 히트율에 영향을 주지 않습니다.
>! 설정 후 자동으로 상응하는 매개변수를 생략하고 설정한 인증 매개변수와 타임스탬프 매개변수를 필터하기 때문에 인증 범위 내 파일의 캐시 키 값에 영향을 미치게 되며, 우선순위는 [Cache Configuration - Cache Key Rule Configuration]에서 설정한 캐시 키 값 규칙보다 높습니다.
예: 여기에서 TypeD를 인증 매개변수: sign, 타임스탬프 매개변수: t, 인증 범위: jpg로 설정하면 [Cache Configuration - Cache Key Rule Configuration]에서 모든 파일 - 매개변수 필터링하지 않음으로 설정해도 jpg 유형의 파일은 자동으로 “sign”과 “t” 매개변수로 필터링됩니다.

**원본 가져오기 정책**
TypeD 인증 모델의 도메인을 활성화하고 액세스 형식을 다음과 같이 설정합니다.
`http://DomainName/FileName?sign=md5hash&t=timestamp`

인증 통과 후 CDN 노드가 미스되면 노드에서 원본 요청을 보냅니다. **형식과 액세스 요청이 일관되면 sign/t 매개변수는 유지됩니다.** 원본 서버에서는 필요에 따라 2차 인증을 생략하거나 실시합니다.
