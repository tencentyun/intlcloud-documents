# 后端问题

### 接口并发是否有限制？

默认 QPIS 限制5次/秒，如果客户评估不能满足需求，可以沟通扩容。

### 传递资源相关问题

见[如何传递资源](https://intl.cloud.tencent.com/zh/document/product/1061/46849?) 


# 集成SDK问题


### Invoke-customs are only supported starting with Android O (--min-api 26)错误

需要在build.gradle中添加如下配置：
  ```
   // java版本支持1.8
   compileOptions {
       sourceCompatibility JavaVersion.VERSION_1_8
       targetCompatibility JavaVersion.VERSION_1_8
   }
```
### 如果集成方使用了AndResGuard的混淆工具，导致资源异常
```
  可以添加混淆配置：
	// for HuiYanSDK
	"R.string.ocr_*",
	"R.string.rst_*",
	"R.string.net_*",
	"R.string.msg_*",
	"R.string.fl_*",
```
### 低版本的设备报错

```
// 低版本的矢量图
implementation 'androidx.vectordrawable:vectordrawable:1.1.0'
   
需要更新support依赖到最新版本28.0.0:
implementation 'com.android.support:appcompat-v7:28.0.0'

// 兼容低版本矢量图依赖的组件库
implementation 'com.android.support:support-vector-drawable:28.0.0'
implementation 'com.android.support:animated-vector-drawable:28.0.0'
```