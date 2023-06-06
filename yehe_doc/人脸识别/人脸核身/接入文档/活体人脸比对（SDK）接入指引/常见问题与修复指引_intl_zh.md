本文主要介绍活体人脸比对SDK的场景问题，并且给出相应的修复指引

## 客户端相关
### Android端常见问题
1. 集成慧眼后出现<b>Invoke-customs are only supported starting with Android O (--min-api 26)</b>错误？
   需要在build.gradle中添加如下配置：

```groovy
   // java版本支持1.8
   compileOptions {
       sourceCompatibility JavaVersion.VERSION_1_8
       targetCompatibility JavaVersion.VERSION_1_8
   }
```


2. 如果集成方使用了AndResGuard的混淆工具，可以添加混淆配置：

```groovy
// for HuiYanSDK
"R.string.ocr_*",
"R.string.rst_*",
"R.string.net_*",
"R.string.msg_*",
"R.string.fl_*",
```


3. Android X针对一些低版本的设备报错 android.content.res.Resources$NotFoundException:from xml type xml resource ID #0x7f0800c3 这一类的错误，可以考虑添加矢量图依赖：

```groovy
 // 低版本的矢量图
 implementation 'androidx.vectordrawable:vectordrawable:1.1.0'

```


4. Android Support 如果在低版本设备上（6.0及以下）出现如下报错：

```java
android.content.res.Resources$NotFoundException: File res/drawable/$txy_face_id_logo__0.xml from color state list resource ID #0x7f070001
         at android.content.res.Resources.loadColorStateListForCookie(Resources.java:2800)
         at android.content.res.Resources.loadColorStateList(Resources.java:2749)
         at android.content.res.TypedArray.getColor(TypedArray.java:441)
         at android.content.res.XResources$XTypedArray.getColor(XResources.java:1286)
         at android.support.v4.content.res.TypedArrayUtils.getNamedColor(TypedArrayUtils.java:124)
         at android.support.graphics.drawable.VectorDrawableCompat$VFullPath.updateStateFromTypedArray(VectorDrawableCompat.java:1746)
         at android.support.graphics.drawable.VectorDrawableCompat$VFullPath.inflate(VectorDrawableCompat.java:1712)
         at android.support.graphics.drawable.VectorDrawableCompat.inflateInternal(VectorDrawableCompat.java:743)
         at android.support.graphics.drawable.VectorDrawableCompat.inflate(VectorDrawableCompat.java:631)
         at android.support.graphics.drawable.VectorDrawableCompat.createFromXmlInner(VectorDrawableCompat.java:590)
         at android.support.v7.widget.AppCompatDrawableManager$VdcInflateDelegate.createFromXmlInner(AppCompatDrawableManager.java:775)

```

需要更新support依赖到最新版本28.0.0:

```groovy
implementation 'com.android.support:appcompat-v7:28.0.0'
// 兼容低版本矢量图依赖的组件库
implementation 'com.android.support:support-vector-drawable:28.0.0'
implementation 'com.android.support:animated-vector-drawable:28.0.0'
```


### iOS端常见问题
1. 进入SDK，出现crash 打印日志 "**reason: '\**\* -[__NSDictionaryM setObject:forKey:]: key cannot be nil'**" ,处理方法是在build Settings - Other Linker Flags 添加 **-ObjC**


2. 编译时报 :
   Undefined symbol: _vImageConvert_Planar16FtoPlanarF
   Undefined symbol: _vImageConvert_PlanarFtoPlanar16F
   处理方法：添加系统库Accelerate.framework 


3. "**face-tracker-v001 bundle path is nil**" 或者 **HuiYanSDKUI bundle path is nil** 添加两个bundle 资源文件至Copy Bundle Resources

