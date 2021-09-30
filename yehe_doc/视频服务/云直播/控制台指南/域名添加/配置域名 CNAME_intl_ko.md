CSS에 도메인 연결 후, 시스템에서 CNAME 도메인(`.liveplay.myqcloud.com`을 접미사로 함)을 자동으로 할당하며 [[도메인 이름 관리](https://console.cloud.tencent.com/live/domainmanage)]리스트에서 조회할 수 있습니다. CNAME 도메인은 직접 액세스할 수 없으며, 도메인 서비스 제공 업체 측에서 CNAME 설정을 완료하고 관련 설정이 적용되면 CSS 서비스를 즐기실 수 있습니다.

다음 비디오는 Tencent Cloud에서의 도메인 CNAME 리졸브 설정 방법을 소개합니다.



주의 사항

- 푸시 스트리밍 도메인과 재생 도메인은 모두 CNAME 리졸브를 완료해야 합니다. 
- 사용자의 도메인 리졸브 서비스 제공 업체 측으로 이동하여 CNAME 레코드를 설정합니다. 자세한 작업 방법은 도메인 리졸브 서비스 제공 업체에 문의하십시오.
- CNAME 설정 완료 후 약 15분이 지나면 적용됩니다. 멀티 레이어 CNAME 을 설정한 경우 CSS에서 효과적으로 리졸브 결과를 모니터링할 수 없습니다. 실제 액세스 상황을 참고하십시오.
- CNAME 설정 완료 후 오랫동안 완료 메세지가 뜨지 않으면 [도메일 설정 관련](https://intl.cloud.tencent.com/document/product/267/32478)을 참고하십시오.

## 전제 조건
- [도메인 등록](https://console.cloud.tencent.com)에서 도메인 회원가입 및 ICP 비안 완료. 
- CSS 콘솔의 [[도메인 이름 관리](https://console.cloud.tencent.com/live/domainmanage)]에서 [자체 도메인 추가](https://intl.cloud.tencent.com/document/product/267/35970)를 완료했고, 도메인 CNAME 주소 상태가 ![](https://main.qcloudimg.com/raw/ed1ac2f8541f629814a3f2420b1eb79c.png)(CNAME 미설정)임.



## 설정 단계
본 문서는 Tencent Cloud, Alibaba Cloud, Baidu Cloud, DNSPod, www.net.cn, Sina에서 CNAME 도메인 리졸브를 설정하는 것을 예로 들어 설명합니다. 작업 단계는 참고용으로 실제 설정에 부합하지 않는다면 본인이 사용하는 DNS 서비스 업체 정보를 기준으로 하시기 바랍니다. 도메인 CNAME 설정 완료 후, [CNAME 유효성 인증](#check)에서 설명하는 방법에 따라 도메인에 CNAME 설정이 완료되었는지 확인할 수 있습니다.


[](id:tencent)
### Tencent Cloud 설정 방법
DNS 서비스 제공 업체가 Tencent Cloud인 경우 다음 단계에 따라 CNAME 레코드를 추가 할 수 있습니다.

1. [도메인 서비스 콘솔](https://console.cloud.tencent.com/domain)에 로그인합니다.
2. CNAME을 추가할 도메인을 선택하고 [리졸브]를 클릭합니다.
3. 해당 도메인의 도메인 리졸브 페이지에서 [레코드 추가]를 클릭합니다.
4. 신규 열에 도메인 CNAME 레코드를 입력합니다. 구체적인 입력 내용은 다음과 같습니다. 
<table>
    <tr><th width="12%" >매개변수 이름</th><th width="38%">매개변수 설명</th><th width="50%">설정 방법</th></tr>
    <tr>
    <td>호스트 레코드</td>
        <td>서브 도메인의 접두사 입력  </td>
        <td>
            <ul style="margin-bottom:0;">
                <li>도메인이<code>play.myqcloud.com</code>인 경우, <code>play</code></li>를 선택하십시오.
                <li>메인 도메인<code>myqloud.com</code>을 리졸브하는 경우, :<code>@</code></li>를 선택하십시오.
                <li>와일드카드 서브도메인을 리졸브하는 경우, :<code>\*</code></li>을 선택하십시오.
            </ul>
        </td>
    </tr>
    <tr>
    <td>레코드 유형</td>
        <td>레코드 유형, 여기에서는 CNAME 유형</td>
        <td>도메인을 다른 도메인으로 지정하는 경우, :<b>CNAME</b></td>을 선택하십시오.
    </tr>
    <tr>
        <td>회선 유형</td>
        <td>DNS 서버가 도메인을 리졸브할 때 사용되며, 방문자 출처에 따라, 해당 서버 IP 주소를 반환합니다.</td>
        <td>선택: <b>기본 설정:</b></td>
    </tr>
    <tr>
        <td>레코드값</td>
        <td>지정할 도메인. Tencent Cloud 콘솔 [<a href="https://console.cloud.tencent.com/live/domainmanage">도메인 이름 관리</a>] 도메인에 상응하는 CNAME 값을 입력합니다.</td>
        <td>[<a href="https://console.cloud.tencent.com/live/domainmanage">도메인 이름 관리</a>]에서 해당 도메인이 할당한 미설정 CNAME을 조회하고 복사하여 [레코드값]에 입력합니다. 입력 형식:<ul style="margin:0">
				<li/><code><b style="color:red;">xxxx</b>.tlivecdn.com</code>
				<li/><code><b style="color:red;">xxxx</b>.tlivepush.com</code>
				</ul></td>
    </tr>
    <tr>
        <td>TTL(초)</td>
        <td>캐시의 유효 시간. 기본적으로는 가장 많이 사용하는<b>600초</b></td>
        <td><b>600초</b>입력 권장</td>
    </tr>
</table>
5. [저장]을 클릭하여, CNAME 설정 완료합니다.

>! 
>- 도메인 리졸브 레코드 관련 자세한 내용은 호스트 레코드와 레코드값을 참고하십시오.
>- 도메인 리졸브의 각 레코드 유형 간에는 우선순위의 차이가 있으므로 호스트 레코드가 동일한 경우 같은 회선에 서로 다른 레코드 유형이 공존할 수 없으며, 이 같은 상황 발생 시 충돌 메세지가 뜹니다. CNAME 레코드는 다른 모든 레코드 유형과 충돌하므로 설정하기 전에 먼저 다른 레코드를 삭제해야 합니다. 자세한 내용은 ‘리졸브 레코드 추가 시 ‘레코드 충돌’ 메세지가 뜨는 이유는 무엇입니까?’를 참고하시기 바랍니다. 

[](id:ali)

### Alibaba Cloud 설정 방법
DNS 서비스 제공 업체가 Alibaba Cloud이고 도메인 ICP비안을 완료하였다면 다음 단계를 참고하여 CNAME을 설정할 수 있습니다.

1 . Alibaba Cloud 콘솔에 로그인하여 [클라우드 DNS]>[도메인 리졸브](https://dns.console.aliyun.com/#/dns/domainList)로 이동합니다.
2. CNAME을 추가할 도메인을 선택하고 [리졸브 설정]을 클릭합니다.
3. [레코드 추가]를 선택하고 레코드 추가 페이지에 다음과 같이 설정합니다.
  -  레코드 유형: `CNAME`을 선택합니다.
  -  호스트 레코드: 서브 도메인의 접두사를 작성합니다. 예를 들어 재생 도메인이 ‘play.myqcloud.com’인 경우 `play`를 추가하고, 직접 메인 도메인 ‘myqloud.com’을 리졸브하는 경우 `@`을 입력합니다. 와일드카드 서브도메인을 리졸브하는 경우에는 `\*`을 입력합니다.
  -  리졸브 경로: `기본 설정` 선택을 권장합니다.
  -  레코드값: Tencent Cloud 콘솔의 도메인 이름 관리 페이지에서 도메인의 해당 CNAME 값을 입력합니다. 형식은 `domain.livecdn.liveplay.myqcloud.com`입니다.
  -  TTL: `10분` 입력을 권장합니다.
4. [확인]을 클릭합니다.


[](id:baidu)
### Baidu Cloud 설정 방법
도메인 서비스 제공 업체가 Baidu Cloud인 경우 다음 단계에 따라 CNAME 레코드를 추가 할 수 있습니다.
1. Baidu Cloud 콘솔에 로그인하고 [도메인 이름 관리](https://console.bce.baidu.com/bcd/?_=1550137564099#/bcd/manage/list)를 선택하여 도메인 관리 리스트 페이지로 이동합니다.
2. CSS에 추가한 도메인을 선택하고 작업 열에서 [리졸브]를 클릭해 DNS 리졸브 페이지로 이동합니다.
3. 해당 페이지에서 다음과 같이 설정하여 리졸브 레코드를 추가합니다.
 - 호스트 레코드: 서브 도메인, 즉 접두사를 작성합니다. 예를 들어 재생 도메인이 ‘play.myqcloud.com’인 경우`play`를 추가하고, 직접 메인 도메인 ‘myqloud.com’을 리졸브하는 경우 `@`을 입력합니다. 와일드카드 서브도메인을 리졸브하는 경우에는 `\*`을 입력합니다.
 - 레코드 유형: `CNAME 레코드`를 선택합니다.
 - 리졸브 경로: `기본 설정` 선택을 권장합니다.
 - 레코드값: CSS 콘솔의 도메인 이름 관리 페이지에서 도메인의 해당 CNAME 값을 작성합니다. 형식은 `domain.livecdn.liveplay.myqcloud.com`입니다.
 - TTL: `10분` 입력을 권장합니다.
4. [확인]을 클릭하여 제출합니다.

[](id:dnspod)
### DNSPod 설정 방법
DNS 서비스 제공 업체가 DNSPod인 경우 다음 단계에 따라 CNAME 레코드를 추가할 수 있습니다.
1. [DNSPod 도메인 서비스 콘솔](https://console.dnspod.cn/dns/list)에 로그인합니다. 
2. 리스트에서 CNAME 레코드를 추가할 도메인이 속한 열을 확인하고 해당 도메인 이름을 클릭하여 ‘레코드 추가 ’인터페이스로 이동합니다.
3. 다음 단계를 통해 CNAME 레코드를 추가할 수 있습니다. 
  1. 호스트 레코드에 서브 도메인을 입력합니다. 예를 들어 `www.123.com`의 리졸브를 추가해야 할 경우 호스트 레코드에 'www'만 입력하면 됩니다. `123.com`의 리졸브만 추가하려는 경우 호스트 레코드를 공백으로 남겨두면 시스템이 입력창에 "@"를 자동으로 입력합니다. @의 CNAME은 MX 레코드의 정상적인 리졸브에 영향을 주므로 신중하게 추가하십시오.
  2. 레코드 유형은 CNAME입니다.
  3. 회선 유형(필수 항목으로, 설정하지 않을 경우 일부 사용자가 리졸브할 수 없게 됩니다. 위 이미지에서 기본적으로 China Unicom 사용자를 제외한 모든 사용자가 1.com을 사용합니다.)
  4. 레코드 값은 CNAME이 가리키는 도메인 이름입니다. 도메인 이름만 입력할 수 있습니다. 레코드가 생성된 후 도메인 이름 뒤에 ‘.’가 자동으로 추가됩니다.
  5. MX 우선 순위는 작성할 필요가 없습니다.
  9. TTL을 입력할 필요는 없습니다. 추가할 때, 시스템에서 자동으로 생성되며 기본값은 600초입니다(TTL은 캐시 시간으로 값이 작을수록 레코드 변경이 더 빨리 적용됨).


[](id:wwwnet)
### www.net.cn 설정 방법
DNS 서비스 제공 업체가 www.net.cn인 경우 아래 단계에 따라 CNAME 레코드를 추가할 수 있습니다.

1. www.net.cn에 로그인하십시오.
2. 회원 사이트의 왼쪽 메뉴에서 [제품 관리]->[나의 클라우드 리졸브]를 클릭하여 World Wide Web Cloud 리졸브 리스트 페이지로 이동합니다.
3. 리졸브하려는 도메인을 클릭하고 리졸브 레코드 페이지로 이동하십시오.
4. 리졸브 레코드 페이지로 이동한 후 [리졸브 추가]를 클릭하여 리졸브 레코드 설정을 시작하십시오.
5. CNAME 리졸브 레코드를 설정하려면 레코드 유형을 CNAME으로 선택하십시오. 호스트 기록은 도메인 이름의 접두사이며 임의로 입력할 수 있습니다(예 :`www`). 레코드 값은 현재 도메인이 아닌 다른 도메인으로 채워집니다. 리졸브 회선은 TTL 기본값이면 됩니다.
6. 모두 입력 후 [저장]을 클릭하여 리졸브 설정을 완료하십시오.


[](id:xinnet)
### Sina 네트워크 설정 방법
DNS 서비스 제공 업체가 Sina인 경우, **별명(CNAME 레코드) 설정**을 통해 CNAME 레코드를 추가할 수 있습니다. 
별명 레코드를 통해 여러 이름을 동일한 컴퓨터에 매핑할 수 있습니다. 일반적으로 WWW와 MAIL 서비스를 모두 제공하는 컴퓨터에 사용됩니다. 예를 들어`host.mydomain.com` (A 레코드)이라는 컴퓨터는 사용자가 서비스에 액세스할 수 있도록 WWW 및 MAIL 서비스를 동시에 제공하는 경우, 해당 컴퓨터에 WWW와 MAIL의 두 개의 별칭(CNAME)을 설정할 수 있습니다. 다음 이미지를 참고하십시오.

[](id:check)
## CNAME 인증 유효성 확인
DNS 서비스 제공 업체에 따라 CNAME 적용 시간이 조금씩 다르며, 일반적으로 30분 내에 적용됩니다. 다음 방법을 통해 CNAME이 적용되었는지 확인할 수 있습니다.
- **방법1: **CSS 콘솔의 [[도메인 이름 관리](https://console.cloud.tencent.com/live/domainmanage)]로 이동하여 조회 결과 접미사가`.myqcloud.com`인 도메인의 상태 부호가 ![](https://main.qcloudimg.com/raw/0fc346399ae095d69113d4944e511a20.png)로 변경되었다면 CNAME 적용이 완료된 것입니다. 
![](https://main.qcloudimg.com/raw/7930331f6eb7f4271014083cab27fb26.png)
- **방법2: **Linux/Mac 시스템에서 dig 명령어를 통해 확인. 명령 형식: `dig` 외부 도메인. 첫 번째 열에 CSS가 제공한 타깃 도메인으로 리졸브되었다고 표시된다면 CNAME 적용이 완료된 것입니다. 
![](https://main.qcloudimg.com/raw/49aa30e1edc3884c2ae93ec5fdeeb1fb.png)
- **방법3: **Windows 시스템은 [시작]→[실행]→cmd 입력과 엔터키를 통해, 명령 라인 모드에서:`nslookup 외부 도메인`을 입력합니다. CSS가 제공하는 타깃 도메인으로 리졸브되었다면 CNAME 적용이 완료된 것입니다.
![](https://main.qcloudimg.com/raw/8bad41428852a7c32111933b33e8853c.png)


>! CNAME 설정 완료 후 오랫동안 완료 메세지가 뜨지 않으면 [도메일 설정 관련](https://intl.cloud.tencent.com/document/product/267/32478)을 참고하십시오.
