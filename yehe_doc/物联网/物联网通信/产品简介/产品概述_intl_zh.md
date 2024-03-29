

腾讯云物联网通信（Internet of Things Hub， IoT Hub）旨在提供一个安全、稳定、高效的连接平台，帮助开发者低成本、快速地实现“设备-设备”、“设备-用户应用”、“设备-云服务”之间可靠、高并发的数据通信。不仅可以实现设备之间的互动、设备的数据上报和配置下发，还可以基于规则引擎和腾讯云产品打通，方便快捷地实现海量设备数据的存储、计算以及智能分析。


## 产品架构

![](https://main.qcloudimg.com/raw/21942c660de60fe6346c38e272785ccf.png)



### 接入腾讯云物联网通信
用户设备可使用 SDK 接入腾讯云物联网通信。底层数据传输基于 MQTT 或 CoAP 协议，可以有效减少网络带宽。安全方面引入网络安全传输协议（TLS、DTLS），可以防范非法接入和数据窃取、篡改等风险。介于设备资源和使用场景的多样性，支持选择非对称（设备证书加密验证、适用高安全要求场景）和对称加密（密钥加密验证、适用资源受限设备）方式。

### 用户设备基于 SDK 进行消息的发布和订阅
为了实现设备数据安全隔离，目前腾讯云限制设备只能发布和订阅自身 topic ，但可以通过配置规则引擎实现设备与其他实体的消息互通。

### 用户可以在控制台配置规则引擎实现设备与其他实体的消息互通
目前规则引擎支持类 SQL 语法操作，可通过 repub（重新发布消息）实现设备之间的消息通信能力、forward（转发消息到用户服务器）实现设备消息转发第三方服务。同时支持设备消息转发到云数据库、时序数据库、消息队列等腾讯云其他产品（无服务器云函数、大数据分析套件、大数据可视交互系统、商业智能分析等打通功能也在建设中）。

### 打通设备消息与第三方服务
作为设备的唯一接入方，物联网通信平台通过开通消息队列服务，可快速将设备指定消息写入腾讯云 CMQ、CKafka 队列，第三方服务通过 CMQ、CKafka 队列 SDK 取用消费数据，实现设备与第三方服务的异步消息通信。

### 用户可以基于设备影子实现设备与应用之间配置数据、状态数据的双向同步
一方面，用户可以通过云 API 将配置参数设置到设备影子里，设备在线或上线时，都可以从设备影子获取配置参数。 另一方面，设备可以将最新状态上报到设备影子。用户查询设备状态时，只需查询设备影子，而不必与设备进行直接网络通信。


### 用户可以通过云 API 实现设备管理
对于物联场景下设备的管理能力，提供便捷的 SDK 工具，可在后台快速、批量化创建、查询、操作设备，提高效率。当前支持 Python、PHP、Java 工具包。

