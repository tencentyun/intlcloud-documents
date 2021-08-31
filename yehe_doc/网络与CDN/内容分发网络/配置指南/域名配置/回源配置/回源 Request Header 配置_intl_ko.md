## 설정 시나리오

Tencent Cloud CDN은 원본 요청 헤더 추가를 지원합니다.

- X-Forward-For 헤더를 통해 실제 클라이언트 IP를 원본 서버까지 전송할 수 있습니다.
- X-Forward-Port 헤더를 통해 실제 클라이언트 포트를 원본 서버까지 전송할 수 있으며, 이는 원본 서버 분석에 사용됩니다.
- 다양한 사용자 정의 헤더를 추가할 수 있습니다.

사용자 정의 원본 요청 헤더의 설정 및 삭제 기능도 지원합니다.

## 설정 가이드

### 설정 조회

[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인한 후, 메뉴에서 [도메인 관리]를 선택하여 도메인 오른쪽의 [관리]를 클릭하면 [원본 설정]의 원본 요청 헤더 설정을 볼 수 있습니다. 초기에는 비활성화 상태로, 설정이 되어있지 않습니다:
![img](https://main.qcloudimg.com/raw/c41a39a9a851fbe3778ca325edc2e3f8.png)

### 작업 유형

| 작업 유형 | 설명                                                         |
| -------- | ------------------------------------------------------------ |
| 설정     | 지정된 요청 헤더 매개변수의 값을 설정 완료 후의 값으로 변경합니다. <br/>설정된 헤더가 존재하지 않을 경우, 해당 헤더를 추가합니다. <br/>원본 요청 헤더 매개변수가 이미 존재하는 경우, 설정한 요청 헤더가 기존 헤더를 덮어쓰기함으로써 유일한 헤더가 됩니다. |
| 추가     | 지정된 원본 요청 헤더의 매개변수를 추가합니다. <br/>설정된 헤더가 이미 존재하는 경우, 추가한 요청 헤더가 기존 헤더에 덮어쓰기 됩니다. |
| 삭제     | 지정된 응답 헤더의 매개변수를 삭제합니다.                                       |

>!
> - 하단 규칙의 우선순위가 상단 규칙보다 높습니다. 위치에 따른 우선순위는 헤드 추가 규칙, 헤드 삭제 규칙 또는 헤드 설정 규칙과 같이 동일한 유형의 헤더 작업에서 적용됩니다.
> - 하나의 원본 요청 헤더 매개변수에 여러 유형의 작업을 동시 진행하는 경우, 작업 유형의 우선순위에 따라 진행되며 그 순서는 추가, 삭제, 설치 순입니다. 예시: X-CDN 헤드의 추가, 삭제 및 설정 규칙이 동시에 존재하는 경우에는 추가, 삭제, 설정의 순서로 진행됩니다.

### 헤더 매개변수

| 헤더 매개변수       | 설명                                                         |
| -------------- | ------------------------------------------------------------ |
| X-Forward-For  | 실제 클라이언트의 IP 헤더를 전달하는 데 사용됩니다. 기본값은 $client_ip 변수이고, 변경할 수 없습니다. |
| X-Forward-Port | 실제 클라이언트의 포트 헤더를 전달하는 데 사용됩니다. 기본값은 $remote_port 변수이고, 변경할 수 없습니다. |
| 사용자 정의 헤더    | 사용자 정의 헤더 Key 길이의 기본값은 1~100자로, 0~9, a~z, A~Z와 특수부호 `-`로 구성됩니다. <br>Value 길이는 1~1,000자이며, 중국어는 지원하지 않습니다. <br>일부 표준 헤더는 자동 설정/추가/삭제를 지원하지 않습니다. 상세 정보는 [주의사항] 문서(#noice)를 참조 바랍니다. |

> !
> - 원본 요청 Header의 설정 규칙은 최대 10개까지 설정할 수 있습니다.
> - 적용 유형은 모든 파일, 파일 형식, 파일 디렉터리, 지정 파일 경로의 4가지 모드를 지원하며, 현재 정규 매칭은 지원하지 않습니다.



## 설정 예시

가속 도메인이 `cloud.tencent.com`인 원본 요청 헤더의 설정은 다음과 같습니다:
![img](https://main.qcloudimg.com/raw/397759f6f138183d3f1ba60b33c7effc.png)
리소스 `http://cloud.tencent.com/test/test.mp4`에 액세스한 경우

1. `*` 규칙에 도달하는 경우, `X-Forward-For:$client_ip` 헤더를 추가해 원본 가져오기 실행 시 $client_ip를 실제 클라이언트 IP로 변경합니다.
2. `.mp4` 유형의 파일 및 /test 경로에 도달하는 경우는 모두 추가 유형의 헤더 작업이기 때문에 하단 규칙이 상단 규칙 보다 우선 적용되어 `x-cdn:Tencent` 헤더가 추가됩니다.

<span id="noice"></span>

## 주의 사항
다음 표준 헤더는 원본 요청 헤더의 설정/추가/삭제 기능을 제공하지 않습니다.

| www-authenticate              | authorization                    | proxy-authenticate             | proxy-authorization                 |
| ----------------------------- | -------------------------------- | ------------------------------ | ----------------------------------- |
| age                           | cache-control                    | clear-site-data                | expires                             |
| pragma                        | warning                          | accept-ch                      | accept-ch-lifetime                  |
| early-data                    | content-dpr                      | dpr                            | device-memory                       |
| save-data                     | viewport-width                   | width                          | last-modified                       |
| etag                          | if-match                         | if-none-match                  | if-modified-since                   |
| if-unmodified-since           | vary                             | connection                     | keep-alive                          |
| accept                        | accept-charset                   | expect                         | max-forwards                        |
| access-control-allow-origin   | access-control-max-age           | access-control-allow-headers   | access-control-allow-methods        |
| access-control-expose-headers | access-control-allow-credentials | access-control-request-headers | access-control-request-method       |
| origin                        | timing-allow-origin              | dnt                            | tk                                  |
| content-disposition           | content-length                   | content-type                   | content-encoding                    |
| content-language              | content-location                 | forwarded                      | x-forwarded-host                    |
| x-forwarded-proto             | via                              | from                           | host                                |
| referer-policy                | allow                            | server                         | accept-ranges                       |
| range                         | if-range                         | content-range                  | cross-origin-embedder-policy        |
| cross-origin-opener-policy    | cross-origin-resource-policy     | content-security-policy        | content-security-policy-report-only |
| expect-ct                     | feature-policy                   | strict-transport-security      | upgrade-insecure-requests           |
| x-content-type-options        | x-download-options               | x-frame-options(xfo)           | x-permitted-cross-domain-policies   |
| x-powered-by                  | x-xss-protection                 | public-key-pins                | public-key-pins-report-only         |
| sec-fetch-site                | sec-fetch-mode                   | sec-fetch-user                 | sec-fetch-dest                      |
| last-event-id                 | nel                              | ping-from                      | ping-to                             |
| report-to                     | transfer-encoding                | te                             | trailer                             |
| sec-websocket-key             | sec-websocket-extensions         | sec-websocket-accept           | sec-websocket-protocol              |
| sec-websocket-version         | accept-push-policy               | accept-signature               | alt-svc                             |
| date                          | large-allocation                 | link                           | push-policy                         |
| retry-after                   | signature                        | signed-headers                 | server-timing                       |
| service-worker-allowed        | sourcemap                        | upgrade                        | x-dns-prefetch-control              |
| x-firefox-spdy                | x-pingback                       | x-requested-with               | x-robots-tag                        |
| x-ua-compatible               | max-age                          |                                |                                     |
