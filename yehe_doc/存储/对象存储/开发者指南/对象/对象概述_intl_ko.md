## 소개

객체(Object)는 Cloud Object Storage(COS)의 기본 단위로서 이미지, 문서, 멀티미디어 파일 등 다양한 포맷의 데이터라고 할 수 있습니다. 버킷(Bucket)은 객체의 저장 장치이며 각 버킷은 용량 제한 없이 객체를 수용할 수 있습니다. 객체는 COS에서 다양한 스토리지 유형으로 지정 가능합니다. 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)을 참고하십시오.

각 객체는 객체 키(ObjectKey), 객체 값(Value), 객체 메타데이터(Metadata)로 구성됩니다.

- 객체 키(ObjectKey): 객체 키는 버킷에 있는 객체의 고유 ID이며 일반적으로 파일 경로로 이해할 수 있습니다. API, SDK 예시 중 객체의 이름 생성 포맷은 `<ObjectKey>`입니다.
- 객체 값(Value): 업로드하는 객체 자체를 뜻하며 일반적으로 파일 콘텐츠(Object Content)로 이해할 수 있습니다.
- 객체 메타데이터(Metadata): 파일 수정 시간, 스토리지 유형과 같은 파일 속성에 해당하는 키 값 쌍입니다. 객체 업로드 후 조회가 가능합니다.


## 객체 키

Tencent Cloud COS 객체는 합법적인 객체 키를 보유해야 하며 객체 키(ObjectKey)는 버킷에 있는 객체의 고유 ID입니다.
예를 들어, 객체의 액세스 주소 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/folder/picture.jpg`에서 객체 키는 `folder/picture.jpg`입니다.

### 이름 생성 규칙

- 객체 키 이름 생성 시 모든 UTF-8 문자를 사용할 수 있습니다. 이름과 기타 응용 프로그램의 호환성을 위해 영어 알파벳 대소문자와 숫자 [a-z, A-Z, 0-9]의 조합을 사용하는 것이 좋습니다.
- 코드 길이는 최대 850바이트입니다.
- 이름은 슬래시 `/` 또는 백슬래시 <code>\\</code>로 시작할 수 없습니다.
- 객체 키에는 ASCII 제어 부호인 위(↑), 아래(↓), 오른쪽(→), 왼쪽(←)을 포함할 수 없으며 이는 각각 CAN(24), EM(25), SUB(26), ESC(27)에 대응됩니다.
- 파일 이름에 `*` 및 `%`와 같은 특수 기호를 사용하지 마십시오.

>? 사용자가 업로드한 파일 또는 폴더 이름에 중국어 문자가 포함되어 있는 경우 파일 또는 폴더에 액세스하거나 요청할 때 중국어 문자는 URL Encode 규칙에 따라 백분율 인코딩된 문자열로 변환됩니다.
> 예를 들어, `문서.doc`에 액세스할 때 객체 키는 `문서.doc`이지만 실제로는 URL Encode 규칙에 따라 백분율 인코딩된 문자열은 `%e6%96%87%e6%a1%a3.doc`입니다.
> 


다음은 유효한 객체 키 이름의 예시입니다.
- doc/exampleobject
- my.great_photos-2016/01/me.jpg
- videos/2016/birthday/video.wmv

#### 특수 부호

어떤 부호는 객체 키에서 16진법 형태로 URL 인코딩 또는 참조 테이블이 필요합니다. 그 중 일부는 출력이 불가능하여 브라우저가 처리할 수 없으므로 특수한 프로세스가 필요한데, 해당 부호는 다음과 같습니다.

<table>
   <tr>
	 <td>，</td>
      <td>:</td>
      <td>;</td>
      <td>=</td>
   </tr>
   <tr>
      <td>&</td>
      <td>$</td>
      <td>@</td>
      <td>+</td>
   </tr>
   <tr>
      <td>?</td>
      <td>ASCII 부호 범위: 00-1F 16진법(0-31 10진법)과 7F(127 10진법)</td>
      <td>(빈칸)</td>
      <td></td>
   </tr>
</table>


또한 어떤 부호는 많은 특수한 프로세스를 거쳐야만 모든 응용 프로그램 간 일관성을 유지할 수 있으므로 바로 사용하지 않는 것을 권장합니다. 사용을 피해야 할 부호는 아래와 같습니다.
<table>
   <tr>
      <td>`</td>
      <td>^</td>
      <td>"</td>
      <td>\</td>
   </tr>
   <tr>
      <td>{</td>
      <td>}</td>
      <td>[</td>
      <td>]</td>
   </tr>
   <tr>
      <td>~</td>
      <td>%</td>
      <td>#</td>
      <td>|</td>
   </tr>
   <tr>
      <td>*</td>
      <td>></td>
      <td><</td>
      <td>ASCII <br> 128-255 10진법</td>
   </tr>
