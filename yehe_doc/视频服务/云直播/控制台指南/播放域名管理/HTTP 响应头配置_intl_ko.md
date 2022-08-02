Tencent Cloud는 HTTP 헤더를 사용하여 HTTP 트랜잭션에 대한 정보를 전달하는 필드를 정의할 수 있습니다. 헤더 필드는 도메인 차원에서 작동합니다. 즉, 구성한 헤더 필드가 도메인의 모든 응답에 적용됩니다.


## 전제 조건
- [CSS 콘솔](https://console.cloud.tencent.com/live)에 로그인되어 있어야 합니다.
- [재생 도메인 이름](https://intl.cloud.tencent.com/document/product/267/35970)을 추가했습니다.

[](id:limit)
## 사용 제한
- 최대 10개의 헤더 필드를 구성할 수 있습니다.
- 같은 이름으로 두 개의 필드를 추가할 수 없습니다. 필드에 여러 값을 지정하려면 `값1, 값2, 값3` 형식을 사용합니다.
- 구성한 필드가 CSS 백엔드에서 사용하는 필드와 동일한 경우 수정하라는 메시지가 표시됩니다.
- 사용자 정의 필드의 길이는 1자 - 100자이며 알파벳 대소문자, 숫자 및 하이픈(-)으로 구성합니다.
- 필드 값은 비워둘 수 없습니다. 길이는 1자 - 1000자이며 중국어는 포함할 수 없습니다.


## HTTP 응답 헤더 설정
1. [도메인 관리](https://console.cloud.tencent.com/live/domainmanage)로 이동합니다. **재생 도메인 이름**을 클릭하거나 오른쪽에서 **관리**를 클릭합니다.
2. **고급 설정** 탭을 선택하고 **HTTP 응답 헤더 구성** 태그로 이동합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/57a34fdc0b51c2f9384a677163c302ff.png)
3. HTTP 응답 헤더 영역에서 **편집**을 클릭하여 새 헤더 필드를 추가하거나 기존 헤더 필드를 수정/삭제합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2fcc14051e1ed41d2896bbcea41c5293.png)
필드를 추가해야 하는 경우 **필드 추가**를 클릭합니다.

  - **옵션 필드**를 클릭하여 사전 설정 필드(`Access-Control-Allow-Methods`, `Access-Control-Max-Age`, `Access-Control-Expose-Headers`)에서 선택하여 구성합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/416416d2cba4a0cff15a016ce987658c.png)
<table>
<thead><tr><th style="width:30%">헤더 필드</th><th>설명</th></tr></thead>
<tbody>
<tr>
<td>Access-Control-Allow-Methods</td>
<td>cross-origin 요청에 허용되는 HTTP 메소드를 나타냅니다. 한 번에 여러 메소드를 지정할 수 있습니다. <br><code>Access-Control-Allow-Methods: POST, GET, OPTIONS</code>.</td>
</tr>
<tr>
<td>Access-Control-Max-Age</td>
<td>실행 전 요청 결과를 캐시할 수 있는 시간(초)을 나타냅니다.
</tr>
<tr>
<td>Access-Control-Expose-Headers</td>
<td>응답의 일부로 클라이언트에 노출될 수 있는 헤더를 나타냅니다.
</tr>
</tbody></table>

  - **사용자 정의 필드**를 클릭하여 필드를 사용자 정의할 수 있습니다.
>! 사용자 정의 필드의 길이는 1자 - 100자이며 알파벳 대소문자, 숫자 및 하이픈(-)으로 구성합니다. 헤더 필드의 값은 1자 - 1000자이며 중국어를 포함할 수 없습니다.

![](https://qcloudimg.tencent-cloud.cn/raw/31ee91ac9ef344cd26ea5c89ed73740e.png)
5. 완료되면 **확인**을 클릭합니다. 구성은 다음 세 가지 상태 중 하나일 수 있습니다: ‘구성 중, 미적용’, ‘구성 실패: 실패 원인’, ‘구성 적용 완료’.
![](https://qcloudimg.tencent-cloud.cn/raw/d8982f6db31f73de86eae641ab82b6ba.png)

