
## 설정 시나리오

Tencent Cloud CDN은 다음과 같은 원본 요청 헤더의 추가를 지원합니다.

- X-Forward-For 헤더를 사용해 리얼 클라이언트 IP를 원본 서버로 전송할 수 있습니다.
- X-Forward-Port 헤더를 사용해 리얼 클라이언트 포트를 원본 서버로 전송할 수 있으며, 원본 서버 분석에 사용합니다.
- 각 유형의 사용자 정의 헤더를 추가할 수 있습니다.

## 설정 가이드

### 설정 제한

- 사용자 정의 요청 헤더 규칙은 최대 10개까지 설정할 수 있습니다.
- 모든 파일, 파일 유형, 파일 디렉터리, 특정 파일 경로 등 네 가지 방법을 선택해 적용할 수 있으며, 현재 regex match는 지원하지 않습니다.
- 클라이언트가 보낸 요청에 헤더 정보가 이미 있다면, 설정한 Request Header가 Origin-pull일 때 기존 헤더를 덮어씁니다.
- 여러 개의 규칙 헤더 설정이 중복되는 경우, 우선순위가 위에서 아래로 갈수록 높아지며, 아랫부분의 우선순위가 윗부분보다 높습니다.
- 사용자 정의 헤더의 Key 값 길이는 1 - 100글자이며, 숫자 0 - 9, 영어 문자 a - z, A - Z 및 특수문자 `-`로 구성합니다.
- 사용자 정의 헤더의 Value 길이는 1 - 1,000글자이며, 중국어를 지원하지 않습니다.
- 일부 표준 헤더는 직접 추가할 수 없습니다. 자세한 내용은 문서 마지막의 설명을 참조 바랍니다.

### 설정 설명

[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 메뉴에서 [도메인 관리]를 선택한 후, 도메인 오른쪽의 [관리]를 클릭하면 [원본 서버 설정]에서 원본 Request Header 설정을 확인할 수 있으며, 비활성화 및 아무 설정이 없는 상태로 기본 설정되어 있습니다.
![](https://main.qcloudimg.com/raw/253c67e926455bd17f2cda79fa46d2ba.png)
비활성화 상태일 때 신규 원본 헤더 규칙을 추가할 수 있습니다.
![](https://main.qcloudimg.com/raw/895adcd7cebdb0d75bbde1c22244a2a5.png)

> !
> 1. 클라이언트 리얼 IP의 헤더가 X-Forward-For일 때 사용합니다. 그 값은 $client_ip 변수로 기본 설정되며 수정할 수 없습니다.
> 2. 클라이언트 리얼 포트의 헤더가 X-Forward-Port일 때 사용합니다. 그 값은 $remote_port 변수로 기본 설정되며 수정할 수 없습니다.

규칙을 추가하면 전체 설정이 비활성화 상태로 되어 있으며, 적용되지 않습니다.
![](https://main.qcloudimg.com/raw/6d66d2ae51509aa787409ad4d0f301e1.png)
[우선순위 변경] 버튼을 누르고 규칙을 위아래로 움직여 순서를 변경할 수 있습니다. 전체 네트워크 CDN 노드에 배포하려면, 상단의 설정 스위치를 클릭합니다.
![](https://main.qcloudimg.com/raw/f984682c540bdd219c85a3dd3e51d7ca.png)

## 설정 예시

가속 도메인 'cloud.tencent.com'의 원본 서버 Request Header 설정은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/18b181e351aaf4a176ebcb9656921986.png)
액세스 리소스가 `http://cloud.tencent.com/test/test.mp4`인 경우
1. '*' 규칙에 히트하여, 헤더에 `X-Forward-For:$client_ip`를 추가하면, Origin-pull할 때 $client_ip를 리얼 클라이언트 IP로 대체합니다.
2. `.mp4` 파일 유형 및 `/test` 경로에 히트합니다. 아래쪽의 우선순위가 위쪽보다 높으므로 `x-cdn:Tencent` 헤더를 추가합니다.

## 주의 사항

아래의 표준 헤더는 현재 원본 서버 Request Header를 추가할 수 없습니다.

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
