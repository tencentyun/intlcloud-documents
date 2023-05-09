This document describes FAQs related to the liveness detection and face comparison SDK and provides solutions.

## Client
### Android
1. What should I do if I receive the **Invoke-customs are only supported starting with Android O (--min-api 26)** error after integrating FaceID? 
   Add the following configuration to the `build.gradle` file:

```groovy
   // Java 1.8 is supported
   compileOptions {
       sourceCompatibility JavaVersion.VERSION_1_8
       targetCompatibility JavaVersion.VERSION_1_8
   }
```


2. If the integrator uses the obfuscation tool AndResGuard, you can add the following obfuscation configuration:

```groovy
// for HuiYanSDK
"R.string.ocr_*",
"R.string.rst_*",
"R.string.net_*",
"R.string.msg_*",
"R.string.fl_*",
```


3. If Android X reports **android.content.res.Resources$NotFoundException:from xml type xml resource ID #0x7f0800c3** on devices with an earlier version of system, you can add dependent vector diagrams.

```groovy
 // Vector diagrams for earlier versions
 implementation 'androidx.vectordrawable:vectordrawable:1.1.0'

```


4. If **Android Support** reports the following errors on devices with an earlier version (v6.0 or earlier) of system:

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

You need to update the support dependencies to the latest version (v28.0.0):

```groovy
implementation 'com.android.support:appcompat-v7:28.0.0'
// A component library compatible with vector diagrams for earlier versions
implementation 'com.android.support:support-vector-drawable:28.0.0'
implementation 'com.android.support:animated-vector-drawable:28.0.0'
```


### iOS
1. What should I do if the SDK crashes and the following log is printed when I enter the SDK: "**reason: '*** -[__NSDictionaryM setObject:forKey:]: key cannot be nil'**"? Solution: Add **-ObjC** in **Build Settings** > **Other Linker Flags**.


2. What should I do if the following information is displayed during compilation: 
   Undefined symbol: _vImageConvert_Planar16FtoPlanarF
   Undefined symbol: _vImageConvert_PlanarFtoPlanar16F
    Solution: Add the system library `Accelerate.framework`.



3. What should I do if "**face-tracker-v001 bundle path is nil**" or "**HuiYanSDKUI bundle path is nil**" is prompted? Solution: Add the two prompted resource files to `Copy Bundle Resources`.


