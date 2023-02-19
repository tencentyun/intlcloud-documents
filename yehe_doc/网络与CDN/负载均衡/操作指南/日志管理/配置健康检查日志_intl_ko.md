CLB는 상태 확인 로그를 CLS에 저장하여 로그를 보고, 분 단위로 리포트하고, 여러 규칙에 따라 온라인으로 쿼리하여 상태 확인 실패의 원인을 진단할 수 있도록 지원합니다.

<dx-alert infotype="explain" title="">
상태 확인 로그는 현재 베타 사용자가 사용할 수 있습니다. 이 서비스를 이용하시려면 [티켓 제출](https://console.tencentcloud.com/workorder/category)하십시오.
</dx-alert>

상태 확인 로그에는 로그 리포트, 저장 및 쿼리가 포함됩니다.
- 로그 리포트: 서비스 포워딩을 먼저 처리한 후 로그 보고를 처리합니다.
- 로그 스토리지 및 쿼리: 현재 사용 중인 스토리지 서비스를 기반으로 SLA 지원을 제공합니다.

## 제한 설명
- CLB 레이어 4 및 레이어 7 프로토콜은 상태 확인 로그를 CLS에 저장하는 데 사용할 수 있습니다.
- CLB 상태 확인 로그를 CLS에 저장하는 것은 무료입니다. CLS 서비스에 대한 요금만 지불하면 됩니다.
- 이 기능은 애플리케이션 CLB에서만 사용할 수 있습니다.
- IPv4 및 IPv6 NAT64 CLB 인스턴스만 이 기능이 지원됩니다.
- 이 기능은 CLS 사용 가능 리전에서만 지원됩니다. 사용 가능한 리전을 참고하십시오.


## 1단계: 역할 권한 추가[](id:step1)
역할 권한을 추가하려면 CLS 서비스를 활성화했는지 확인하십시오.
1. [CLB 콘솔](https://console.cloud.tencent.com/clb)에 로그인하고 왼쪽 사이드바에서 **상태 확인 로그**를 선택합니다.
2. ‘상태 확인 로그’ 페이지에서 **지금 활성화**를 클릭합니다. 팝업 창에서 **인증 및 활성화**를 클릭합니다.
<img src="" width="50%"/>
3. [CAM 콘솔](https://console.cloud.tencent.com/cam/role)에서 ‘역할 관리’ 페이지로 이동하고 **권한 부여 동의**를 클릭하십시오.

## 2단계: 로그셋 및 로그 테마 생성[](id:step2)
상태 확인 로그를 CLS에 저장하려면 먼저 로그셋 및 로그 테마를 생성해야 합니다.
로그셋 및 로그 테마를 생성한 경우 [3단계](#step3)로 바로 이동할 수 있습니다.
1. [CLB 콘솔](https://console.cloud.tencent.com/clb)에 로그인하고 왼쪽 사이드바에서 **상태 확인 로그**를 선택합니다.
2. **상태 확인 로그** 페이지에서 로그셋에 대한 리전을 선택한 다음 **로그셋 정보** 섹션에서 **로그셋 생성**을 클릭합니다.
3. **로그셋 생성** 팝업 창에서 저장 기간을 설정하고 **저장**을 클릭합니다.
4. **상태 확인 로그** 페이지의 **로그 테마** 섹션에서 **로그 테마 생성**을 클릭합니다.
5. **로그 테마 추가** 팝업 창에서 스토리지 유형 및 로그 저장 시간을 선택한 후, 오른쪽 목록에 추가할 CLB 인스턴스를 선택하고 **저장**을 클릭합니다.
>?
>- 스토리지 유형은 STANDARD, STANDARD_IA로 구분됩니다. 자세한 내용은 [Storage Class Overview](https://www.tencentcloud.com/document/product/614/42003)를 참고하십시오.
>- 로그는 영구적으로 또는 지정된 기간 동안 보관할 수 있습니다.
>- 로그 테마를 생성할 때 필요에 따라 CLB 인스턴스를 추가할 수 있습니다. 추가하려면 목록에서 로그 테마를 선택하고 **작업** 열에서 **관리**를 클릭합니다. 각 CLB 인스턴스는 하나의 로그 테마에만 추가할 수 있습니다.
>- 로그셋에는 여러 로그 테마(Topic)가 포함될 수 있습니다. CLB 로그를 ‘CLB’로 표시되는 다양한 로그 테마로 분류할 수 있습니다.
>
![]()
6. (옵션) 상태 확인 로그를 비활성화하려면 로그 테마 우측의 **작업** 열에서 **중지**를 클릭하기만 하면 됩니다.


## 3단계: 상태 확인 로그 보기[](id:step3)
수동 구성 없이 CLB는 상태 확인 로그 값으로 인덱스 검색으로 자동 구성되었습니다. 검색 및 분석을 통해 상태 확인 로그를 직접 쿼리할 수 있습니다.
1. [CLB 콘솔](https://console.cloud.tencent.com/clb)에 로그인하고 왼쪽 사이드바에서 **상태 확인 로그**를 선택합니다.
2. ‘상태 확인 로그’ 페이지에서 보려는 로그셋의 리전을 선택합니다. ‘로그 테마’ 섹션에서 선택한 로그 테마의 오른쪽의 ‘작업’ 열에서 **검색**을 클릭하여 [CLS 콘솔](https://console.cloud.tencent.com/cls/search)로 이동합니다.
3. CLS 콘솔에서 왼쪽 사이드바의 **검색 분석**을 클릭합니다.
4. **검색 분석** 페이지에서 입력 상자에 검색 구문을 입력하고 시간 범위를 선택한 다음 **검색 분석**을 클릭하여 CLB에서 CLS에 리포트한 상태 확인 로그를 검색합니다.
>?검색 구문에 대한 자세한 내용은 [Overview and Syntax Rules](https://intl.cloud.tencent.com/document/product/614/37803)를 참고하십시오.
>


## 상태 확인 로그 형식 및 변수
### 로그 형식
```	
[$protocol][$rsport][$rs_vpcid][$vport][$vpcid][$time][$vip][$rsip][$status][$domain][$url]
```

### 로그 변수 설명
<table class="table"><thead><tr><th>변수 이름</th><th>설명</th><th>필드 유형</th></tr></thead>
<tbody>
<tr><td>protocol</td><td> 프로토콜 유형(HTTP/HTTPS/SPDY/HTTP2/WS/WSS).</td><td>text</td></tr>
<tr><td>rsport</td><td>RS 포트.</td><td>long</td></tr>
<tr><td>rs_vpcid</td><td>RS의 VPC ID 공중망 CLB 인스턴스의 vip_vpcid는 -1입니다.</td><td>long</td></tr>
<tr><td>vport</td><td>CLB VPort, 즉 수신 포트입니다.</td><td>long</td></tr>
<tr><td>vpcid</td><td>CLB VIP의 VPC ID. 공중망 CLB 인스턴스의 vip_vpcid는 -1입니다.</td><td>long</td></tr>
<tr><td>time</td><td> 액세스 시간 및 시간대(예시: ‘01/Jul/2019:11:11:00 +0800’) 여기서 ‘+0800’은 UTC+8, 즉 베이징 시간을 나타냅니다.</td><td>text</td></tr>
<tr><td>vip</td><td>CLB VIP.</td><td>text</td></tr>
<tr><td>rsip</td><td>RS IP.</td><td>text</td></tr>
<tr><td>status</td><td>상태 확인 상태: <ul><li>true: 정상</li><li>false: 비정상</li></ul></td><td>text</td></tr>
<tr><td>domain</td><td>상태 확인할 도메인 이름입니다. 레이어 4 리스너가 사용되는 경우 이 매개변수는 비어 있습니다.</td><td>text</td></tr>
<tr><td>url</td><td>상태 확인할 URL입니다. 레이어 4 리스너가 사용되는 경우 이 매개변수는 비어 있습니다.</td><td>text</td></tr>
</tbody></table>

## 관련 문서
[Getting Started in Five Minutes](https://intl.cloud.tencent.com/document/product/614/31592)
