## Prerequisites

Before you can integrate TenDI Captcha into a client, you need to create a CAPTCHA and obtain its CaptchaAppId and AppSecretKey from the **CAPTCHA list**. Follow the steps below:

1. Log in to the [Captcha console](https://console.cloud.tencent.com/captcha/graphical) and select **CAPTCHA** -> **Manage CAPTCHA** in the left navigation pane to enter the CAPTCHA management page.
2. Click **Create CAPTCHA** and set parameters such as CAPTCHA name according to your business requirements.
3. Click **OK** to complete the creation. You can view its CaptchaAppId and AppSecretKey in the CAPTCHA list.

## Integration steps
>! You can integrate TenDI Captcha into an (Android/iOS) app only by using a WebView to display H5 pages.

### Integration in Android
#### **General process**
<dx-steps>
- Use a WebView to display H5 pages in an Android app. For more information on how to integrate TenDI Captcha into H5 pages, please see [Web Integration](https://intl.cloud.tencent.com/document/product/1159/49680).

- Call the CAPTCHA JS to render the verification page in an H5 page. Then pass the parameter values returned in JS to the Android app's business client.
- The Android app's business client passes parameters such as ticket and random number to the business server for ticket verification. For more information, please see [Integration to Ticket Verification (Web and App)](https://intl.cloud.tencent.com/document/product/1159/49682).
</dx-steps>

#### **Detailed steps**
1. In a project, create an activity and import the WebView packages required.
```
import android.webkit.WebView;
import android.webkit.WebSettings;
import android.webkit.WebViewClient;
import android.webkit.WebChromeClient;
```
2. Add permissions, such as "Enable network access" and "Allow the app to make non-HTTPS requests".
```
<uses-permission android:name="android.permission.INTERNET"/>
<application android:usesCleartextTraffic="true">...</application>
```
3. Add the WebView in the layout file of the activity.
```
<WebView
android:id="@+id/webview"
android:layout_height="match_parent"
android:layout_width="match_parent"
/>
```
4. In the project, add a custom JavascriptInterface file and define a method to obtain data.
```
import android.webkit.JavascriptInterface;
public class JsBridge {
@JavascriptInterface
public void getData(String data) {
System.out.println(data);
}
}
```
5. In the activity file, load the H5 business page.
```
public class MainActivity extends AppCompatActivity {
private WebView webview;
private WebSettings webSettings;

@Override
protected void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
setContentView(R.layout.activity_main);
initView();
}

private void initView() {
webview = (WebView) findViewById(R.id.webview);
webSettings = webview.getSettings();
webSettings.setUseWideViewPort(true);
webSettings.setLoadWithOverviewMode(true);
// Disable cache
webSettings.setCacheMode(WebSettings.LOAD_NO_CACHE);
webview.setWebViewClient(new WebViewClient(){
@Override
public boolean shouldOverrideUrlLoading(WebView view, String url) {
view.loadUrl(url);
return true;
}
});
// Enable js
webSettings.setJavaScriptEnabled(true);
webview.addJavascriptInterface(new JsBridge(), "jsBridge");
// Or load a local html file (webView.loadUrl("file:///android_asset/xxx.html"))
webview.loadUrl("https://x.x.x/x/");
}
}
```
6. Integrate TenDI Captcha in the H5 business page (for more information, please see [Web Integration](https://intl.cloud.tencent.com/document/product/1159/49680)), and use JSBridge to pass the verification data to the business side.
>! After TenDI Captcha is integrated into the business client, the business server needs to verify the CAPTCHA ticket (if ticket verification is not integrated, the black market can easily forge verification results, which defeats the purpose of human verification via CAPTCHAs). For more information, please see [Integration to Ticket Verification (Web and App)](https://intl.cloud.tencent.com/document/product/1159/49682).


### Integration in iOS

#### **General process**

<dx-steps>
- Open a WebView in iOS, load an HTML page using JSBridge, and inject a method to be called in the HTML page to pass verification results.
- Integrate TenDI Captcha in the HTML page, call the CAPTCHA JS to render the verification page, and then call the injected method to pass the verification result. For more information, please see [Web Integration](https://intl.cloud.tencent.com/document/product/1159/49680).
- Return the verification result to iOS using JSBridge, and pass parameters such as ticket and random number to the business server for ticket verification. For more information, please see [Integration to Ticket Verification (Web and App)](https://intl.cloud.tencent.com/document/product/1159/49682).
</dx-steps>


#### **Detailed steps**
1. In a controller or view, import the WebKit library.
```
#import <WebKit/WebKit.h>
```
2. Create a WebView and render it.
```
-(WKWebView *)webView{
if(_webView == nil){    
    // Create a webpage configuration object
    WKWebViewConfiguration *config = [[WKWebViewConfiguration alloc] init];
    // Create a settings object
    WKPreferences *preference = [[WKPreferences alloc]init];
    // Set "Whether javaScript is supported". The value is YES by default.
    preference.javaScriptEnabled = YES;
    // Set "Allow javaScript to open a window without user interaction". In iOS, the value is set to NO by default.
    preference.javaScriptCanOpenWindowsAutomatically = YES;
    config.preferences = preference;      
    // This class is used to manage interactions between native and JavaScript.
    WKUserContentController * wkUController = [[WKUserContentController alloc] init];
    // Register a js method with the name jsToOcNoPrams. Set objects to handle and receive the JS method.
    [wkUController addScriptMessageHandler:self  name:@"jsToOcNoPrams"];
    [wkUController addScriptMessageHandler:self  name:@"jsToOcWithPrams"]; 
    config.userContentController = wkUController;     
    _webView = [[WKWebView alloc] initWithFrame:CGRectMake(0, 0, SCREEN_WIDTH, SCREEN_HEIGHT) configuration:config];
    // UI delegate
    _webView.UIDelegate = self;
    // Navigation delegate
    _webView.navigationDelegate = self;        
    // Webpage to be rendered
    NSString *path = [[NSBundle mainBundle] pathForResource:@"JStoOC.html" ofType:nil];
    NSString *htmlString = [[NSString alloc]initWithContentsOfFile:path encoding:NSUTF8StringEncoding error:nil];
    [_webView loadHTMLString:htmlString baseURL:[NSURL fileURLWithPath:[[NSBundle mainBundle] bundlePath]]];       
}
return _webView;
}
[self.view addSubview:self.webView];
```
3. Set delegate methods to process some response events.
```
// Called when the page starts to load
-(void)webView:(WKWebView *)webView didStartProvisionalNavigation:(WKNavigation *)navigation {
}
// Called when the page fails to load
-(void)webView:(WKWebView *)webView didFailProvisionalNavigation:(null_unspecified WKNavigation *)navigation withError:(NSError *)error {
[self.progressView setProgress:0.0f animated:NO];
}
// Called when content starts to be returned
-(void)webView:(WKWebView *)webView didCommitNavigation:(WKNavigation *)navigation {
}
// Called when the page finishes loading
-(void)webView:(WKWebView *)webView didFinishNavigation:(WKNavigation *)navigation {
[self getCookie];
}
// Called when a submission error occurs
-(void)webView:(WKWebView *)webView didFailNavigation:(WKNavigation *)navigation withError:(NSError *)error {
[self.progressView setProgress:0.0f animated:NO];
}
// Called after receiving the server's redirect request, i.e., when the service is redirected
-(void)webView:(WKWebView *)webView didReceiveServerRedirectForProvisionalNavigation:(WKNavigation *)navigation {
}
```
4. Pass the parameters to OC with JS.
```
<p style="text-align:center"> <button id="btn2" type = "button" onclick = "jsToOcFunction()"> Call OC with parameters with JS  </button> </p>
function jsToOcFunction()
{
window.webkit.messageHandlers.jsToOcWithPrams.postMessage({"params":"res.randstr"});
}
```
5. Display the rendered WebView in the view, and then call the Captcha service and pass data to the client.
```
-(void)userContentController:(WKUserContentController *)userContentController didReceiveScriptMessage:(WKScriptMessage *)message{
// message.body is the json data passed to the client
// Use message.body to obtain the parameter body passed with JS
NSDictionary * parameter = message.body;
// Call OC with JS
if([message.name isEqualToString:@"jsToOcWithPrams"]){
// The client obtains the data passed with js and performs operations on the data
parameter[@"params"]
}
}
```

>! After TenDI Captcha is integrated into the business client, the business server needs to verify the CAPTCHA ticket (if ticket verification is not integrated, the black market can easily forge verification results, which defeats the purpose of human verification via CAPTCHAs). For more information, please see [Integration to Ticket Verification (Web and App)](https://intl.cloud.tencent.com/document/product/1159/49682).

## FAQs

For more information, please see [FAQs About Integration](https://intl.cloud.tencent.com/document/product/1159/49692).