</table>

### 객체 액세스 주소

객체 액세스 주소는 버킷 액세스 주소와 객체 키로 구성되어 `<버킷 도메인>/<객체 키>`의 구조로 이루어져 있습니다.
예를 들어, 객체 `exampleobject.txt`를 광저우(화남) 리전 버킷 `examplebucket-1250000000`에 업로드하면 `exampleobject.txt` 액세스 주소는 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject.txt`입니다.

### 폴더와 디렉터리

COS 자체에는 폴더나 디렉터리의 개념이 없습니다. COS는 객체 `project/a.txt`를 업로드했다고 해서 `project` 폴더를 생성하지는 않습니다. 간편하게 사용할 수 있도록 COS는 콘솔과 COS browser 등의 도식화 툴에서 '폴더' 또는 '디렉터리' 디스플레이 방식을 모방합니다. 예를 들어, 키 값을 `project/`로 하여 생성하면 콘텐츠가 없는 객체는 일반적인 폴더로 표시됩니다.

예를 들어 API, SDK를 통해 객체 `project/doc/a.txt`를 업로드하면 세퍼레이터 `/`가 '폴더'의 디스플레이 방식을 모방하고, 콘솔에서 '폴더' `project`와 `doc`가 나타납니다. 그 중 `doc`는 `project`의 하위 '폴더'이며 `a.txt` 파일을 포함합니다.

>! 버킷의 각 객체는 각 분산형 클러스터에 수평적으로 분포되어 있습니다. 따라서 특정한 객체 키 접두사로 객체의 크기를 바로 알 수 없으며 각 객체 크기를 누적 계산해야 전체 크기를 알 수 있습니다.
>

파일이나 디렉터리 삭제 작업은 비교적 복잡합니다. 자세한 내용은 다음과 같습니다.

| 경로 삭제 | 객체 또는 폴더 삭제  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                            | 결과                                                         |
| -------- | --------------------------------- | ------------------------------------------------------------ |
| 콘솔   | 폴더 `project`                  | 객체 키 접두사가 `project/`인 모든 객체를 삭제합니다.               |
| 콘솔   | 객체 `project/doc/a.txt`          | `project`와 `doc`폴더는 보관할 수 있습니다.                            |
| API, SDK | 객체 `project/` 또는 `project/doc/` | 객체 `project/doc/a.txt`는 보관할 수 있습니다. 폴더 내 객체를 모두 삭제하고 싶다면 코드 순회를 이용해 폴더 내 객체를 삭제해야 합니다. |


## 객체 메타데이터

객체 메타데이터는 객체의 키 값 쌍을 의미하며, 서버가 HTTP 프로토콜 형식으로 HTML 데이터를 브라우저에 전송하기 전 보내는 문자열로써, HTTP Header라고도 합니다. 객체 업로드 시 HTTP Header를 수정하여 페이지 응답 형식을 바꾸거나 캐시 수정 시간과 같은 설정 정보를 전송할 수 있습니다. 

객체 메타데이터는 시스템 메타데이터와 사용자 정의 메타데이터의 2가지 종류가 있습니다.

>? 객체의 HTTP Header를 수정해도 객체 자체를 수정할 수는 없습니다.
>

### 시스템 메타데이터

객체 수정 시간, 객체 크기, 스토리지 유형 등 객체의 속성 정보를 의미합니다.

<table>
<thead>
<tr>
<th width="25%">이름</th>
<th width="75%">설명</th>
</tr>
</thead>
<tbody><tr>
<td>Content-Length</td>
<td>RFC 2616에서 정의한 HTTP 요청 콘텐츠 길이(바이트)를 의미합니다.</td>
</tr>
<tr>
<td>Last-Modified</td>
<td>객체 생성 날짜 또는 마지막 수정 날짜(나중에 생성된 객체 기준)를 의미합니다.</td>
</tr>
<tr>
<td>x-cos-version-id</td>
<td>객체 버전 ID. 버킷 버전 제어가 활성화될 경우 객체의 버전 ID를 반환하여 ID가 동일한 객체의 이전 버전을 표시합니다.</td>
</tr>
<tr>
<td>ETag</td>
<td>PUT Object를 통해 업로드한 객체의 MD5 값이나 멀티파트 업로드나 이전 버전 API를 통해 업로드한 객체의 고유 ID로 인증 기능이 없습니다.</td>
</tr>
</tbody></table>



### 사용자 정의 메타데이터

Content-Type, Cache-Control, Expires, x-cos-meta-\* 등 객체의 사용자 정의가 가능한 매개변수를 의미합니다. 자세한 내용은 [사용자 정의 Headers](https://intl.cloud.tencent.com/document/product/436/13361)를 참조하십시오.

<table>
<thead>
<tr>
<th width="25%">이름</th>
<th width="76%">설명</th>
</tr>
</thead>
<tbody><tr>
<td>Cache-Control</td>
<td>RFC 2616에서 정의한 캐시 정책으로, 객체 메타데이터로 저장됩니다.</td>
</tr>
<tr>
<td>Content-Disposition, <br>Content-Encoding, <br>Content-Type</td>
<td>RFC 2616에서 정의한 파일 이름/인코딩 포맷/콘텐츠 유형(MIME)으로, 객체 메타데이터로 저장됩니다.</td>
</tr>
<tr>
<td>Expires</td>
<td>RFC 2616에서 정의한 유효하지 않은 캐시 시간으로, 객체 메타데이터로 저장됩니다.</td>
</tr>
<tr>
<td>x-cos-acl</td>
<td>객체의 액세스 제어 리스트(ACL) 속성을 정의합니다. 유효 값은 private, public-read-write, public-read이고, 기본값은 private입니다.</td>
</tr>
<tr>
<td>x-cos-grant-*</td>
<td>권한을 보유한 계정에 특정 권한을 부여합니다.</td>
</tr>
<tr>
<td>x-cos-meta-*</td>
<td>사용자 정의한 헤더 정보를 허용하며, 객체 메타데이터로 반환합니다. (용량 제한 2KB)</td>
</tr>
<tr>
<td>x-cos-storage-class</td>
<td>객체의 스토리지 레벨을 설정하며, 열거 값은 STANDARD, STANDARD_IA, ARCHIVE이고, 기본값은 STANDARD입니다.</td>
</tr>
<tr>
<td>x-cos-server-side-encryption</td>
<td>객체를 위한 서버 암호화 활성화 여부와 암호화 방식을 지정합니다.</td>
</tr>
</tbody></table>


## 객체 작업

사용자는 Tencent Cloud 콘솔, 툴, API, SDK 등의 방식으로 객체를 관리할 수 있습니다.

>!지원하는 최대 업로드 파일 크기에 따라 [간편 업로드](https://intl.cloud.tencent.com/document/product/436/14113)와 [멀티파트 업로드](https://intl.cloud.tencent.com/document/product/436/14112)로 나눌 수 있습니다.
>- 간단 업로드는 객체 크기 5GB 이내로 제한됩니다.
>- 멀티파트 업로드 사용 시 각 파트의 크기는 5GB 이내로 제한되고 파트 수는 10,000개보다 작아야 합니다. 즉 최대 업로드 객체 크기는 약 48.82TB입니다. 제한 사항에 대한 자세한 내용은 [규격 및 제한](https://intl.cloud.tencent.com/document/product/436/14518)을 참조하십시오.

객체 업로드 완료 후 사용자는 콘솔에서 객체 관련 설정을 진행할 수 있습니다. 자세한 사항은 아래 내용을 참조하십시오.

- [객체 검색](https://intl.cloud.tencent.com/document/product/436/13325)
- [객체 정보 조회](https://intl.cloud.tencent.com/document/product/436/13326)
- [객체의 액세스 권한 설정](https://intl.cloud.tencent.com/document/product/436/13327)
- [사용자 정의 Headers](https://intl.cloud.tencent.com/document/product/436/13361)

## 객체 서브 리소스

COS는 버킷 및 객체와 관련된 서브 리소스를 가집니다. 서브 리소스는 객체에 종속되므로 독립적으로 존재할 수 없고, 객체 또는 버킷과 같은 다른 엔티티와 연결됩니다. 액세스 제어 리스트(Access Control List)는 특정 객체의 액세스 제어 정보 리스트를 의미하며 COS에서 객체의 서브 리소스 역할을 합니다.

액세스 제어 리스트는 권한을 보유한 계정과 허가된 권한 리스트로 나눌 수 있고, 이를 통해 객체의 액세스 제어를 관리합니다. 객체 생성 시 ACL은 객체를 전체 제어할 수 있는 객체 소유자를 식별합니다. 사용자는 객체 ACL을 인덱스하거나 업데이트된 권한 리스트로 교체할 수 있습니다.

>? ACL을 업데이트하려면 기존 ACL을 교체해야 합니다.
>

## 액세스 권한 유형

COS는 **공개 권한**과**사용자 권한**이라는 2가지 객체 권한 설정 유형을 지원합니다.
**공개 권한**은 권한 상속, 개인 읽기/쓰기와 공개 읽기/쓰기를 포함합니다.
- 권한 상속: 객체가 버킷 권한을 상속하여 버킷과 액세스 권한이 일치합니다. 객체에 액세스할 경우 COS가 객체 권한을 버킷 권한 상속으로 인식하면 버킷과 권한을 매칭하여 액세스에 응답합니다. 다른 새로운 객체를 추가할 경우 버킷 권한의 상속을 기본으로 합니다.
- 개인 읽기/쓰기: 객체에 액세스할 경우 COS가 객체 권한을 개인 읽기/쓰기로 인식하면 버킷의 권한 종류와 무관하게 [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)를 통해서 액세스해야 합니다.
- 공개 읽기/개인 쓰기: 객체에 액세스할 경우 COS가 객체 권한을 공개 읽기로 인식하면 버킷의 권한 종류와 무관하게 객체를 바로 다운로드할 수 있습니다.

**사용자 권한**: 루트 계정은 기본적으로 객체에 대한 모든 권한 즉, 전체 제어 권한을 갖습니다. 그 외에, COS는 서브 계정을 추가 생성하여 데이터 읽기/쓰기, 권한 읽기/쓰기 및 전체 제어가 가능한 최고 권한을 갖도록 지원합니다.

#### 적용 시나리오
개인 읽기/쓰기가 가능한 버킷에서 특정 객체에 공개 액세스를 설정했거나, 공개 읽기/쓰기가 가능한 버킷에서 특정 객체에 필요한 인증을 설정한 경우에만 액세스가 가능합니다.
