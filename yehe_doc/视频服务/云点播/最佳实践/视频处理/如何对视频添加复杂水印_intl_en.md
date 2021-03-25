VOD’s [watermarking](https://intl.cloud.tencent.com/document/product/266/33939) feature allows the adding of simple image or text watermarks, but cannot meet more sophisticated needs such as adding text-image watermarks or applying filters to watermarks. Given this, VOD has supported Scalable Vector Graphics (SVG) watermarks, allowing you to design text and image layout as you like, draw your own images, and apply filters, gradients, and other special effects.

## What is SVG
- [SVG](https://developer.mozilla.org/zh-CN/docs/Web/SVG) is an XML-based markup language for describing two-dimensional vector graphics. It has been widely applied to web standards including CSS, DOM, and JavaScript.
- VOD does not set height or width limits for SVG. It can identify the smallest rectangle that contains all the elements of an image and use  it as the original dimension of an SVG watermark. In the figure below, the dotted frame is the smallest rectangle identified.
![](https://main.qcloudimg.com/raw/539c2ca84d5ff2f6738b03c086bf7c2a.png)
<span id="editor"></span>
>?
>- You can find on the internet different free, web-based SVG editors. Use them to draw the graphics you want and export them as XML files.
>- Before getting the final XML code, you can manually fine-tune your image, for example, align element attributes or change font size, and check the result in an editor.

## How to Add SVG Watermarks
### Step 1. Edit an SVG watermark.
1. Use an SVG editor (e.g., the simple tool [Tryit Editor](https://www.w3schools.com/graphics/tryit.asp?filename=trysvg_myfirst),  or [Online SVG Editor](https://c.runoob.com/more/svgeditor/), which incorporates more advanced features) to draw your graphics. The graphics are displayed in real time as you edit. After editing, you can save the code as an HTML file, which you can open with a browser later to check the effect.
>? If you need to align different elements, we recommend that you make flexible use of the elements’ alignable attributes and check if the alignment is effective by changing the values of the elements, for example, placing images next to text, or reducing/increasing text length. For detailed instructions, see this [SVG tutorial](https://www.runoob.com/svg/svg-tutorial.html). An [example](#example) is offered below.

### Step 2. Create an SVG watermark template.

Call the [`CreateWatermarkTemplate`](https://intl.cloud.tencent.com/document/product/266/34163) API and specify parameters including the watermark coordinates and dimensions. After the creation, you get a watermark template ID.

### Step 3. Add the SVG watermark to a video.

For how to start a video processing task and get the result, see [Video Processing Task System](https://intl.cloud.tencent.com/document/product/266/33931).
Take the [`ProcessMedia`](https://intl.cloud.tencent.com/document/product/266/34125) API as an example. In [Example2 Initiating a transcoding task](https://intl.cloud.tencent.com/document/product/266/34125#.E7.A4.BA.E4.BE.8B2-.E5.8F.91.E8.B5.B7.E5.B8.A6.E6.B0.B4.E5.8D.B0.E7.9A.84.E8.BD.AC.E7.A0.81.E4.BB.BB.E5.8A.A1), you should set `WatermarkSet.N.Definition` to the template ID obtained in step 2 and, as an SVG watermark is used, pass the XML code obtained in step 1 in `WatermarkSet.N.SvgContent`.
<span id="example"></span>
## Example
This section uses an example to guide you through the process of adding a complex watermark that contains an image and replaceable text.

### Use case
A client wants to watermark videos and has the following requirements:
- The watermark consists of a brand logo and ID of the logged in account (text).
- The watermark appears in the top right corner of videos. The distance between its [origin](https://intl.cloud.tencent.com/document/product/266/34163) and the right and top border of videos is 2% of video width and 5% of video height respectively.
- The width of the watermark is 30% of video width, and the height scales proportionally.
- The text is beneath the logo and aligns to right of the logo.
- The font for the text is SimHei, the background in white, with Gaussian blur and shadow in black. The font size is 50 px when the brand logo is not scaled.

### Step 1. Edit the SVG watermark.
Below is the XML source code for the SVG watermark:

```xml
<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" width="1000px" height="1000px">
    <defs>
        <filter id="filter" x="0" y="0">
            <feGaussianBlur stdDeviation="2"/>
            <feOffset dx="0" dy="3"/>
        </filter>
    </defs>

    <image id="img_watermark"  xlink:href="data:image/png;base64,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"
        x="74.4%" y="0px" height="185px" width="256px"/>
    <text id="text_watermark_shadow" text-anchor="end" font-family="SimHei" font-style="Regular" font-size="50px"
        x="100%" y="245px" style="opacity:1;" fill="black" filter="url(#filter)">@Tencent</text>
    <text id="text_watermark" text-anchor="end" font-family="SimHei" font-style="Regular" font-size="50px"
        x="100%" y="245px" fill="white">@Tencent</text>
</svg>
```

Result checking:
- Method 1: copy the above code to the input field of [Tryit Editor](https://www.w3schools.com/graphics/tryit.asp?filename=trysvg_myfirst), and click **Run** at the top. The watermark appears on the right side:
![](https://main.qcloudimg.com/raw/3a2d9e5234339fe78e39670d0b5db9e3.png)
- Method 2: save the code as an HTML file and open it with a browser. The watermark (white background) in figure 2 below appears.

| Figure 1: Transparent Background| Figure 2: White Background | Figure 3: Black Background |
|---------|---------|---------|
|![](https://main.qcloudimg.com/raw/703d7f9818c4cecb9eb3cb8733835312.png)|   ![](https://main.qcloudimg.com/raw/c96e49aec06dd4d5795788b50e86c65d.png)           |![](https://main.qcloudimg.com/raw/e3ac33c3bb998ddcfc6343681ee8c06d.png)|


#### Code explanation

| Parameter | Description | Attribute|
|---------|---------|---------|
| `<svg>`|Define the SVG canvas | `width="1000px" height="1000px"`: both height and are 1000 px. Just make sure that the canvas is large enough to include all the elements of the watermark.|
|`<filter id="filter">`|Define the filter to be used|-|
|`<feGaussianBlur>`|Set the Gaussian blur filter|`stdDeviation="2"`|
|`<feOffset>`|Set the filter offset|`dx="0" dy="3"`: offset the filter by 3 px **down**. |
|`<image id="img_watermark">`|Brand logo|<li>`xlink:href="data:image/png;base64,{Base64-encoded image data}"`: reference a local image.</li><li>`height="185px" width="256px"`: set the original aspect ratio.</li><li>`x="74.4%" y="0px"`: as the logo is above the text, set the Y-axis offset to 0 px. Keep ***adjusting*** the X-axis offset until the expected result is achieved (`x="74.4%"`). </li>|
|`<text id="text_watermark_shadow">`|Add a shadow to text|<li>`font-family="SimHei" font-style="Regular" font-size="50px"`: set font and font size.</li><li>`text-anchor="end"`: set the end of the text as its original position for alignment.</li><li>`x="100%"`: set `text-anchor` and `x` to **pin** the last character of the text to the **right** of the canvas so as to adjust the position of the brand logo (`x` attribute of `<image id="img_watermark">`).</li><li>`style="opacity:1;": set the opacity.</li><li>`fill="black"`: set the shadow-fill-color to black.</li><li>`filter="url(#filter)`: apply the filter whose `id` is `filter`.</li><li>`y="245px"`: set the Y-axis offset. The height of the brand logo is 185 px, and the font size 50 px, which is basically equivalent to the font height, so `y` must not be smaller than `185+50=235`. After ***testing***, the value is set to `245`.</li>|
|`<text id="text_watermark">`|Text|Most of this parameter’s attributes are the same as those of `<text id="text_watermark_shadow">`, but it does not use a filter（without the `filter` attribute), and the text-fill-color is white (`fill="white"`).|

- When checking the final result, you are advised to change the length of the text, for example, by replacing `@Tencent` with `@Tencent is a kind person` to see if the result still meets the requirements.
- To use a different user ID, just replace the value of `<text>` in the SVG code.

### Step 2. Create an SVG watermark template.
```http
https://vod.tencentcloudapi.com/?Action=CreateWatermarkTemplate
&Type=svg
&Name=Test
&CoordinateOrigin=TopRight
&XPos=2%
&YPos=5%
&SvgTemplate.Width=30S%
&SvgTemplate.Height=0px
&<Common request parameters>
```

Parameter description:

| Parameter | Description |
|---------|---------|
| Type=svg |Set the watermark type to SVG. |
|Name=Test|Set the name of the template (optional). |
|CoordinateOrigin=TopRight| Pin the watermark to the top right of the video. |
|XPos=2%|Set the distance between the [watermark origin](https://intl.cloud.tencent.com/document/product/266/34163) and the right border of videos to 2% of video width. |
|YPos=5%|Set the distance between the [watermark origin](https://intl.cloud.tencent.com/document/product/266/34163) and the top border of videos to 5% of video height.|
|SvgTemplate.Width=30S%|Set the watermark width to 30% of video width.|
|SvgTemplate.Height=0px|The height of the watermark scales proportionally.|

Suppose the ID of the SVG watermark template created is 12345.

### Step 3. Add the SVG watermark to a video.
Initiates a video processing task:
```http
https://vod.tencentcloudapi.com/?Action=ProcessMedia
&FileId=5285485487985271487
&MediaProcessTask.TranscodeTaskSet.0.Definition=30
&MediaProcessTask.TranscodeTaskSet.0.WatermarkSet.0.Definition=12345
&MediaProcessTask.TranscodeTaskSet.0.WatermarkSet.0.SvgContent={the XML code in step 1}
&<Common request parameters>
```

### Below is an example of the result
![](https://main.qcloudimg.com/raw/a9ed65074f61b99324b55ccc86c4e659.gif)


## Appendix

### Supported fonts

- SimHei:style=Regular
- Roboto:style=Bold

[Contact us](https://intl.cloud.tencent.com/document/product/266/19905) if you want other fonts supported.
