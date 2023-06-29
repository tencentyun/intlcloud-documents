
## 설정 시나리오
CDN이 콘텐츠를 반환할 때 스마트 압축 설정을 통해 설정한 규칙에 따라 리소스를 Gzip, Brotli로 압축하여 전송 콘텐츠의 용량을 축소하고 비용을 절감할 수 있습니다.

> ! 
> - 도메인의 가속 리전이 글로벌인 경우, 스마트 압축 설정을 활성화해야 글로벌 범위에 적용되며 현재는 중국 본토 내/외를 다르게 설정할 수 없습니다.
> - 구성 파일의 Content-Type 유형 및 Brotli 압축 방식은 현재 중국 본토 이외의 지역에서 지원되지 않습니다.


## 설정 가이드
### 설정 조회
[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하고 메뉴바에서 **도메인 관리**를 선택한 뒤 도메인 오른쪽의 **관리**를 클릭하면 설정 페이지로 이동하며, **고급 설정**에서 스마트 압축 설정을 확인할 수 있습니다. 활성화 상태로 기본 설정되어 있습니다.
- 가속 도메인 연결 후에는 CDN에서 기본적으로 확장자가 .js, .html, .css, .xml, .json, .shtml, .htm이고, 크기가 256Byte - 2MB인 리소스를 Gzip으로 압축합니다.

![](https://main.qcloudimg.com/raw/db292e0fcc2a0d993b72117756c76b63.png)

### 설정 수정
작업 열의 **수정**을 클릭하여 압축 규칙을 수정할 수 있습니다.
![](https://main.qcloudimg.com/raw/887c62b7a53f6193f061ffc14b372de2.png)

**설정 제한**
- 유형은 파일 접미사로 기본 설정되며, 모든 파일을 추가할 수 있습니다. Content-Type 유형입니다.
- 파일 형식은 최대 200자까지 허용됩니다.
- 파일 Content-Type 유형의 콘텐츠는 기본적으로 text/html, text/xml, text/plain, text/css, text/javascript, application/json, application/javascript, application/x-javascript, application/rss+xml, application/xmltext, image/svg+xml, image/tiff 입니다. 필요에 따라 설정할 수 있습니다. 100개 그룹을 초과할 수 없으며, 다른 그룹의 콘텐츠는 ‘;’으로 구분하고, 각 그룹의 콘텐츠는 50자를 초과할 수 없습니다.
- 파일 Content-Type 형식 및 Brotli 압축은 현재 업그레이드 중인 일부 플랫폼에서 지원되지 않습니다.


>? 
> - 비활성화 상태에서도 하단의 설정을 변경할 수는 있지만, 현재 사용 중인 네트워크에는 배포되지 않습니다. 이 스위치를 활성화해야만 사용 중인 네트워크에 설정을 전달합니다.
> - Gzip과 Brotli 압축을 동시에 선택할 경우 요청 압축 헤더에 따라 해당되는 압축 파일을 반환합니다.
> - Brotli 압축만 활성화하는 경우 요청 헤더가 Brotli 압축을 지원하지 않으면 압축을 진행하지 않고 원본 리소스를 반환합니다.


