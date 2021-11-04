[](id:Q1)
### IM과 TPNS를 동시에 통합한 후 많은 벤더 충돌이 발생합니다. 어떻게 해야 하나요?
현재 IM은 [TPNS](https://intl.cloud.tencent.com/product/tpns)에서 제공하는 벤더 jar 패키지를 사용합니다. [IM 오프라인 푸시(Android)](https://intl.cloud.tencent.com/document/product/1047/39156) 문서를 참고하여 관련 종속성 패키지를 교체하면 이 문제를 해결할 수 있습니다.

[](id:Q2)
### 메시지 미수신 또는 메시지 손실 시 어떻게 해결합니까?

-  1:1 채팅 메시지
 - 메시지가 성공적으로 발송되었는지 확인합니다.
 - 수신자가 성공적으로 로그인했는지 확인합니다.
 - 메시지를 보낸 대화가 수신자의 대화와 일치하는지 확인합니다. 
- 그룹 메시지
 - 메시지가 성공적으로 발송되었는지 확인합니다.
 - 수신자가 성공적으로 로그인했는지 확인합니다.
 - 수신자가 그룹 구성원인지 확인합니다.

C2C 메시지 또는 그룹 메시지 모두 상기 방법으로 문제를 확인할 수 없는 경우, 다음 내용을 확인하십시오.
1. 메시지 리스너가 등록되었는지 확인합니다.
2. 발신자가 메시지를 보낼 때 메시지에 ‘elem’을 추가했는지 확인합니다(메시지를 보낼 때 ‘addElement’의 반환 값 확인). 
3. Android 사용자의 경우 여러 메시지 리스너 등록 여부 및 메시지 리스너에 ‘true’ 반환 여부를 확인합니다.


[](id:Q3)
### 오프라인 푸시 수신 실패 시 어떻게 해야 합니까?

- APNs
[오프라인 푸시 설정(iOS)](https://intl.cloud.tencent.com/zh/document/product/1047/34347) 설명 문서를 참고하여 다음을 확인합니다.
 - Tencent Cloud 콘솔에 올바른 인증서가 업로드되었는지 확인합니다.
 - 로그인 성공 후 token이 Tencent Cloud에 성공적으로 업로드되었는지 확인합니다.
 - token을 리포트 시 올바른 인증서 ID가 리포트되는지 확인합니다.
 - 포그라운드/백그라운드 전환 이벤트가 올바르게 리포트되는지 확인합니다.
 - 메시지에 ‘TIMCustomElem’만 포함되어 있고 ‘desc’ 속성은 비어 있지 않은지 확인합니다.
 - ‘MsgRandom’과 같은 중복 제거 식별자가 동일한 값으로 설정되어 중복 제거로 인한 푸시 실패가 발생하지 않았는지 확인합니다.
 - 그룹 메시지의 경우 메시지 알림 음소거가 활성화되어있는지 확인합니다.

- Android
[오프라인 푸시](https://intl.cloud.tencent.com/document/product/1047/34336) 설명 문서를 참고하여 다음을 확인합니다.
 - 올바른 푸시 인증서가 업로드되었는지 확인합니다.
 - token이 성공적으로 리포트되었는지 확인합니다.
 - 서드 파티 오프라인 푸시(Huawei, Xiaomi, Meizu)를 사용하지 않은 경우, QALService 프로세스가 활성화 상태인지 확인하십시오. 프로세스가 활성화되어 있지 않으면 오프라인 푸시를 수신할 수 없습니다. 이 경우 시스템의 자동 시작 권한이 필요합니다.
 - 다중 프로세스의 경우 IM SDK 초기화가 메인 프로세스에서만 수행되었는지 확인하십시오. 그렇지 않은 경우, IM SDK 초기화가 메인 프로세스에서만 수행되도록 구성을 수정해야 합니다.
 - 서드 파티 오프라인 푸시(Xiaomi, Huawei, Meizu 등)를 사용할 때 먼저 해당 서드 파티 콘솔을 통해 메시지를 직접 푸시하여 휴대폰의 메시지 수신 가능 여부를 확인할 수 있습니다. 휴대폰이 수신할 수 없는 경우, 가능한 원인은 다음 2가지가 있습니다.
    1) 사용자의 서드 파티 오프라인 푸시 통합 오류. 이 경우 관련 문서를 참고하십시오.
    2) 휴대폰 오프라인 푸시 호환성 문제. 예를 들어, 일부 Huawei 휴대폰은 Huawei의 오프라인 푸시를 수신할 수 없습니다.
 - OPPO 오프라인 푸시의 경우, IM 콘솔의 Android 푸시 인증서에 AppSecret 대신 MasterSecret을 입력해야 합니다.

APNs 푸시 또는 Android 오프라인 푸시를 사용할 때, 상기 방법을 통해 문제를 찾을 수 없는 경우, 다음의 경우를 확인하십시오.
1. 받는 사람 ID가 메시지 푸시 대상자 ID와 일치하는지 확인합니다.
2. 오프라인 푸시 리스너(Android)를 활성화했는지 확인합니다.
3. 방해 금지를 설정했는지 확인합니다. iOS는 [사용자 정의 푸시 알림음 설정](https://intl.cloud.tencent.com/zh/document/product/1047/34347)을, Android는 [전역 오프라인 푸시 구성 설정](https://intl.cloud.tencent.com/document/product/1047/34336#.E8.AE.BE.E7.BD.AE.E5.85.A8.E5.B1.80.E7.A6.BB.E7.BA.BF.E6.8E.A8.E9.80.81.E9.85.8D.E7.BD.AE)을 참고하시기 바랍니다.
4. 메시지가 ‘sendOnlineMessage’ API를 통해 전송된 온라인 메시지인지, 또는 REST API를 통해 푸시할 때 ‘MsgLifeTime’이 ‘0’으로 설정되었는지 확인합니다.
5. 메시지에 오프라인 푸시 하지 않음 식별자가 설정되었는지 확인합니다. iOS는 [사용자 정의 오프라인 메시지 속성](https://intl.cloud.tencent.com/zh/document/product/1047/34347)을, Android는 [단일 메시지의 오프라인 푸시 구성 설정](https://intl.cloud.tencent.com/document/product/1047/34336#.E9.92.88.E5.AF.B9.E5.8D.95.E6.9D.A1.E6.B6.88.E6.81.AF.E8.AE.BE.E7.BD.AE.E7.A6.BB.E7.BA.BF.E6.8E.A8.E9.80.81)을 참고하시기 바랍니다.
6. 여전히 문제를 진단할 수 없으면, 기술 지원 담당자에게 관련 정보를 제공하여 해결할 수 있습니다.

[](id:Q4)
### 그룹 @ 메시지는 어떻게 처리되나요?
그룹 내의 @메시지와 일반 메시지는 본질적인 차이는 없으며, 다만 @대상자가 메시지를 받았을 때 UI에서 특별 처리됩니다. 예를 들어, QQ 메시지 목록에서 빨간색으로 강조 표시됩니다. 다음을 참고하여 구현할 수 있습니다.
1. 메시지를 보낼 때 키보드 이벤트를 수신하여 @ 텍스트가 입력되었는지 감지합니다. 입력이 감지되면 발신자의 UI에 그룹 구성원 목록이 팝업되어, 발신자가 @ 대상자를 선택할 수 있도록 합니다. 선택된 사용자가 user1이라고 가정합니다.
2. @ 대상자를 선택한 후, 메시지 입력 상자에 @와 선택한 사용자의 ID(예: “@user1”)를 추가합니다.
3. 메시지에 ‘TIMCustomElem’을 추가하고 ‘TIMCustomElem’에 사용자 지정 메시지 프로토콜을 추가하여, 메시지를 @ 메시지로 표시합니다.
간단한 프로토콜 정의는 다음과 같습니다.
```
{
	“type”:“REMIND”,
	“target”:“user1”
}
```
@ 메시지를 구성하는 샘플 코드는 다음과 같습니다(Android 플랫폼):

```java
// 텍스트 메시지를 보내고, user1을 @ 대상자로 지정합니다.
TIMMessage msg = new TIMMessage();
// 텍스트 메시지 요소를 구성합니다.
TIMTextElem txtElem = new TIMTextElem();
txtElem.setText(“@user1 nice to meet u”);
if(msg.addElement(txtElem) != 0){
	Log.e(TAG, “add text elem failed”);
	return;
}
try{
	// 사용자 정의 메시지 프로토콜 지정
	JSONObject remindProto = new JSONObject();
	remindProto.put(“type”, “REMIND”);
	remindProto.put(“target”, “user1”);
	// 사용자 정의 프로토콜을 기반으로 사용자 정의 메시지 요소 구성
	TIMCustomElem customElem = new TIMCustomElem();
	customElem.setDesc(“remind msg”);
	customElem.setData(remindProto.toString().getBytes(“utf-8”));
	if(msg.addElement(customElem) != 0){
		Log.e(TAG, “add custom elem failed”);
		return;
	}
}catch(Exception e){
	Log.e(TAG, “build custom elem failed”);
	return;
}
```

>!이 중, ‘TIMTextEle’은 필수 사항이 아닙니다. 비속어 필터링이 필요 없는 경우, ‘TIMTextElem’의 메시지 내용을 ‘TIMCustomElem’의 ‘desc’ 속성에 입력할 수 있습니다.
>
4. 메시지 구성 완료 후, 그룹에 메시지를 보냅니다.
5. 그룹 구성원이 메시지를 수신한 후 ‘TIMCustomElem’의 메시지 프로토콜이 @ 메시지 프로토콜인지 확인합니다. 그렇다면 다음 단계로 이동하고 그렇지 않으면 건너뜁니다.
6. @ 대상자가 현재 로그인한 사용자와 일치하는지 확인합니다. 그렇다면 UI에서 특수 처리를 수행하고 그렇지 않으면 처리가 필요하지 않습니다.

[](id:Q5)
### 홍바오 메시지는 어떻게 처리됩니까?

홍바오 메시지는 @ 메시지와 유사하며 ‘TIMCustomElem’을 통해 구현할 수 있습니다. 홍바오 메시지는 앱이 UI에서 특수 처리를 수행해야 합니다. 예를 들어, 시스템이 현재 메시지가 홍바오 메시지임을 감지하면 메시지는 홍바오 형태로 표시됩니다.
또한, 홍바오 메시지는 중요한 메시지이므로, 홍바오 메시지 우선 순위를 높게 설정하는 것이 좋습니다. 우선 순위를 높게 설정하면, 홍바오 메시지가 메시지 빈도 제한에 걸리더라도 전달될 가능성이 높아집니다(기본 빈도 제한: 그룹 메시지 40개/초, 1:1 메시지: 5개/초).

메시지 우선 순위에 대한 자세한 내용은 [메시지 우선순위](https://intl.cloud.tencent.com/document/product/1047/33526)를 참고하십시오.

>!홍바오 메시지의 결제 기능을 사용하려면, 해당 결제 SDK를 수동으로 통합해야 합니다. 현재 IM SDK는 이 결제 기능을 제공하지 않습니다.

간단하게 홍바오 메시지를 구성하는 과정은 다음과 같습니다(Android).
```java
// 새 메시지 생성
TIMMessage msg = new TIMMessage();
try{
	// 사용자 정의 메시지 프로토콜 지정
    JSONObject redPacket= new JSONObject();
	redPacket.put(“type”, “RED_PACKET”);
    redPacket.put(“amount”, 2018);
	redPacket.put(“msg”, “Happy new year!”);

    // 사용자 정의 프로토콜을 기반으로 사용자 정의 메시지 요소 구성
	TIMCustomElem customElem = new TIMCustomElem();
    customElem.setDesc(“red packet”);
	customElem.setData(redPacket.toString().getBytes(“utf-8”);
    if(msg.addElement(customElem) != 0){
	    Log.e(TAG, “add custom elem failed”);
	    return;
	}
}catch(Exception e){
	Log.e(TAG, “build custom elem failed”);
    return;
}

// 메시지 우선순위를 높음으로 설정
msg.setPriority(TIMMessagePriority.High);
```

[](id:Q6)
### IM 메시지의 저장 기간은 어떻게 됩니까?
1:1 메시지 및 라이브 방송 그룹 외 기타 그룹 메시지는 메시지 기록 저장 기능을 지원합니다. <a href=“https://console.cloud.tencent.com/im”>IM 콘솔</a>에 로그인하여 관련 설정을 수정할 수 있습니다. 패키지별 기본 구성은 다음과 같습니다. <ul style=“margin:0;”><li>체험판: 7일, 연장 불가능</li><li>프로 버전: 7일, 연장 가능</li><li>울티메이트 버전: 30일, 연장 가능 </li></ul>메시지 기록 보관 기간 연장은 부가 가치 서비스입니다. 자세한 내용은 <a href=“https://intl.cloud.tencent.com/document/product/1047/34350”>부가 가치 서비스 요금</a>을 참고하십시오.

[](id:Q7)

### 발신자가 블랙리스트에 포함되었는데 왜 계속 메시지에 발송 성공이라고 표시되나요?
IM 콘솔의 [블랙리스트 확인](https://intl.cloud.tencent.com/document/product/1047/34419)에서 메시지 발송 후 발송 성공 표시 기능을 제공합니다. 해당 기능을 활성화하면 블랙리스트에 포함된 사용자가 메시지를 발송한 후에도 발송 성공이 표시됩니다(실제로 상대방은 메시지를 수신하지 않음). 해당 설정을 비활성화하면 블랙리스트에 추가된 사용자는 메시지 발송 후 실패 알람을 받으며 SDK는 [에러 코드 20007](https://intl.cloud.tencent.com/document/product/1047/34348)를 수신합니다. 자세한 설정은 [블랙리스트 확인](https://intl.cloud.tencent.com/document/product/1047/34419) 문서를 참고하십시오.

