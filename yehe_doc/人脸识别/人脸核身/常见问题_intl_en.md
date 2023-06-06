# Backend FAQs

### What is the limit on concurrent API calls?

The default QPS is 5 calls/sec. If this does not meet your needs, you can contact us to increase the limit.

### Resource passing FAQs

See [Passing Resources](https://intl.cloud.tencent.com/document/product/1061/46849?!editLang=en). 


# SDK integration FAQs


### What should I do if "Invoke-customs are only supported starting with Android O (--min-api 26)" appears?

Add the following configuration to the `build.gradle` file:
  ```
   // Java 1.8 is supported
   compileOptions {
       sourceCompatibility JavaVersion.VERSION_1_8
       targetCompatibility JavaVersion.VERSION_1_8
   }
```
### What should I do if there is a resource exception caused by the obfuscation tool AndResGuard used by the integrator?
```
  Add the following obfuscation configuration:
	// for HuiYanSDK
	"R.string.ocr_*",
	"R.string.rst_*",
	"R.string.net_*",
	"R.string.msg_*",
	"R.string.fl_*",
```
### Errors on devices with an earlier version of system

```
// Vector diagrams for earlier versions
implementation 'androidx.vectordrawable:vectordrawable:1.1.0'
   
You need to update the support dependencies to the latest version (v28.0.0):
implementation 'com.android.support:appcompat-v7:28.0.0'

// A component library compatible with vector diagrams for earlier versions
implementation 'com.android.support:support-vector-drawable:28.0.0'
implementation 'com.android.support:animated-vector-drawable:28.0.0'
```
