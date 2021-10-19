
## 설정 시나리오

Tencent Cloud CDN은 원본 요청 헤더 추가 기능을 제공합니다.

- X-Forward-For 헤더를 통해 실제 클라이언트 IP를 원본 서버까지 전달하는 것이 지원됩니다.
- X-Forward-Port 헤더를 통해 실제 클라이언트 포트를 원본 서버까지 전달하는 것이 지원되며, 이는 원본 서버 분석에 사용됩니다.
- 다양한 사용자 정의 헤더를 추가할 수 있습니다.

## 설정 가이드

### 설정 약관

- 사용자 정의 요청 헤더 규칙은 최대 10개까지 설정할 수 있습니다.
- 지원하는 적용 유형(4가지): 모든 파일, 파일 형식, 파일 목록, 지정 파일 경로(현재 정규 매칭은 지원되지 않습니다).
- 클라이언트에서 발송한 요청에 헤더 정보가 존재할 경우, 설정한 Request Header는 원본 가져오기를 진행할 때 기존 헤더를 덮어씌웁니다.
- 헤더 규칙 설정이 중복될 경우, 상-하, 낮음-높음 순으로 우선순위가 적용됩니다. bottom의 우선순위는 top보다 높습니다.
- 사용자 정의 헤더의 키 Key 길이는 1~100자로, 0~9, a-z, A-Z, `-` 부호로 구성됩니다.
- 사용자 정의 헤더의 Value 길이는 1~1000자이며, 중국어는 지원되지 않습니다.
- 일부 표준 헤더는 직접 추가할 수 없습니다. 자세한 내용은 문서 마지막 부분의 설명을 참조하십시오.

### 설정 설명

