There are four ways to access Ti Customer Service Robot (TICSR) including WeChat Official Account, WeChat Mini Program, desktop site and mobile website (app and HTML5).

## Access via WeChat Official Account
In **System Management** > **Bot management**, select **Access via WeChat**. There are two access ways via WeChat Official Account:
- Embed TICSR in WeChat custom menu or redirect to website customer service page
- Authorize the iask smart customer service on WeChat Official Account

#### There is a link to add TICSR you can put in the WeChat Official Account menu
Copy the link below and paste it directly to the custom menu of your WeChat Official Account. You need to manually replace the productId and UUID.

```
http://iask.qq.com/mclient/#/client?productId=${botID}Service=0&uuid=${userID}
```

ProductId is bot ID, which can be viewed in **Bot management**. 
Uuid is a unique user identifier corresponding to native system's real user. Uuid can be a combination of up to 22 digits, letters and underscores. Empty entry represents anonymous user. 

![](https://main.qcloudimg.com/raw/2880b9ccae189d6f305fd367fd9b9f83.png)

Example of access via WeChat menu:
![](https://main.qcloudimg.com/raw/ea0e1d39bc902d233e7fcbd1cb95f1f6.png)

#### Bind and authorize on WeChat Official Accounts Platform

Use a WeChat account with WeChat Official Account admin permissions to scan the QR code and tap **Authorize**. After the binding is successful, conversations can be started directly within the WeChat Official Account.

Example:
![](https://main.qcloudimg.com/raw/15f3a6f71aa364ef29713386e90b3196.png)

>!
- Your WeChat Official Account must be a verified WeChat subscription account or service account; otherwise, the customer questions cannot be answered normally.
- After binding, the automatic replies originally configured for your WeChat Official Account may conflict with the customer service messages. It is recommended to move the automatic replies at the WeChat backend to the intelligent customer service platform.
- The unbinding operation only removes the relationship between the WeChat Official Account and the knowledge base; to completely remove the service, you need to go to the WeChat Official Account backend and perform the **deauthorization** operation.

![](https://main.qcloudimg.com/raw/024a40080f631084bdb4f2c4665e7123.png)


## Access via WeChat Mini Program

In **System Management** > **Bot management**, select **Access via WeChat Mini Program**. You can access the service via WeChat Mini Program in two ways:
- Embed it in the WeChat Mini Program page or directly jump to the mobile customer service chat link
- Bind and authorize access to iask intelligent customer service via WeChat Official Accounts Platform

#### Embed a chat link for TICSR in the WeChat Mini Program page
Embed the link below directly in the custom customer service button of the WeChat Mini Program (you need to manually replace the productId and UUID):
```
http://iask.qq.com/mclient/#/client?productId=${botID}Service=0&uuid=${userID}
```
productId is the bot ID, which can be viewed in **Bot management**.
uuid is the unique identifier of the user, which corresponds to the real user in the native system and can be a combination of up to 22 digits, letters and underscores. If it is left blank, the user is anonymous.

Example of access via WeChat Mini Program:
![](https://main.qcloudimg.com/raw/641094e1c80f9f1564ffc7944be66d7e.png)

#### Bind and authorize on WeChat Official Accounts Platform

Go to **System Management** > **Bot management** > **Access via WeChat Mini Program**, click **Go to the WeChat Official Accounts Platform for binding and authorizing**, use a WeChat account with WeChat Mini Program admin permissions to scan the QR code and tap **Authorize**. After the binding is successful, conversations can be started directly within the WeChat Mini Program.

Example of access via WeChat Mini Program:
![](https://main.qcloudimg.com/raw/ae511907f23caaa586aa08e295a5fd67.png)
>!
- Your WeChat Mini Program must be verified; otherwise, the customer questions cannot be answered normally.
- After binding, the automatic replies originally configured for your WeChat Official Account may conflict with the customer service messages. It is recommended to move the automatic replies at the WeChat backend to the intelligent customer service platform.
- Your WeChat Mini Program must have a **[contact button](https://developers.weixin.qq.com/miniprogram/dev/component/contact-button.html)** which can start a customer service conversation when tapped.
- The unbinding operation only removes the relationship between the WeChat Mini Program and the knowledge base; to completely remove the service, you need to go to the WeChat Official Account backend and perform the **deauthorization** operation.

 ![](https://main.qcloudimg.com/raw/024a40080f631084bdb4f2c4665e7123.png)


## Access via Desktop Website

Organizational users can set up an inquiry button on their desktop websites for accessing intelligent customer service, which helps them serve customers better.
In **System Management** > **Bot management**, select **Access via desktop website** and paste the following code to the frontend of the website (you need to manually replace the productId and UUID):

```
var h5Script = document.createElement('script');
h5Script.src = 'http://iask.qq.com/h5ClientSdkNew.js?random=' + Math.random();
document.body.appendChild(h5Script);
h5Script.onload = function() {
  AICSH5Client.init({productId: 'bot ID', staffService: 0, uuid: 'user ID'})
}
```

If you don't know how to deal with the code, please consult your website administrator or builder.
![](https://main.qcloudimg.com/raw/5f70bf238f18f4db3e87037429a17d47.png)
After the code is placed, if the bot icon is displayed in the lower right corner as shown below, the access process has succeeded; otherwise, please check the code position first.
![](https://main.qcloudimg.com/raw/4df716b4a652052e699dcd532e48efe5.png)

## Access via Mobile Website (App and HTML5)

### Access instructions
If you have your own webpage icons, styles or buttons, you can embed the link as a separate page in your webpage, allowing the customers to tap and get redirected directly to the conversation page. 
In **System Management** > **Bot management**, select **Access via mobile website** and directly embed the link below in the webpage as needed (you need to manually replace the productId and UUID). After that, customers can tap and get redirected directly to the conversation page:
```
http://iask.qq.com/mclient/#/client?productId=${botID}Service=0&uuid=${userID}
```
You can also copy this link directly in your mobile website access.
Example of access via mobile website (the conversation page will be displayed after the intelligent customer service icon is tapped):
![](https://main.qcloudimg.com/raw/3bb0981276c13bbbe11856f0cb2db4e3.png)
![](https://main.qcloudimg.com/raw/c5ba4b3eeed3aacab1275d4cf86c74c7.png)

### Embed an HTML5 page in an iOS app
#### Project configuration
Add **support for HTTP** and **camera access** in the Info.plist of the Xcode project.
```
    <key>NSCameraUsageDescription</key>
    <string>This is to enable image and video uploads</string>
    <key>NSAppTransportSecurity</key>
    <dict>
    <key>NSAllowsArbitraryLoads</key>
    <true/>
    </dict>
```

#### UI component

It is recommended to use WKWebView (iOS 8.0+) and create the component using encoding. The code below can be used for reference. If you need downward compatibility with an earlier version of the operating system, please use UIWebView.
```
var webView: WKWebView!
    override func viewDidLoad() {
        super.viewDidLoad()
       // Do any additional setup after loading the view, typically from a nib.
       let url = "https://iask.qq.com/mclient/#/client?productId=1d3fcb6a901d42136c01e1ced113bc7e&uuid="
       let request = URLRequest(url: URL(string: url)!)
       webView.load(request)
    }
override func loadView() {
    let webConfiguration = WKWebViewConfiguration()
    webView = WKWebView(frame: .zero, configuration: webConfiguration)
    view = webView
}
```

#### Troubleshooting

If the Xcode console outputs the following log:
```
[discovery] errors encountered while discovering extensions: Error Domain=PlugInKit Code=13 "query cancelled" UserInfo={NSLocalizedDescription=query cancelled}
```

Solution:
- (Recommended) Ignore as this does not affect the use of the component.
- Modify the project settings:
  1. Open the Xcode menu and select **Product** > **Scheme** > **Edit Scheme**;
  2. Add `key-value: OS_ACTIVITY_MODE = disable` to the Environment Variables option.

### Embed an HTML5 page in an Android app

#### Use WebView to open the gallery and get the Android file image

1. Initialize WebView
```
private static final int FILE_SELECT_CODE = 0;
private ValueCallback<Uri> mUploadMessage;// Select the callback image, for versions below 4.4
private ValueCallback<Uri[]> mUploadCallbackAboveL;// Select the callback image, for versions above 5.0

    // Allow JavaScript execution
    webView.getSettings().setJavaScriptEnabled(true);
    webView.getSettings().setLoadsImagesAutomatically(true);
    webView.setVerticalScrollBarEnabled(false);

    // Run WebView to get Android files by URI
    webView.getSettings().setAllowFileAccess(true);
    webView.getSettings().setAllowFileAccessFromFileURLs(true);
    webView.getSettings().setAllowUniversalAccessFromFileURLs(true);
    webView.setWebChromeClient(new MyWebChromeClient());// Set that the image manager can be opened
    webView.loadUrl("xxxxxxxx");
```

2. Inherit WebChromeClient (the processing varies for different Android versions)
```
private class MyWebChromeClient extends WebChromeClient {

    // For Android 3.0+
    public void openFileChooser(ValueCallback<Uri> uploadMsg) {
        mUploadMessage = uploadMsg;
        Intent i = new Intent(Intent.ACTION_GET_CONTENT);
        i.addCategory(Intent.CATEGORY_OPENABLE);
        i.setType("image/*");
    startActivityForResult(Intent.createChooser(i, "File Chooser"), FILE_SELECT_CODE);
    }

    // For Android 3.0+
    public void openFileChooser(ValueCallback uploadMsg, String acceptType) {
        mUploadMessage = uploadMsg;
        Intent i = new Intent(Intent.ACTION_GET_CONTENT);
        i.addCategory(Intent.CATEGORY_OPENABLE);
        i.setType("*/*");
        startActivityForResult(Intent.createChooser(i, "File Browser"), FILE_SELECT_CODE);
    }

    // For Android 4.1
    public void openFileChooser(ValueCallback<Uri> uploadMsg, String acceptType, String capture) {
        mUploadMessage = uploadMsg;
        Intent i = new Intent(Intent.ACTION_GET_CONTENT);
        i.addCategory(Intent.CATEGORY_OPENABLE);
        i.setType("image/*");
        startActivityForResult(Intent.createChooser(i, "File Chooser"), FILE_SELECT_CODE);
    }

    // For Android 5.0+
    public boolean onShowFileChooser(WebView webView, ValueCallback<Uri[]> filePathCallback, WebChromeClient.FileChooserParams fileChooserParams) {
        mUploadCallbackAboveL = filePathCallback;
        Intent i = new Intent(Intent.ACTION_GET_CONTENT);
        i.addCategory(Intent.CATEGORY_OPENABLE);
        i.setType("*/*");
        startActivityForResult(
            Intent.createChooser(i, "File Browser"),
            FILE_SELECT_CODE);
        return true;
    }
}
```

3. Process the returned image URI in the onActivityResult callback of the page
```
@Override
public void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (resultCode != Activity.RESULT_OK) {
           return;
    }

    switch (requestCode) {
        case FILE_SELECT_CODE: {
            if (Build.VERSION.SDK_INT >= 21) {// For version 5.0 and higher
                Uri uri = data.getData();
                Uri[] uris = new Uri[]{uri};

               /* ClipData clipData = data.getClipData();  // Select multiple images
                if (clipData != null) {
                    for (int i = 0; i < clipData.getItemCount(); i++) {
                        ClipData.Item item = clipData.getItemAt(i);
                        Uri uri = item.getUri();
                        uris[i]=uri;
                    }
                }*/
                mUploadCallbackAboveL.onReceiveValue(uris);// Call back to js
            } else {// For versions below 4.4
                Uri uri = data.getData();
                mUploadMessage.onReceiveValue(uri);
            }
        }
        break;
    }
}
```

#### Troubleshooting

In Android 5.0 and above, if the link loaded by WebView starts with HTTPS but the content inside the link (such as image) is an HTTP link, the content will not be successfully loaded.

Solution: Set the loading mode to mixed mode (`MIXED_CONTENT_COMPATIBILITY_MODE = 2`) before WebView loads the page, i.e., when initializing.

```
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP) {
webView.getSettings().setMixedContentMode(WebSettings.MIXED_CONTENT_COMPATIBILITY_MODE);
｝
webView.getSettings().setBlockNetworkImage(false)；
```

## Configuring the Conversation Window

When you access TICSR, you can configure the conversation window. Currently, this is only supported for desktop and mobile websites but not WeChat Official Accounts.

**The conversation window with buttons at a desktop website**
![](https://main.qcloudimg.com/raw/54b9caebf8f2352d6b7935b5abf54b62.png)

**The conversation window at a mobile website**
![](https://main.qcloudimg.com/raw/461d5a3a2d01c4468735a263e5389d38.png)

In **System Settings** > **Bot settings** > **Basic settings**, you can upload your organizational logo and define your organization name.
![](https://main.qcloudimg.com/raw/11c0e0a8ce3a90e1e4e4ceca9749dedc.png)

After human customer service is enabled, files and images can be uploaded to the conversation window; before that, only text messages are supported for conversations with bots.

Buttons for a desktop website:
- You can configure FAQs which are displayed on the right in the conversation window
- You can configure the "Talk with an agent" button which is displayed above the input box

![img](https://iask.qq.com/static/docs/images/import_set_4.png)

Buttons for a mobile website:
- You can configure the FAQs which are displayed above the input box to help with quick customer queries
- You can configure the "Talk with an agent" button which can be displayed by tapping "+" on the right in the input box

![img](https://iask.qq.com/static/docs/images/import_set_5.png)
