## Overview

Blind watermarking is a brand-new watermarking feature based on Tencent Cloud CI. It allows you to add a watermark to the input image information without displaying the watermark or significantly affecting the image quality. If you think your image might have been stolen, you can extract the blind watermark from the suspected image to check whether the image belongs to you.

Blind watermarking comes in three types: semi-blind watermarking, perfectly blind watermarking, and text blind watermarking:

| Blind Watermarking Type | Feature | Applicable Scenario |
| :---------------- | :----------------------------------------- | :---------------------- |
| Semi-blind watermarking (type 1) | Has strong anti-theft effects but requires the input image for watermark extraction | Images smaller than 640 x 640 |
| Perfectly blind watermarking (type 2) | Is easy to extract and requires only the image watermark itself for watermark extraction | Batch adding and verification  |
| Text blind watermarking (type 3) | Adds text to the image | Adding terminal information  |

>?
>- Blind watermarking is a paid service, which needs to be activated with the **Enable** button in the configuration page of the bucket. Each account is entitled to a free tier of 3,000 blind watermarks, and any excessive usage will be billed by CI as detailed in [Billing Overview](https://intl.cloud.tencent.com/document/product/1045/33431).
>- The blind watermarking feature is available in all public cloud regions.

## Use Cases

- **Authentication and accountability**: By adding semi-blind watermarks to your images, you can claim your images when they are stolen and extract blind watermarks using the corresponding input images to prove that you own the images.

- **Duplicate check upon upload**: Sometimes, other users might upload duplicate images (such as real estate images, car images, and product images). To solve this problem, you can perform perfectly blind watermark extraction before the upload, and if you can extract a blind watermark from an image, it has been uploaded before. In this case, you can perform corresponding operations, such as telling the user not to upload duplicate images. If an image does not contain a blind watermark, you can add one to it to prevent duplicate uploads.

- **Image disclosure avoidance**: For internal images, you can add information about the requester to the images by using text blind watermarks. In this way, when an image is disclosed, you can extract the blind watermark and get information about the disclosing party.

## Notes

- Currently, you cannot add a blind watermark to animated images such as GIF.
- Both the width and height of the image watermark must not be greater than 1/8 of the input image.
- You need to choose a white watermark with a black background for the effect of blind watermarking.
- Each account is entitled to a free tier of 3,000 blind watermarks, and any excessive usage will be billed. The unused part of the free tier will not roll over to the next month. For more information, see [Free Tier].
- Text watermarks can contain digits and letters.
- Blind watermarking can protect against different kinds of image theft attacks such as clipping, smudging, and color change. The anti-theft effect is related to the original image size and the attack intensity. For more information, [contact us](https://intl.cloud.tencent.com/contact-sales).

## How to Use

### Using COS console

You can enable blind watermarking in the COS console as instructed in [Setting Blind Watermarking].

### Using REST APIs

You can use APIs to add or extract blind watermarks. For more information, see [Blind Watermarking](https://intl.cloud.tencent.com/document/product/1045/43029).
