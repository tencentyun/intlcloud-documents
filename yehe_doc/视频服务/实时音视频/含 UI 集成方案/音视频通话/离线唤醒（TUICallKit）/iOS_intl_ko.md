오프라인 푸시 기능을 사용하면 App이 백그라운드에서 실행되거나 오프라인인 경우에도 오디오/비디오 통화를 수신할 수 있습니다. TUICallKit은 Apple에서 제공하는 APNs(Apple 푸시 알림 서비스)를 사용하여 메시지 알림을 푸시합니다.

## 1단계: 오프라인 푸시 구성

1. [APNs](https://www.tencentcloud.com/document/product/1047/39157#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E7.94.B3.E8.AF.B7-apns-.E8.AF.81.E4.B9.A6)의 1단계 지침에 따라 **APNs 인증서를 신청**합니다.

2. [APNs](https://www.tencentcloud.com/document/product/1047/39157#.E6.AD.A5.E9.AA.A42.EF.BC.9A.E4.B8.8A.E4.BC.A0.E8.AF.81.E4.B9.A6.E5.88.B0.E6.8E.A7.E5.88.B6.E5.8F.B0)의 2단계 지침에 따라 **IM 콘솔에서 구성**합니다.

3. [APNs](https://www.tencentcloud.com/document/product/1047/39157#.E6.AD.A5.E9.AA.A43.EF.BC.9Aapp-.E5.90.91.E8.8B.B9.E6.9E.9C.E5.90.8E.E5.8F.B0.E8.AF.B7.E6.B1.82-devicetoken)의 3단계 지침에 따라 사용자가 **App에 로그인할 때마다 Apple에서 deviceToken을 가져옵니다**.

4. [APNs](https://www.tencentcloud.com/document/product/1047/39157#.E6.AD.A5.E9.AA.A44.EF.BC.9A.E7.99.BB.E5.BD.95-im-sdk-.E5.90.8E.E4.B8.8A.E4.BC.A0-devicetoken-.E5.88.B0.E8.85.BE.E8.AE.AF.E4.BA.91)의 4단계 지침에 따라 **IM SDK에 로그인한 후 deviceToken을 Tencent Cloud에 업로드**합니다.

>? TUICallKit이 후속 단계를 완료했으므로 [APNs](https://www.tencentcloud.com/document/product/1047/39157)의 다른 단계는 무시할 수 있습니다.

## 2단계: 프로젝트 구성

애플리케이션에 필요한 권한을 추가하려면 Xcode 프로젝트에서 푸시 알림 기능을 활성화하십시오.

**Xcode**에서 프로젝트를 열고 **Project** > **Target** > **Signing & Capabilities** 탭에서 **+**를 클릭하고 **Push Notifications**를 선택하여 이 권한을 추가합니다. 결과는 아래와 같습니다.

![](https://qcloudimg.tencent-cloud.cn/image/document/954340261de64a1aab536cf8744d6136.png)

상기 단계를 완료한 후 프로젝트를 실행하여 `TUICallKit`의 오프라인 푸시 기능을 사용해 볼 수 있습니다.

## FAQ 

### 1. 푸시 메시지를 수신할 수 없고 백엔드에서 bad devicetoken 오류를 보고하면 어떻게 해야 합니까?

Apple 장치의 경우 deviceToken은 현재 컴파일 환경과 관련이 있습니다. IMSDK에 로그인한 후 Tencent Cloud에 deviceToken을 업로드하는 데 사용된 인증서 ID가 환경 token과 일치하지 않는 경우 오류가 보고됩니다.

컴파일 환경이 Release인 경우 `- application:didRegisterForRemoteNotificationsWithDeviceToken:` 콜백은 릴리스 환경 token을 반환합니다. 이 경우 businessID는 프로덕션 환경의 인증서 ID로 설정해야 합니다.

컴파일 환경이 Debug인 경우 `- application:didRegisterForRemoteNotificationsWithDeviceToken:` 콜백은 개발 환경 token을 반환합니다. 이 경우 businessID는 개발 환경의 인증서 ID로 설정해야 합니다.

```objectivec
V2TIMAPNSConfig *confg = [[V2TIMAPNSConfig alloc] init];
/* Apple에 개발자 인증서를 등록하고 개발자 계정에서 인증서(p12 파일)를 다운로드 및 생성하고 생성된 p12 파일을 Tencent 인증서 콘솔에 업로드해야 합니다. 콘솔은 자동으로 인증서 ID를 생성하여 busiId 매개변수에 전달합니다.*/
//인증서 ID 푸시
confg.businessID = sdkBusiId;
confg.token = self.deviceToken;
[[V2TIMManager sharedInstance] setAPNS:confg succ:^{

} fail:^(int code, NSString *msg) {

}];
```

### 2. iOS 개발 환경에서 가끔 deviceToken이 등록을 위해 반환되지 않거나 APNs의 token 요청이 실패하면 어떻게 해야 하나요?

이 문제는 APNs 불안정으로 인해 발생합니다. 다음과 같은 방법으로 수정할 수 있습니다.

1. SIM 카드를 전화기에 삽입하고 4G 네트워크를 사용합니다.

2. 애플리케이션을 제거했다가 다시 설치하거나, App을 다시 시작하거나, 전화기를 종료했다가 다시 시작합니다.

3. 프로덕션 환경용 패키지를 사용합니다.

4. 다른 iPhone을 사용합니다.
