도메인이 CSS에 연결되면 시스템은 자동으로 CNAME 도메인(.liveplay.myqcloud.com 형식이 뒤에 붙음) 이름을 할당합니다.  [도메인 관리]에서 확인 가능합니다. CNAME 도메인은 직접 액세스할 수 없으므로 도메인 서비스 제공 업체에서 CNAME 설정을 완료해야 합니다. 설정이 적용되면 바로 CSS 서비스를 이용할 수 있습니다. 
## 주의 사항
	
재생 도메인 및 푸시 스트리밍 도메인은 모두 CNAME 리졸브를 완료해야 합니다. 

사용자의 도메인 리졸브 서비스 제공 업체 측으로 이동하여 CNAME 기록을 설정합니다. 자세한 작업 방법은 도메인 리졸브 서비스 제공 업체에 문의하십시오.

CNAME 설정은 완료 후 약 15분 후에 적용됩니다. 멀티레이어 CNAME을 설정을 하면 CSS 분석 결과를 효과적으로 모니터링할 수 없으므로 실제 접속 상황을 참조하시기 바랍니다.

CNAME 설정 완료 후 오랜 시간이 지나도 성공 표시가 나타나지 않는 경우 CNAME 설정 문제를 참조하여 점검할 수 있습니다.

## 도메인을 준비하십시오.  
CSS 콘솔에 로그인하여 [도메인 관리](https://console.cloud.tencent.com/live/domainmanage)에서 도메인을 추가하시고, 도메인의 CNAME 주소 상태는 (CNAME 미설정)으로 합니다.


## Tencent Cloud 설정 방법
DNS 서비스 제공 업체가 Tencent Cloud인 경우 다음 단계에 따라 CNAME 기록을 추가 할 수 있습니다.
1. [도메인 서비스 콘솔](https://console.cloud.tencent.com/domain)에 로그인합니다.
2. CNAME을 추가할 도메인을 선택하고 [리졸브]를 클릭합니다.
3. 해당 도메인의 도메인 리졸브 페이지에서 [기록 추가]를 클릭합니다.
4. 신규 열에 도메인 접두사를 호스트 기록으로 작성하고 기록 유형을 CNAME으로 선택한 후 CNAME 도메인을 기록값으로 작성합니다.
	- 기록 유형: `CNAME`을 선택합니다.
	- 호스트 기록: 서브 도메인의 접두사를 작성합니다. 예를 들어 재생 도메인이 play.myqcloud.com인 경우 `play`를 추가하고, 직접 메인 도메인 myqloud.com을 리졸브하는 경우 `@`을 입력합니다. 와일드카드 서브도메인을 리졸브하는 경우에는 `\*`를 입력합니다.
	- 리졸브 경로: "기본" 선택을 권장합니다.
	- 기록값: Tencent Cloud 콘솔의 [Domain Management](https://console.cloud.tencent.com/live/domainmanage)에서 도메인의 해당 CNAME 값을 작성합니다. 포맷은 `domain.livecdn.liveplay.myqcloud.com`입니다.
	- TTL: 10분 입력을 권장합니다.
5. [저장]을 클릭합니다.

6. CNAME 인증이 적용됩니다. CNAME 설정 완료 후 약 15분 후 적용이 완료되며, CSS [도메인 관리](https://console.cloud.tencent.com/live/domainmanage)에 도메인의 해당 CNAME 값에 ![](https://main.qcloudimg.com/raw/bd92cce6703d3703582c0c2a194fd866.png)가 표시되면 CNAME 설정이 완료되었다는 의미입니다. CNAME 설정 완료 후 오랜 시간이 지나도 성공 표시가 나타나지 않는 경우 [CNAME 설정 문제](https://intl.cloud.tencent.com/document/product/267/32478#.E9.85.8D.E7.BD.AE.E5.AE.8C.E6.88.90-cname-.E5.90.8E.EF.BC.8C.E4.BE.9D.E6.97.A7.E6.98.BE.E7.A4.BA-cname-.E6.9C.AA.E9.85.8D.E7.BD.AE.E6.98.AF.E4.BB.80.E4.B9.88.E5.8E.9F.E5.9B.A0.EF.BC.9F)를 참조하여 점검할 수 있습니다.


## Alibaba Cloud 설정 방법
DNS 서비스 제공 업체가 Alibaba Cloud이고 도메인 ICP비안을 완료하였다면 다음 순서를 참고하여 CNAME을 설정할 수 있습니다.

1. Alibaba Cloud 콘솔에 로그인하여 [클라우드 DNS]>[도메인 리졸브](https://dns.console.aliyun.com/#/dns/domainList)로 이동합니다.
2. CNAME을 추가할 도메인을 선택하고 [리졸브 설정]을 클릭합니다.
3. [기록 추가]를 선택하고 기록 추가 페이지에서 다음과 같이 설정합니다.
	- 기록 유형: `CNAME`을 선택합니다.
	- 호스트 기록: 서브 도메인의 접두사를 작성합니다. 예를 들어 재생 도메인이 play.myqcloud.com인 경우 `play`를 추가하고, 직접 메인 도메인 myqloud.com을 리졸브하는 경우 `@`을 입력합니다. 와일드카드 서브도메인을 리졸브하는 경우에는 `\*`를 입력합니다.
	- 리졸브 경로: `기본` 선택을 권장합니다.
	- 기록값: Tencent Cloud 콘솔의 도메인 관리 페이지에서 도메인의 해당 CNAME 값을 작성합니다. 포맷은 `domain.livecdn.liveplay.myqcloud.com`입니다.
	- TTL: `10분 입력`을 권장합니다.
4. [확인]을 클릭합니다.

4. CNAME 인증이 적용됩니다. CNAME 설정 완료 후 약 15분 후 적용이 완료되며, CSS [도메인 관리](https://console.cloud.tencent.com/live/domainmanage)에 도메인의 해당 CNAME 값에 ![](https://main.qcloudimg.com/raw/ca12667bfcfd9716639c27d51f3beed3.png)가 표시되면 CNAME 설정이 완료되었다는 의미입니다. CNAME 설정 완료 후 오랜 시간이 지나도 성공 표시가 나타나지 않는 경우 [CNAME 설정 문제](https://intl.cloud.tencent.com/document/product/267/32478#.E9.85.8D.E7.BD.AE.E5.AE.8C.E6.88.90-cname-.E5.90.8E.EF.BC.8C.E4.BE.9D.E6.97.A7.E6.98.BE.E7.A4.BA-cname-.E6.9C.AA.E9.85.8D.E7.BD.AE.E6.98.AF.E4.BB.80.E4.B9.88.E5.8E.9F.E5.9B.A0.EF.BC.9F)를 참조하여 점검할 수 있습니다.

>본 문서는 Alibaba Cloud의 2019년 10월 31일 버전을 기반으로 설명하였습니다. Alibaba Cloud 콘솔이 업데이트되어도, 본 문서는 일시적으로 업데이트되지 않을 수 있으며 설명 순서에 따라 자체적으로 조정하시기 바랍니다. 설정에 실패하는 경우 [고객 서비스](https://intl.cloud.tencent.com/support)로 문의해 주십시오.

## Baidu Cloud 설정 방법
도메인 서비스 제공 업체가 Baidu Cloud이고 도메인 ICP비안을 완료하였다면 다음 순서를 참고하여 CNAME을 설정할 수 있습니다.
1. Baidu Cloud 콘솔에 로그인하고 [도메인 관리](https://console.bce.baidu.com/bcd/?_=1550137564099#/bcd/manage/list)를 선택하여 도메인 관리 리스트 페이지로 이동합니다.
2. CSS에 추가한 도메인을 선택하고 작업 열에서 [리졸브]를 클릭해 DNS 리졸브 페이지로 이동합니다.
3. 해당 페이지에서 다음과 같이 설정하여 리졸브 기록을 추가합니다.
 - 호스트 기록: 서브 도메인, 즉 접두사를 작성합니다. 예를 들어 재생 도메인이 play.myqcloud.com인 경우`play`를 추가하고, 직접 메인 도메인 myqloud.com을 리졸브하는 경우 `@`을 입력합니다. 와일드카드 서브도메인을 리졸브하는 경우에는 `\*`를 입력합니다.
 - 기록 유형: `CNAME 기록`을 선택합니다.
 - 리졸브 경로: `기본` 선택을 권장합니다.
 - 기록값: CSS 콘솔의 도메인 관리 페이지에서 도메인의 해당 CNAME 값을 작성합니다. 포맷은 `domain.livecdn.liveplay.myqcloud.com`입니다.
 - TTL: `10분` 입력을 권장합니다.
4. [확인]을 클릭하여 제출합니다.

5. CNAME 인증이 적용됩니다. CNAME 설정 완료 후 약 15분 후 적용이 완료되며, CSS 도메인 관리에 도메인의 해당 CNAME 값에 ![](https://main.qcloudimg.com/raw/bd92cce6703d3703582c0c2a194fd866.png)가 표시되면 CNAME 설정이 완료되었다는 의미입니다. CNAME 설정 완료 후 오랜 시간이 지나도 성공 표시가 나타나지 않는 경우 [CNAME 설정 문제](https://intl.cloud.tencent.com/document/product/267/32478#.E9.85.8D.E7.BD.AE.E5.AE.8C.E6.88.90-cname-.E5.90.8E.EF.BC.8C.E4.BE.9D.E6.97.A7.E6.98.BE.E7.A4.BA-cname-.E6.9C.AA.E9.85.8D.E7.BD.AE.E6.98.AF.E4.BB.80.E4.B9.88.E5.8E.9F.E5.9B.A0.EF.BC.9F)를 참조하여 점검할 수 있습니다.

>본 문서는 Baidu Cloud의 2019년 3월 01일 버전을 기반으로 설명하였습니다. Baidu Cloud 콘솔이 업데이트되어도, 본 문서는 일시적으로 업데이트되지 않을 수 있으며 설명 순서에 따라 자체적으로 조정하시기 바랍니다. 설정에 실패하는 경우 [고객 서비스](https://intl.cloud.tencent.com/support)로 문의해 주십시오.

## DNSPod 설정 방법
DNS 서비스 제공 업체가 DNSPod인 경우 다음 순서에 따라 CNAME 기록을 추가할 수 있습니다.


## www.net.cn 설정 방법
DNS 서비스 제공 업체가 www.net.cn인 경우 아래 순서에 따라 CNAME 기록을 추가할 수 있습니다.



## Sina 설정 방법
DNS 서비스 제공 업체가 Sina인 경우 아래 순서에 따라 CNAME 기록을 추가할 수 있습니다.


## CNAME 인증 유효성 확인
CNAME 적용 시간은 각 DNS 서비스 제공 업체별로 상이하며 일반적으로 30분내에 적용됩니다. 명령 라인에서 dig 또는 nslookup 명령어를 통해 CNAME 적용 여부를 확인할 수 있으며 뒤에 .myqcloud.com이 붙은 도메인이 표시되면 CNAME이 적용 완료되었다는 의미입니다.

