云函数（Serverless Cloud Function，SCF）提供代码部署、镜像部署两种部署方式，支持事件函数和 Web 函数两种函数类型。不同的部署方式以及函数类型在代码开发时需要采用不同的规范。本文主要介绍代码部署的事件函数的编写规范及相关概念，[镜像部署](https://intl.cloud.tencent.com/document/product/583/41076) 和 [Web 函数](https://intl.cloud.tencent.com/document/product/583/40688) 详情请参考对应文档。

SCF 事件函数有三个基本概念：执行方法、函数入参和函数返回。

<dx-alert infotype="notice" title="">
上述概念在通常的项目开发中分别对应：
**执行方法**：对应项目的主函数，是程序执行的起点。
**函数入参**：即通常理解的函数入参，但在云函数环境下，入口函数的入参为平台固定值，详情见 [函数入参](#input)。
**函数返回**：对应项目中主函数的返回值，函数返回后，代码执行结束。
</dx-alert>



## 执行方法
SCF 平台在调用云函数时，首先会寻找执行方法作为入口，执行用户的代码。此时，用户需以**文件名.执行方法名**的形式进行设置。
例如，用户设置的执行方法为 `index.handler`，则 SCF 平台会首先寻找代码程序包中的 `index` 文件，并找到该文件中的 `handler` 方法开始执行。
在执行方法中，用户可对入口函数入参进行处理，也可任意调用代码中的其他方法。SCF 的某个函数以入口函数执行完成或函数执行异常作为执行结束。


## 函数入参[](id:input)

函数入参，是指函数在被触发调用时所传递给函数的内容。通常情况下，函数入参包括 **event** 和 **context** 两部分，但根据开发语言和环境的不同，入参个数可能有所不同，详情请参见 [开发语言说明](https://intl.cloud.tencent.com/document/product/583/40190)。
<dx-tabs>
::: event 入参

#### 作用
event 参数类型为 dict，event 中包含了触发函数执行的基本信息，可以是平台定义的格式，也可以自定义格式。函数被触发开始执行后，可以在代码内部对 event 进行处理。
#### 使用说明
有两种方法可以触发云函数 SCF 执行：
1. 通过调用 [云 API](https://intl.cloud.tencent.com/document/product/583/17243) 触发函数执行。
2. 通过绑定 [触发器](https://intl.cloud.tencent.com/document/product/583/9705) 触发函数执行。 

SCF 两种触发方式对应两种event格式：
- 云 API 触发函数执行：
可以在调用方和函数代码之间自定义一个 dict 类型的参数。调用方按照定义好的格式传入数据，函数代码按格式获取数据。
**示例**：
定义一个 dict 类型的数据结构 {"key":"XXX"} ，当调用方传入数据 {"key":"abctest"} 时，函数代码可以通过 event[key] 来获得值 abctest。

- 触发器触发函数执行：
  SCF 和 API 网关、对象存储 COS、消息队列 Ckafka 等多种云服务打通，可以通过给函数绑定对应的云服务触发器触发函数执行。触发器触发函数时，event 会以一种平台预定义的、不可更改的格式作为 event 参数传给函数，您可以根据此格式编写代码并从 event 参数中获取信息。
  **示例**：
  通过对象存储 COS 触发函数时会将对象存储桶及文件的具体信息以 <a href="https://intl.cloud.tencent.com/document/product/583/9707">JSON 格式</a> 传递给 event 参数，在函数代码中通过解析 event 信息即可完成对触发事件的处理。
  :::
  ::: context 入参
#### 作用
context 为 SCF 平台提供的入参，将  context 入参传递给执行方法，代码可通过解析 context 入参对象，获取到运行环境及当前请求的相关信息。
#### 使用说明
SCF 提供的入参 context 包含的字段及含义如下：

<table>
<thead><tr><th align="left">字段名称</th><th align="left">描述</th></tr></thead>
<tbody>
<tr><td align="left"><code>memory_limit_in_mb</code></td><td align="left">函数配置内存</td></tr>
<tr><td align="left"><code>time_limit_in_ms</code></td><td align="left">函数执行超时时间</td></tr>
<tr><td align="left"><code>request_id</code></td><td align="left">函数执行请求 ID</td></tr>
<tr><td align="left"><code>environment</code></td><td align="left">函数命名空间信息</td></tr>
<tr><td align="left"><code>environ</code></td><td align="left">函数命名空间信息</td></tr><tr><td align="left"><code>function_version</code></td><td align="left">函数版本信息</td></tr>
<tr><td align="left"><code>function_name</code></td><td align="left"> 函数名称</td></tr><tr><td align="left"><code>namespace</code></td><td align="left">函数命名空间信息</td></tr>
<tr><td align="left"><code>tencentcloud_region</code></td><td align="left">函数所在地域</td></tr>
<tr><td align="left"><code>tencentcloud_appid</code> </td><td align="left">函数所属腾讯云账号 APPID</td></tr><tr><td align="left"><code>tencentcloud_uin</code></td><td align="left">函数所属腾讯云账号 ID </td></tr>
</tbody>
</table>



<dx-alert infotype="notice" title="">
为保证兼容性，context 中保留了 SCF 不同阶段对命名空间的描述方式。
 context 结构内容将会随着 SCF 平台的开发迭代而增加。
</dx-alert>


您可以在函数代码中通过标准输出语句打印 context 信息，以 `python` 运行环境为例：

``` Python
# -*- coding: utf8 -*-
import json
def main_handler(event, context):
    print(context)
    return("Hello World")
```

可得到以下context信息：
<dx-codeblock>
::: json
{"memory_limit_in_mb": 128, "time_limit_in_ms": 3000, "request_id": "f03dc946-3df4-45a0-8e54-xxxxxxxxxxxx", "environment": "{\"SCF_NAMESPACE\":\"default\"}", "environ": "SCF_NAMESPACE=default;SCF_NAMESPACE=default", "function_version": "$LATEST", "function_name": "hello-from-scf", "namespace": "default", "tencentcloud_region": "ap-guangzhou", "tencentcloud_appid": "12xxxxx384", "tencentcloud_uin": "10000xxxxx36"}
:::
</dx-codeblock>

:::

</dx-tabs>


了解 event 入参和 context 入参的基本用法后，在编写函数代码时您还需注意以下几点：
<ul>
	<li>为保证针对各开发语言和环境的统一性，event 入参和 context 入参均使用 `JSON` 数据格式统一封装。</li>
	<li>不同触发器在触发函数时，所传递的数据结构均有所不同。详情请参见 <a href="https://intl.cloud.tencent.com/document/product/583/9705">函数触发器说明</a>。</li>
		<li>当云函数不需要任何输入时，您可以在代码中忽略 event 和 context 参数。</li>
	</ul>

## 函数返回
SCF 平台会获取到云函数执行完成后的返回值，并根据下表中不同的触发方式进行处理。
<table>
	<tr>
	<th>触发方式</th>
	<th>处理方式</th>
	</tr>
	<tr>
	<td>同步触发</td>
	<td>
		<ul class="params">
<li>通过 API 网关、云 API 同步 invoke 触发函数的方式为同步触发。</li>
		<li>使用同步方式触发的函数在执行期间，SCF 平台不会返回触发结果。</li>
		<li>在函数执行完成后，SCF 平台会将函数返回值封装为 JSON 格式并返回给调用方。</li>
		</ul>
	</td>
	</tr>
	<tr>
	<td>异步触发</td>
	<td>
		<ul class="params">
	<li>使用异步方式触发的云函数，SCF 平台接收触发事件后，会返回触发请求 ID 。</li>
			<li>在函数执行完成后，函数的返回值会封装为 JSON 格式并存储在日志中。</li>
			<li>用户可在函数执行完成后，通过返回的请求 ID 查询日志获取该异步触发函数的返回值。</li>
		</ul>
	</td>
	</tr>
</table>

当函数中的代码返回具体值时，通常返回特定的数据结构。例如 ：

<table>
<tr>
<th>运行环境</th>
<th>返回数据结构类型</th>
</tr>
<tr>
<td>Python</td>
<td>简单数据结构或 <code>dict</code> 数据结构</td>
</tr>
<tr>
<td>Node.js</td>
<td> <code>JSON Object</code></td>
</tr>
<tr>
<td>PHP</td>
<td><code>Array</code> 结构</td>
</tr>
<tr>
<td>GO</td>
<td>简单的数据结构或带有 JSON 描述的 <code>struct</code></td>
</tr>
</table>

为保证针对各开发语言和环境的统一性，函数返回会使用 **JSON 数据格式统一封装**。SCF 平台在获取到例如以上运行环境函数的返回值后，将会对返回的数据结构进行 JSON  化，并返回 JSON 内容到调用方。
>!
>- 需确保函数的返回值均可被 JSON 化，若直接返回对象且不具备 JSON 化方法，将会导致 SCF 平台在 JSON 化操作时失败并报错。
>- 例如以上运行环境的返回值，无需在 return 前自行 JSON 化，否则会导致输出的字符串会进行再次 JSON 化。


## 异常处理
若函数在调试和运行过程中出现异常，SCF 平台会尽最大可能捕获异常并将异常信息写入日志中。函数运行产生的异常包括捕获的异常（Handled error）和未捕获的异常（Unhandled Error）。

### 处理方式


您可以前往 [SCF 控制台](https://console.cloud.tencent.com/scf/index) 按照以下步骤进行异常处理测试：
1. 新建函数并复制以下函数代码，不添加任何触发器。
2. 单击控制台**测试**，选择 “Hello World” 测试示例进行测试。

本文提供以下三种抛出异常方式，您可根据实际需求选择在代码中进行异常处理。
<dx-tabs>
::: 显式抛出异常

**示例**

```python
def always_failed_handler(event,context):
    raise Exception('I failed!')
```
**说明**
此函数在运行过程中将引发异常，返回以下错误信息，SCF 平台会将此错误信息记录到函数日志中。

```
File "/var/user/index.py", line 2, in always_failed_handler
raise Exception('I failed!')
Exception: I failed!
```
:::
::: 继承 Exception 类

**示例**

```python
class UserNameAlreadyExistsException(Exception): pass
def create_user(event):
    raise UserNameAlreadyExistsException('
		The username already exists,
		please change a name!')
```

**说明**

您可以在代码中自行定义错误的处理方式，保障应用程序的健壮性和可扩展型。

:::
::: 使用 Try 语句捕获错误

**示例**

```python
def create_user(event):
    try:
        createUser(event[username],event[pwd])
    except UserNameAlreadyExistsException,e: //catch error and do something
```

**说明**

您可以在代码中自行定义错误的处理方式，保障应用程序的健壮性和可扩展型。

:::
</dx-tabs>

### 返回错误信息
当用户的代码逻辑中未进行异常处理及错误捕获时，SCF 平台会尽可能的捕获错误。例如，用户函数在运行过程中突然崩溃退出，当出现此类平台也无法捕获错误的情况时，系统将会返回一个通用的错误信息。
下表展示了代码运行中常见的一些错误：

| 错误场景            | 返回消息                                                     |
| ------------------- | ------------------------------------------------------------ |
| 使用 raise 抛出异常 | {File "/var/user/index.py", line 2, in always_failed_handler raise Exception('xxx') Exception: xxx} |
| 处理方法不存在      | {'module' object has no attribute 'xxx'}                     |
| 依赖模块并不存在    | {global name 'xxx' is not defined}                           |
| 超时                | {"time out"}                                                 |

## 日志
SCF 平台会将函数调用的所有记录及函数代码中的全部输出存储在日志中，请使用编程语言中的打印输出语句或日志语句生成输出日志，方便调试及故障排除时使用。详情见 [日志管理](https://intl.cloud.tencent.com/document/product/583/39777)。


## 注意事项
由于 SCF 的特点，您须以**无状态**的风格编写您的函数代码。本地文件存储等函数生命周期内的状态特征，在函数调用结束后将随之销毁。
因此，持久状态建议存储在关系型数据库 TencentDB、对象存储 COS、云数据库 Memcached 或其他云存储服务中。

## 开发流程
了解更多云函数开发流程，请参见 [使用流程](https://intl.cloud.tencent.com/document/product/583/9179)。




<style>
	.params{
		margin-bottom:0px !important;
	}
</style>
