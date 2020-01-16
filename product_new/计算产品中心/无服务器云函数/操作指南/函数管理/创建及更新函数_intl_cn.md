
通过控制台或腾讯云命令行均可以完成函数创建。


## 通过控制台创建函数

1. 登录 [无服务器云函数控制台](https://console.cloud.tencent.com/scf)，在左侧选择函数服务。
2. 在主界面上方选择期望创建函数的地域。单击【新建】按钮，进入函数创建流程。
3. 可选择使用【空白函数】或选择使用【函数模板】来新建函数。
 - 使用【空白函数】时，通过填写必填的函数名称、运行环境来完成函数的创建。
 - 使用【函数模板】时，通过填写必选的函数名称即可创建函数，运行环境等配置依赖函数模板中的配置来创建。

## 通过腾讯云命令行创建函数

在使用腾讯云命令行前，可以通过 [命令行安装及配置](https://intl.cloud.tencent.com/document/product/1013/33463) 方法完成命令行的安装和配置。
使用`tccli scf CreateFunction`命令即可完成函数创建。

### 通过本地 zip 包创建函数

如下示例为通过本地 zip 包完成函数创建。
首先将命名为 hello.zip 的 zip 包转变为 base64 编码并 URL Encode ：
```
$ alias urlencode='python -c "import sys, urllib as ul;print ul.quote_plus(sys.argv[1])"'
$ urlencode `base64 -i hello.zip` 
UEsDBBQACAAIAFaEJU0AAAAAAAAAAAAAAAAIABAAaW5kZXgucHlVWAwAQpWPWyOVj1v2ARQAU07OT8nMS7ctLUnTteDiSklNU8hNzMzTSC1LzSvRUUjOzytJrSjRtOJSAIKCosy8Eg2ljNScnHyF8vyinBQlTSQJsB6IQFFqSWlRngJYhAsAUEsHCAg25ABRAAAAZAAAAFBLAwQKAAAAAABnhCVNAAAAAAAAAAAAAAAACQAQAF9fTUFDT1NYL1VYDABClY9bQpWPW%2FYBFABQSwMEFAAIAAgAVoQlTQAAAAAAAAAAAAAAABMAEABfX01BQ09TWC8uX2luZGV4LnB5VVgMAEKVj1sjlY9b9gEUAGNgFWNnYGJg8E1MVvAPVohQgAKQGAMnEBsBcR0Qg%2FgbGIgCjiEhQVAmSMcCIBZAU8KIEJdKzs%2FVSywoyEnVy0ksLiktTk1JSSxJVQ4IBik0mtofDaIPhAvogWgAUEsHCAyTbm5cAAAAsAAAAFBLAQIVAxQACAAIAFaEJU0INuQAUQAAAGQAAAAIAAwAAAAAAAAAAECkgQAAAABpbmRleC5weVVYCABClY9bI5WPW1BLAQIVAwoAAAAAAGeEJU0AAAAAAAAAAAAAAAAJAAwAAAAAAAAAAED9QZcAAABfX01BQ09TWC9VWAgAQpWPW0KVj1tQSwECFQMUAAgACABWhCVNDJNublwAAACwAAAAEwAMAAAAAAAAAABApIHOAAAAX19NQUNPU1gvLl9pbmRleC5weVVYCABClY9bI5WPW1BLBQYAAAAAAwADANIAAAB7AQAAAAA%3D
```

然后通过生成的 base64 编码的内容来创建函数：
```
$ tccli scf CreateFunction --FunctionName testclifunc --Handler index.main --Runtime Python2.7 --Code '{"ZipFile":"UEsDBBQACAAIAFaEJU0AAAAAAAAAAAAAAAAIABAAaW5kZXgucHlVWAwAQpWPWyOVj1v2ARQAU07OT8nMS7ctLUnTteDiSklNU8hNzMzTSC1LzSvRUUjOzytJrSjRtOJSAIKCosy8Eg2ljNScnHyF8vyinBQlTSQJsB6IQFFqSWlRngJYhAsAUEsHCAg25ABRAAAAZAAAAFBLAwQKAAAAAABnhCVNAAAAAAAAAAAAAAAACQAQAF9fTUFDT1NYL1VYDABClY9bQpWPW%2FYBFABQSwMEFAAIAAgAVoQlTQAAAAAAAAAAAAAAABMAEABfX01BQ09TWC8uX2luZGV4LnB5VVgMAEKVj1sjlY9b9gEUAGNgFWNnYGJg8E1MVvAPVohQgAKQGAMnEBsBcR0Qg%2FgbGIgCjiEhQVAmSMcCIBZAU8KIEJdKzs%2FVSywoyEnVy0ksLiktTk1JSSxJVQ4IBik0mtofDaIPhAvogWgAUEsHCAyTbm5cAAAAsAAAAFBLAQIVAxQACAAIAFaEJU0INuQAUQAAAGQAAAAIAAwAAAAAAAAAAECkgQAAAABpbmRleC5weVVYCABClY9bI5WPW1BLAQIVAwoAAAAAAGeEJU0AAAAAAAAAAAAAAAAJAAwAAAAAAAAAAED9QZcAAABfX01BQ09TWC9VWAgAQpWPW0KVj1tQSwECFQMUAAgACABWhCVNDJNublwAAACwAAAAEwAMAAAAAAAAAABApIHOAAAAX19NQUNPU1gvLl9pbmRleC5weVVYCABClY9bI5WPW1BLBQYAAAAAAwADANIAAAB7AQAAAAA%3D"}'

{
    "RequestId": "296275c4-d45f-41d4-b5c2-4ffd4156f783"
}

```

### 通过 COS 对象存储创建函数

如下示例为通过 COS Bucket 中的 zip 包完成函数创建。
由于通过 COS 创建函数，需要将相应 Bucket 授权给 SCF 云函数平台，以便云函数平台可以通过授权访问到代码文件并下载到平台。
您可以通过控制台进行一次函数创建并使用 Bucket 上传代码，系统会自动在前台完成授权操作。
若从未通过控制台创建过函数，可以自行设置 Bucket 授权以便云函数平台可以访问到代码文件，详细操作可见 [权限管理](https://intl.cloud.tencent.com/document/product/583/18014)。

首先将命名为 hello.zip 的 zip 包上传至同地域名称为 gzcode 的存储桶中，然后通过如下命令完成函数创建：
```
$ tccli scf CreateFunction --FunctionName testclifunc --Handler index.main --Runtime Python2.7 --Code '{"CosBucketName":"gzcode","CosObjectName":"/hello.zip"}'

{
    "RequestId": "59b6c32f-56e2-4322-b81d-f6ab910f5265"
}

```


## 更新函数配置
通过控制台或腾讯云命令行均可以完成函数更新，函数更新分为函数的配置更新和函数的代码更新。
### 通过控制台更新函数配置
1. 登录 [无服务器云函数控制台](https://console.cloud.tencent.com/scf)，在左侧选择函数服务。
2. 在主界面上方选择期望更新的函数所在地域。在列表页中单击期望更新的函数，进入函数详情页面。
3. 切换至函数配置子页面，并单击右上角的【编辑】按钮，进入编辑模式。
4. 可根据需求修改函数的描述、配置内存、超时时间、环境变量和网络配置等信息。
5. 修改完成后，单击【保存】按钮保存修改后的配置。若想取消，通过单击【取消】按钮，取消修改的配置。

### 通过腾讯云命令行更新函数配置
通过命令行中的 `tccli scf UpdateFunctionConfigration` 命令即可完成函数配置更新，其中 `FunctionName` 为必选参数，指明期望修改的函数名。
```
$ tccli scf UpdateFunctionConfiguration --FunctionName testcli --Timeout 30
{
    "RequestId": "153496c8-0cd2-40ef-a435-9d67ee6e4387"
}
```

## 更新函数代码
### 通过控制台更新函数代码
1. 通过 [无服务器云函数控制台](https://console.cloud.tencent.com/scf)，在左侧选择函数服务。
2. 在主界面上方选择期望更新的函数所在地域。在列表页中单击期望更新的函数，进入函数详情页面。
3. 切换至函数代码子页面，针对脚本类语言，可以看到函数代码编辑器，针对非脚本类语言，仅有函数上传方式。
4. 可通过代码编辑器直接编辑入口函数，或者切换代码上传方式，选择通过 zip 包上传，或通过对象存储 COS 上传的方式提交函数。
5. 修改完成后，单击【保存】按钮保存或提交新的代码。若想取消，通过单击【取消】按钮取消修改。

### 通过腾讯云命令行更新函数代码
通过命令行中的 `tccli scf UpdateFunctionCode` 命令即可完成函数代码更新，其中 `FunctionName` 为必选参数，指明期望修改的函数名，可以通过 `Handler` 参数更新函数的执行方法。
```
$ tccli scf UpdateFunctionCode --FunctionName testclifunc --CosBucketName gzcode --CosObjectName "/hello.zip" --Handler index.main
{
    "RequestId": "2a15e5bc-e6ec-409f-ba8c-8524e642e528"
}
```

