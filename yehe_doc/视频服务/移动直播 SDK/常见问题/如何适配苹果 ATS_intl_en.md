
Apple made it clear at WWDC 2016 that all app submitted since January 1, 2017 could no longer use `NSAllowsArbitraryLoads=YES` to bypass ATS restrictions. Tencent Cloud has supported HTTPS. To meet the ATS requirements, you only need to update to the new version of the SDK (no change to APIs was made) and replace the prefix `http://` with `https://`.

It should be noted that HTTPS may provide greater security (which is not that important for video services) than HTTP, but it leads to slower connection speed and higher CPU usage. To continue using HTTP in your app while meeting Apple’s new requirements, you can add `myqcloud.com` to `NSExceptionDomains` in `Info.plist`, as shown below.  

![](https://main.qcloudimg.com/raw/9cd1a8754cb0b2e7d2d407fec1f82db1.png)

Apple allows disabling ATS for specific domain names, but you may need to explain to Apple’s review team that `myqcloud.com` is used for video playback.
 
 
  
  
 
 
 
