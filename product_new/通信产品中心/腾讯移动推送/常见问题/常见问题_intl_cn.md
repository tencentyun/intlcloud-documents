
#常见问题


**问：iOS开发环境可以收到推送，为什么生产环境打包后收不到了？**

```
答：
1. 检查打包后是否缺少这个文件“ archived-expanded-entitlements.xcent”，
此时可能还会报错：

No valid 'aps-environment' entitlement string found for application 'com.xxx.xxx': (null).

解决方法：找到 TARGET -> Build Setting -> Code Signing Identity -> Code Signing Entitlements
 看看有没有 aps-environment 字段,没有的话可以加上。 
<plist version="1.0">
<dict>
	<key>aps-environment</key>
	<string>development</string>
</dict>
</plist>

```

**问: 生产环境推送收不到？**


答: 生产环境的测试满足条件：App是ad-hoc打包/App Store版本（发布证书 Production），上传了发布证书并验证通过。


**问: iOS token 失效的原因？**

答: <br>
（1）系统注销或者是应用被卸载<br>
（2）用户在新的设备上安装App<br>
（3）用户从backup中恢复设备<br>
（4）用户重新安装OS<br>
（5）其他系统定义的事件(1.调用unregisterNotification接口之后再注册通知，清除device data and settings)

**问: 集成小米通道的设备，为什么只能显示一条推送消息？**

答: 小米官网文档指明：默认情况下，通知栏只显示一条推送消息。如果通知栏要显示多条推送消息，需要针对不同的消息设置不同的notify_id（相同notify_id的通知栏消息会覆盖之前的消息）。信鸽官网的参数为：n_id。


**问: 设备通知栏展示消息的条数有没有限制，为什么消息抵达了设备却没有展示？**


答:<br> 手机接收并展示通知栏消息的条数没有限制，没有展示出来可能的原因是：<br>
（1）小米手机的通知栏消息是展示最新的一条，如果每条都要展示 需要设置n_id。<br>
（2）消息广播被手机管家屏蔽了。<br>
（3）魅族手机有一个消息盒子，一些不常用的消息会直接进入到消息盒子中，可以在消息盒子中查看。


**问: 如何设置自定义铃声？**


答:<br>
1. 管理台设置方法：推送通知->高级设置->提醒方式->声音->自定义（android选择位于raw目录下的铃声文件，铃声文件不需要后缀名，例如 ：xg_ring。iOS选择bundle 目录下的铃声文件，需要后缀名，例如：xg_ring.wav）<br>
2. Rest API V3设置方法： android在推送的消息体中设置ring=1，同时设置ring_raw为指定Android工程里raw目录中的铃声文件名，不需要后缀名。iOS在推送的消息体中设置sound为指定工程里bundle目录中的铃声文件名，需要后缀。<br>
注意：如客户端集成厂商通道，由于华为和魅族的厂商的限制，厂商手机无法使用自定义声音文件，默认使用系统音效；小米目前已经适配自定义铃声。


**问: 如何自定义状态栏小图标？**

答: 原生Android 5.0以上的ROM都会对target sdk大于等于21的app的小图标做处理, 加了一层颜色,导致图标变灰。如果要显示成有颜色的, 需要把target sdk设成低于21,如果不想target sdk设成低于21,可以将一张背景透明的的png格式小图片名字改成notification_icon.png,放在drawable里，这样显示的小图标就是灰色的但是有形状的。


**问: 应用关闭或结束进程后，还能收到推送消息吗？**


答：<br>
（1）信鸽通道推送主要依赖信鸽的service进行消息的收发，杀死进程之后信鸽service也被杀死，只能等待service被拉活或重启app才可以收到推送。若手机中有其他接入信鸽的app被打开，则可以利用其他app的service接收消息，但共享service通道也受手机ROM限制，无法保证百分之百的成功率。<br>
（2）厂商通道支持结束进程后收到推送消息。


**问:Android版本4.4.4编译报错，找不到XGPushProvider、MidProvider？**

答: 由于工程加载方法数超过65K,请对工程做分包处理



**问: 设备注册为什么收不到回调信息？**


答: 

(1)厂商通道的回调是厂商服务器返回的。<br>

(2)检查是否有安全软件拦截广播。


**问: 账号在设备A上登录过，又在设备B上登录？给这个账号发信息会怎么样？**


答: 设备B上能够收到推送，设备A无法收到推送。只有最后一个绑定该账号的设备可以收到推送。


**问：指定打开某个activity页面，但经常不能正常跳转**

```
答：在部分手机，通知栏跳转到某个页面可能会出现权限问题
处理方法：在androidManifest.xml中，需要打开的activity加上android:exported="true"
```

**问: 用户重连上线后收到多条push的顺序是怎样？**

答: 按照消息ID递增。客户端也是按照此规则收取消息，因此，收消息的顺序就是发消息的顺序

**问: 如果定时push选择的是过去的时间，是不是不会push出去？**

答: 不是，选择过去的时间系统则会立刻发送


**问：注册方法能不能放到线程里创建，能不能在APPLICATON onCreate里就创建?**

答：注册方法可以在任何地方调用，但注意要传递applicationContext

























