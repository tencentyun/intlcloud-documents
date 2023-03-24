## 소개

[WordPress](https://cn.wordpress.org/)는 PHP 언어를 사용해 개발된 블로그 플랫폼입니다. 사용자는 PHP와 MySQL 데이터베이스를 지원하는 서버에 개인 웹 사이트를 구축할 수 있고, WordPress를 콘텐츠 관리 시스템(CMS)으로 사용할 수도 있습니다.

WordPress의 강력한 기능과 확장성은 플러그 인이 많아 기능 확충이 쉽기 때문입니다. 완전한 하나의 웹 사이트가 기본적으로 갖추어야 할 모든 기능은 3rd party 플러그 인을 통해 실행할 수 있습니다.

본 문서에서는 플러그 인을 사용한 원격 파일 첨부 기능을 통해 WordPress의 미디어 라이브러리 첨부 파일을 Tencent Cloud의 [Cloud Object Storage(COS)](https://www.tencentcloud.com/products/cos)에 저장하는 방법을 소개합니다.

COS는 고확장성, 저비용, 신뢰성, 보안과 같은 특징이 있습니다. 미디어 라이브러리 첨부 파일을 COS에 저장할 경우 장점은 다음과 같습니다.

- 첨부 파일의 신뢰성이 높아집니다.
- 서버에 첨부 파일을 위한 별도의 스토리지 용량을 마련하지 않아도 됩니다.
- 이미지 첨부 파일을 조회할 때 바로 COS 서버에 연결하면 서버의 다운스트림 대역폭/트래픽을 점유하지 않으며, 액세스 속도가 더 빨라집니다.
- Tencent Cloud [Content Delivery Network(CDN)](https://www.tencentcloud.com/products/cdn)와 함께 사용하면 사용자의 이미지 첨부 파일 확인 속도를 더욱 향상시키고 웹사이트 액세스 속도를 최적화할 수 있습니다.



## 전제 조건

1. 버킷을 생성 완료해야 하며, 그렇지 않은 경우 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309)의 지침에 따라 버킷을 생성합니다.
2. [Cloud Virtual Machine](https://www.tencentcloud.com/document/product/213)에 설명된 대로 CVM(Cloud Virtual Machine) 인스턴스와 같은 서버를 생성했습니다.


## 실행 순서

### Wordpress 웹사이트 배포

CVM에서 WordPress 웹사이트를 빠르게 구축하려면 이미지를 통해 또는 수동으로 배포할 수 있습니다. 비즈니스 웹 사이트의 확장성에 대한 요구 사항이 높은 경우 다음 문서의 지침에 따라 수동으로 배포할 수 있습니다.

- [WordPress 웹사이트 구축(Linux)](https://intl.cloud.tencent.com/document/product/213/8044)
- [WordPress 웹사이트 구축(Windows)](https://intl.cloud.tencent.com/document/product/213/34806)

다음과 같이 쉽게 이미지를 통해 WordPress 웹 사이트를 배포할 수 있습니다.

1. 이미지를 통해 WordPress 웹사이트를 배포합니다.
   1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인 한 후 인스턴스 관리 페이지에서 **생성**을 클릭합니다.
   2. 프롬프트에 따라 모델을 선택합니다. **인스턴스 구성 > 이미지**에서 **이미지 마켓플레이스**를 클릭하고 **이미지 마켓플레이스에서 선택**을 선택합니다.
   3. ‘이미지 마켓플레이스’ 팝업 창에서 **기본 소프트웨어**를 선택하고 검색을 위해 **wordpress**를 입력합니다.
   4. 필요에 따라 이미지를 선택합니다. 여기서는 **WordPress 블로그 프로그램 \_v5.5.3(CentOS | LAMP)**을 선택합니다. 그 다음 **무료 평가판**을 클릭합니다.
   5. 구매 후 CVM 콘솔에 로그인하여 새로 생성된 인스턴스를 보안 그룹과 연결하고 인바운드 규칙에서 포트 80을 엽니다.
2. CVM 인스턴스 관리 페이지에서 인스턴스의 **공중망 IP**를 복사하고 로컬 브라우저에서 `http://공중망 IP/wp-admin`에 액세스하여 WordPress 웹 사이트 설치를 시작합니다.
   1. WordPress 언어를 선택하고 **Continue**를 클릭합니다.
   2. WordPress 웹 사이트 제목과 관리자 사용자 이름, 비밀번호 및 이메일 주소를 입력합니다.
   3. **WordPress 설치**를 클릭합니다.
   4. **로그인**을 클릭합니다.
4. WordPress를 v6.0.2로 업그레이드합니다.
왼쪽 사이드바에서 대시보드 > ‘업데이트’를 클릭하여 WordPress를 v6.0.2로 업데이트합니다.





### COS 버킷 생성

1. **공개 읽기 및 개인 쓰기** 버킷을 생성합니다. 버킷 리전은 WordPress 블로그 플랫폼을 실행하는 CVM과 동일한 리전을 권장합니다. 자세한 생성 방법은 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309) 문서를 참고하십시오.
2. **버킷 리스트**에서 방금 생성한 버킷을 찾아 이름을 클릭한 후 버킷 페이지로 이동합니다.
3. 왼쪽 메뉴에서 **개요**를 클릭하여 액세스 도메인을 조회하고 기록합니다.


### 플러그인 설치 및 구성

플러그인 라이브러리 또는 소스 코드를 통해 플러그인을 설치할 수 있습니다.

#### 플러그인 라이브러리에 설치(권장)

WordPress 백엔드에서 **플러그인**을 클릭하고 **tencentcloud-cos** 플러그인을 직접 검색한 다음 **지금 설치**를 클릭합니다.


#### 소스 코드를 통한 설치

플러그인 소스 코드를 다운로드하고 WordPress 플러그인 디렉터리 `wp-content/plugins`에 업로드하고 백엔드에서 실행합니다.

다음 단계에서는 Ubuntu를 예로 들어 플러그인을 설치하는 방법을 설명합니다.

1. wp-content의 상위 디렉터리로 이동: 
```
cd /var/www/html 
```
2. 권한 추가: 
```
chmod -R 777 wp-content 
```
3. 플러그인 디렉터리 생성:
```
cd wp-content/plugins/
mkdir tencent-cloud-cos
cd tencent-cloud-cos
```
4. 플러그인 디렉터리에 플러그인 다운로드:
```
wget https://cos5.cloud.tencent.com/cosbrowser/code/tencent-cloud-cos.zip
unzip tencent-cloud-cos.zip
rm tencent-cloud-cos.zip -f
```
5. 왼쪽 사이드바에서 ‘플러그인’을 클릭하면 플러그인을 볼 수 있습니다. 활성화를 클릭하여 활성화합니다.





#### **플러그인 구성**

tencent-cloud-cos 플러그인에서 COS 버킷 정보를 구성합니다.

1. ‘설정’을 클릭하여 tencent-cloud-cos 플러그인을 구성합니다.

2. 다음과 같이 COS 정보를 구성합니다.
<table>
<thead>
<tr>
<th align="left">구성 항목</th>
<th align="left">구성 값</th>
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
<td align="left">이 옵션을 활성화 후에는 원본 파일이 로컬에 보관되지 않습니다</td>
</tr>
<tr>
<td align="left">원격 파일 보관</td>
<td align="left">이 옵션을 활성화한 후 파일이 삭제되면 로컬 파일 사본만 삭제되고 원격 COS 버킷의 파일 사본은 복구하려는 경우에 대비하여 계속 보관됩니다</td>
</tr>
<tr>
<td align="left">썸네일 금지</td>
<td align="left">이 옵션을 활성화하면 썸네일 파일이 업로드되지 않습니다</td>
</tr>
<tr>
<td align="left">Cloud Infinite(CI)</td>
<td align="left">CI 서비스가 활성화되면 이미지에 편집, 압축, 형식 변환, 워터마크 추가 등 이미지에 대한 다양한 작업을 수행할 수 있으며, 자세한 내용은 <a href="https://www.tencentcloud.com/products/ci">Cloud Infinite</a>를 참고하십시오</td>
</tr>
<tr>
<td align="left">파일 조정</td>
<td align="left">파일 조정이 활성화되면 이미지, 비디오, 오디오, 텍스트, 파일 및 웹 페이지의 멀티미디어 콘텐츠를 지능적으로 조정합니다. 음란물, 저속, 불법, 혐오, 공격적인 정보와 같은 비준수 콘텐츠를 효과적으로 식별하여 운영상의 위험을 방지할 수 있습니다. 자세한 내용은 <a href="https://www.tencentcloud.com/document/product/436/53946">민감한 콘텐츠 조정 개요</a>를 참고하십시오.</td>
</tr>
<tr>
<td align="left">파일 미리보기</td>
<td align="left">파일 미리보기가 활성화되면 파일을 이미지, PDF 파일 또는 HTML5 페이지로 변환하여 웹 페이지에 파일 콘텐츠를 표시합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/49159">파일 미리보기 개요</a>를 참고하십시오.</td>
</tr>
<tr>
<td align="left">디버깅</td>
<td align="left">이 기능은 오류, 예외 및 경고를 기록합니다</td>
</tr>
</tbody></table>


2. 구성이 완료되면 **구성 저장**을 클릭합니다.



## **COS에 대한 WordPress 첨부 파일 스토리지 확인**

Wordpress에서 이미지로 게시물을 작성하고 이미지가 COS에 저장되어 있는지 확인할 수 있습니다.

1. WordPress 대시보드에서 왼쪽 사이드바의 ‘게시물’을 클릭하여 이미지가 포함된 게시물을 생성합니다.

2. ‘Hello world!’ 편집 기본적으로 WordPress에서 생성된 게시물입니다.

3. 오른쪽에서 ‘+’를 클릭합니다.

4. 이미지를 업로드합니다.

5. 그 다음 업로드된 이미지의 URL이 `https://<BucketName-APPID>.cos.<Region>.myqcloud.com/<ObjectKey>` 형식의 `https://wd-125000000.cos.ap-nanjing.myqcloud.com/2022/10/입하-1200x675.jpeg`와 같은 COS URL인지 확인하고 그렇다면 이미지가 COS 버킷에 업로드된 것입니다.

6. COS 콘솔에 로그인하면 버킷에서 새로 업로드된 이미지를 볼 수 있습니다.

>? 상기 테스트에 성공하면 [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976) 또는 [COS Migration](https://intl.cloud.tencent.com/document/product/436/15392)을 사용하여 이전 WordPress 리소스를 COS 버킷에 동기화합니다. **이 단계를 수행해야 합니다. 그렇지 않으면 COS에서 이러한 리소스를 볼 수 없습니다**. 그 다음 아래의 [Origin-pull 설정](#1)에 따라 Origin-pull을 선택적으로 활성화할 수 있습니다.


## 확장

1. CDN 가속을 사용하여 액세스합니다.
버킷에 CDN 가속 설정이 필요한 경우 [CDN 가속 구성](https://intl.cloud.tencent.com/document/product/436/18670) 문서를 참고하십시오. 플러그 인 설정에서 URL 접두사의 기본값을 CDN 가속 도메인 또는 사용자 정의 가속 도메인으로 수정하면 됩니다.
2. 데이터베이스의 리소스 주소를 변경합니다.
새로 생성한 사이트가 아니라면 데이터베이스에는 반드시 기존 리소스 링크 주소가 존재하며, 이 리소스 주소를 변경해야 합니다. 플러그 인에서 변경 기능을 제공하며, 최초 변경 전 반드시 백업해 두시기 바랍니다.
 - 기존 도메인에 원본 리소스 도메인을 입력합니다. 예: `https://example.com/`
 - 신규 도메인에 현재의 리소스 도메인을 입력합니다. 예: `https://img.example.com/`
3. 크로스 도메인 액세스를 설정합니다.
본 문서의 상응하는 리소스 링크 인용 시 콘솔은 크로스 도메인 오류 `No 'Access-Control-Allow-Origin' header is present on the requested resource`를 표시합니다. 이는 header를 추가하지 않았기 때문입니다. 크로스 도메인 액세스 CORS 설정에서 HTTP Header 설정을 추가해야 하며, 다음 두 가지 방법으로 구성할 수 있습니다.
 - COS 콘솔에서 구성

>? 크로스 도메인 설정 작업 순서는 [CORS 설정](https://intl.cloud.tencent.com/document/product/436/13318) 문서를 참고하십시오.
>
 - CDN 콘솔에서 구성
    - 모든 도메인을 허용할 경우, 다음과 같이 구성합니다.
```plaintext
Access-Control-Allow-Origin: *
```
    - 사용자 개인 도메인 액세스만 허용할 경우, 다음과 같이 구성합니다.
```plaintext
Access-Control-Allow-Origin: https://example.com
```
<span id=1></span>
4. Origin-pull을 설정합니다.
COS 콘솔을 통해 WordPress 미디어 라이브러리에 리소스를 업로드하지 않는 경우 COS Origin-pull을 사용하는 것이 좋습니다. 자세한 내용은 [Origin-pull 설정](https://intl.cloud.tencent.com/document/product/436/31508)을 참고하십시오.
Origin-pull이 활성화되면 클라이언트가 처음으로 COS의 원본 객체에 액세스할 때 COS가 객체에 도달할 수 없는 경우 302 HTTP 상태 코드를 반환하고 자동으로 요청을 Origin-pull 주소로 리디렉션합니다. 그 다음 원본에서 액세스할 객체를 제공합니다. 한편 COS는 원본에서 이 객체를 복사하여 해당 COS 디렉터리에 저장하므로 COS는 후속 요청에서 객체를 클라이언트에 직접 반환할 수 있습니다.




