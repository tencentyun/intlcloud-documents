MediaConnect控制台基于Flow维度进行管理，每一个Flow都对应一个流的传输链路。基于MediaConnect的控制台能可快速稳定地传输视频流媒体，同时还可对传输过程中的视频流进行全方位的质量监控。

## 一、 选择Region


Region表示您Flow传输链路的起始点，您可在开始使用前于控制台顶部选择可用区。目前控制台操作界面上可选择亚洲、欧洲、美西等多个区域的多个节点，需要更多的节点部署及支持欢迎随时[联系我们](https://intl.cloud.tencent.com/contact-sales)。

## 二、 主界面

![](https://main.qcloudimg.com/raw/ede8fc9543079f0ed9ae11af6c3e7867.png)

MediaConnect主界面会显示所有您创建的Flow以及其运行状态，每一路Flow支持主备流输入，您可以同时推送主备两路流，以保证您传输过程中的稳定性。点击右侧操作中的启动/停止，您可启动/暂停您的传输行为，正在传输过程中的Flow不允许删除。

## 三、 新建Flow

点击控制台上方的 Create Flow 按钮可新建一条传输链路，您可在此设置Flow的Name，并选择传输流的`最大带宽`（目前支持10Mbps、20Mbps、50Mbps）。
接着您还需要配置输入源的相关信息：在选择传输协议后，您需要设置Latency参数，此参数影响Server的发送以及接收buffer的大小，当网络状况不好时建议调大此参数。控制台默认会设置该参数为120ms，您可结合您的实际需求进行更改。

>? Latency 可以对创建后给出的IP地址进行ping 测试，确定最佳设置再进行修改。另外也可以直接使用默认值，然后调整发送侧的Latency即可达到相同的目的。 

![](https://main.qcloudimg.com/raw/cc8fa08079c4b37902ac8ce9aa707b4e.png)

MediaConnect支持SRT协议的加解密传输，如果您推送至MediaConnect的流为加密后的传输流，您可打开解密配置填入Decryption key，并选择Key Length以供我们对您上行的流进行解密。

![](https://main.qcloudimg.com/raw/fa39d86e4fd351e94421b0b9a44e4cb8.png)

同时您可设置输入源的IP白名单（CIDR格式），只能通过白名单中的IP向此Flow进行推流。
您也可对Flow的输入源配置一些描述信息，以便于您对不同的输入源进行区分开来。
点击Create后，Flow就创建完毕了，我们会您创建的Flow自动生成主备两个通道的输入IP地址，您可以向此地址进行推流操作。

> ! 在未创建outputs节点时无法开启使用

## 四、 查看Flow

在主页面点击您刚创建的Flow名称可进入Flow详情查看界面。您可在此查看Flow的信息、输入源状况并配置您的Flow 输出节点。
点击右上角的edit按钮可对您的Flow进行二次编辑。

![](https://main.qcloudimg.com/raw/d6897c517e505289ee4a97ff2b74941f.png)

## 五、 Outputs

您可在Flow的详情页-Outputs tab中查看您所有的outputs节点信息，也可新建/删除/编辑一个output节点。

> ! 运行中的Flow无法进行此操作

![](https://main.qcloudimg.com/raw/58635595342363458b60bcd704641a60.png)

点击新建output，您可新建一个output。MediaConnect支持一路多出的设置，针对一个Flow的输入源您可配置不同region的输出节点。

![](https://main.qcloudimg.com/raw/2bc94f3f111e3b9087bf1184ca2da641.png)

MediaConnect支持传输协议的转封装，您可在创建output时选择您输出的协议。当您选择SRT协议时，您需要填写`目的地的IP地址`和`端口`（主和备）。同样您还可在此填写`延迟设置`，默认为120ms，您可根据您业务的实际需求进行更改。

>! Output节点的主流与备流通道各自独立，与输入源的主备通道一一对应。即您朝着Flow主通道推的流经过MediaConnect传输后会通过主目的地地址进行输出，而朝着Flow备通道推的流经过MediaConnect传输后会通过备目的地地址进行输出，两者各自独立。
> 其中主输出地址为必填项，备输出地址为选填项。

如果您需要对SRT协议的输出流进行加密，您可在此开启加密设置，同样您需要填写加密密钥并选择密钥长度。

![](https://main.qcloudimg.com/raw/d1db5d2467bc2407a49e0c7cbb037853.png)

而当您选择RTMP协议进行输出时，您需要填写`目的地的URL`及`Stream Key`（主和备），主备通道的逻辑同上。

![](https://main.qcloudimg.com/raw/60eb05dc28c112e7f0bc22c9dcb6ae94.png)

## 六、 启动/停止Flow

完成Flow及Outputs节点的创建后，点击启动即可成功运行Flow。当使用完毕后，点击停止即可停止运行Flow。
![](https://main.qcloudimg.com/raw/160685a685708d2aacb24ff28c3a8bbc.png)
