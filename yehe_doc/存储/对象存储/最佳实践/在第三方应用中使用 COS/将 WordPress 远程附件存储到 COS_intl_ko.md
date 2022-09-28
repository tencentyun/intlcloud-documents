## 소개

[WordPress](https://cn.wordpress.org/)는 PHP 언어를 사용해 개발된 블로그 플랫폼입니다. 사용자는 PHP와 MySQL 데이터베이스를 지원하는 서버에 개인 웹 사이트를 구축할 수 있고, WordPress를 콘텐츠 관리 시스템(CMS)으로 사용할 수도 있습니다.

WordPress의 강력한 기능과 확장성은 플러그 인이 많아 기능 확충이 쉽기 때문입니다. 완전한 하나의 웹 사이트가 기본적으로 갖추어야 할 모든 기능은 3rd party 플러그 인을 통해 실행할 수 있습니다.

본 문서에서는 플러그 인을 사용한 원격 파일 첨부 기능을 통해 WordPress의 미디어 라이브러리 첨부 파일을 Tencent Cloud의 [Cloud Object Storage(COS)](https://www.tencentcloud.com/products/cos)에 저장하는 방법을 소개합니다.

COS는 고확장성, 저비용, 신뢰성, 보안과 같은 특징이 있습니다. 미디어 라이브러리 첨부 파일을 COS에 저장할 경우 장점은 다음과 같습니다.

- 첨부 파일의 신뢰성이 높아집니다.
- 서버에 첨부 파일을 위한 별도의 스토리지 용량을 마련하지 않아도 됩니다.
- 이미지 첨부 파일을 조회할 때 바로 COS 서버에 연결하면 서버의 다운스트림 대역폭/트래픽을 점유하지 않으며, 액세스 속도가 더 빨라집니다.
- Tencent Cloud [Content Delivery Network(CDN)](https://www.tencentcloud.com/products/cdn)와 함께 사용하면 사용자의 이미지 첨부 파일 확인 속도를 더욱 향상시키고 웹사이트 액세스 속도를 최적화할 수 있습니다.

## 준비 작업

1. WordPress 블로그 플랫폼을 구축합니다.
 - [WordPress 공식 홈페이지](https://cn.wordpress.org/download/)에서 WordPress의 최신 버전 다운로드 및 설치 가이드를 조회할 수 있습니다.

2. **공개 읽기 및 개인 쓰기** 버킷을 생성합니다. 버킷 리전은 WordPress 블로그 플랫폼을 실행하는 CVM과 동일한 리전을 권장합니다. 자세한 생성 방법은 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309) 문서를 참조하십시오.
3. **버킷 리스트**에서 방금 생성한 버킷을 찾아 이름을 클릭한 후 버킷 페이지로 이동합니다.

4. 왼쪽 메뉴에서 **개요**를 클릭하여 액세스 도메인을 조회하고 기록합니다.


## 플러그 인 설치 및 설정

### 플러그 인 설치

WordPress 백그라운드에서 **플러그 인 > 플러그 인 설치**를 클릭하여 플러그 인 설치를 시작합니다. 다음의 두 가지 방식으로 플러그 인을 획득 및 설치할 수 있습니다.

 - 백그라운드에서 직접 **tencentcloud-cos**를 검색하여 설치합니다(권장).
 - [Github](https://github.com/Tencent-Cloud-Plugins/tencentcloud-wordpress-plugin-cos)에서 최신 releases 소스 코드를 다운로드하여 WordPress 백그라운드 업로드를 통해 설치하거나 직접 소스 코드를 WordPress의 플러그 인 디렉터리 `wp-content/plugins`에 업로드한 후 백그라운드에서 활성화할 수도 있습니다.

### 플러그 인 설정

1. WordPress 왼쪽 사이드바에서 **Tencent Cloud 설정**을 클릭하고, 페이지에서 COS 관련 정보를 설정합니다. 설정에 대한 설명은 아래 표를 참조하십시오.
<table>
<thead>
<tr>
<th align="left">설정 항목</th>
<th align="left">설정 값</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">SecretId, SecretKey</td>
<td align="left">키 정보에 액세스하려면 <a href="https://console.cloud.tencent.com/capi">Tencent Cloud API 키</a>로 이동하여 생성 및 가져오기</td>
</tr>
<tr>
<td align="left">소속 리전</td>
<td align="left">버킷 생성 시 선택한 리전</tdz
</tr>
<tr>
<td align="left">스페이스 이름</td>
<td align="left">버킷 생성 시 사용자 지정된 버킷 이름, 예시: examplebucket-1250000000</td>
</tr>
<tr>
<td align="left">액세스 도메인</td>
<td align="left">COS의 기본 버킷 도메인을 말하며, 사용자가 버킷을 생성하면 시스템에서 버킷 이름과 리전에 따라 자동으로 생성합니다. 다른 리전의 버킷은 각각 다른 기본 도메인이 있습니다. <a href="https://console.cloud.tencent.com/cos5">COS 콘솔</a>로 이동하여 버킷의 <strong>개요 > 도메인 정보</strong>에서 확인하실 수 있습니다.</td>
</tr>
<tr>
<td align="left">자동 이름 변경</td>
<td align="left">파일을 COS에 업로드한 후 동일한 이름의 기존 파일과 충돌을 피하기 위해 자동으로 지정된 형식에 따라 이름 변경</td>
</tr>
<tr>
<td align="left">로컬에 저장하지 않음</td>
<td align="left">활성화 후에는 원본 파일이 로컬에 보관되지 않으므로, 활성화하지 않을 것을 제안</td>
</tr>
<tr>
<td align="left">썸네일 금지</td>
<td align="left">활성화 후에는 해당 썸네일 파일이 업로드되지 않으므로 활성화하지 않을 것을 제안</td>
</tr>
<tr>
<td align="left">Cloud Infinite(CI)</td>
<td align="left">CI 서비스를 활성화하면, 이미지에 편집, 압축, 형식 변환, 워터마크 추가 등의 작업 가능, 자세한 내용은 <a href="https://www.tencentcloud.com/products/ci">Cloud Infinite 제품 소개</a> 참고</td>
</tr>
<tr>
<td align="left">디버깅</td>
<td align="left">오류, 예외 및 경고 정보 기록, 활성화 선택 가능</td>
</tr>
</tbody></table>
2. 설정이 완료되면 **설정 저장**을 클릭합니다.
3. 새로운 파일을 업로드하여 테스트합니다. 첨부 파일의 상세 내용 및 첨부 이미지의 URL을 조회하여 첨부 이미지의 URL이 Tencent Cloud COS로 지정되어 있는지 확인합니다.

>? 테스트에 성공하면 기존 리소스를 COS 버킷에 동기화해야 합니다([COSCMD 툴](https://intl.cloud.tencent.com/document/product/436/10976) 또는 [COS Migration 툴](https://intl.cloud.tencent.com/document/product/436/15392) 사용 가능). **동기화하지 않으면 백그라운드에서 기존 리소스 미리보기를 할 수 없습니다**. 동기화가 완료되면 Origin-pull 설정을 활성화할 수 있습니다. 아래 [Origin-pull 설정](#1)을 참조하십시오.
>

## 확장

1. CDN 가속을 사용하여 액세스합니다.
버킷에 CDN 가속 설정이 필요한 경우 [CDN 가속 설정](https://intl.cloud.tencent.com/document/product/436/18670) 문서를 참조하십시오. 플러그 인 설정에서 URL 접두사의 기본값을 CDN 가속 도메인 또는 사용자 정의 가속 도메인으로 수정하면 됩니다.
2. 데이터베이스의 리소스 주소를 변경합니다.
새로 생성한 사이트가 아니라면 데이터베이스에는 반드시 기존 리소스 링크 주소가 존재하며, 이 리소스 주소를 변경해야 합니다. 플러그 인에서 변경 기능을 제공하며, 최초 변경 전 반드시 백업해 두시기 바랍니다.
 - 기존 도메인에 원본 리소스 도메인을 입력합니다. 예: `https://example.com/`
 - 신규 도메인에 현재의 리소스 도메인을 입력합니다. 예: `https://img.example.com/`
3. 크로스 도메인 액세스를 설정합니다.
본 문서의 상응하는 리소스 링크 인용 시 콘솔은 크로스 도메인 오류 `No 'Access-Control-Allow-Origin' header is present on the requested resource`를 표시합니다. 이는 header를 추가하지 않았기 때문입니다. 크로스 도메인 액세스 CORS 설정에서 HTTP Header 설정을 추가해야 하며, 다음 두 가지 방법으로 설정할 수 있습니다.
 - COS 콘솔에서 설정

>? 크로스 도메인 설정 작업 순서는 [CORS 설정](https://intl.cloud.tencent.com/document/product/436/13318) 문서를 참조하십시오.
>
 - CDN 콘솔에서 설정
    - 모든 도메인을 허용할 경우, 다음과 같이 설정합니다.
```plaintext
Access-Control-Allow-Origin: *
```
    - 사용자 개인 도메인 액세스만 허용할 경우, 다음과 같이 설정합니다.
```plaintext
Access-Control-Allow-Origin: https://example.com
```
<span id=1></span>
4. Origin-pull을 설정합니다.
리소스를 WordPress 백그라운드 미디어 라이브러리에서 업로드하지 않는 경우 Origin-pull 설정 활성화를 권장합니다. 자세한 방법은 [Origin-pull 설정](https://intl.cloud.tencent.com/document/product/436/31508) 문서를 참조하십시오.
Origin-pull 설정을 활성화한 후 클라이언트에서 최초로 COS 원본 파일에 액세스할 때, 객체를 히트하지 못한 경우 클라이언트에 302 HTTP 상태 코드를 반환함과 동시에 Origin-pull 주소에 상응하는 주소로 리디렉션됩니다. 이때 원본 서버에서 클라이언트에 객체를 제공함으로써 액세스를 보장합니다. 또한 COS는 원본 서버에서 해당 파일을 복사하여 버킷의 상응하는 디렉터리에 저장하고, 두 번째 액세스 시 COS에서 직접 객체가 히트되고 클라이언트에 반환합니다.

