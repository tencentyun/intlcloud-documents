## TPNS Android SDK v1.2.7.0

### Adding support for supplementary push via in-app messages
The API for setting whether to allow in-app message display is added. Please pay attention to the compatibility between WebView and higher Android version. For more information, see [API Documentation](https://intl.cloud.tencent.com/document/product/1024/30715).

## TPNS Android SDK v1.2.5.0

### 1. Configure the dependent environment for your project (optional)

If you cannot pull the dependencies when using SDK dependencies, you can consider adding the Google-recommended image source `MavenCentral` and Tencent Cloud image source in the `allprojects.repositories` file of your project’s root directory `build.gradle`. Below is a code sample:
```
allprojects {
    repositories {
        google()
        // Google-recommended image source `MavenCentral`
        mavenCentral()
        jcenter()
        // Tencent Cloud image source
        maven { url 'https://mirrors.tencent.com/nexus/repository/maven-public/' }
    }
}
```

### 2. Add configuration (required)
When using the newly added tag query API, you need to add the implementation method `onQueryTagsResult` in the implementation class that inherits `XGPushBaseReceiver`. Below is a code sample:
``` 
public class MessageReceiver extends XGPushBaseReceiver {

    // Other callback APIs
		// ...
		// Tag query callback API
    public void onQueryTagsResult(Context context, int errorCode, String data, String operateName) {
        Log.i(LogTag, "action - onQueryTagsResult, errorCode:" + errorCode + ", operateName:" + operateName + ", data: " + data);
    }
}
```

