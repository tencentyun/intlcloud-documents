## Overview

When you use the content moderation service, you can specify a moderation category through a moderation policy to moderate content in custom scenes. For different file types, CI provides different scenes for your choice, making it easier for you to customize moderation policies that suit your business.

Currently, the file types and corresponding moderation scenes supported by CI are as follows:

<table>
   <tr>
      <th>Supported File Types</td>
      <th>Moderation Scenes</td>
      <th>Specific Moderation Categories</td>
   </tr>
   <tr>
      <td rowspan="9">Image moderation policy, video moderation policy, <br>audio moderation policy, text moderation policy, file moderation policy</td>
      <td rowspan="5">Pornographic content</td>
      <td>Sexually suggestive/vulgar behaviors</td>
   </tr>
   <tr>
      <td>Genital nudity/Sexual behaviors</td>
   </tr>
   <tr>
      <td>Sex toys</td>
   </tr>
   <tr>
      <td>Sexy content</td>
   </tr>
   <tr>
      <td>Pornographic text moderation</td>
   </tr>
   <tr>
      <td rowspan="3">Advertising content</td>
      <td>QR code and barcode recognition</td>
   </tr>
   <tr>
      <td>Logo detection and recognition</td>
   </tr>
   <tr>
      <td>Advertising text moderation</td>
   </tr>
   <tr>
      <td>Other non-compliant content</td>
      <td>Fire, explosion, bloody scene, etc.</td>
   </tr>
</table>

>! WEBP images involving advertising QR codes cannot be moderated currently.

## Directions

### Default policy

Each moderation type has a default moderation policy, which is configured by Tencent Cloud based on your historical moderation conditions. If you have never used the moderation service, the policy developed by algorithm experts based on models for multiple industries will be used by default, which will be suitable for most content security requirements.

>? The default policy can be viewed and edited but not deleted.
>

### Custom policy

If the default policy cannot meet your business needs, or you have multiple scenes that require different moderation policies, you can create custom policies as needed.

1. Log in to the [CI console](https://console.cloud.tencent.com/ci).
2. Click **Bucket Management** on the left sidebar.
3. Click the name of the target bucket to enter the configuration page.
4. Select **Content Moderation** > **Moderation Policy** on the left sidebar.
5. Create a moderation policy based on your business needs. Currently, you can create policies for **image moderation**, **video moderation**, **audio moderation**, **text moderation**, and **file moderation**.
    Take the image moderation policy as an example:
    i. Click **Create Image Moderation Policy** and enter the policy name.
    ii. Select the category you need to moderate under the moderation type, where OCR pornographic text moderation indicates to moderate image content based on OCR.

    iii. Click **Save** to create the policy.
6. After the moderation policy is created, the backend will automatically generate a unique `Biztype` value.
7. You can view or edit the created moderation policy; however, you cannot change its name and `Biztype` value.


### Using moderation policy

After the moderation policy is created, configure [automatic moderation](https://cloud.tencent.com/document/product/460/56344), create a historical data moderation job, or call a [content moderation API](https://cloud.tencent.com/document/product/460/46426). You can select the corresponding policy to moderate content in custom categories.

#### Automatic moderation

Create an automatic moderation configuration in the console, and you can manually select a moderation policy.


#### Historical data moderation

Create a historical data moderation job in the console, and you can manually select a moderation policy.


#### Moderation APIs

When calling an API for content moderation, you can manually pass in the `Biztype` value to the API, which you can view in the list of moderation policies in the console. If you don't pass it in, the default policy will be used.




