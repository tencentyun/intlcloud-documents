IM 오프라인 푸시 기능은 [TPNS(Tencent Push Notification Service)](https://intl.cloud.tencent.com/document/product/1024/32592)에서 제공합니다. 본문은 TPNS에 액세스하고 오프라인 푸시 기능을 실행하는 자세한 단계를 소개합니다.

>!
>
>- TPNS에 액세스하려면 IM SDK를 [6.0.1975 버전 이상](https://intl.cloud.tencent.com/document/product/1047/33996)으로 업그레이드해야 합니다.

## TPNS를 연결하여 오프라인 푸시 기능 실행

[](id:step1)
### 1단계: 벤더 푸시 플랫폼에 애플리케이션 등록

오프라인 푸시 기능은 벤더의 기존 채널에 종속되며, AppID, AppKey 등의 매개변수를 얻기 위해서는 각 벤더의 푸시 플랫폼에 애플리케이션을 등록해야 합니다. 현재 중국 내에서 지원되는 휴대폰 벤더는 다음과 같습니다. [Xiaomi](https://dev.mi.com/console/doc/detail?pId=68), [Huawei](https://developer.huawei.com/consumer/cn/doc/development/HMSCore-Guides/service-introduction-0000001050040060), [OPPO](https://open.oppomobile.com/wiki/doc#id=10195), [VIVO](https://dev.vivo.com.cn/documentCenter/doc/281), [Meizu](http://open-wiki.flyme.cn/doc-wiki/index#id?129), 중국 본토 외 지역에서는 [Google FCM](https://console.firebase.google.com/u/0/?hl=zh-cn)이 지원됩니다.

[](id:step2)
### 2단계: TPNS 콘솔 설정 
이전에 IM 콘솔에서 오프라인 푸시 정보를 설정하지 않았다면 [TPNS 콘솔](https://console.cloud.tencent.com/tpns/product)에 직접 로그인한 후 아래 단계에 따라 오프라인 푸시 정보를 설정하십시오.
1. 제품 생성: **TPNS 콘솔** > **제품 관리** > **제품 추가**로 이동하여 이름 및 설명과 등 정보를 입력합니다.
>! 서비스 액세스 포인트 선택:
>- 해외 고객을 지원하기 위해 Google FCM을 연결하려면 싱가포르/중국홍콩 액세스 포인트를 선택하십시오.
>- 중국 내 고객만 지원하려면 광저우/상하이 액세스 포인트를 선택하십시오.
>
![](https://qcloudimg.tencent-cloud.cn/raw/2253167ef7cdb850b22e6f603a68a6aa.png)
2. **기본 설정** 열에서 새 제품을 선택하고 설정할 애플리케이션의 패키지 이름을 입력합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/eaec2f774dfe3efb552d75a043b917e4.png)
3. 제품이 성공적으로 생성되면 TPNS의 AccessID, AsscessKey 등과 같은 매개변수를 얻습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/aa8ecc7474d153afc23ba31474a8d087.png)
4. 벤더 푸시 매개변수 설정: **TPNS 콘솔** > **제품 선택** > **기본 설정** > **벤더 채널 선택** > **활성화**에서 1단계에서 획득한 벤더의  AppID, AppKey, AppSecret 등 매개변수를 TPNS에 설정합니다.
<table>
<thead><tr><th>벤더</th><th>벤더 푸시 플랫폼</th><th>TPNS 벤더 채널 설정</th></tr></thead>
<tbody><tr>
<td>Xiaomi</td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/235758a1895063b7b99f67cc4ef8e4f3.png" alt=""></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/4d3478e48213c849a26f05274bca2c96.png" alt=""></td>
</tr><tr>
<td>Huawei</td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/f8c7c0c9c259919c1f93e79707ddde1d.png" alt=""></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/0b9bf72afcd07318dbd73629256e676f.png" alt=""></td>
</tr><tr>
<td>OPPO</td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/051de434b51f77711e5a6aa7682abb72.png" alt=""></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/d910fa76031b8b7c7c302fd50b01eeab.png" alt=""></td>
</tr><tr>
<td>vivo</td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/a764b271e3ac1de64b3c9342fa9e96b1.png"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/d15454a306afd84fd3872ac522d01140.png"></td>
</tr><tr>
<td>Meizu</td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/70ad94d8e843f92247c67a3ae4004c15.png" ></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/58583dd8abbcbc4b97ed958f6ff912d5.png"></td>
</tr><tr>
<td>Google FCM</td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/b344dee87f9d946e21480cd57556730d.png"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/2fa68e5577e657f6ebabcd9a66d6f656.png"></td>
</tr>
</tbody></table>
5. 타사 서비스 권한: 타사 서비스 권한을 입력하고 IM 애플리케이션의 오프라인 푸시 기능 권한을 TPNS에 부여합니다.
    1. Cloud IM 애플리케이션 권한 부여를 선택하고 **권한 추가**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/55cf9d53a066ee9ec7c9a646c667151e.png)
    2. 바인딩 권한을 부여할 IM 애플리케이션을 선택하고 새로 생성된 TPNS 제품 애플리케이션을 선택한 후 권한 부여를 제출합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/284b12d42b8035311567c1e9eb2de463.png" width=500>

>? 이전에 IM 콘솔에서 오프라인 푸시 정보를 설정한 경우 이러한 설정 정보는 [TPNS 콘솔](https://console.cloud.tencent.com/tpns/product)로 자동 마이그레이션되며, [TPNS 콘솔](https://console.cloud.tencent.com/tpns/product)에 로그인하여 설정 정보를 수정할 수 있습니다. IM은 오프라인 푸시에 이러한 설정 정보를 계속 사용합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2a9c1c81da25d94d55227e0223495111.png)

[](id:step3)
### 3단계: TPNS 프로젝트 설정
**설정 관리** 페이지에서 **빠른 연결**을 클릭합니다.
1. 빠른 연결 1단계 가이드에 따라 `tpns-configs.json` 파일을 다운로드하고 Android Studio 프로젝트에 추가합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/18e22286a9c159b75e7ac31dfefd3220.png)
2. 빠른 연결 2단계 가이드를 참고하여 프로젝트 설정을 추가하고, 프로젝트와 애플리케이션의 Gradle 설정을 각각 수정합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/12a5120ec10eeec69035f229db7c6f0c.png)

[](id:step4)
### 4단계: 오프라인 푸시 리디렉션 매개변수 설정
오프라인 푸시 수신 후 알림 표시줄에 푸시 정보가 표시됩니다. 이미지와 같이 알림 표시줄을 클릭하여 애플리케이션을 열고 설정 리디렉션 인터페이스로 이동합니다. 메시지 알림을 클릭 시 리디렉션될 Activity를 설정하려면 아래 단계를 참고하십시오.
<img src="https://qcloudimg.tencent-cloud.cn/raw/7e6b56b3bb60bc9ccf7d5d0179eb51ea.png" width=400>
1. TPNS 콘솔에서 리디렉션 매개변수를 설정합니다. 리디렉션 매개변수 설정 형식은 `protocol://hostname/path/`입니다.
 ![](https://qcloudimg.tencent-cloud.cn/raw/d85b48a8e6014a984ea83af6683e5fdb.png)
2. [매니페스트 파일 AndroidManifest.xml](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/src/main/AndroidManifest.xml)에서 오프라인 푸시 리디렉션 매개변수의 설정을 완료합니다.
>! 이 리디렉션 매개변수는 TPNS 콘솔의 설정과 일치해야 합니다.
>
```
<activity
    android:name="애플리케이션 리디렉션 인터페이스의 전체 클래스 이름"
    android:launchMode="singleTask"
    android:screenOrientation="portrait"
    android:windowSoftInputMode="adjustResize|stateHidden">

        <intent-filter>
            <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <!-- Scheme 프로토콜 개발자 사용자 정의 가능. 형식: protocol://hostname/path/.-->
                <data
                    android:host="설정된 hostname"
                    android:path="설정된 path"
                    android:scheme="설정된 프로토콜, 즉 정의된 scheme" />
        </intent-filter>

</activity>
```


[](id:step5)
### 5단계: TPNS 푸시 규칙 설정

[매니페스트 파일 AndroidManifest.xml](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/src/main/AndroidManifest.xml)에서 TPNS 서비스 액세스 포인트, TPNS 푸시 클래스 등 TPNS 푸시 규칙을 설정합니다.

```
<!-- 1단계: TPNS 서비스 액세스 포인트 설정, 2단계에서 TPNS 콘솔에서 제품 생성 시 선택한 서비스 액세스 포인트를 참고하십시오. 해외 고객을 지원하기 위해 Google FCM을 연결하려면 싱가포르/홍콩 액세스 포인트를 선택하십시오. 국내 고객만 지원하는 경우 TPNS의 기본 서비스 액세스 포인트는 광저우이며 추가 설정이 필요하지 않습니다.

        상하이: tpns.sh.tencent.com
        싱가포르: tpns.sgp.tencent.com
        중국홍콩: tpns.hk.tencent.com -->

<!-- 설정 형식은 다음과 같음 -->
<meta-data
       android:name="XG_SERVER_SUFFIX"
       android:value="기타 서비스 액세스 포인트 도메인" />

<!-- 2단계: TPNS receiver, 오프라인 푸시로부터 메시지 및 결과 피드백을 받는 Receiver, 메시지 통과, token 콜백 등록 등-->
<receiver android:name="com.tencent.qcloud.tim.demo.thirdpush.TPNSPush.TPNSMessageReceiver">
    <intent-filter>
        <!-- 메시지 통과 수신 -->
        <action android:name="com.tencent.android.xg.vip.action.PUSH_MESSAGE" />
        <!-- 등록 수신, 등록 취소, 태그 설정/삭제, 클릭 등 처리 결과 알림 -->
        <action android:name="com.tencent.android.xg.vip.action.FEEDBACK" />
    </intent-filter>
</receiver>

<!-- 3단계: TPNS가 Android P와 호환되는 경우 Apache HTTP client 라이브러리를 추가하고 AndroidManifest의 application 노드에 다음 설정을 추가해야 합니다. -->
<uses-library android:name="org.apache.http.legacy" android:required="false"/>
```

[](id:step6)
### 6단계: TPNS SDK 통합
TPNS SDK에 연결하기 위해서는 아래의 단계를 따르십시오. 예시 코드는 [TPNSPushSetting](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/src/main/java/com/tencent/qcloud/tim/demo/thirdpush/TPNSPush/TPNSPushSetting.java)의 init() 메소드를 참고하십시오.

1. [gradle](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/build.gradle) 파일에 각 벤더에서 푸시한 SDK를 추가하고, 2단계에서 제품이 성공적으로 생성되면 AccessID와 AsscessKey 매개변수를 받습니다.
```
android{
    ......
    defaultConfig {
        ......

        manifestPlaceholders = [
            // 2단계에서 TPNS 콘솔 가져오기
            XG_ACCESS_ID : "애플리케이션의 accessid 등록",
            XG_ACCESS_KEY : "애플리케이션의 accesskey 등록",
        ]
        ......
    }
    ......
}

dependencies {
    ......
    // 메인 패키지
    implementation 'com.tencent.tpns:tpns:1.3.1.1-release'
    // Xiaomi
    implementation "com.tencent.tpns:xiaomi:1.3.1.1-release"
    // Meizu
    implementation "com.tencent.tpns:meizu:1.3.1.1-release"
    // OPPO
    implementation "com.tencent.tpns:oppo:1.3.1.1-release"
    // vivo
    implementation "com.tencent.tpns:vivo:1.3.1.1-release"
    // Huawei
    implementation 'com.tencent.tpns:huawei:1.3.1.1-release'
    implementation 'com.huawei.hms:push:5.0.2.300'
}
```
2. 애플리케이션 실행 후 TPNS 서비스를 등록하고 가입 성공 후 획득한 token을 저장합니다.
```
final Context context = DemoApplication.instance();

XGPushConfig.enableDebug(context, true);
// OPPO 예시
XGPushConfig.setOppoPushAppId(context, PrivateConstants.OPPO_PUSH_APPKEY);
XGPushConfig.setOppoPushAppKey(context, PrivateConstants.OPPO_PUSH_APPSECRET);
// 중요: 벤더 채널 등록 활성화
XGPushConfig.enableOtherPush(context, true);
// TPNS 푸시 서비스 등록
XGPushManager.registerPush(context, new XGIOperateCallback() {
        @Override
        public void onSuccess(Object o, int i) {
            DemoLog.w(TAG, "tpush register success token: " + o);
            // 이 token은 저장하여 후속 프로세스에 사용
            String token = (String) o;
        }

        @Override
        public void onFail(Object o, int i, String s) {
            DemoLog.w(TAG, "tpush register failed errCode: " + i + ", errMsg: " + s);
        }
});
```
- IM 로그인 성공 후 IM SDK의 [setOfflinePushConfig](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) 인터페이스를 호출하여 TPNS token을 리포트합니다.
>! V2TIMOfflinePushConfig 클래스를 구성하고, businessID를 0으로, isTPNSToken을 true로 설정하고, TPNS 등록 시 받은 token을 리포트합니다.
>
```
V2TIMOfflinePushConfig v2TIMOfflinePushConfig = null;
// businessID를 0으로, isTPNSToken을 true로 설정해야 하며, 리포트 token은 2단계에 TPNS 등록 후 받습니다.  
v2TIMOfflinePushConfig = new V2TIMOfflinePushConfig(0, token, true);
V2TIMManager.getOfflinePushManager().setOfflinePushConfig(v2TIMOfflinePushConfig, new V2TIMCallback() {
        @Override
        public void onError(int code, String desc) {
            DemoLog.d(TAG, "setOfflinePushToken err code = " + code);
        }

        @Override
        public void onSuccess() {
            DemoLog.d(TAG, "setOfflinePushToken success");
        }
});
```
3. TPNS 푸시 클래스 [TPNSMessageReceiver](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/src/main/java/com/tencent/qcloud/tim/demo/thirdpush/TPNSPush/TPNSMessageReceiver.java)에서 TPNS token 변경 수신 시 TPNS token을 다시 리포트하십시오.
```
/**
 *  등록 콜백
 * @param context
 * @param errorCode 0은 성공, 나머지는 에러 코드
 */
@Override
public void onRegisterResult(Context context, int errorCode, XGPushRegisterResult message) {
  if (context == null || message == null) {
    return;
  }
  String text = "";
  if (errorCode == XGPushBaseReceiver.SUCCESS) {
    String token = message.getToken();
    text = "등록 성공 1. token：" + token;
    // IM SDK의 setOfflinePushConfig 인터페이스 호출하여 TPNS token 리포트
    ...
  } else {
    text = message + "등록 실패, 에러 코드:" + errorCode;
  }
}

```
- TPNS token을 성공적으로 리포트한 후 IM 로그인 계정을 TPNS에 바인딩하고 오프라인 푸시 수신을 시작합니다.
``` 
public void bindUserID(String userId) {
    // 중요: IM 사용자 계정 로그인 시 TPNS 계정 바인딩 인터페이스를 호출하여 비즈니스 계정을 바인딩하면 이 계정을 타깃으로 TPNS 오프라인 푸시를 진행할 수 있습니다.
    XGPushManager.AccountInfo accountInfo = new XGPushManager.AccountInfo(
            XGPushManager.AccountType.UNKNOWN.getValue(), userId);
    XGPushManager.upsertAccounts(DemoApplication.instance(), Arrays.asList(accountInfo), new XGIOperateCallback() {
        @Override
        public void onSuccess(Object o, int i) {
            DemoLog.w(TAG, "upsertAccounts success");
        }

        @Override
        public void onFail(Object o, int i, String s) {
            DemoLog.w(TAG, "upsertAccounts failed");
        }
    });
}
```
- IM 계정 로그아웃 시 오프라인 푸시 수신을 중지하려면 TPNS 계정 바인딩을 해제해야 합니다.
```
public void unBindUserID(String userId) {
        // TPNS 계정 비즈니스 계정 바인딩 해제
        XGIOperateCallback xgiOperateCallback = new XGIOperateCallback() {
            @Override
            public void onSuccess(Object data, int flag) {
                DemoLog.i(TAG, "onSuccess, data:" + data + ", flag:" + flag);
            }
            @Override
            public void onFail(Object data, int errCode, String msg) {
                DemoLog.w(TAG, "onFail, data:" + data + ", code:" + errCode + ", msg:" + msg);
            }
        };

        //XGPushManager.delAccount(context, UserInfo.getInstance().getUserId(), xgiOperateCallback);
        Set<Integer> accountTypeSet = new HashSet<>();
        accountTypeSet.add(XGPushManager.AccountType.CUSTOM.getValue());
        accountTypeSet.add(XGPushManager.AccountType.IMEI.getValue());
        XGPushManager.delAccounts(DemoApplication.instance(), accountTypeSet, xgiOperateCallback);
} 
```
- 애플리케이션 백그라운드 전환 후 수신된 새 메시지를 휴대폰의 알림 표시줄에 표시되게 하려면 IM SDK의 [doBackground()](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a2b191294ac4d68a2d69e482eae1b638f) 인터페이스를 호출하여 앱의 상태를 IM 백그라운드와 동기화하십시오. 포그라운드 전환 후 IM SDK의 [doForeground()](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a4c2ff4eea609da1d0950648905fbf6aa) 인터페이스를 호출하여 애플리케이션 상태를 IM 백그라운드와 동기화하십시오. APP의 포그라운드/백그라운드 전환 수신 방안은 [DemoApplication](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/src/main/java/com/tencent/qcloud/tim/demo/DemoApplication.java)의 StatisticActivityLifecycleCallback 클래스의 관련 로직을 참고하시길 추천합니다.
```
// 애플리케이션 백그라운드 전환 시
V2TIMManager.getOfflinePushManager().doBackground(totalCount, new V2TIMCallback() {
    @Override
    public void onError(int code, String desc) {
        DemoLog.e(TAG, "doBackground err = " + code + ", desc = " + desc);
    }

    @Override
    public void onSuccess() {
        DemoLog.i(TAG, "doBackground success");
    }
});
// 애플리케이션 포그라운드 전환 시
V2TIMManager.getOfflinePushManager().doForeground(new V2TIMCallback() {
    @Override
    public void onError(int code, String desc) {
        DemoLog.e(TAG, "doForeground err = " + code + ", desc = " + desc);
    }

    @Override
    public void onSuccess() {
        DemoLog.i(TAG, "doForeground success");
    }
});
```
- 상기 설정을 완료한 후 TPNS 콘솔 [푸시 작업](https://console.cloud.tencent.com/tpns/push)에서 오프라인 푸시 메시지를 테스트하여 통합이 성공적인지 확인합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/250b5ef9c7e1fc66af4bdf028f2820fe.png)

[](id:step7)
### 7단계: 메시지 전송 시 오프라인 푸시 매개변수 설정

[sendMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795)를 호출하여 메시지를 보낼 때 V2TIMOfflinePushInfo를 통해 오프라인 푸시 매개변수를 설정할 수 있습니다. [ChatProvider](https://github.com/tencentyun/TIMSDK/blob/master/Android/TUIKit/TUIChat/tuichat/src/main/java/com/tencent/qcloud/tuikit/tuichat/model/ChatProvider.java)의 sendMessage() 메소드를 참고하시기 바랍니다.

```
OfflineMessageContainerBean containerBean = new OfflineMessageContainerBean();
OfflineMessageBean entity = new OfflineMessageBean();
entity.content = message.getExtra().toString();
entity.sender = message.getFromUser();
entity.nickname = chatInfo.getChatName();
entity.faceUrl = TUIChatConfigs.getConfigs().getGeneralConfig().getUserFaceUrl();
containerBean.entity = entity;
        
V2TIMOfflinePushInfo v2TIMOfflinePushInfo = new V2TIMOfflinePushInfo();
v2TIMOfflinePushInfo.setExt(new Gson().toJson(containerBean).getBytes());
// OPPO는 ChannelID를 설정해야 푸시 메시지를 수신할 수 있으며, 이 channelID는 콘솔과 일치해야 함
v2TIMOfflinePushInfo.setAndroidOPPOChannelID("tuikit");

final V2TIMMessage v2TIMMessage = message.getTimMessage();
String msgID = V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, isGroup ? null : userID, isGroup ? groupID : null,
    V2TIMMessage.V2TIM_PRIORITY_DEFAULT, false, v2TIMOfflinePushInfo, new V2TIMSendCallback<V2TIMMessage>() {
        @Override
        public void onProgress(int progress) {

        }

        @Override
        public void onError(int code, String desc) {
            TUIChatUtils.callbackOnError(callBack, TAG, code, desc);
        }

        @Override
        public void onSuccess(V2TIMMessage v2TIMMessage) {
            TUIChatLog.v(TAG, "sendMessage onSuccess:" + v2TIMMessage.getMsgID());
            message.setMsgTime(v2TIMMessage.getTimestamp());
            TUIChatUtils.callbackOnSuccess(callBack, message);
        }
    });
```

[](id:step8)
### 8단계: 오프라인 푸시 메시지 리졸브

휴대폰이 오프라인 푸시 메시지를 수신하면 시스템 알림 표시줄에 수신된 푸시 메시지가 표시됩니다. 알림 표시줄에서 메시지를 클릭하면 자동으로 4단계에서 설정한 인터페이스로 리디렉션합니다. 이 인터페이스에서 `getIntent().getData()`를 호출하여 [7단계](#step7)에서 설정한 오프라인 푸시 매개변수를 가져올 수 있습니다. 예시 코드는 TUIKitDemo의 [handleOfflinePush()](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/src/main/java/com/tencent/qcloud/tim/demo/main/MainActivity.java) 메소드를 참고하십시오.


```
private void handleOfflinePush() {
    // 로그인 상태에 따라 IM에 다시 로그인해야 하는지 판단
    // 1. 로그인 상태가 V2TIMManager.V2TIM_STATUS_LOGOUT이면 로그인 인터페이스로 리디렉션하여 IM에 다시 로그인
    if (V2TIMManager.getInstance().getLoginStatus() == V2TIMManager.V2TIM_STATUS_LOGOUT) {
        Intent intent = new Intent(MainActivity.this, SplashActivity.class);
        if (getIntent() != null) {
            intent.setData(getIntent().getData());
        }
        startActivity(intent);
        finish();
        return;
    }
 
    // 2. 그렇지 않으면 App 백그라운드 상태임을 의미하며 오프라인 푸시 매개변수를 직접 리졸브합니다.
    final OfflineMessageBean bean = OfflineMessageDispatcher.parseOfflineMessage(getIntent());
    if (bean != null) {
        setIntent(null);
        NotificationManager manager = (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);
        if (manager != null) {
            manager.cancelAll();
        }

        if (bean.action == OfflineMessageBean.REDIRECT_ACTION_CHAT) {
            if (TextUtils.isEmpty(bean.sender)) {
                return;
            }
            TUIKit.startChat(bean.sender, bean.nickname, bean.chatType);
        } else if (bean.action == OfflineMessageBean.REDIRECT_ACTION_CALL) {
            IBaseLiveListener baseCallListener = TUIKitLiveListenerManager.getInstance().getBaseCallListener();
            if (baseCallListener != null) {
                baseCallListener.handleOfflinePushCall(bean);
            }
        }
    }
}
    
```


## FAQ
### Android 휴대폰 오프라인 푸시의 푸시 사운드를 사용자 정의하는 방법은 무엇입니까?
현재 대부분의 벤더에서 오프라인 푸시음 설정을 지원하지 않습니다. IM SDK도 지원하지 않습니다.

### OPPO 휴대폰이 오프라인 푸시를 받을 수 없는 이유는 무엇입니까?
OPPO 휴대폰이 푸시 알림을 수신할 수 없는 일반적인 상황은 다음과 같습니다.

- OPPO 푸시 공식 웹사이트의 요구 사항에 따라 Android 8.0 이상의 시스템 버전이 설치된 OPPO 휴대폰에서 ChannelID를 설정해야 하며, 그렇지 않으면 푸시 메시지가 표시되지 않습니다. 설정 방법은 [OPPO 푸시 설정](https://intl.cloud.tencent.com/document/product/1047/39156#oppo-.E6.8E.A8.E9.80.81)을 참고하십시오.
- 메시지의 [통과된 오프라인 푸시 사용자 정의 콘텐츠](https://intl.cloud.tencent.com/document/product/1047/39156#.E9.80.8F.E4.BC.A0.E8.87.AA.E5.AE.9A.E4.B9.89.E5.86.85.E5.AE.B93)가 JSON 형식이 아닌 경우 OPPO 휴대폰에서 푸시를 수신하지 못합니다.

### 사용자 정의 메시지 오프라인 푸시 알림을 받을 수 없는 이유는 무엇입니까?

사용자 정의 메시지의 오프라인 푸시는 일반 메시지와 다릅니다. 사용자 정의 메시지 내용을 리졸브할 수 없고 푸시 내용을 확인할 수 없으므로 기본적으로 푸시되지 않습니다. 푸시하려면 [sendMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe) 시 [offlinePushInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html)의 [desc](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a78c8e202aa4e0859468ce40bde6fd602) 필드를 설정해야 하며 푸시 시 기본적으로 desc 정보가 표시됩니다.

### 오프라인 푸시 메시지가 수신되지 않는 이유는 무엇입니까?
오프라인 푸시 기능은 문서 가이드를 따르면 정상적으로 실행할 수 있습니다. 오프라인 메시지를 받을 수 없는 경우 다음과 같은 상황일 수 있습니다.
- 먼저 IM 콘솔에서 [오프라인 테스트 툴](https://console.cloud.tencent.com/im-detail/tool-push-check) 또는 TPNS 콘솔 [푸시 작업](https://console.cloud.tencent.com/tpns/push)의 새로운 푸시 테스트를 통해 정상 푸시 가능 여부를 테스트합니다.
푸시가 비정상이고 장치 상태도 비정상인 경우 IM 콘솔 설정의 매개변수가 올바른지 확인하고, 또한 벤더 푸시 서비스 가입 및 IM 설정 오프라인 푸시 설정 관련 로직을 포함한 코드 초기화 가입 로직이 올바르게 설정되어 있는지 확인해야 합니다.
푸시가 비정상이고 장치 상태는 정상이면 channelID를 정확하게 입력했는지 또는 백그라운드 서비스가 정상인지 확인해야 합니다.

- 오프라인 푸시는 벤더의 능력에 종속되며, 일부 단순 문자는 벤더에 의해 필터링되어 푸시되지 않을 수 있습니다. 또한 일부 벤더는 알림을 분류하고 유형별로 다른 푸시 정책을 적용합니다. 이 경우 푸시가 즉각적이지 않거나 또는 푸시되지 않는 경우가 있습니다. 벤더 공식 홈페이지에서 해당 애플리케이션에 대한 상위 권한 분류를 신청해야 실시간으로 푸시될 수 있습니다.

### 인터페이스 리디렉션 실패 원인은 무엇입니까?
오프라인 푸시 메시지의 알림 표시줄을 클릭하면 지정된 인터페이스로 리디렉션됩니다. 원리는 백그라운드가 콘솔에 설정된 각 벤더의 리디렉션 방식 및 인터페이스 매개변수, 벤더의 인터페이스 규칙에 따라 벤더의 서버에 전달되고 해당 인터페이스를 클릭하면 해당 인터페이스 리디렉션이 실행되는 것입니다. 해당 인터페이스 실행은 매니페스트 파일의 설정에 종속됩니다. 콘솔 설정과 일치해야 정확하게 실행 및 리디렉션됩니다.

따라서 인터페이스 리디렉션 실패는 콘솔과 매니페스트 파일의 설정의 일치성과 정확성을 중점 진단해야 합니다. TUIKitDemo 설정을 참고하시기 바랍니다. 주의할 점은 일부 벤더는 인터페이스를 제공하는 방식에 차이가 있습니다.

