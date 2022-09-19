You can connect WAF CAPTCHA to frontend-backend separated sites or app sites to dynamically send CAPTCHAs from such sites.

You can connect a frontend-backend separated site to the WAF CAPTCHA process to dynamically verify human operations for the site in various scenarios, including custom rule hit, CC attack protection, and bot traffic management. Both iOS and Android apps are connected through web frontend HTML5.


## Prerequisites
 You have purchased [WAF](https://intl.cloud.tencent.com/document/product/627/47799) (Premium or higher) and [connected to it](https://intl.cloud.tencent.com/document/product/627/18635). 


## How to Detect
This feature dynamically checks whether the packets returned from the server contain the CAPTCHA fields delivered by WAF, and if so, it will render the CAPTCHA at the top floating layer to connect the frontend-backend separated site or app to WAF CAPTCHA.

## Directions
Below is the sample code for WAF CAPTCHA connection (with Axios as an example). You can refer to the following to connect a frontend-backend separated site to WAF CAPTCHA based on your actual use case:
1. Add interceptors to the Axios response.
```
 	// Regexes related to WAF CAPTCHA `seqid`
const sig_data = /seqid\s=\s"(\w+)"/g
const waf_id_data = /TencentCaptcha\((\'\d+\')/g

const service = axios.create({ 
    baseURL: '/api',
    timeout: 10000, 
    withCredentials: true
});

service.interceptors.response.use((response)=>{
    const res = response.data;
    if(res.code === 0){
      return res;
    }else{
      // Capture the error and render the CAPTCHA
      const matches = sig_data.exec(res);
      if(matches){
        // Display the CAPTCHA
        let seqid = matches[1];      
	      const wid_matches = waf_id_data.exec(res);
        let wid = wid_matches[1]
        var captcha = new TencentCaptcha(wid, function(res){
          var captchaResult = []
          captchaResult.push(res.ret)
          if(res.ret === 0){
              captchaResult.push(res.ticket)
              captchaResult.push(res.randstr)
              captchaResult.push(seqid)
          }
          var content = captchaResult.join('\n')
          axios.post(
            "/WafCaptcha",content
          ).then().catch();
        });
        captcha.show()
      }else{
        return res;
      }   
    }
},()=>{});
export default service;


Vue.prototype.$axios = service;
```
2.	Add the Axios response with added interceptors during API call.
```
 	getTopic:function(){
  this.$axios.get("/api.php").then(res => {
	  this.topic = res
  });
  }
```
3.	Import the CAPTCHA script globally by adding `<script src="https://ssl.captcha.qq.com/TCaptcha.js"></script>` to `public/index.html`.
```
<!DOCTYPE html>
<html lang="">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1.0">
    <link rel="icon" href="<%= BASE_URL %>favicon.ico">
    <title><%= htmlWebpackPlugin.options.title %></title>
  </head>
  <body>
    <noscript>
      <strong>We're sorry but <%= htmlWebpackPlugin.options.title %> doesn't work properly without JavaScript enabled. Please enable it to continue.</strong>
    </noscript>
    <script src="https://ssl.captcha.qq.com/TCaptcha.js"></script>
    <div id="app"></div>
    <!-- built files will be auto injected -->
  </body>
</html>
```
4. After entering the above code, compile and deploy it on the server.
5. Configure a custom rule in WAF and use an async request to check whether the current page pops up the CAPTCHA window.
![](https://qcloudimg.tencent-cloud.cn/raw/adcbb4e7386562475abb52367422f083.png)
