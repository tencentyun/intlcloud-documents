This document describes the statistical methods and configurations passed in for page, API, and resource speed tests.


## Page Speed Test
<dx-alert infotype="explain" title="">
RUM enables the page speed test feature for you by default.
</dx-alert>


After you successfully install and initialize the SDK, the Aegis instance will report the following metrics by default:  

**1. DNS query**: domainLookupEnd - domainLookupStart  
**2. TCP connection**: connectEnd - connectStart  
**3. SSL connection establishment**: requestStart - secureConnectionStart  
**4. Request response**: responseStart - requestStart  
**5. Content transfer**: responseEnd - responseStart  
**6. DOM parsing**: domInteractive - domLoading  
**7. Resource loading**: loadEventStart - domInteractive  
**8. FMP**: RUM listens on the **first screen** DOM changes within 3 seconds after a page is opened and takes the time when the number of DOM changes reaches the highest as the time when the first screen framework rendering is completed. (`setTimeout` is used to start first screen element collection 3 seconds after SDK initialization. As JavaScript is executed in a single-thread environment, the collection time point may be more than 3 seconds after SDK initialization.)  
**9. Complete page loading duration**: sum of 1–7 (DNS query, TCP connection, SSL connection establishment, request response, content transfer, DOM parsing, and resource loading)  

<dx-alert infotype="explain" title="">
For more information on how to calculate page open performance metrics 1–7, see [PerformanceTiming](https://developer.mozilla.org/zh-CN/docs/Web/API/PerformanceTiming). You can print `aegis.firstScreenInfo` to view the corresponding DOM element of `firstScreenTime`. If a DOM element cannot represent the first screen, you can add the <code>&lt;div AEGIS-FIRST-SCREEN-TIMING&gt;&lt;/div&gt;</code> attribute to recognize it as the key first screen element, so that the SDK will consider that the first screen is loaded if it is displayed on the first screen. You can also add the <code>&lt;div AEGIS-IGNORE-FIRST-SCREEN-TIMING&gt;&lt;/div&gt;</code> attribute to add the element to the blocklist.
</dx-alert>


RUM provides the page loading waterfall plot based on the above metrics.

![](https://main.qcloudimg.com/raw/c2bdd61387f8bf433d28825e645129ab.png)

<dx-alert infotype="explain" title="">
 In server scenarios, the `firstScreenTime` in the waterfall plot may be longer than the DOM parsing duration, which is caused by incompatibility of mobile devices. As some devices cannot get the durations of DNS query, TCP connection, and SSL connection establishment, the three metrics will have a smaller average value after being aggregated, causing metrics except `firstScreenTime` to shift to the left.
</dx-alert>

## API Speed Test


<dx-alert infotype="explain" title="">
How to enable: pass in `reportApiSpeed: true` during initialization.  
</dx-alert>

Aegis tests the API speed by hijacking `XHR` and `fetch`.

## Resource Speed Test
<dx-alert infotype="explain" title="">
How to enable: pass in `reportAssetSpeed: true` during initialization.  
</dx-alert>

Aegis uses `PerformanceResourceTiming` provided by the browser to test the resource speed.

