노드 캐시 유효성 구성은 CDN 노드에서 원본 서버 리소스의 캐시 만료 시간을 설정하여 CDN 노드에서 원본 서버 리소스의 캐시 업데이트 빈도를 조정할 수 있습니다. 비즈니스 요구 사항에 따라 디렉터리, 파일 접미사 및 전체 파일 경로별로 리소스의 캐시 만료 시간을 구성할 수 있습니다.

## 기능 소개
CDN은 노드 캐시 유효성 구성 캐시 만료 시간에 따라 CDN 노드의 캐시 리소스 만료 여부를 판단합니다.
- CDN 노드에서 사용자가 액세스한 리소스의 캐시가 만료되지 않은 경우 CDN 노드는 캐시를 사용자에게 직접 반환합니다.
- CDN 노드에서 사용자가 액세스한 리소스가 캐시되지 않았거나 캐시가 만료된 경우 CDN 노드는 원본 서버로 돌아가 최신 리소스를 가져와 CDN 노드에 캐시하고 동시에 사용자에게 반환합니다.

원본 서버 리소스가 업데이트되면 CDN 노드의 캐시를 즉시 업데이트해야 합니다. [캐시 퍼지](https://console.cloud.tencent.com/cdn/refresh) 기능을 사용하여 CDN 노드의 만료되지 않은 캐시를 능동적으로 업데이트하여 CDN 노드 캐시가 원본 서버의 리소스와 일치하도록 할 수 있습니다.

## 주의 사항
- 캐시 만료 시간은 Origin-pull 빈도에 영향을 미치므로 실제 비즈니스 요구 사항에 따라 리소스 캐시 기간을 설정하는 것이 좋습니다. 캐시 만료 시간이 너무 짧으면 CDN이 자주 Origin-pull되어 원본 서버의 대역폭을 증가시킬 수 있습니다. 캐시 만료 시간이 너무 길면 CDN 캐시 업데이트가 느려져 사용자가 최신 리소스에 액세스할 수 없게 됩니다.
- CDN 노드는 [Tencent Cloud CDN 캐시 규칙 및 우선 순위](#m1)에 따라 리소스를 캐시합니다. 그러나 낮은 요청 빈도로 인해 캐시 만료 시간이 되기 전에 CDN 노드의 캐시 리소스도 노드에서 미리 삭제될 수 있습니다.
- 원본 서버에서 리소스의 내용을 변경한 후 버전 번호(img-v1.jpg, img-v2.jpg) 형태로 다른 콘텐츠로 리소스를 명명하는 등 업데이트 전후 원본 서버의 리소스에 다른 이름을 사용하는 것을 권장합니다. CDN 노드는 캐시가 만료되지 않았기 때문에 여전히 이전 리소스를 사용하여 사용자에게 반환합니다.
- 기존 버전(기본 모드)의 노드 캐시 유효성 구성을 계속 사용하고 있는 경우, 고급 모드 설정에 따라 최신 버전으로 업그레이드된 노드 캐시 유효성 구성을 제출하여 더 많은 기능을 지원 받을 수 있습니다. 고급 모드로 업그레이드한 후에는 기존 기본 모드로 복구할 수 없습니다. 노드 캐시 유효성 구성 문서의 이전 버전: [노드 캐시 만료 설정(Old)](https://intl.cloud.tencent.com/document/product/228/35317)
- 원본 서버는 응답 헤더 Cache-Control을 설정하여 CDN 노드의 캐시 만료 시간을 제어할 수 있으며(캐시 옵션: 원본 서버 따르기) CDN 노드는 Cache-Control 응답 헤더를 사용자에게 전달하여 브라우저의 캐시 시간을 제어합니다. 브라우저 캐시 시간을 CDN 노드에서 설정해야 하는 경우 [브라우저 캐시 만료 설정](https://intl.cloud.tencent.com/document/product/228/38932)을 통해 CDN 노드가 사용자에게 응답하는 Cache-Control 헤더를 수정할 수 있습니다.


## 구성 설명
### 작업 단계
1. [CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인합니다;
2. 왼쪽 사이드바에서 **도메인 관리**를 클릭하여 도메인 관리 목록으로 이동합니다;
3. 구성할 도메인을 선택하고 **관리**를 클릭하여 도메인 설정 페이지로 이동합니다;
4. **캐시 구성**을 클릭하여 **노드 캐시 유효성 구성**을 볼 수 있는 캐시 설정 태그로 전환합니다.
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/cd08be49dbf25e88f28b32f019284231.png" width="850px">
<br>
5. **규칙 추가**를 클릭하여 새 규칙 페이지로 이동하고 노드 캐시 유효성 구성을 추가합니다.
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/a57bc131850fc1a49c69e2aa86d0050e.png" width="450px">
<br>
<table>
<thead>
<tr>
<th>구성 항목</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>유형</td>
<td>모든 파일, 파일 접미사, 파일 디렉터리, 전체 경로 파일 및 홈 페이지 설정 지원:<br> 모든 파일: 기본 규칙을 설정할 모든 파일을 지정합니다.<br> 파일 접미사: 파일의 접미사 설정 규칙을 지정합니다.<br> 파일 디렉터리: 파일에 대한 디렉터리 설정 규칙을 지정합니다.<br> 전체 경로 파일: 규칙을 설정할 파일의 전체 경로를 지정합니다.<br> 메인 화면: 도메인 루트 디렉터리 설정 규칙을 지정합니다.</td>
</tr>
<tr>
<td>콘텐츠</td>
<td>선택한 다양한 파일 형식에 따라 콘텐츠 입력 제한:</br>유형이 모든 파일인 경우: 모든 파일로 고정됩니다.</br>유형이 파일 접미사인 경우: 파일 접미사의 이름 입력 지원. 여러 개는 ";"으로 구분합니다. 예시: jpg;png;css.</br>유형이 파일 디렉터리일 때: 파일 디렉터리 입력이 지원됩니다. "/"로 끝날 수 없으며, 여러 개는 ";"으로 구분합니다. 예시: /test;/a/b/c.</br>유형이 전체 경로 파일인 경우: 파일 전체 경로 입력이 지원됩니다. 여러 개는 ";"으로 구분합니다. 예시: /index.html;/test/.jpg.</td>
</tr>
<tr>
<td>캐시 옵션</td>
<td>다음 원본 서버, 캐시 및 캐시하지 않음 규칙 설정 지원:<br> 원본 서버 따르기: 원본 서버 응답 헤더의 Cache-Control 헤더에 따라 CDN 노드 캐시 시간을 설정하고 휴리스틱 캐시 설정을 지원합니다. <br>캐시: CDN 노드의 캐시 시간을 사용자 지정하고 강제 캐시 설정을 지원합니다. <br>캐시하지 않음: 리소스를 캐시하지 않도록 CDN 노드를 설정합니다.<br></td>
</tr>
</tbody></table>

[](id:m1)	
### Tencent Cloud CDN 캐시 규칙 및 우선 순위
#### 캐시 옵션: 원본 서버 따르기
<img src="https://qcloudimg.tencent-cloud.cn/raw/0d0086b11c0e9968707865af46a4c23d.jpg" width="850px">



CDN 노드는 원본 서버 응답 헤더의 Cache-Control 헤더에 따라 캐시 시간을 설정합니다.
- 원본 서버 응답 헤더의 Cache-Control 필드는 max-age이며, CDN 노드 캐시 시간은 max-age 값에 따라 설정됩니다. 예를 들어, Cache-Control: max-age=300, 캐시 시간은 300초입니다;
	- 원본 서버 응답 헤더의 Cache-Control 필드가 no-cache 또는 no-store 또는 private이면 CDN 노드는 리소스를 캐시하지 않습니다;
	- 원본 서버 응답 헤더에 Cache-Control 또는 Expires가 없는 경우, 휴리스틱 캐시 상태에 따라 캐시 규칙을 설정하며, 세부 사항은 다음과 같습니다:
		- 휴리스틱 캐시 비활성화 시 원본 서버의 응답 헤더에 Cache-Control 또는 Expires가 없는 경우 캐시 시간은 600초입니다.
		- 휴리스틱 캐시 활성화 시 원본 서버의 응답 헤더에 Cache-Control 또는 Expires가 없는 경우 다음 규칙에 따라 휴리스틱 캐시 시간을 설정합니다:
		 i. 기본 구성: 원본 서버 응답 헤더에 Last-Modified가 있는 경우, 캐시 시간=(현재 시간 - Last-Modified)\* 0.1입니다. 원본 서버 응답 헤더에 Last-Modified가 없는 경우, 기본 캐시 시간은 600초입니다.
		 <br>
		 <img src="https://qcloudimg.tencent-cloud.cn/raw/80612ba1e40f345e14b188939cb7b557.png" width="450px">
		 <br>
		 ii. <b>사용자 정의 정책</b>: 휴리스틱 캐시의 시간을 사용자 정의할 수 있습니다.
		 <br>
		 <img src="https://qcloudimg.tencent-cloud.cn/raw/06629eb849a9e56ee0c16db1f8bfe3c6.png" width="450px">
		 <br>

#### 캐시 옵션: 캐시
<img src="https://qcloudimg.tencent-cloud.cn/raw/dc781cff77d79f57fa3c9df800e21a4d.jpg" width="850px">

CDN 노드의 캐시 시간을 사용자 정의합니다.	
- 강제 캐시 비활성화:
	- 원본 서버 응답 헤더의 Cache-Control 필드가 max-age이거나 원본 서버 응답 헤더에 Cache-Control이 없으면 사용자 정의 CDN 노드 캐시 규칙에 따라 캐시됩니다.
	- 원본 서버 응답 헤더의 Cache-Control 필드가 no-cache 또는 no-store 또는 private이면 CDN 노드는 리소스를 캐시하지 않습니다.
	<br>
	<img src="https://qcloudimg.tencent-cloud.cn/raw/35f0cf1d08f6395e541ec9c1c5ae364b.png" width="450px">
	<br>
- 강제 캐시 활성화: 원본 서버 응답 헤더 Cache-Control을 무시하고 사용자 정의 CDN 노드 캐시 규칙에 따라 캐시합니다.
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/fb2670449e6c40f5df4e8231c8f050b0.png" width="450px">
<br>

#### 캐시 옵션: 캐시하지 않음
리소스를 캐시하지 않도록 CDN 노드를 설정합니다. 리소스에 대한 각 사용자 요청에 대해 CDN 노드는 리소스를 획득하고 사용자에게 응답하기 위해 직접 Origin-pull을 수행합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/621483c2535ca8e950e7a36c46c96983.png" width="450px">
<br>

#### 여러 캐시 규칙의 우선 순위
여러 캐시 규칙이 동시 구성된 경우 하단 규칙이 상단 규칙보다 **우선 순위가 높습니다**. **우선순위 조정**을 클릭하고 캐시 규칙 순서를 드래그하여 우선순위를 조정할 수 있습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/dcdbba45c63c0a18022fa73ecb76cb13.png" width="850px">	

### 권장 구성
- 자주 업데이트되지 않는 정적 파일(예: 이미지 유형, 애플리케이션 다운로드 유형 등)의 경우 30일 설정을 권장합니다.
- 자주 업데이트되는 정적 파일(예: js, css 등)의 경우 비즈니스의 업데이트 빈도에 따라 캐시 시간을 설정할 것을 권장합니다.
- 동적 파일(예: php, jsp, asp, aspx 등의 동적 파일), **캐시하지 않음으로 설정해야 합니다**.
- **웹 사이트 로그인**(예: wordpress 백그라운드 로그인 디렉터리 /wp-admin) 또는 **인터페이스 쿼리** 등 원본 서버와 직접 상호 작용해야 하는 기타 요청의 경우 **캐시하지 않음으로 설정해야 합니다**. 그렇지 않으면 액세스 오류가 발생할 수 있습니다.

	
### 구성 제한
- 도메인당 최대 100개까지 캐시 규칙을 추가할 수 있습니다.
- 다수 캐시 규칙의 우선순위: 하단 우선순위가 상단 우선순위보다 높습니다.
- 단일 파일 확장자/파일 디렉터리/전체 경로 파일 규칙에는 최대 100개까지 콘텐츠를 입력할 수 있으며, 각 콘텐츠 사이에 ‘;’ 부호를 사용하여 분리합니다. 예: 파일 확장자  jpg;png.	
- 규칙을 구성하지 않거나 요청이 구성된 규칙에 맞지 않으면 CDN 노드는 원본 서버 응답 헤더의 Cache-Control 헤더에 따라 캐시 시간을 설정합니다. Cache-Control 필드에서 CDN 노드는 기본적으로 600s 동안 캐시된 리소스로 설정됩니다.
- CDN 노드는 GET 및 HEAD 요청 유형의 요청 콘텐츠만 캐시하고, POST 및 OPTIONS 등 기타 요청 유형의 요청 콘텐츠는 CDN 노드에 의해 캐시되지 않습니다.


## 구성 예시
### 예시1
기존 캐시 규칙: php;jsp;asp;aspx 파일 접미사가 있는 리소스는 캐시되지 않으며, 다른 모든 파일은 30일 동안 캐시됩니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/5129af6e01dd139afcf5c44a7ba97ef3.png" width="850px">
<br>
추가: jpg 및 png 파일의 접미사를 가진 리소스는 10일 동안 캐시되며 원본 서버의 응답 헤더 Cache-Control은 무시해야 합니다. 즉, 강제 캐시를 활성화합니다. 다른 모든 파일의 캐시 규칙은 원본 서버를 따르도록 수정됩니다.

1. **규칙 추가**를 클릭하고, 유형은 파일 접미사, 콘텐츠는 jpg;png, 캐시 옵션은 캐시, 캐시 시간은 10일, 강제 캐시는 Yes, **확인**을 클릭합니다.
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/a1db0f8cbc470efa0b5749114ca8ea07.png" width="450px">
<br>
2. 모든 파일에 대한 캐시 규칙을 선택하고 **수정**을 클릭하고, 원본 서버를 따르도록 캐시 옵션을 수정한 후 **확인**을 클릭합니다.
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/c0442f19e230b69456f59d1874d784a9.png" width="450px">
<br>
3. 변경된 캐시 규칙은 다음과 같습니다:
	- jpg 및 png 파일 접미사가 있는 리소스는 10일 동안 캐시되고 캐시는 강제 실행됩니다;
	- php;jsp;asp;aspx 파일 접미사가 있는 리소스는 캐시되지 않습니다;
	- 기타 모든 파일은 30일 동안 캐시됩니다.
	<br>
	<img src="https://qcloudimg.tencent-cloud.cn/raw/bfc24f2fca1ab9a184b0bf415c85a0f4.png" width="850px">
	<br>
	실제 캐시 상황은 다음과 같습니다.
	-  `www.test.com/abc.jpg`  리소스 노드 캐시 시간은 원본 서버 응답 헤더의 Cache-Control 필드가 no-cache 또는 no-store 또는 private인 경우에도 10일입니다.
	-  'www.test.com/def.php'  리소스가 노드에 캐시되지 않습니다;

	
### 예시2
**WordPress로 사이트 구축을 위한 노드 캐시 유효성 구성 제안:**
- 백그라운드 로그인 주소/wp-admin 디렉터리의 리소스는 캐시하지 않음으로 설정해야 합니다. 그렇지 않으면 백그라운드 로그인 관련 리소스가 캐시되어 로그인 오류가 발생합니다. 다른 인터페이스 관련 리소스가 있는 경우 캐시를 설정하지 않아도 됩니다.
- 동적 파일 접미사가 있는 php;jsp;asp;aspx 리소스는 캐시되지 않도록 설정해야 합니다(CDN 기본 캐시 규칙);
- html;js;css 접미사 파일은 자주 업데이트되며, 업데이트 빈도에 따라 캐시 시간을 설정해야 합니다. 캐시 시간을 7일로 설정하고 강제 캐시를 설정하지 않는 것이 좋습니다.
- 기타 모든 파일은 30일 동안 캐시됩니다(CDN 기본 캐시 규칙).

**CDN 기본 캐시 규칙에 따라 다음과 같이 규칙을 추가합니다:**
1. **규칙 추가**를 클릭하고 유형은 디렉터리, 콘텐츠는 /wp-admin, 캐시 옵션은 캐시하지 않음, **확인**을 클릭합니다.
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/93a9e55ac5c35bbe1e955eda302f41f1.png" width="450px">
<br>
2. **규칙 추가**를 클릭하고 유형은 파일 접미사, 콘텐츠는 html;js;css, 캐시 옵션은 캐시, 캐시 시간은 7일, 강제 캐시는 NO를 클릭하고 **확인**을 클릭합니다.
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/1e0248cf175dd0158f73300d3bf7dc2f.png" width="450px">
<br>
3. 우선 순위에 따라 하단 우선 순위가 상단보다 높으며, **우선 순위 조정**을 클릭하여 "/wp-admin 디렉터리는 규칙을 캐시하지 않음" 규칙을 맨 아래로 드래그하여, 이 규칙을 최우선 순위로 설정합니다.
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/ba9b0809fc20a354ebadfbed4f19eee5.png" width="850px">
<br>
4. 변경된 캐시 규칙은 다음과 같습니다:
	- /wp-admin 디렉터리의 모든 리소스는 캐시되지 않습니다;
	- html;js;css 파일 접미사가 있는 리소스는 7일 동안 캐시됩니다;
	- php;jsp;asp;aspx 파일 접미사가 있는 리소스는 캐시되지 않습니다;
	- 기타 모든 파일은 30일 동안 캐시됩니다.
	<br>
	<img src="https://qcloudimg.tencent-cloud.cn/raw/da6e9921da144c97f7b80e569f2d8444.png" width="850px">
	<br>

## FAQ
- [원본 서버에서 파일이 변경되면 CDN 캐시 노드의 캐시가 실시간으로 업데이트되나요?](https://intl.cloud.tencent.com/document/product/228/11203)
- [사용자 액세스가 CDN cache에 히트되었는지 어떻게 알 수 있습니까?](https://intl.cloud.tencent.com/document/product/228/11203)
