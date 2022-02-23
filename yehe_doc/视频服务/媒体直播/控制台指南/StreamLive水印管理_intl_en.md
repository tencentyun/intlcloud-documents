StreamLive provides the feature of adding watermarks to channels. You can create text or image watermark templates on the **Watermark Management** page in the StreamLive console. The created templates can be configured on the **Channel Management** page.
![](https://qcloudimg.tencent-cloud.cn/raw/2be49fa4bd0ee5ec87a5dbb2f1281c3b.jpg)

### Creating a watermark template

Choose **Watermark Management** on the left sidebar and click **Create Watermark Template** to create a watermark template.

#### Creating a text watermark template

**Text Watermark** is selected as the watermark type by default. You can select the image watermark type from the **Watermark Type** drop-down list.

![](https://qcloudimg.tencent-cloud.cn/raw/d7bc227e5d28378e849ce2a544be957e.jpg)

To create a text watermark template, you need to enter the template name (**Template Name**) and the watermark content to display (**Watermark Text**). You can also set the font size (25-50 px) and watermark color.

In addition, you can set the position of the watermark. When setting the watermark position, you need to determine the initial position of the watermark first, and then adjust the position via **Vertical Offset** and **Horizontal Offset**.

![](https://qcloudimg.tencent-cloud.cn/raw/f05a8121f13d086a2073077188bcbed7.jpg)



#### Creating an image watermark template

To create an image watermark template, you need to enter the template name (**Template Name**) and upload the watermark image. You can also set the font size (25-50 px) and watermark color.

You need to set the image size by adjusting the width and height ratios so that the image can be displayed on the screen in accordance with the corresponding proportions. If you want to maintain the current aspect ratio of the watermark image, only adjust either the height or width ratio, and the other will be stretched or scaled accordingly.
![](https://qcloudimg.tencent-cloud.cn/raw/ad8955e56c150811433b4045e488af5e.jpg)

For example:
- If the width ratio is 50% and the height ratio is 25%, the watermark will be stretched to half of the width of the screen and 1/4 of the height of the screen.
- If the width ratio is 50% and the height ratio is 0%, the watermark will be stretched to half of the width of the screen, and the height will change according to the original aspect ratio of the watermark image.

### Associating a watermark template with a channel

After creating a watermark template, you can associate it with a channel on the channel management page.

![](https://qcloudimg.tencent-cloud.cn/raw/81b30d06e27aa8ab19ec3433356a82bd.jpg)

To associate a watermark template with a channel, select a desired channel, toggle on the watermark switch on the **Output Group Setting** page, and select the created watermark template.
>!  Configuration changes do not take effect until the next live streaming.

### Managing watermark templates

On the watermark management page, you can add, modify, or delete watermark templates.

Before deleting a watermark template, ensure that you have unassociated it from all associated channels. You can view the channels currently associated with a watermark template in the **Template Binding** column. You can delete a watermark template only when the corresponding number in the **Template Binding** column is 0.
![](https://qcloudimg.tencent-cloud.cn/raw/291d919592bb7c66ef63015bd154c851.jpg)


