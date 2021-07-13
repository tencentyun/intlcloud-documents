Serverless 应用基于 Serverless Framework 部署，支持的 CLI 命令如下：

- <b>`serverless registry`</b>：查看可用的 Components 列表。

- <b>`serverless registry publish`</b>：发布 Component 到 Serverless 注册中心。

   `--dev`：支持 dev 参数用于发布 `@dev` 版本的 Component，用于开发或测试。

- <b>`serverless init xxx`</b>：从注册中心下载指定模版，init 后填入您想下载的模版名称，例 "$ serverless init fullstack"
  
    `sls init xxx --name my-app`：支持自定义项目目录名称。
	
	 `--debug`：列出模版下载过程中的日志信息。

- <b>`serverless deploy`</b>：部署 Component 实例到云端。

    `--debug`：列出组件部署过程中 `console.log()` 输出的部署操作和状态等日志信息。

    `---inputs publish=true`：部署时函数发项目所有函数发版本。

    `---inputs traffic=0.1`：部署时切换10%流量到 $latest 函数版本，其余流量到最后一次发的函数版本上。

    >?旧版本命令为`sls deploy --inputs.key=value`，Serverless CLI V3.2.3 后命令统一格式为 `sls deploy --inputs key=value` ，旧版本命令在新版本 Serverless CLI 中不可用，升级 Serverles CLI 的用户请使用新版本命令。

- <b>`serverless remove`</b>：从云端移除一个 Component 实例。

    `--debug`：列出组件移除过程中 `console.log()` 输出的移除操作和状态等日志信息。

- <b>`serverless info`</b>：获取并展示一个 Component 实例的相关信息。

   `--debug`：列出更多 `state`。

- <b>`serverless dev`</b>：启动 DEV MODE 开发者模式，通过检测 Component 的状态变化，自动部署变更信息。同时支持在命令行中实时输出运行日志，调用信息和错误等。此外，支持对 Node.js 应用进行云端调试。

