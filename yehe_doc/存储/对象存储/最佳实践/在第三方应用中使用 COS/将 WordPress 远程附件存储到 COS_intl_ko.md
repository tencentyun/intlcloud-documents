## 소개

[WordPress](https://cn.wordpress.org/)는 PHP 언어를 사용해 개발된 블로그 플랫폼입니다. 사용자는 PHP와 MySQL 데이터베이스를 지원하는 서버에 개인 웹 사이트를 구축할 수 있고, WordPress를 콘텐츠 관리 시스템(CMS)으로 사용할 수도 있습니다.

WordPress의 강력한 기능과 확장성은 플러그 인이 많아 기능 확충이 쉽기 때문입니다. 완전한 하나의 웹 사이트가 기본적으로 갖추어야 할 모든 기능은 3rd party 플러그 인을 통해 실행할 수 있습니다.

본 문서에서는 플러그 인을 사용한 원격 파일 첨부 기능을 통해 WordPress의 미디어 라이브러리 첨부 파일을 Tencent Cloud의 [COS](https://intl.cloud.tencent.com/product/cos)에 저장하는 방법을 소개합니다.

COS는 고확장성, 저비용, 신뢰성, 보안과 같은 특징이 있습니다. 미디어 라이브러리 첨부 파일을 COS에 저장할 경우 장점은 다음과 같습니다.

- 첨부 파일의 신뢰성이 높아집니다.
- 서버에 첨부 파일을 위한 별도의 스토리지 용량을 마련하지 않아도 됩니다.
- 이미지 첨부 파일을 조회할 때 서버의 다운스트림 대역폭/트래픽을 점유하지 않으며, 액세스 속도가 더 빨라집니다.
- Tencent Cloud의 [Content Delivery Network(CDN)](https://intl.cloud.tencent.com/product/cdn)와 결합하여 이미지 첨부 파일 조회 속도를 향상함으로써 웹 사이트 액세스 속도가 최적화됩니다.

## 준비 작업

1. WordPress 블로그 플랫폼을 구축합니다.
 - [WordPress 공식 홈페이지](https://cn.wordpress.org/download/)에서 WordPress의 최신 버전 다운로드 및 설치 가이드 조회가 가능합니다.
 - 서버 시스템 설치 시 사전 설치된 WordPress 블로그 플랫폼의 CVM 이미지를 이미지 마켓에서 선택할 수 있습니다.
2. **공개 읽기 및 개인 쓰기** 버킷을 생성합니다. 버킷 리전은 WordPress 블로그 플랫폼을 실행하는 CVM과 동일한 리전을 권장합니다. 자세한 생성 방법은 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309) 문서를 참조하십시오.
3. [버킷 리스트]에서 방금 생성한 버킷을 찾아 이름을 클릭한 후 버킷 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/13d88e1cf3ad72e6f198a328d21cef13.png)
4. 왼쪽의 [기본 설정]을 클릭하여 액세스 도메인을 조회하고 기록합니다.
![](https://main.qcloudimg.com/raw/a8eb4239f4ad0e0b24881e3d710318a3.png)

## 플러그 인 설치 및 설정

### 플러그 인 설치

WordPress 백그라운드에서 [플러그 인]>[플러그 인 설치]를 클릭하여 플러그 인 설치를 시작합니다. 다음의 두 가지 방식으로 플러그 인을 획득 및 설치할 수 있습니다.

 - 백그라운드에서 직접 **Sync QCloud COS**를 검색해 설치합니다(권장).
 - [Github](https://github.com/sy-records/wordpress-qcloud-cos/releases/latest)에서 최신 releases 소스 코드를 다운로드하여 WordPress 백그라운드 업로드를 통해 설치하거나 직접 소스 코드를 WordPress의 플러그 인 디렉터리 `wp-content/plugins`에 업로드한 후 백그라운드에서 활성화할 수도 있습니다.

### 플러그 인 설정

1. WordPress 왼쪽 메뉴에서 [설정]을 클릭하고, 페이지에서 COS 관련 정보를 설정합니다. 설정에 대한 설명은 아래 표를 참조하십시오.

| 설정 항목              | 설정값                                                       |
| :------------------ | :----------------------------------------------------------- |
| 버킷 이름          | 버킷 생성 시 사용자 정의된 이름                                     |
| 버킷 리전          | 버킷 생성 시 선택한 리전                                     |
| APPID               | APPID는 Tencent Cloud 계정 신청 후 획득하게 되는 계정으로 시스템에서 자동으로 할당합니다. 변경 불가능한 고유 ID이며 [계정 정보](https://console.cloud.tencent.com/developer)에서 확인할 수 있습니다. |
| SecretID, SecretKey | 액세스 키 정보는 [Tencent Cloud API 키](https://console.cloud.tencent.com/capi)에서 획득할 수 있습니다. |
| 섬네일 업로드하지 않음        | 선택 시 상응하는 섬네일 파일을 업로드하지 않습니다. 선택하지 않을 것을 권장합니다.                   |
| 로컬 백업하지 않음    | 선택 시 로컬에 원본 파일을 보관하지 않습니다. 선택하지 않을 것을 권장합니다.                       |
| 로컬 폴더          | 로컬에 경로를 저장합니다. 예: `wp-content/uploads`                       |
| URL 접두사            | 포맷은 `<COS 액세스 도메인>/<로컬 폴더>`입니다. 예: `https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/wp-content/uploads` |

2. 설정 완료 후 [저장]을 클릭합니다.
3. 새로운 파일을 업로드하여 테스트합니다. 첨부 파일의 상세 내용 및 첨부 이미지의 URL을 조회하여 첨부 이미지의 URL이 Tencent Cloud COS로 지정되어 있는지 확인합니다.

>테스트에 성공하면 기존 리소스를 COS 버킷에 동기화해야 합니다([COSCMD 툴](https://intl.cloud.tencent.com/document/product/436/10976) 또는 [COS Migration 툴](https://intl.cloud.tencent.com/document/product/436/15392)을 사용할 수 있습니다). **동기화하지 않으면 백그라운드에서 기존 리소스 미리보기를 할 수 없습니다**. 동기화가 완료되면 Origin-pull 설정을 활성화할 수 있습니다. 아래 [Origin-pull 설정](#1)을 참조하십시오.

## 확장

1. CDN 가속을 사용하여 액세스합니다.
버킷에 CDN 가속 설정이 필요한 경우 [CDN 가속 설정](https://intl.cloud.tencent.com/document/product/436/18670) 문서를 참조하십시오. 플러그 인 설정에서 URL 접두사의 기본값을 CDN 가속 도메인 또는 사용자 정의 가속 도메인으로 수정하면 됩니다.
2. 데이터베이스의 리소스 주소를 변경합니다.
새로 생성한 사이트가 아닌 경우 데이터베이스에는 반드시 기존 리소스 링크 주소가 있습니다. 이 리소스 주소를 변경해야 하는데, 플러그 인이 변경 기능을 제공합니다. 최초 변경 전에 반드시 백업해 두시기 바랍니다.
 - 기존 도메인에 원본 리소스 도메인을 입력합니다. 예: `https://example.com/`
 - 신규 도메인에 현재의 리소스 도메인을 입력합니다. 예: `https://img.example.com/`
3. 크로스 도메인 액세스를 설정합니다.
본 문서의 상응하는 리소스 링크 인용 시 콘솔은 크로스 도메인의 오류 `No 'Access-Control-Allow-Origin' header is present on the requested resource`를 표시합니다. header를 추가하지 않았기 때문입니다. 크로스 도메인 액세스 CORS 설정에서 HTTP Header 설정을 추가해야 합니다. 다음의 두 가지 경로로 설정할 수 있습니다.
 - COS 콘솔에서 설정합니다.
![](https://main.qcloudimg.com/raw/71dcabb63c9d0d4120eb33bfd7df92f1.png)
>크로스 도메인 설정 작업 순서는 [크로스 도메인 액세스 설정](https://intl.cloud.tencent.com/document/product/436/13318) 문서를 참조하십시오.
 - CDN 콘솔에서 설정합니다.
    - 모든 도메인이 허용되었을 경우 설정은 다음과 같습니다.
```plaintext
Access-Control-Allow-Origin: *
```
    - 귀하의 개인 도메인 액세스만 허용되었을 경우 설정은 다음과 같습니다.
```plaintext
Access-Control-Allow-Origin: https://example.com
```

<span id=1>

4. Origin-pull을 설정합니다.
WordPress 백그라운드 미디어 라이브러리에서 리소스를 업로드하지 않을 경우 Origin-pull 설정 활성화를 권장합니다. 자세한 순서는 [Origin-pull 설정](https://intl.cloud.tencent.com/document/product/436/31508) 문서를 참조하십시오.
Origin-pull 설정을 활성화한 후 클라이언트가 최초로 COS 원본 파일에 액세스할 때, 객체를 히트하지 못한 COS는 클라이언트에 302 HTTP 상태 코드를 반환함과 동시에 Origin-pull 주소에 상응하는 주소로 리디렉션됩니다. 이때 원본 서버는 클라이언트에 객체를 제공함으로써 액세스를 보증합니다. 또한 COS는 원본 서버에서 해당 파일을 복사하여 버킷의 상응하는 디렉터리에 저장합니다. 두 번째 액세스 시 COS는 객체를 히트하고 클라이언트에 반환합니다.