[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인한 후, 메뉴에서 [Domain Management]를 선택하고, 도메인 이름 우측의 [Manage]를 클릭하면 [Origin Configuration]의 원본 가져오기 Request Header 설정을 볼 수 있습니다(초기에는 비활성화 상태입니다).
![](https://main.qcloudimg.com/raw/c41a39a9a851fbe3778ca325edc2e3f8.png)
비활성화 상태에서 원본 헤더 규칙 가져오기를 새로 추가할 수 있습니다.
![](https://main.qcloudimg.com/raw/e2972a9d697e45b3f081b68ea5e6badb.png)

> !
> 1. 실제 클라이언트의 IP를 전달하는 데 사용되는 헤더는 X-Forward-For이며, 기본값은 $client_ip 변수이고, 변경할 수 없습니다.
> 2. 실제 클라이언트의 포트를 전달하는 데 사용되는 헤더는 X-Forward-Port이며, 기본값은 $remote_port 변수이고, 변경할 수 없습니다.

규칙 추가 완료 후 전체 설정은 여전히 비활성 상태이므로 적용되지 않습니다.
![](https://main.qcloudimg.com/raw/10c8061c2e98c8828e3b153c028db86e.png)
[우선순위 변경] 버튼을 눌러 규칙의 순서를 변경할 수 있습니다. 모든 네트워크 CDN 노드에 적용해야 할 경우, 상단의 설정 버튼을 클릭하십시오.
![](https://main.qcloudimg.com/raw/10c8061c2e98c8828e3b153c028db86e.png)

## 설정 예시

가속 도메인 이름이 `cloud.tencent.com`인 원본 서버의 설정은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/397759f6f138183d3f1ba60b33c7effc.png)
액세스한 리소스가 `http://cloud.tencent.com/test/test.mp4`인 경우
1. `*` 규칙에 도달하는 경우, `X-Forward-For:$client_ip` 헤더를 추가해 원본 가져오기 시 $client_ip를 실제 클라이언트 IP로 교체합니다.
2. `.mp4` 유형의 파일 및 `/test` 경로에 도달하는 경우, bottom의 우선순위가 top보다 높으므로 `x-cdn:Tencent` 헤더를 추가합니다.

## 주의사항

다음 표준 헤더는 원본 가져오기 Request Header 기능을 제공하지 않습니다.

<table>
<tbody><tr>
<td>www-authenticate</td>
<td>authorization</td>
<td>proxy-authenticate</td>
<td>proxy-authorization</td>
</tr>
<tr>
<td>age</td>
<td>cache-control</td>
<td>clear-site-data</td>
<td>expires</td>
</tr>
<tr>
<td>pragma</td>
<td>warning</td>
<td>accept-ch</td>
<td>accept-ch-lifetime</td>
</tr>
<tr>
<td>early-data</td>
<td>content-dpr</td>
<td>dpr</td>
<td>device-memory</td>
</tr>
<tr>
<td>save-data</td>
<td>viewport-width</td>
<td>width</td>
<td>last-modified</td>
</tr>
<tr>
<td>etag</td>
<td>if-match</td>
<td>if-none-match</td>
<td>if-modified-since</td>
</tr>
<tr>
<td>if-unmodified-since</td>
<td>vary</td>
<td>connection</td>
<td>keep-alive</td>
</tr>
<tr>
<td>accept</td>
<td>accept-charset</td>
<td>expect</td>
<td>max-forwards</td>
</tr>
<tr>
<td>access-control-allow-origin</td>
<td>access-control-max-age</td>
<td>access-control-allow-headers</td>
<td>access-control-allow-methods</td>
</tr>
<tr>
<td>access-control-expose-headers</td>
<td>access-control-allow-credentials</td>
<td>access-control-request-headers</td>
<td>access-control-request-method</td>
</tr>
<tr>
<td>origin</td>
<td>timing-allow-origin</td>
<td>dnt</td>
<td>tk</td>
</tr>
<tr>
<td>content-disposition</td>
<td>content-length</td>
<td>content-type</td>
<td>content-encoding</td>
</tr>
<tr>
<td>content-language</td>
<td>content-location</td>
<td>forwarded</td>
<td>x-forwarded-host</td>
</tr>
<tr>
<td>x-forwarded-proto</td>
<td>via</td>
<td>from</td>
<td>host</td>
</tr>
<tr>
<td>referer</td>
<td>referer-policy</td>
<td>allow</td>
<td>server</td>
</tr>
<tr>
<td>accept-ranges</td>
<td>range</td>
<td>if-range</td>
<td>content-range</td>
</tr>
<tr>
<td>cross-origin-embedder-policy</td>
<td>cross-origin-opener-policy</td>
<td>cross-origin-resource-policy</td>
<td>content-security-policy</td>
</tr>
<tr>
<td>content-security-policy-report-only</td>
<td>expect-ct</td>
<td>feature-policy</td>
<td>strict-transport-security</td>
</tr>
<tr>
<td>upgrade-insecure-requests</td>
<td>x-content-type-options</td>
<td>x-download-options</td>
<td>x-frame-options(xfo)</td>
</tr>
<tr>
<td>x-permitted-cross-domain-policies</td>
<td>x-powered-by</td>
<td>x-xss-protection</td>
<td>public-key-pins</td>
</tr>
<tr>
<td>public-key-pins-report-only</td>
<td>sec-fetch-site</td>
<td>sec-fetch-mode</td>
<td>sec-fetch-user</td>
</tr>
<tr>
<td>sec-fetch-dest</td>
<td>last-event-id</td>
<td>nel</td>
<td>ping-from</td>
</tr>
<tr>
<td>ping-to</td>
<td>report-to</td>
<td>transfer-encoding</td>
<td>te</td>
</tr>
<tr>
<td>trailer</td>
<td>sec-websocket-key</td>
<td>sec-websocket-extensions</td>
<td>sec-websocket-accept</td>
</tr>
<tr>
<td>sec-websocket-protocol</td>
<td>sec-websocket-version</td>
<td>accept-push-policy</td>
<td>accept-signature</td>
</tr>
<tr>
<td>alt-svc</td>
<td>date</td>
<td>large-allocation</td>
<td>link</td>
</tr>
<tr>
<td>push-policy</td>
<td>retry-after</td>
<td>signature</td>
<td>signed-headers</td>
</tr>
<tr>
<td>server-timing</td>
<td>service-worker-allowed</td>
<td>sourcemap</td>
<td>upgrade</td>
</tr>
<tr>
<td>x-dns-prefetch-control</td>
<td>x-firefox-spdy</td>
<td>x-pingback</td>
<td>x-requested-with</td>
</tr>
<tr>
<td>x-robots-tag</td>
<td>x-ua-compatible</td>
<td>max-age</td>
<td></td>
</tr>
</tbody></table>
