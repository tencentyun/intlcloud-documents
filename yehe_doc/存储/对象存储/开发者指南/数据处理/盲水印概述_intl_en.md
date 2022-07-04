## Overview

Blind watermarking is a brand-new watermarking feature based on Tencent Cloud CI. It allows you to add a watermark to the input image information without displaying the watermark or significantly affecting the image quality. If you suspect that your image has been stolen, you can extract the blind watermark from the suspected image to check whether the image belongs to you.

Blind watermarking comes in three types: semi-blind watermarking, perfectly blind watermarking, and text blind watermarking:

| Blind Watermarking Type | Feature | Applicable Scenario |
| :---------------- | :----------------------------------------- | :---------------------- |
| Semi-blind watermarking (type 1) | Has strong anti-theft effects but requires the input image for watermark extraction | Images smaller than 640 x 640 |
| Perfectly blind watermarking (type 2) | Is easy to extract and requires only the watermarked image for watermark extraction | Batch adding and verification  |
| Text blind watermarking (type 3) | Adds text to the image | Adding terminal information  |

>?
>- Blind watermarking is a paid service, which needs to be activated with the **Enable** button in the configuration page of the bucket.
>- The blind watermarking feature is available in all public cloud regions.

## Use Cases

- **Authentication and accountability**: By adding semi-blind watermarks to your images, you can claim your images when they are stolen and extract blind watermarks using the corresponding input images to prove that you own the images.

- **Duplicate check upon upload**: Sometimes, other users might upload duplicate images (such as real estate images, car images, and product images). To solve this problem, you can perform perfectly blind watermark extraction before the upload, and if you can extract a blind watermark from an image, it has been uploaded before. In this case, you can perform corresponding operations, such as telling the user not to upload duplicate images. If an image does not contain a blind watermark, you can add one to it to prevent duplicate uploads.

- **Image disclosure avoidance**: For internal images, you can add information about the requester to the images by using text blind watermarks. In this way, when an image is disclosed, you can extract the blind watermark and get information about the disclosing party.

## Notes

- Currently, you cannot add a blind watermark to animated images such as GIF.
- Both the width and height of the image watermark must not be greater than 1/8 of the input image.
- You need to choose a white watermark with a black background for the effect of blind watermarking.
- When this service is used for the first time under an account, CI will issue a free resource pack of 6,000 times valid for two months, and any excessive usage and usage after the resource pack expires will be billed. For more information, see CI Free Tier.
- Text watermarks can contain digits and letters.
- Blind watermarking can protect against different kinds of image theft attacks such as clipping, smudging, and color change. The anti-theft effect is subject to the original image size and the attack intensity. For more information, [contact us](https://intl.cloud.tencent.com/contact-sales).
https://intl.cloud.tencent.com/contact-sales)。

## How to Use

### Through COS console

You can enable blind watermarking in the COS console as instructed in Setting Blind Watermark.

### Through RESTful APIs

You can use APIs to add or extract blind watermarks. For more information, see Blind Watermarking.
