귀하의 사이트 리소스가 불법 사이트에 의해 다운로드 및 도난당하지 않도록 보호하기 위해 Type ABCD의 4가지 인증 방법 중 하나를 필요에 따라 선택할 수 있습니다. 본문에서는 Type C의 다양한 매개변수 필드와 원리를 자세히 소개합니다.

## 알고리즘 설명

-  **액세스 URL 형식**
`http://DomainName/md5hash/timestamp/FileName` 
  >!액세스 URL에 중국어를 포함할 수 없습니다.

-  **인증 필드 설명**
  
  <table>
  <thead>
  <tr>
  <th>필드</th>
  <th>설명</th>
  </tr>
  </thead>
  <tbody><tr>
  <td>DomainName</td>
  <td>CDN 도메인.</td>
  </tr>
  <tr>
  <td>Filename</td>
  <td>리소스 액세스 경로, Filename은 인증 시 슬래시( <code>/</code> )로 시작해야 합니다.   </td>
  </tr>
  <tr>
  <td>timestamp</td>
  <td>서버에 의해 인증 URL이 생성된 시간, 16진법 정수가 포함된 Unix 타임스탬프로 1970년 01월 01일 UTC 시간 00:00:00부터 현재까지의 총 시간(초)입니다. 정의는 시간대와 무관합니다. </td>
  </tr>
  <tr>
  <td>md5hash</td>
  <td>MD5 알고리즘으로 계산된 고정 길이 32비트 문자열입니다. 구체적인 계산식은 다음과 같습니다. <br>•  md5hash = md5sum(pkeytimestampuri) 매개변수 사이에 부호가 없습니다.  <br>•  pkey: 사용자 지정 키: 6 - 40개의 대소문자와 숫자로 구성되며, 키는 철저히 기밀로 유지되어야 하며 클라이언트와 서버만 알 수 있습니다. <br>•   uri 리소스 액세스 경로는 슬래시(/)로 시작합니다. <br>•  timestamp: 위의 타임스탬프 값입니다. </td>
  </tr>
  </tbody></table>
-  **인증 로직 설명**
	클라이언트 요청을 수신한 CDN 서버는 url의 timestamp 매개변수 + 인증 URL의 유효 기간을 파싱하여 현재 시간과 비교합니다.
	1. timestamp + 인증 URL의 유효 기간이 현재 시간보다 짧으면 서버는 만료되어 유효하지 않은 것으로 판단하고 HTTP 403 오류를 반환합니다.
	2. timestamp + 인증 URL의 유효 기간이 현재 시간보다 긴 경우 MD5 알고리즘을 사용하여 md5hash 값을 계산한 다음 계산된 md5hash 값을 url에 전달된 md5hash 값과 비교합니다. 일관성이 있으면 그대로 두고 일관성이 없으면 HTTP 403 오류를 반환합니다.

## 구성 가이드 

**Type-C 인증 구성을 예로 들면 매개변수 및 콘솔 구성은 다음과 같습니다.**

- **필드 구성**
  - 인증 키: dimtm5evg50ijsx2hvuwyfoiu65
  - 인증 URL의 유효 기간: 1s   
  - 서명 서버가 인증 URL을 생성한 시간: 2020년 02월 27일 16:10:32(UTC+8), 10진법으로 변환된 정수 값은 1582791032(timestamp)
  - 요청 원본 서버 주소: `http://cloud.tencent.com/test.jpg`
	
- 생성 과정
  - 인증 매개변수 가져오기
    <table>
    <thead>
    <tr>
    <th>매개변수</th>
    <th>값</th>
    </tr>
    </thead>
    <tbody><tr>
    <td>uri</td>
    <td>리소스 액세스 경로: /test.jpg</td>
    </tr>
    <tr>
    <td>timestamp</td>
    <td>1582791032</td>
    </tr>
    <tr>
    <td>dimtm5evg50ijsx2hvuwyfoiu65</td>
    </tr>
    </tbody></table>
  - 서명 문자열 스플라이싱: dimtm5evg50ijsx2hvuwyfoiu651582791032/test.jpg
  - 서명 문자열의 md5 값 계산: md5hash = md5sum(pkeytimestampuri) =md5sum(dimtm5evg50ijsx2hvuwyfoiu651582791032/test.jpg) = ea68b93ac23ebbc6eebf7f163c6e9c4c

-   **인증 URL 생성:**
`http://cloud.tencent.com/ea68b93ac23ebbc6eebf7f163c6e9c4c/1582791032/test.jpg` 
클라이언트가 암호화된 URL을 통해 액세스할 때 CDN 서버에서 계산한 md5hash 값이 액세스 요청에 포함된 md5hash 값과 같으면 모두 ea68b93ac23ebbc6eebf7f163c6e9c4c인 경우 인증에 통과하고, 그렇지 않으면 인증에 실패합니다.

## 주의 사항 

**캐시 히트율** 
TypeC 인증 모델의 도메인을 활성화하면 액세스 URL 경로에 서명 및 타임스탬프가 수반되고, CDN 노드에서 리소스를 캐시할 때 자동으로 인증 경로를 생략해 도메인 캐시 히트율에 영향을 주지 않습니다.

**Origin-pull 정책**
TypeC 인증 모델의 도메인을 활성화하고 액세스 형식을 다음과 같이 설정합니다.
 `http://DomainName/md5hash/timestamp/FileName` 

인증 완료 후 CDN 노드가 미스되는 경우, 노드에서 원본 가져오기 요청을 발송하며 **원본 가져오기 요청 시 경로 상의 md5hash와 timestamp 경로를 제거하여** 원본 서버에서 특수 처리를 하지 않아도 됩니다.
