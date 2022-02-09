This document describes page and API speed tests.



## Page Speed Test

The Aegis SDK for mini program automatically collects and reports page performance data, including:
1. Program start time.
2. Code injection time.
3. First contentful paint (FCP).
4. Route switch time.


<dx-alert infotype="notice" title="">
Acquisition of the page data depends on the Performance API of the mini program. Make sure that the base library version is above 2.11.0.
QQ Mini Program does not yet implement the Performance API and therefore cannot report the page performance data.
</dx-alert>


## API Speed Test

>? How to enable: pass in `reportApiSpeed: true` during initialization.

Aegis tests the API speed by hijacking `wx.request || qq.request`.
