# Android平台常见问题
<hr>

## 收不到推送的问题

用获取到的Token，在「[信鸽官网](http://xg.qq.com/)」推送。如无法收到推送请根据以下情况进行排查（请确保SDK版本是最新的版本，如果是旧版本出现问题，在新版本可能已经修复，如遇到web端推送报错，请刷新页面重试）

### 注册成功无法收到推送

* 请查看当前的应用包名是否和注册信鸽应用时填写的应用包名是否一致。如果不一致，推送的时候建议开启多包名推送
* 检查手机网络是是否异常，切换4G网络测试一下
* 信鸽推送分为「通知栏消息」，和「应用内消息」（透传消息），通知栏消息可以展示到通知栏，应用内消息不能展示到通知栏
* 确认手机当前模式是正常模式，部分手机在低电量，勿扰模式，省电模式下，会对后台信鸽进程进行一系列网络和活动的限制
* 查看设备是否开启通知栏权限，oppo,vivo等手机，需要手动开启通知栏权限

### 注册不成功无法收到推送

* 新创建的app会有一分钟左右的数据同步过程，在此期间注册可能返回20错误码，稍后重试即可

**\[参数填写有误\]**

* access id和access key是否正确配置，常见错误是误用secret key或者access key头尾有空格

**\[注册返回错误\]**

* 若控制台返回「10004」、「10002」、「20」等错误码，请参考：[Android SDK 错误码对照表](/android_access/android_returncode.md)

**\[注册无回调\]**

* 是否添加
  **wup包**
* 确认当前
  **网络情况**
  是否良好,建议使用4G网络测试，WIFI由于使用人数过多可能造成 网络带宽不足
* **努比亚手机**
  在2015年下半年和2016年出的机器都无法注册，具体机型包括「Nubia Z11系列」，「NubiaZ11S系列」，「NubiaZ9S系列」。可以的注册的机器都是之前的机器，包括「Z7系列」，「My布拉格系列」（在信鸽2.47和信鸽3.X上都有这个现象）

### 关闭应用无法收到推送

* 目前第三方推送都无法保证关闭应用过后还可以收到推送消息，这个是手机定制ROM对信鸽service的限制问题，信鸽的一切活动都需要建立在信鸽的service能够正常联网运行，service被终止后，由系统、安全软件和用户操作限定是否能够再次启动
* QQ，微信是系统级别的应用白名单，相关的service不会因为关闭应用而退出，所以用户感知推出应用过后还可以收到消息，其实相关的service 还是能够在后台存活的
* Android端在应用退出，信鸽service和信鸽的服务器断开连接后，这个时候给这个设备下发的消息，会变成离线消息，离线消息最多保存72小时，每个设备最多保存两条，如果有多条离线消息。在关闭应用期间推送的消息，如开启应用无法收到，请检查是否调用了反注册接口：XGPushManager.unregisterPush\(this\);

### 账号推送收不到

「账号」，又称「别名」，指带有账号登录功能的APP的用户账号，这里不仅仅是QQ或微信，只要是用户的账号都支持，比如手机QQ的账号就是QQ号码，gmail的账号就是邮箱，中国移动的账号就是手机号码。

对于希望根据帐号进行推送的用户，首先需要将账号与Token进行绑定，否则将无法推送成功。Android绑定账号在注册时绑定，即：registerPush\(context,account\)接口，ios通过setAccount设置。

* 选择帐号推送时，提示Token not found,check registration，说明账号没和Token关联上，这种情况有两种可能：

（1）账号或别名注销了，不一定是app调用，某些情况下可能会自动触发注销的

（2）该设备注册了别的账号或别名，这样会自动与原来的解绑。（一个设备只能对应一个别名如果当前别名下没有设备了，就not found了）

* 绑定账号后，可以通过指定别名（账号）下发通知。通常情况下，这个账号最近登陆过的设备都可以收到通知。用户账号退出时，调用registerPush\(context,"\*"\)解除当前账号的绑定。
* 账号（别名）不允许单字符，一个帐号最多可以绑定100个设备，只有最后一个绑定的设备才可以收到推送。

### 标签推送收不到

请确认tag标签是否绑定成功，一个应用最多有10000个 标签「tag」， 每个Token在一个应用下最多100个 标签「tag」， 标签「tag」中不准包含空格

* **用服务端推送SDK来查询「tag」与「Token」绑定关系**

```php
/**
     * 查询token的标签
     */
public function QueryTokenTags($deviceToken)
    {
        $ret = array('ret_code' => -1);
        if (!is_string($deviceToken)) {
            $ret['err_msg'] = 'deviceToken is not valid';
            return $ret;
        }
        $params = array();
        $params['access_id'] = $this->accessId;
        $params['device_token'] = $deviceToken;
        $params['timestamp'] = time();

        return $this->callRestful(self::RESTAPI_QUERYTOKENTAGS, $params);
    }
```
## 推送数据问题

**\[推送暂停\]**

* 全量推送限制(V2、V3)：
  1. 全量推送每小时最多只能创建30次推送，超过30次会推送失败。
  2. 相同内容的全量推送每小时只能推送一次，超过一次推送会推送失败。

* 标签推送限制(V3)：
  1. 同一应用每小时最多只能创建30次标签推送，超过30次会推送失败。
  2. 同一标签相同内容的推送每小时只能推送一次，超过一次推送会推送失败。


**\[效果统计\]**

* 次日：推送完第二天才能看到推送数据
* 实时：推送完马上可以看到推送数据。目前每周仅支持14次的实时数据统计

**\[实发量\]**

* 在消息离线保存时间内，有成功连接到信鸽服务器，并且有正常下发的量。（如：消息离线保存时间为3天，实发数据会在第四天稳定，数据会随着设备不断开启连接到信鸽服务器的数量而增加）

**\[历史明细\]**

* 历史明细只展示：全量推送、tag推送、和官网的号码包推送。（批量账号和批量设备暂不展示推送详情）

**\[数据概览\]**

* 展示的是当天的数据，某天的数据是在那一天中各种推送行为的推送总量。（分为单推，广播也就是批量和全量推送，通知栏消息和应用内消息四类）

## 消息点击事件以及跳转页面方法

---

由于目前SDK点击消息默认会有点击事件，默认的点击事件是打开主界面。所以在终端点击消息回调的「onNotifactionClickedResult」方法内设置跳转操作时，自定义的跳转和默认的点击事件造成冲突。结果是点击之后会跳转到指定界面过后再回到主界面，所以不能再「onNotifactionClickedResult」内设置跳转

**解决办法如下\(推荐使用第一种方式\)：**

**\[1\] 使用Intent来跳转指定页面（Android 3.2.3 以上版本使用此方式）**

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



## 信鸽Android SDK集成厂商通道相关问题

### 厂商通道功能支持

- 小米通道支持抵达回调，不支持点击回调，支持透传
- 华为通道不支持抵达回调，支持点击回调（需要自定义参数），支持透传（但忽略自定义参数）
- 魅族通道支持抵达回调，支持点击回调，不支持透传

**注：如果需要通过点击回调获取参数或者跳转自定义页面，可以通过使用Intent来实现，[点击查看教程](http://docs.developer.qq.com/xg/android_access/android_faq.html#%E6%B6%88%E6%81%AF%E7%82%B9%E5%87%BB%E4%BA%8B%E4%BB%B6%E4%BB%A5%E5%8F%8A%E8%B7%B3%E8%BD%AC%E9%A1%B5%E9%9D%A2%E6%96%B9%E6%B3%95)**

### 调试过程中可能遇到的otherpushToken = null的问题
*  4.X的otherpush版本检查是否开启厂商通道初始化代码，在你的Application的attachBaseContext函数里面增加

 ```
 StubAppUtils.attachBaseContext(context);
 ```
*  4.X的otherpush版本，等待云控成功下载对应设备的厂商dex包后，需杀死应用进程，并再次启动应用才能完成注册。下载完成的日志如下：
  ```xml
10-25 15:16:31.067 16551-16551/? D/XINGE: [DownloadService] onCreate()
10-25 15:16:31.073 16551-16757/? D/XINGE: [DownloadService] action:onHandleIntent
10-25 15:16:31.083 16551-16757/? V/XINGE: [CloudCtrDownload] Create downloadControl
10-25 15:16:31.089 16551-16757/? I/XINGE: [CloudCtrDownload] action:download - url:https://pingjs.qq.com/xg/Xg-Xm-plug-1.0.2.pack, saveFilePath:/data/user/0/com.qq.xgdemo1122/app_dex/XG/5/, fileName:Xg-Xm-plug-1.0.2.pack
10-25 15:16:31.097 16551-16757/? V/XINGE: [CloudCtrDownload] Download file: Xg-Xm-plug-1.0.2.pack
10-25 15:16:31.641 16551-16757/? D/XINGE: [DownloadService] download file Succeed
10-25 15:16:31.650 16551-16757/? D/XINGE: [CloudCtrDownload] Download succeed.
10-25 15:16:31.653 16551-16551/? D/XINGE: [CloudControlDownloadReceiver] onReceive
10-25 15:16:31.673 16551-16738/? I/test: Download file SuccessXg-Xm-plug-1.0.2.pack to /data/user/0/com.qq.xgdemo1122/app_dex/XG/5/
```
* 若始终无法下载dex配置包可采用非动态加载方式集成，需使用信鸽4.x不包含厂商通道版本jar，再集成各个厂商通道的jar，集成配置可参考文档。


**\[小米通道排查路径\]**

* 检查信鸽SDK版本是否为V3.2.0以上版本
* 根据开发文档检查manifest文件配置，尤其是需要修改包名的地方是否修改

```
<permission android:name="com.example.mipushtest.permission.MIPUSH_RECEIVE" android:protectionLevel="signature" />
<!-- 这里com.example.mipushtest改成app的包名 -->
<uses-permission android:name="com.example.mipushtest.permission.MIPUSH_RECEIVE" />
<!-- 这里com.example.mipushtest改成app的包名 -->
```

* 在信鸽注册前是否设置了小米的APPID和APPKEY，以及第三方推送有没有启动

```
//打开第三方推送
XGPushConfig.enableOtherPush(this,true);
// 设置小米的Appid和Appkey
XGPushConfig.setMiPushAppId(this,MIPUSH_APPID);
XGPushConfig.setMiPushAppKey(this,MIPUSH_APPKEY);
```

* APP包名是否和小米开放推送平台、信鸽管理台注册的包名一致


* 通过实现自定义的继承PushMessageReceiver的广播来监听小米的注册结果，查看注册返回码
* 启动logcat，观察tag为PushService的日志，看看有什么错误信息

**\[华为通道排查路径\]**

* 检查信鸽SDK版本是否为V3.2.0以上版本以及 华为手机中【设置】->【应用管理】->【华为移动服务】的版本信息是否大于2.5.3
* 按照开发文档华为通道接入指南部分检查manifest文件配置
* 在信鸽注册之前是否启动了第三方推送，以及华为APPID是否配置正确
* APP的包名和华为推送官网、信鸽管理台注册包名是否一致
* 在注册代码之前调用：XGPushConfig.setHuaweiDebug\(true\),手动确认给应用存储权限，然后查看SD卡目录下的huawei.txt文件内输出的华为注册失败的错误原因，然后根据华为开发文档对应的错误码查找原因
* cmd里执行adb shell setprop log.tag.hwpush VERBOSE和
  adb shell logcat -v time &gt; D:/log.txt 开始抓日志，然后进行测试，测完再关闭cmd窗口。将log发给技术支持

**\[魅族通道排查路径\]**

* 和小米通道的排查方法类似，参考小米通道的排查路径即可





