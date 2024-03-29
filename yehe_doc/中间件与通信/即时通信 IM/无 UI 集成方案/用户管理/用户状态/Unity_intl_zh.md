## 功能描述

从 Native SDK 6.3 版本开始，IMSDK 提供了用户状态管理的功能，每个用户拥有两种不同类型的状态：

* 普通状态。SDK 内置状态，客户无法直接修改。
* 自定义状态。客户自定义的状态，可以自行修改。利用自定义状态，您可以对该帐号设置诸如“听歌中”、“通话中”等一些自定义信息。

> ? 用户状态针对的是当前用户，跟设备无关。如果有多台设备同时登录同一个帐号，不支持按设备查询、设置状态。

用户的普通状态有以下 3 种：
* 在线（ONLINE）：当前用户已登录上线，可以正常收发消息。
* 离线（OFFLINE）：用户未主动调用 `logout` ([点击查看详情](https://comm.qq.com/im/doc/unity/zh/api/loginOrlogout/Logout.html)) 退出登录，但长连接中断的状态。通常情况下，此时可以接收到离线推送的消息。
* 未登录（UNLOGINED）：用户注册帐号后从未登录过，或者用户主动调用 `logout` 退出登录。

关于离线状态，需要注意的是：
1. App 登录过程中杀进程或者网络异常中断（例如 4G/Wifi 切换、电梯信号弱等），此时帐号会处于离线状态。
2. App 登录后按 Home 键进入后台，如果 App 进程被系统 kill，此时帐号会处于离线状态。如果 App 进程处于后台保活，此时帐号仍然是在线状态。
3. 在线/离线的状态切换，依赖于 IMSDK 与后台服务之间的 TCP 长连接。当客户端处于飞行模式、网络彻底中断或者某些设备厂商不支持时，可能会出现 TCP 协议的 FIN 包或 RST 包无法发出的现象，从而导致无法立即切换成离线状态。但由于后台服务接收不到心跳包，400 秒后依然会将当前用户状态设置为离线状态。

> !
>
> - 下文所述的**部分功能**仅旗舰版客户支持，使用前请确认。
> - 下文所述的**部分功能**需要在  [即时通信 IM 控制台](https://console.cloud.tencent.com/im) 打开对应的用户状态开关，使用前请确认。

[](id:set)

## 设置自己的自定义状态
您可以调用接口 `SetSelfStatus`([点击查看详情](https://comm.qq.com/im/doc/unity/zh/api/UserApi/SetSelfStatus.html)) 设置 `current_user_status` 字段来设置自己的自定义状态。
如果您提前调用 `SetUserStatusChangedCallback`([点击查看详情](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetUserStatusChangedCallback.html)) 添加了 SDK 监听器，设置成功后会触发 `UserStatusChangedCallback`（[点击查看详情](https://comm.qq.com/im/doc/unity/zh/callback/UserStatusChangedCallback.html)) 回调。
`UserStatusChangedCallback` 的使用参见下文的 [状态变更通知](#notify)。

自定义状态清除机制：
1. 您可以在调用 `SetSelfStatus` 接口时，设置 `current_user_status` 为空来主动清除状态。
2. 当 SDK 监测到当前帐号处于离线状态后，会自动清除自定义状态，此时也会触发状态变更通知。

> ?
> 1. 调用 `SetSelfStatus` 不需要升级到旗舰版，也无需开启控制台开关。
> 2. 本接口不做限频控制。

示例代码如下所示：

```c#
    // 设置用户状态
    UserStatus status = new UserStatus
    {
      user_status_identifier = "userID",
      user_status_status_type = TIMUserStatusType.kTIMUserStatusType_Online
    };
    TIMResult res = TencentIMSDK.SetSelfStatus(status, (int code, string desc, string result, string user_data)=>{
      // 设置用户状态异步结果
    });
```


[](id:get)
## 查询用户状态
您可以调用 `GetUserStatus` ([点击查看详情](https://comm.qq.com/im/doc/unity/zh/api/UserApi/GetUserStatus.html)) 接口查询自己和其他用户的状态，接口会返回被查询者的普通状态和自定义状态。

[](id:getMyselfStatus)
### 查询自己的状态
调用 `GetUserStatus`，设置 `identifier_array` 仅包含自己的 userID，可查询自己的状态。

> ?
> 1. 查询自己的状态不需要升级到旗舰版，也无需开启控制台开关。
> 2. 查询自己的状态不做接口限频控制。

示例代码：

```c#
  // 查询用户状态
    TIMResult res = TencentIMSDK.GetUserStatus(new List<string> {"userID1"}, (int code, string desc, List<UserStatus> results, string user_data)=>{
      // 查询用户状态异步结果
    });
```

[](id:getOthersStatus)
### 查询其他人的状态
设置 `identifier_array` 为其他人的 userID 列表，可查询其他人的状态。

> ?
> 1. 查询其他用户状态需要升级到旗舰版套餐，详情请参见 [基础服务详情](https://intl.cloud.tencent.com/document/product/1047/34350)。
> 2. 查询其他用户状态需要提前在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) 开启 “用户状态查询及状态变更通知”。不开启，调用 `GetUserStatus` 会报错。
> <img src="https://qcloudimg.tencent-cloud.cn/raw/1adfc878b14e6a6a62de3a7db159b0a6.png" style="zoom:30%;"/>
> 3. 接口限频默认为 5 秒 20 次请求，单次查询最大用户数不超过 500 人。

[](id:subscribe)
## 订阅用户状态
您可以调用接口 `SubscribeUserStatus`([点击查看详情](https://comm.qq.com/im/doc/unity/zh/api/UserApi/SubscribeUserStatus.html)) 订阅指定用户的状态。IM SDK 默认只支持订阅 200 个用户，当超过限制后，会淘汰掉最早订阅的用户。
当您所订阅的用户状态变更时（包括普通状态和自定义状态），您可以在 `UserStatusChangedCallback`([点击查看详情](https://comm.qq.com/im/doc/unity/zh/callback/UserStatusChangedCallback.html)) 回调中收到该用户的状态变更通知。

接口特性：

1. 该接口不支持订阅自己的状态。如果您想感知自己的状态变更，可直接监听 `UserStatusChangedCallback` 回调。详情请参见下文的 [状态变更通知](#notify)。
2. 该接口支持订阅好友的状态，订阅好友会占用上述 200 个用户的名额。
 * 如果您关心所有好友的状态，不需要调用本接口，直接在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) 开启好友状态自动通知开关，开启后可以在 `UserStatusChangedCallback` 回调中收到所有好友的状态变更通知。
好友状态自动通知开关如下图所示：
<img src="https://qcloudimg.tencent-cloud.cn/raw/17b70799301407e46b14ca144646eb98.png" style="zoom:30%;"/>
 * 如果您仅关心部分好友的状态，只能调用 `SubscribeUserStatus` 主动订阅。订阅后可以在 `UserStatusChangedCallback` 回调中所订阅的好友的状态变更通知。

> ?
> 1. 订阅用户状态需要升级到旗舰版套餐，详情请参见 [基础服务详情](https://intl.cloud.tencent.com/document/product/1047/34350)。
> 2. 订阅用户状态需要提前在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) 开启 ”用户状态查询及状态变更通知“。如果开关关闭，调用 `SubscribeUserStatus` 会报错。
> <img src="https://qcloudimg.tencent-cloud.cn/raw/1adfc878b14e6a6a62de3a7db159b0a6.png" style="zoom:30%;"/>
> 3. 接口限频默认为 5 秒 20 次请求，单次订阅最大用户数不超过 100 人。

示例代码如下所示：
```c#
    // 订阅用户状态
    TIMResult res = TencentIMSDK.SubscribeUserStatus(new List<string> {"userID1"}, (int code, string desc, string result, string user_data)=>{
      // 订阅用户状态异步结果
    });
```

[](id:unsubscribe)
## 取消订阅用户状态
如果您不想接收用户的状态变更通知，可以调用接口 `UnsubscribeUserStatus` ([点击查看详情](https://comm.qq.com/im/doc/unity/zh/api/UserApi/UnsubscribeUserStatus.html)) 取消订阅用户的状态或清空订阅列表。
如果您不主动清空订阅列表，当帐号离线或者退出登录后，IMSDK 默认延迟一段时间后自动清空订阅列表。

取消订阅用户状态的接口限制，跟 [订阅用户状态](#subscribe) 接口限制一致，详情请参考上文。

示例代码如下所示：

```c#
    // 取消订阅用户状态
    TIMResult res = TencentIMSDK.UnsubscribeUserStatus(new List<string> {"userID1"}, (int code, string desc, string result, string user_data)=>{
      // 取消订阅用户状态异步结果
    });
```


[](id:notify)
## 状态变更通知
根据您希望感知用户状态的类型，可以将状态变更分为 3 种：
1. 感知自己的状态变更。
2. 感知好友的状态变更。
3. 感知用户（非好友）的状态变更。

上述 3 种方式的状态变更通知，都是通过 `UserStatusChangedCallback` ([点击查看详情](https://comm.qq.com/im/doc/unity/zh/callback/UserStatusChangedCallback.html)) 回调出来，但不同类型的用户触发该通知的方式不同。

### 自己的状态变更通知
如果您提前调用 `SetUserStatusChangedCallback` 添加了 SDK 监听器，设置成功后，当自己的状态发生变更时，会触发 `UserStatusChangedCallback` 回调，您可以在其中获取到自己的最新状态。

### 好友的状态变更通知
1. 如果您在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) 开启了好友状态自动通知，当好友的状态发生变更时，会自动触发 `UserStatusChangedCallback` 回调。
2. 如果您没有开启好友状态自动通知，但仍然想感知好友的状态变更，需调用 `SubscribeUserStatus` 主动订阅好友状态。当好友的状态发生变更时，会自动触发 `UserStatusChangedCallback` 回调。
`SubscribeUserStatus` 的使用有限制，参考上文 [订阅用户状态](#subscribe)。
3. 如果您既没有开启好友状态自动通知，也没有调用 `SubscribeUserStatus` 主动订阅好友状态，那么当好友状态发生变更时，您将无法感知到。

### 普通用户（非好友）的状态变更
如果您希望感知普通用户（非好友）的状态变更，只能调用 `SubscribeUserStatus` 主动订阅。当该用户状态发生变更时，会触发 `UserStatusChangedCallback` 回调。
`SubscribeUserStatus` 的使用有限制，参考上文 [订阅用户状态](#subscribe)。

示例代码如下：

```c#
    //设置用户状态变更通知回调
    TencentIMSDK.SetUserStatusChangedCallback((List<UserStatus> json_user_status_array, string user_data)=>{
      // 处理回调逻辑
    });
```

### 状态变更通知多端同步
如果您开启了多端登录（参考 [多端登录](https://intl.cloud.tencent.com/document/product/1047/34419))，同一个帐号可以在不同设备上登录。当其中一个设备上所登录的用户的状态发生变更时，后台会给其他登录的设备也下发 `UserStatusChangedCallback` ([点击查看详情](https://comm.qq.com/im/doc/unity/zh/callback/UserStatusChangedCallback.html)) 通知。

[](id:limit)

## 接口限制

### 套餐包限制
* `SetSelfStatus` 接口不限制旗舰版。
* `GetUserStatus` 查询自己的状态，不限制旗舰版。
* `GetUserStatus` 除了查询自己外的其他能力，均需要升级到旗舰版。
* `SubscribeUserStatus` / `UnsubscribeUserStatus` 接口的所有能力，均需要升级到旗舰版


### 接口限频
* `SetSelfStatus` 接口不限频。
* `GetUserStatus` 查询自己的状态，不限频。
* `GetUserStatus` 除了查询自己的状态外，默认限制 5 秒 20 次请求，单次查询最大用户数不超过 500。
* `SubscribeUserStatus` 接口，默认限制 5 秒 20 次请求，单次订阅最大用户数不超过 100。
* `UnsubscribeUserStatus` 接口，默认限制 5 秒 20 次请求，单次取消订阅最大用户数不超过 100。


## 常见问题

### 调用订阅/取消订阅接口时，接口提示 ”72001“ 的错误码

72001 错误码表示在控制台上并没有开启对应的能力，请登录  [即时通信 IM 控制台](https://console.cloud.tencent.com/im)  打开对应的功能开关。
