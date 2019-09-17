# Android平台常见问题
<hr>

#### 推送消息收不到？

用获取到的Token，在「[控制台](https://console.cloud.tencent.com/tpns)」推送。如无法收到推送请根据以下情况进行排查（请确保SDK版本是最新的版本，如果是旧版本出现问题，在新版本可能已经修复，如遇到web端推送报错，请刷新页面重试）

####为什么注册成功了无法收到推送？

* 请查看当前的应用包名是否和注册信鸽应用时填写的应用包名是否一致。如果不一致，推送的时候建议开启多包名推送
* 检查手机网络是是否异常，切换4G网络测试一下
* 信鸽推送分为「通知栏消息」，和「应用内消息」（透传消息），通知栏消息可以展示到通知栏，应用内消息不能展示到通知栏
* 确认手机当前模式是正常模式，部分手机在低电量，勿扰模式，省电模式下，会对后台信鸽进程进行一系列网络和活动的限制
* 查看设备是否开启通知栏权限，oppo,vivo等手机，需要手动开启通知栏权限

#### 设备注册失败有哪些原因 ？

* 新创建的app会有一分钟左右的数据同步过程，在此期间注册可能返回20错误码，稍后重试即可

**\[参数填写有误\]**

* access id和access key是否正确配置，常见错误是误用secret key或者access key头尾有空格

**\[注册返回错误\]**

* 若控制台返回「10004」、「10002」、「20」等错误码，请参考：[Android SDK 错误码对照表]

**\[注册无回调\]**
  确认当前网络情况是否良好,建议使用4G网络测试，WIFI由于使用人数过多可能造成 网络带宽不足
 **是否是努比亚品牌的手机**
  在2015年下半年和2016年出的机器都无法注册，具体机型包括「Nubia Z11系列」，「NubiaZ11S系列」，「NubiaZ9S系列」。可以的注册的机器都是之前的机器，包括「Z7系列」，「My布拉格系列」

#### 为什么关闭应用后无法收到推送？

* 目前第三方推送都无法保证关闭应用过后还可以收到推送消息，这个是手机定制ROM对信鸽service的限制问题，信鸽的一切活动都需要建立在信鸽的service能够正常联网运行，service被终止后，由系统、安全软件和用户操作限定是否能够再次启动
* QQ，微信是系统级别的应用白名单，相关的service不会因为关闭应用而退出，所以用户感知推出应用过后还可以收到消息，其实相关的service 还是能够在后台存活的
* Android端在应用退出，信鸽service和信鸽的服务器断开连接后，这个时候给这个设备下发的消息，会变成离线消息，离线消息最多保存72小时，每个设备最多保存两条，如果有多条离线消息。在关闭应用期间推送的消息，如开启应用无法收到，请检查是否调用了反注册接口：XGPushManager.unregisterPush\(this\);

### 如何设置消息点击事件以及跳转页面方法？

由于目前SDK点击消息默认会有点击事件，默认的点击事件是打开主界面。所以在终端点击消息回调的「onNotifactionClickedResult」方法内设置跳转操作时，自定义的跳转和默认的点击事件造成冲突。结果是点击之后会跳转到指定界面过后再回到主界面，所以不能再「onNotifactionClickedResult」内设置跳转

**解决办法如下\(推荐使用第一种方式\)：**

**\[1\] 使用Intent来跳转指定页面**

* 需要在客户端app的manifest上配置要跳转的页面，如要跳转AboutActivity指定页面：

```
<activity
android:name="com.qq.xg.AboutActivity"
android:theme="@android:style/Theme.NoTitleBar.Fullscreen" >
<intent-filter >
<action android:name="android.intent.action.VIEW" />
<category android:name="android.intent.category.DEFAULT"/>
<data android:scheme="xgscheme"
android:host="com.xg.push"
android:path="/notify_detail" />
</intent-filter>
</activity>
```
* 若使用信鸽管理台设置intent进行跳转，填写方式如下：

![](/assets/intent.png)

* 若使用服务端SDK设置intent进行跳转，可设置intent为（以Java SDK为例）：
```
action.setIntent("xgscheme://com.xg.push/notify_detail");
```
* 如果要带上param1和param2等参数可以这么设置：
```
action.setIntent("xgscheme://com.xg.push/notify_detail?param1=aa&param2=bb");
```

* 终端获取参数：
1.在你跳转指定的页面onCreate方法里面：
```
Uri uri = getIntent().getData();
    if (uri != null) {                
String url = uri.toString();
String p1= uri.getQueryParameter("param1");
String p2= uri.getQueryParameter("param2");
 }
```
2.如果传参包含有特殊字符，如 # & 等等
可以参考使用如下方式解析：
```
Uri uri = getIntent().getData();
    if (uri != null) {                
 String url = uri.toString();
 UrlQuerySanitizer sanitizer = new UrlQuerySanitizer();
 sanitizer.setUnregisteredParameterValueSanitizer(UrlQuerySanitizer.getAllButNulLegal());
   sanitizer.parseUrl(url);
   String value1 = sanitizer.getValue("key1");
   String value2 = sanitizer.getValue("key2");
   Log.i("XG" , "value1 = " + value1 + " value2 = " + value2);
}
```

**\[2\] 在下发消息的时候设置点击消息要跳转的页面**

（a）可以直接在web端高级功能内设置deeplink包名+类名） ;

（b）后台设置Messege 类中的 Action字段的 的SetActivity方法（包名+类名），通过XGPushClickedResult 可以获取到消息的相关内容: 标题 ，内容和附加参数

* 后台设置跳转页面的方法如下（以javaSDK为例）：

```js
......
XingeApp android = new XingeApp(accessID,secretkey);
Message message_android =new Message();
message_android.setExpireTime(86400);
message_android.setTitle("信鸽推送");
message_android.setType(1);
message_android.setContent("android test2");
ClickAction action =new ClickAction();
action.setActivity("com.qq.xgdemo.activity.SettingActivity");
message_android.setAction(action);
JSONObject ret1 = android.pushSingleDevice("token",message_android);
......
```

* 终端获取Message参数的方法如下:

```
//this必须为点击消息要跳转到页面的上下文。
XGPushClickedResult clickedResult = XGPushManager.onActivityStarted(this);
//获取消息附近参数
String ster = clickedResult.getCustomContent();
//获取消息标题
String set = clickedResult.getTitle();
//获取消息内容
String s = clickedResult.getContent();

```
**\[3\] 发应用内消息到终端，用户自定义通知栏，采用本地通知弹出通知，设置要跳转的页面**

