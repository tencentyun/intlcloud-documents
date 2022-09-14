如果您想将输入实时的送入StreamLive，但是又不想让系统立马处理并且进行输出展示，那该场景非常适合使用延播功能。延播是指系统根据指定的时间Hold住输入源，达到指定的延迟时间后才将Input输入到系统中进行转码处理，并且封装为指定的Output。目前仅对RTMP_PUSH输入协议类型支持延播。开启Delay的步骤非常简单：
1. 首先选择需要延播的**Input**，进入到编辑功能，若该Input当前处于绑定中且在被使用，需要先Stop Channel。
![](https://qcloudimg.tencent-cloud.cn/raw/9b45272668f6d18330fc932df4c9a4d0.png)
2. 可以看到上图中的**Delay**默认是OFF的状态，点击**Edit**，打开**Delay**开关，可以看到此时可以设置延播时长，单位是秒，最小10秒，最大600秒。
![](https://qcloudimg.tencent-cloud.cn/raw/65f41a79185c43c1a3c7ab76bd192f53.png)

设置完成后点击**Confirm**，将开始生效，此时的Input将不会马上产生Output，而是在指定时长后在开始进行媒体处理。

