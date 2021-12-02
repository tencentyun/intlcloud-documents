CSS provides live stream mix feature, which can synchronously mix multiple streams of input sources into a new stream based on the configured stream mix layout for interactive live streaming. In addition, the stream mix feature has been connected to TencentCloud API 3.0. For more information, please see [CreateCommonMixStream](https://intl.cloud.tencent.com/document/product/267/35997). This document uses examples to describe how to implement live stream mix in different scenarios.

## Notes
- Using stream mix will incur transcoding fees. For details, please see [Live Transcoding (Watermarking, Stream Mixing)](https://intl.cloud.tencent.com/document/product/267/39604).
- To use the mixing and cropping feature, the value of the cropping parameter cannot exceed the value of input stream parameter.


## Supported Features
- Up to **16** concurrent streams can be mixed.
- Up to **5** types of input sources (audio and video, pure audio, pure video, image, and canvas) can be mixed.
- Mixed streams can be output as a new stream.
- Cropping and watermarking are supported.
- Template configuration is supported.
- Recording based on stream mix is supported.
- Automatic stream mix is supported.
- Stream mix types and positions can be switched in real time.
- Stream mix can be started/canceled seamlessly.


## Common Layout Templates
Common templates include 10, 30, 40, 310, 390, 410, 510, and 610. When using them, you do not need to enter the position and length/width parameters of the input stream, and **the original image will be auto-scaled.** You only need to pass in the template ID.

**Figures of common layout templates:**
<table>
<style>#m_img{width:90%;height:auto;display:block;margin-left:auto;margin-right:auto; }</style>
<thead><tr><th>Template 10</th><th >Template 30</th></tr></thead><tr>
<td><img src="https://main.qcloudimg.com/raw/a6b395f6fc7c1d07e4325836a3b725e6.jpg" id="m_img"></td>
<td><img src="https://main.qcloudimg.com/raw/05fbe1c32bec1aed0624785d51b8a2ef.jpg"  id="m_img"></td>
</tr>
<thead><tr><th >Template 40</th><th>Template 310</th></tr></thead><tr>
<td><img src="https://main.qcloudimg.com/raw/06cd40976b29452fa297d52db0d3435c.jpg"  id="m_img"></td>
<td><img src="https://main.qcloudimg.com/raw/e1f4aa6f198856c47d8175302c649448.jpg"  id="m_img"></td>
</tr>
<thead><tr><th>Template 390</th><th >Template 410</th></tr></thead><tr>
<td><img src="https://main.qcloudimg.com/raw/50157bb0b01d511c10b3637c13b1471a.png"  id="m_img"></td>
<td><img src="https://main.qcloudimg.com/raw/6a420d03e7921453cbc461d1f1176f6c.jpg"  id="m_img"></td>

</tr>
<thead><tr><th>Template 510</th><th>Template 610</th></tr></thead>
<td><img src="https://main.qcloudimg.com/raw/c0e5bd29f275a6f055af9830ceea0a02.jpg"  id="m_img"></td>
<td><img src="https://main.qcloudimg.com/raw/5ca8ba33cc08e80d6aeb403645e75aac.jpg"  id="m_img"></td>

</tr>
</tbody></table>	




## Creating Stream Mix Session
### Parameters
For more information, please see [CreateCommonMixStream](https://intl.cloud.tencent.com/document/product/267/35997).



### Scenario 1. Applying for stream mix - using template 20
This example shows you how to use a preset stream mix template to mix streams.

#### Sample input code
```
https://live.tencentcloudapi.com/?Action=CreateCommonMixStream
&MixStreamSessionId=test_room
&MixStreamTemplateId=20
&OutputParams.OutputStreamName=test_stream1
&InputStreamList.0.InputStreamName=test_stream1
&InputStreamList.0.LayoutParams.ImageLayer=1
&InputStreamList.1.InputStreamName=test_stream2
&InputStreamList.1.LayoutParams.ImageLayer=2
&<Common request parameters>
```

#### Sample output code
```
{
  "Response": {
    "RequestId": "e8fa8015-0892-40d5-95c4-12a4bc06ed31"
  }
}
```

#### Stream mix effect for mic connect
![img](https://main.qcloudimg.com/raw/a9bdfd2622e3152e61d8cb15a1b21aa1.jpg)


### Scenario 2. Applying for stream mix - using template 390
This example shows you how to use a preset stream mix template to mix streams.

#### Sample input code

```
https://live.tencentcloudapi.com/?Action=CreateCommonMixStream
&MixStreamSessionId=test_room
&MixStreamTemplateId=390
&OutputParams.OutputStreamName=test_stream2
&InputStreamList.0.InputStreamName=test_stream1
&InputStreamList.0.LayoutParams.ImageLayer=1
&InputStreamList.0.LayoutParams.InputType=3
&InputStreamList.0.LayoutParams.ImageWidth=1920 (canvas width)
&InputStreamList.0.LayoutParams.ImageHeight=1080 (canvas height)
&InputStreamList.0.LayoutParams.Color=0x000000
&InputStreamList.1.InputStreamName=test_stream2
&InputStreamList.1.LayoutParams.ImageLayer=2
&InputStreamList.2.InputStreamName=test_stream3
&InputStreamList.2.LayoutParams.ImageLayer=3
&<Common request parameters>
```

#### Sample output code

```
{
  "Response": {
    "RequestId": "9d8d5837-2273-4936-8661-781aeab9bc9c"
  }
}
```

#### Stream mix effect for host competition
![img](https://main.qcloudimg.com/raw/cad10f080a239725893e5221faa21c17.jpg)



### Scenario 3. Custom stream mix
Use the custom layout, where the position parameters `LocationX` and `LocationY` represent the absolute pixel distance between the top-left corner of the small image and that of the background image.
![](https://main.qcloudimg.com/raw/e1f81cd4a9b08af4ad7e4658fc643f0d.png)

#### Sample input code
```
https://live.tencentcloudapi.com/?Action=CreateCommonMixStream
&MixStreamSessionId=test_room
&OutputParams.OutputStreamName=test_stream2
&InputStreamList.0.InputStreamName=test_stream1
&InputStreamList.0.LayoutParams.ImageLayer=1
&InputStreamList.0.LayoutParams.InputType=3
&InputStreamList.0.LayoutParams.ImageWidth = 1920
&InputStreamList.0.LayoutParams.ImageHeight= 1080
&InputStreamList.0.LayoutParams.Color=0x000000
&InputStreamList.1.InputStreamName=test_stream2
&InputStreamList.1.LayoutParams.ImageLayer=2
&InputStreamList.1.LayoutParams.ImageWidth = 640
&InputStreamList.1.LayoutParams.ImageHeight= 360
&InputStreamList.1.LayoutParams.LocationX= 50
&InputStreamList.1.LayoutParams.LocationY= 720
&InputStreamList.2.InputStreamName=test_stream3
&InputStreamList.2.LayoutParams.ImageLayer=3
&InputStreamList.2.LayoutParams.ImageWidth = 640
&InputStreamList.2.LayoutParams.ImageHeight= 360
&InputStreamList.2.LayoutParams.LocationX= 740
&InputStreamList.2.LayoutParams.LocationY= 720
&<Common request parameters>
```


#### Sample output code
```
{
  "Response": {
    "RequestId": "8c443359-ba07-4b81-add8-a6ff54f9bf54"
  }
}
```


#### Custom stream mix effect
![](https://main.qcloudimg.com/raw/db6a87baba1f1891f514d4bea9b38ee4.png)

## Canceling Stream Mix
### Parameters
For more information, please see [CancelCommonMixStream](https://intl.cloud.tencent.com/document/product/267/35998).

### Examples
This example shows you how to cancel a stream mix by session ID.
#### Sample input code
```
https://live.tencentcloudapi.com/?Action=CancelCommonMixStream
&MixStreamSessionId=test_room
```

#### Sample output code
```
{
  "Response": {
    "RequestId": "3c140219-cfe9-470e-b241-907877d6fb03"
  }
}
```

>! 
>- After applying for canceling stream mix, wait at least for 5s before canceling it.
>- After canceling the stream mix, wait at least for half a minute before you can apply for stream mix using the same session ID.

## Error Codes
For stream mix API 3.0, most common error codes have been transformed into the style of [API 3.0 error code](https://intl.cloud.tencent.com/document/product/267/35997#6.-.E9.94.99.E8.AF.AF.E7.A0.81). However, some error codes remain unchanged, which will be provided in the format of `err_code [ $code ],msg [ $message ]` in `Message` and prompted as an `InvalidParameter` error. The causes of specific codes are as detailed below:

<table>
<thead><tr><th>Error Code</th><th>Reason</th><th>Troubleshooting</th></tr></thead>
<tbody><tr>
<td>-1</td>
<td>An error occurred while parsing the input parameters</td>
<td><ul style="margin:0">
    <li>Check whether the JSON format of the request body is correct.</li>
    <li>Check whether `InputStreamList` is empty.</li>
    </ul></td>
</tr><tr>
<td>-2</td>
<td>Incorrect input parameter</td>
<td>Check whether the image parameter is too large.</td>
</tr><tr>
<td>-3</td>
<td>The number of streams is incorrect</td>
<td>Check whether the number of input streams is within the range of [1,16].</td>
</tr><tr>
<td>-4</td>
<td>Incorrect stream parameter</td>
<td><ul style="margin:0">
    <li>Check whether the length/width of the input/output stream are within the range of (0,3000).</li>
    <li>Check whether the number of input streams is within the range of (0,16].</li>
    <li>Check whether the input stream carries `LayoutParams`.</li>
    <li>Check whether `InputType` is supported (valid values: 0, 2, 3, 4, 5).</li>
    <li>Check whether the stream ID length is within the range of (1,80).</li>
    </ul></td>
</tr><tr>
<td>-11</td>
<td>Layer error</td>
<td><ul style="margin:0">
    <li>Check whether the number of layers is the same as the number of input streams.</li>
    <li>Check whether the layer ID is duplicate.</li>
    <li>Check whether the layer ID is within the range of (0,16].</li>
    </ul></td>
</tr><tr>
<td>-20</td>
<td>The input parameter does not match the API</td>
<td><ul style="margin:0">
    <li>Check whether the number of input streams matches the template ID.</li>
    <li>Check whether the color parameter is correct.</li>
    </ul></td>
</tr><tr>
<td>-21</td>
<td>The number of input streams for stream mix is incorrect</td>
<td>Check whether there are at least two input streams.</td>
</tr><tr>
<td>-28</td>
<td>Failed to get the background length/width</td>
<td><ul style="margin:0">
    <li>Check whether the canvas length and width are set when setting the canvas.</li>
    <li>Check whether the background stream exists (stream mix needs to start 5 seconds after push starts).</li>
    </ul></td>
</tr><tr>
<td>-29</td>
<td>Incorrect cropping parameter</td>
<td>Check whether the cropping position is out of the stream length/width range.</td>
</tr><tr>
<td>-33</td>
<td>Incorrect watermark image ID</td>
<td>Check whether the input image ID is set.</td>
</tr><tr>
<td>-34</td>
<td>Failed to get the URL of the watermark image</td>
<td>Check whether the image has been successfully uploaded and whether the URL has been generated.</td>
</tr><tr>
<td>-111</td>
<td>The `OutputStreamName` parameter does not match `OutputStreamType`</td>
<td><ul style="margin:0">
    <li>If `OutputStreamType` is set to `0`, `OutputStreamName` should be in `InputStreamList`.</li>
    <li>If `OutputStreamType` is set to `1`, `OutputStreamName` should not be in `InputStreamList`.</li>
    </ul></td>
</tr><tr>
<td>-300</td>
<td>The output stream ID has already been used</td>
<td>Check whether the current output stream belongs to another stream mix task.</td>
</tr><tr>
<td>-505</td>
<td>Failed to find the input stream in `upload`</td>
<td>Check whether stream mix is initiated 5 seconds after the push and whether the stream can be played back.</td>
</tr><tr>
<td>-507</td>
<td>Failed to query the stream length/width parameters</td>
<td><ul style="margin:0">
    <li>Check whether the canvas length and width are set.</li>
    <li>Check whether the push succeeds. We recommend you start stream mix 5 seconds after push starts.</li>
    </ul></td>
</tr><tr>
<td>-508</td>
<td>Incorrect output stream ID</td>
<td>Check whether different output stream IDs are used by the same `MixStreamSessionId`.</td>
</tr><tr>
<td>-10031</td>
<td>Failed to trigger stream mix</td>
<td>We recommend you start stream mix 5 seconds after push starts.</td>
</tr><tr>
<td>-30300<br>-31001<br>-31002</td>
<td>The `sessionid` does not exist when stream mix is canceled</td>
<td>Check whether the `MixStreamSessionId` exists.</td>
</tr><tr>
<td>-31003</td>
<td>The output stream ID does not match that in `session`</td>
<td>Check the output stream ID entered when stream mix is canceled.</td>
</tr><tr>
<td>-31004</td>
<td>The output stream bitrate is invalid</td>
<td>Check whether the output stream bitrate is within the range of [1,50000].</td>
</tr><tr>
<td>Others</td>
<td>For other errors, please <a href="https://cloud.tencent.com/act/event/connect-service">contact customer service</a> for assistance.</td>
<td>-</td>
</tr>
</tbody></table>

## FAQs
- [How do I ensure that the input streams can be auto scaled with no black bars in the video image during stream mix?](https://intl.cloud.tencent.com/document/product/267/38255)
- [What should I do if error code -505 is returned for stream mix after push?](https://intl.cloud.tencent.com/document/product/267/38255)
- [What will happen if stream mix is not canceled after it is applied for?](https://intl.cloud.tencent.com/document/product/267/38255)
- [Why is the assistant host's video image in the mixed stream not in the expected position?](https://intl.cloud.tencent.com/document/product/267/38255)

>? For more FAQs about stream mix, please see [On-cloud Stream Mix](https://intl.cloud.tencent.com/document/product/267/38255).





