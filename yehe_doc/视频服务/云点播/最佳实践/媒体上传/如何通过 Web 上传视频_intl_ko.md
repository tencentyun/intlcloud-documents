## 사용 수칙

### Demo 기능 소개

이 Demo는 Web 페이지를 통해 VOD에 동영상을 업로드하는 방법을 보여줍니다. SCF를 기반으로 두 개의 HTTP 서비스를 구축합니다.

- 첫 번째 서비스는 [클라이언트 업로드 서명](https://intl.cloud.tencent.com/document/product/266/33922)을 가져오기 위해 브라우저에서 요청을 수신하고 서명을 계산하여 반환하는 데 사용됩니다.
- 두 번째 서비스는 VOD의 [Web 업로드 SDK](https://intl.cloud.tencent.com/document/product/266/33924)를 사용하여 페이지를 구현합니다. 브라우저에서 페이지에 액세스하여 로컬 동영상을 VOD에 업로드할 수 있습니다.

### 아키키텍처와 프로세스

시스템은 주로 브라우저, API Gateway, SCF 및 VOD의 네 가지 구성 요소로 구성됩니다. 여기에서 API Gateway 및 SCF는 아래와 같이 이 Demo의 배포 객체입니다.
<img src="https://main.qcloudimg.com/raw/a5243b83531f4a2d98a63970d1f7a1b3.png" width="500">

주요 업무 프로세스는 다음과 같습니다.

1. 브라우저는 업로드 페이지에 대해 SCF를 요청합니다.
2. 로컬 동영상을 선택하고 업로드 페이지에서 업로드를 클릭하면 브라우저에서 업로드 서명을 위해 SCF를 요청합니다.
3. 브라우저는 업로드 서명을 사용하여 VOD에 대한 업로드 요청을 시작하고 완료 후 업로드 페이지에 업로드 결과를 표시합니다.

> ?Demo의 SCF 코드는 Python3.6을 기반으로 개발되었습니다. 또한 SCF는 Python2.7, Node.js, Golang, PHP, Java 등 여러 프로그래밍 언어를 지원하며, 개발자가 상황에 따라 자유롭게 선택할 수 있습니다. 자세한 내용은 [SCF 개발 가이드](https://intl.cloud.tencent.com/document/product/583/11061)를 참고하십시오.

### 요금

이 문서에서 제공하는 VOD Web 업로드 Demo(Web페이지 코드 및 서비스 백엔드 코드 포함)는 오픈 소스이며 무료이지만 서비스 구축 및 사용 시 다음과 같은 비용이 발생할 수 있습니다.

- 서비스 배포 스크립트 실행을 위해 Tencent Cloud CVM 구매 시 비용이 발생합니다. 자세한 내용은 [CVM 과금](https://intl.cloud.tencent.com/document/product/213/2180)을 참고하십시오.
- Tencent Cloud SCF에서 제공하는 업로드 페이지 및 서명 배포 서비스 이용 비용이 발생합니다. 자세한 내용은 [SCF 과금](https://intl.cloud.tencent.com/document/product/583/12284) 과 [SCF 무료 한도](https://intl.cloud.tencent.com/document/product/583/12282)를 참고하십시오.
- Tencent Cloud API 게이트웨이를 사용하여 SCF에 공인 네트워크 인터페이스 제공 시 비용이 발생합니다. 자세한 내용은 [API 게이트웨이 과금](https://intl.cloud.tencent.com/document/product/628/11771)을 참고하십시오.
- 업로드된 동영상의 VOD 저장 비용입니다. 자세한 내용은 [스토리지 과금](https://intl.cloud.tencent.com/document/product/266/14666)을 참고하십시오.
- 동영상 재생에 사용된 VOD 트래픽에 대한 요금입니다. 자세한 내용은 [트래픽 과금](https://intl.cloud.tencent.com/document/product/266/14666)을 참고하십시오.

## Web 업로드 Demo의 빠른 배포

Web 업로드 Demo는 API Gateway에서 제공하는 서비스 항목을 사용하여 SCF에 배포됩니다. 서비스를 더 쉽게 구축할 수 있도록 아래에 설명된 대로 빠른 배포 스크립트를 제공합니다.
<span id="p1"></span>
### 1단계: CVM 인스턴스 준비

배포 스크립트는 다음 요건에 부합하는 Tencent Cloud CVM에서 실행되어 야 합니다.

- 리전: 랜덤
- 모델: 공식 웹 사이트의 최저 사양(1코어 1GB).
- 공용 네트워크: 공용 IP를 보유해야 하며 대역폭은 1Mbps 이상.
- 운영 체제: 공식 웹 사이트의 공용 이미지 `Ubuntu Server 16.04.1 LTS 64비트` 또는 `Ubuntu Server 18.04.1 LTS 64비트`.

CVM 구매 방법은 [운영 가이드 - 인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참고하십시오. 시스템 재설치 방법은 [운영 가이드 - 시스템 재설치](https://intl.cloud.tencent.com/document/product/213/4933)를 참고하십시오.

>!
>- **Web 업로드 Demo는 CVM에 의존하지 않고 CVM을 사용하여 배포 스크립트를 실행합니다**.
>- 위 조건에 부합하는 Tencent Cloud CVM이 없을 경우, 다른 공인 네트워크의 Linux(예: CentOS, Debian 등) 또는 Mac 디바이스에서도 배포 스크립트를 실행할 수 있으나 운영 체제에 따라 스크립트의 개별 명령을 수정해야 합니다. 자세한 수정 방법은 개발자가 직접 검색하시기 바랍니다.

### 2단계: VOD 활성화

[시작하기 - 1단계](https://intl.cloud.tencent.com/document/product/266/8757)에 따라 VOD 서비스를 활성화하십시오.
<span id="p3"></span>
### 3단계: API 키 및 APPID 가져오기

Web 업로드 Demo 서비스를 배포하고 실행하려면 API 키(예: SecretId 및 SecretKey)와 APPID가 필요합니다.
- 아직 API 키를 생성하지 않았다면 [보안키 생성 파일](https://intl.cloud.tencent.com/document/product/598/34228)을 참고하여 새로운 API 키를 생성하십시오. 이미 키를 생성했다면 [보안키 조회 파일](https://intl.cloud.tencent.com/document/product/598/34228)을 참고하여 API 키를 가져옵니다.
- 다음 이미지와 같이 콘솔의 [계정 정보](https://console.cloud.tencent.com/developer) 페이지에서 APPID를 조회할 수 있습니다.

### 4단계: 서비스 백엔드 및 Web 페이지 배포

[1단계에서 준비된 CVM](#p1)(로그인 방식은 [운영 가이드 - Linux 로그인](https://intl.cloud.tencent.com/document/product/213/5436)참고)에 로그인하여, 원격 터미널에 다음 명령어를 입력하고 실행합니다.

```
ubuntu@VM-69-2-ubuntu:~$ export SECRET_ID=AKxxxxxxxxxxxxxxxxxxxxxxx; export SECRET_KEY=xxxxxxxxxxxxxxxxxxxxx;export APPID=125xxxxxxx;git clone https://github.com/tencentyun/vod-server-demo.git ~/vod-server-demo; bash ~/vod-server-demo/installer/web_upload_scf.sh
```
>?명령에서 SECRET_ID, SECRET_KEY, APPID [3단계](#p3)에서 얻은 값을 할당하십시오.

해당 명령은 Github로부터 Demo 소스 코드를 다운로드하고 설치 스크립트를 자동 실행합니다. 설치 프로세스는 수 분(실제 시간은 CVM 네트워크 상태에 따라 다름)이 소요되며, 원격 터미널에서 다음과 같은 정보를 인쇄합니다.

```
[2020-04-25 23:03:20] pip3 설치 시작.
[2020-04-25 23:03:23]pip3 설치 성공.
[2020-04-25 23:03:23]Tencent Cloud SCF 툴 설치 시작.
[2020-04-25 23:03:26]scf 설치 성공.
[2020-04-25 23:03:26]scf 구성 시작.
[2020-04-25 23:03:28]scf 구성 완료.
[2020-04-25 23:03:28]VOD 클라이언트 업로드 클라이언트 서명 배포 서비스 배포 시작.
[2020-04-25 23:03:40]VOD 클라이언트 업로드 서명 배포 서비스 배포 완료.
[2020-04-25 23:03:44]VOD Web 업로드 페이지 배포 시작.
[2020-04-25 23:03:53]VOD Web 업로드 페이지 배포 완료.
[2020-04-25 23:03:53]데모를 사용하려면 브라우저에서 다음 주소에 액세스하십시오: https://service-xxxxxxxx-125xxxxxxx.gz.apigw.tencentcs.com/release/web_upload_html
```

<span id="p4"></span>출력 로그에서 Web 페이지 주소를 복사합니다(예시 중의 `https://service-xxxxxxxx-125xxxxxxx.gz.apigw.tencentcs.com/release/web_upload_html`).

> !출력 로그에 다음과 같은 경고가 표시되는 경우는 일반적으로 CVM가 방금 배포된 서비스 도메인을 즉시 분석할 수 없기 때문으로, 해당 경고를 무시할 수 있습니다.
>```
>[2020-04-25 17:18:44]경고: 클라이언트 업로드 서명 배포 서비스 테스트 실패.
>```

### 5단계: Web 업로드 Demo 사용

1. 브라우저에서 [4단계](#p4)에서 복사한 주소에 액세스하여 아래와 같이 Web 업로드 Demo 사용을 시작합니다.
2. 이 페이지에서 동영상 업로드 작업 수행:
	1. 로컬 동영상 파일을 선택합니다(MP4 형식 권장).
	2. 로컬 표지 이미지(JPG 또는 PNG 형식)를 선택합니다(선택 사항).
	3. 동영상 이름을 입력합니다(선택 사항).
	4. [업로드 시작]을 클릭하여 동영상을 업로드합니다.
3. 업로드가 완료되면 VOD 미디어 ID (즉, fileId)와 업로드된 동영상 및 커버의 URL이 아래와 같이 페이지 하단에 표시됩니다.
업로드된 동영상은 아래와 같이 [VOD 콘솔](https://console.cloud.tencent.com/vod/media)에서 볼 수 있습니다.

>?페이지 안내에 따라 업로드 페이지에서 다른 기능을 사용해 볼 수 있습니다.

## 시스템 설계 설명

### API 프로토콜 및 테스트

**업로드 페이지**와**업로드 서명 배포** 기능 모두 API Gateway를 사용하여 API를 제공합니다. 구체적인 API 프로토콜은 아래와 같습니다.

| 서비스         | SCF 이름        | API 양식  | 반환 내용  |
| ------------ | --------------- | --------- | --------- |
| 업로드 페이지     | web_upload_html | HTTP GET  | HTML 페이지 |
| 서명 배포 업로드 | ugc_upload_sign | HTTP POST | 서명 업로드  |

<span id="p6"></span>
#### 업로드 페이지

[SCF 서비스 목록](https://console.cloud.tencent.com/scf/list)에 액세스하여 업로드 페이지 서비스의 세부 정보를 볼 수 있습니다.

>?
>- Demo에서 사용하는 두 개의 SCF 기능은 광저우 지역의 vod_demo 네임스페이스에 배포됩니다.
>- 배포된 SCF 기능을 보려면 콘솔에서 해당 지역 및 네임스페이스를 선택해야 합니다.

함수명을 클릭하고 왼쪽에서 [트리거 관리]를 선택합니다. 오른쪽의 [액세스 경로]가 업로드 페이지의 URL입니다. [API 서비스 이름]을 클릭하여 아래와 같이 해당 API 게이트웨이 페이지로 리디렉션합니다.
서비스를 테스트하려면 브라우저에서 페이지 URL에 직접 접속하여 업로드 페이지가 정상적으로 표시되는지 확인하십시오.

#### 서명 배포 업로드

업로드 페이지에서 설명한 것과 동일한 방식으로 [SCF 서비스 목록](https://console.cloud.tencent.com/scf/list)에 액세스하여 업로드 서명 배포 서비스의 세부 정보를 볼 수 있습니다(보기 방법은 [업로드 페이지](#p6)).

함수 이름을 클릭하고 왼쪽에서 [트리거 관리]를 선택합니다. 오른쪽의 [액세스 경로]가 서비스의 URL입니다. [API 서비스 이름]을 클릭하여 아래와 같이 해당 API 게이트웨이 페이지로 리디렉션합니다.
서비스를 테스트하려면 HTTP 요청을 수동으로 보내고 공용 네트워크 액세스 권한이 있는 Linux 또는 macOS 장치에서 다음 명령을 실행합니다(실제 상황에 따라 서비스 URL을 수정하십시오).
```
curl -d '' https://service-xxxxxxxx-125xxxxxxx.gz.apigw.tencentcs.com/release/ugc_upload_sign
```
서비스가 정상이면 업로드 서명이 반환됩니다. 다음은 서명 예시입니다.
```
VYapc9EYdoZLzGx0CglRW4N6kuhzZWNyZXRJZD1BS0lEZk5xMzl6dG5tYW1tVzBMOXFvZERia25hUjdZa0xPM1UmY3VycmVudFRpbWVTdGFtcD0xNTg4NTg4MDIzJmV4cGlyZVRpbWU9MTU4ODU4ODYyMyZyYW5kb209MTUwNzc4JmNsYXNzSWQ9MCZvbmVUaW1lVmFsaWQ9MCZ2b2RTdWJBcHBJZD0w
```
Postman과 같은 타사 도구를 사용하여 HTTP 요청을 보낼 수도 있습니다. 구체적인 사용법은 인터넷에서 검색하시기 바랍니다. 

### 업로드 페이지 서비스 코드 해석

1. `Main_handler()`는 엔트리 함수입니다.
2. 업로드 페이지 콘텐츠인 `web_upload.html` 파일의 콘텐츠 읽기.
```
		html_file = open(HTML_FILE, encoding='utf-8')
		html = html_file.read()
```
3. SCF 서비스를 작성할 때 예측할 수 없고 배포 과정에서 결정해야 하는 내용을 참고하는 `config.json`에서 구성 항목을 읽습니다. 콘텐츠는 업로드 페이지 서비스를 배포하기 전에 배포 스크립트에 의해 실시간으로 `config.json`에 작성됩니다.
```
		conf_file = open(CONF_FILE, encoding='utf-8')
		conf = conf_file.read()
		conf_json = json.loads(conf)
```
4. `render_template`을 호출하고 이전 단계에서 얻은 구성 정보에 따라 업로드 페이지 콘텐츠를 수정합니다. 구성 항목은 `config.json` 파일에서 ‘변수 이름’: ‘값’ 형식으로, `web_upload.html` 파일에서 `{변수 이름}` 형식으로 표현됩니다. **수정 시 특정 값으로 대체하십시오**. 세부 사항은 다음과 같습니다.
```
  def render_template(html, keys):
      """HTML의 변수(${변수 이름} 형식)를 특정 콘텐츠로 교체하십시오."""
      for key, value in keys.items():
          html = html.replace("${" + key + "}", value)
      return html
```
<table>
<thead>
<tr>
<th>변수 이름</th>
<th>의미</th>
<th>값 유형</th>
<th>값 소스</th>
</tr>
</thead>
<tbody><tr>
<td>UGC_UPLOAD_SIGN_SERVER</td>
<td>서명 배포 서비스의 URL 업로드</td>
<td>String</td>
<td>업로드 서명 배포 서비스 배포가 완료된 후 SCF TCCLI <a href="https://intl.cloud.tencent.com/document/product/583/36267" target="_blank">scf</a>에서 출력합니다</td>
</tr>
</tbody></table>
5. 업로드 페이지의 수정된 내용을 반환합니다. 반환된 데이터의 형식 및 설명은 [API Gateway 트리거 개요](https://intl.cloud.tencent.com/document/product/583/12513)를 참고하십시오.
  ```
      return {
          "isBase64Encoded": False,
          "statusCode": 200,
          "headers": {'Content-Type': 'text/html'},
          "body": html
      }
  ```


### 서명 배포 서비스 코드 해석 업로드

1. `Main_handler()`는 엔트리 함수입니다.
2. `parse_conf_file()`을 호출하고, `config.json` 파일에서 설정 정보를 읽습니다. 설정 항목에 대한 설명은 다음과 같습니다(자세한 매개변수는 [클라이언트 업로드 서명 매개변수](https://intl.cloud.tencent.com/document/product/266/33922#.3Cspan-id-.3D.22p2.22.3E.3C.2Fspan.3E.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0.E8.AF.B4.E6.98.8E)를 참고하십시오).
<table>
<thead>
<tr>
<th>필드</th>
<th>데이터 유형</th>
<th>기능</th>
</tr>
</thead>
<tbody><tr>
<td>secret_id</td>
<td>String</td>
<td>API 키</td>
</tr>
<tr>
<td>secret_key</td>
<td>String</td>
<td>API 키</td>
</tr>
<tr>
<td>sign_expire_time</td>
<td>Integer</td>
<td>서명 유효 기간. 단위: 초.</td>
</tr>
<tr>
<td>class_id</td>
<td>Integer</td>
<td>업로드된 동영상 카테고리 ID. 0은 기본 카테고리.</td>
</tr>
<tr>
<td>otp</td>
<td>Integer</td>
<td>서명이 일회성인지 여부</td>
</tr>
<tr>
<td>subappid</td>
<td>Integer</td>
<td><a href="https://intl.cloud.tencent.com/document/product/266/33987" target="_blank">VOD 서브 애플리케이션</a> 업로드 여부</td>
</tr>
</tbody></table>
3. `parse_source_context()`를 호출하여 요청 Body의 `sourceContext` 필드를 구문 분석합니다. 이 필드는 동영상 [업로드 완료 이벤트 알림](https://intl.cloud.tencent.com/document/product/266/33950) 중에 이벤트 알림 수신 서비스(이 Demo에서는 사용되지 않음)로 전달할 수 있습니다.
>?이 필드는 업로드 과정에서 선택 사항입니다. 이 기능이 필요하지 않은 경우 코드의 이 부분을 무시할 수 있습니다.
4. `generate_sign()` 함수를 호출하여 서명을 계산합니다. 자세한 내용은 [클라이언트 업로드 서명](https://intl.cloud.tencent.com/document/product/266/33922)을 참고하십시오.
5. 서명을 반환합니다. 반환된 데이터 포맷 및 의미는 [SCF 통합 응답](https://intl.cloud.tencent.com/document/product/583/12513)을 참고하십시오.
  ```
      return {
          "isBase64Encoded": False,
          "statusCode": 200,
          "headers": {"Content-Type": "text/plain; charset=utf-8",
                      "Access-Control-Allow-Origin": "*",
                      "Access-Control-Allow-Methods": "POST,OPTIONS"},
          "body": str(signature, 'utf-8')
      }
  ```

